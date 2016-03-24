---
layout: post
title: 'Airflow实战'
description: "airflow in action"
keywords: "airflow"
category: 数据挖掘 
tags: [Airflow]
---

在数据挖掘中，[ETL](https://zh.wikipedia.org/wiki/ETL)是十分重要的一环。

在数据处理时，我们可能会用`crontab`工具把任务例行起来。随着业务增多会发现任务的管理变得越来越吃力了，而[Airflow](http://pythonhosted.org/airflow/)可能就是你想要找的那个方案。

![]({{ site.qiniudn }}/images/2016/03/06.png)

<!-- more -->

#### 为什么要工作流管理平台

换句话说，传统的crontab任务管理存在什么不足：

1. 查看任务执行情况不直观方便；

2. 一些存在依赖关系的任务没办法保证；

3. 任务多了难以理清任务之间的关系。

#### 什么是Airflow

[Airflow](http://pythonhosted.org/airflow/)是Airbnb内部发起的一个工作流(数据管道Data Pipeline)管理平台。

- 查看任务执行情况直观方便；

![]({{ site.qiniudn }}/images/2016/03/07.png)

- 可以解决依赖性任务的高度；

- 任务之间的逻辑一目了然；

![]({{ site.qiniudn }}/images/2016/03/08.png)

- 可追踪历史的任务执行情况；

![]({{ site.qiniudn }}/images/2016/03/09.png)
![]({{ site.qiniudn }}/images/2016/03/10.png)

- Email通知；

- 可拓展性强(HDFS、Hive...)

- ...

#### 下载安装与配置

##### 安装

{% highlight %}
# 可选，默认是~/airflow
export AIRFLOW_HOME=~/.airflow

# 从pypi里安装airflow
pip install airflow

# 初始化数据库(即${AIRFLOW_HOME}/airflow.db)
airflow initdb

{% endhighlight %}

安装后`airflow webserver`就可以开启后台管理界面了。

##### 简单的登录密码设置

Airflow提供一个类似插件的方式让使用者可以更好地按自己的需求定制，[这里](http://pythonhosted.org/airflow/installation.html)列出了官方的一定Extra Packages.

默认安装后是，后台管理的webserver是无须登录，如果想加一个登录过程很简单：

首先安装密码验证模块。

{% highlight %}
pip install airflow[password]
{% endhighlight %}

有可能在安装的过程中会有一些依赖包没有，只需要相应地装上就可以了。比如`libffi-dev`、`flask-bcrypt`

然后在配置文件`airflow.cfg`中的`webserver`开启密码验证功能。

{% highlight %}
authenticate = true
auth_backend = airflow.contrib.auth.backends.password_auth
{% endhighlight %}

最后运行以下代码，将用户帐号密码信息写入DB。

{% highlight python %}
import airflow
from airflow import models, settings
from airflow.contrib.auth.backends.password_auth import PasswordUser
user = PasswordUser(models.User())
user.username = 'user1'
user.email = 'user1@example.com'
user.password = 'passwd1'
session = settings.Session()
session.add(user)
session.commit()
session.close()
exit()
{% endhighlight %}

重启webserver即可看见登录页面。

##### 设置Email功能

Email功能也是一个十分实用的功能，下面以126的smtp服务为例，在`airflow.cfg`设置smtp：

{% highlight %}
smtp_host = smtp.126.com
smtp_starttls = True
smtp_user = example@126.com
smtp_port = 25
smtp_password = example
smtp_mail_from = example@126.com 
{% endhighlight %}

#### Airflow几个重要概念

- DAG(directed acyclic graphs):Airflow中用有向无环图表示务的依赖结构

- Task:单个任务节点

- Operator:任务图中一个任务节点的具体类型. 用的有BashOperator, DummyOperator

![]({{ site.qiniudn }}/images/2016/03/11.png)

#### 怎么使用Airflow管理任务

首先，当然得打开后台守护进行，这样Airflow才能实时监控任务的调度情况

{% highlight %}
airflow scheduler
{% endhighlight %}

##### 使用Airflow的大致步骤

1. 写任务脚本(.py)
2. 测试任务脚本(command)
3. WebUI 自查

###### 编写任务脚本(存放${AIRFLOW_HOME}/dags下)

下面是一个简单的示例：

{% highlight python %}
from airflow.operators import BashOperator, DummyOperator
from airflow.models import DAG
from datetime import datetime, timedelta

seven_days_ago = datetime.combine(datetime.today() - timedelta(7),
                                  datetime.min.time())
args = {
    'owner': 'xiaohei',
    'start_date': seven_days_ago,
    'email': ['xiaohei@126.com'],
    'email_on_failure': False
}

dag = DAG(
    dag_id='dag2', default_args=args,
    schedule_interval=‘@daily’  # 这里可以填crontab时间格式
    )

task0 = DummyOperator(task_id='task0', dag=dag)

cmd = 'ls -l'
task1 = BashOperator(
    task_id = 'task1',
    bash_command = cmd,
    dag = dag)

task0.set_downstream(task1)

task2 = DummyOperator(
        trigger_rule = 'all_done',
        task_id =  'task2',
        dag = dag,
        depends_on_past = True)

task2.set_upstream(task1)

task3  = DummyOperator(
        trigger_rule = 'all_done',
        depends_on_past = True,
        task_id = 'task3',
        dag = dag)

task3.set_upstream(task2)

task4 = BashOperator(
    task_id = 'task4',
    bash_command = 'lsfds-ljss',
    dag = dag)

task5 = DummyOperator(
        trigger_rule = 'all_done',
        task_id = 'task5',
        dag = dag)

task5.set_upstream(task4)
task5.set_upstream(task3)


{% endhighlight %}

这里有的`start_date`有点特别，如果你设置了这个参数，那么airflow就会从start_date开始以`schedule_interval`的规则开始执行，例如设置成3天前每小时执行一次，那么在调度正常启动时，就会立即调度`24*3`次，但注意，脚本执行环境的时间还是当前的系统时间，而不会说真是把系统时间模拟成3天前，所以感觉这个功能应用场景比较好限。

上面这个例子中，task1与task2是“弱依赖”关系——有时间上的关系，但父节点不一定都得成功执行。注意在task2中加上以下两句：

{% highlight python %}
trigger_rule = 'all_done',
depends_on_past = True
{% endhighlight %}

![]({{ site.qiniudn }}/images/2016/03/12.png)

task5需要直接父节点(task3 & task4)必须成功执行，但不一定全部父节点都得成功执行

{% highlight python %}
trigger_rule = 'all_done',
{% endhighlight %}

![]({{ site.qiniudn }}/images/2016/03/13.png)

###### 测试任务脚本(command)

Example - ${AIRFLOW_HOME}/test_impoort.py：

{% highlight python %}
from airflow.operators import BashOperator, DummyOperator
from airflow.models import DAG
from datetime import datetime, timedelta

seven_days_ago = datetime.combine(datetime.today() - timedelta(7),
                                  datetime.min.time())
args = {
    'owner': 'xiaohei',
    'start_date': seven_days_ago,
}

dag = DAG(
    dag_id='test_import_dag', default_args=args,
    schedule_interval='0 0 * * *',
    dagrun_timeout=timedelta(minutes=60))

run_test = BashOperator(
    task_id = 'test_import_task',
    bash_command = 'cd /home/jiwoDev/xiaohei/tmp; python test_import.py',
    dag = dag)
 
{% endhighlight %}

1. `$ cd ${AIRFLOW_HOME}/dags`

2. `$ python test_import.py` \# 保证代码无语法错误

3. `$ airflow list_dags` \# 查看dag是否成功加载

4. `airflow list_tasks test_import_dag –tree` \# 查看dag的树形结构是否正确

5. `$ airflow test test_import_dag \ test_import_task 2016-3-7` \# 测试具体的dag的某个task在某个时间的运行是否正常

6. `$ airflow backfill test_import_dag -s 2016-3-4 \ -e 2016-3-7` \# 对dag进行某段时间内的完整测试

###### WebUI自查

![]({{ site.qiniudn }}/images/2016/03/14.png)
![]({{ site.qiniudn }}/images/2016/03/15.png)

#### 相关资源

源码： [https://github.com/airbnb/airflow](https://github.com/airbnb/airflow/)
官方文档： [http://pythonhosted.org/airflow/](http://pythonhosted.org/airflow/)
