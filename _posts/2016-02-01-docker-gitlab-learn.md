---
layout: post
title: '记docker-gitlab那些踩过的坑'
description: "docker gitlab"
keywords: "docker gitlab"
category: 程序开发 
tags: [Docker]
---

久闻Docker是运营神器，最近捣鼓了一下，深感其中的精妙，Host上可以运行多个镜像，每个镜像上又可以搭建不同的应用，应用之间可以互相通信，也能做到相对独立，还有类似于git版本控制的思想，可以构建不同时期不同版本的docker，让跨域合作、团队开发环境一致化、环境搭建逻辑的梳理等运营问题得到一定程序上的解决，也因为docker的架构，使得一切变得更加简单，以及资源整合得更好。

但是docker涉及的概念比较多，对于新手或不是很熟悉的人来说，在面对docker触发的bug面前往往显得一头雾水。

本文记录一下使用docker-gitlab时，或者接手一个docker-gitlab时出现的问题以及解决的方法。

![]({{ site.qiniudn }}/images/2016/02/3.jpg)

<!-- more -->

#### 安装Docker 启动Docker

网上教程有很多，最好还是看[官网](https://docs.docker.com/linux/step_one/)最新的。

1. `$ sudo apt-get update`
2. `$ sudo apt-get install linux-image-generic-lts-trusty`
3. `$ sudo reboot`
4. `$ wget -qO- https://get.docker.com/ | sh`
5. `$ sudo usermod -aG docker username`
6. `$ sudo reboot`
7. `$ docker run hello-world`

#### 安装docker-gitlab

作者说[此处](https://github.com/sameersbn/docker-gitlab)最新。

安装方式有两种：

###### 一、docker-compose方式

这种方式其实就是要把启动的docker和参数写在一个配置文件里，然后由`docker-compose up`去调用。

`wget https://raw.githubusercontent.com/sameersbn/docker-gitlab/master/docker-compose.yml`

`docker-compose up`

###### 二、分步安装

Step 1. Launch a postgresql container

{% highlight bash %}
docker run --name gitlab-postgresql -d \
    --env 'DB_NAME=gitlabhq_production' \
    --env 'DB_USER=gitlab' --env 'DB_PASS=password' \
    --volume /srv/docker/gitlab/postgresql:/var/lib/postgresql \
    sameersbn/postgresql:9.4-12
{% endhighlight %}

Step 2. Launch a redis container

{% highlight bash %}
docker run --name gitlab-redis -d \
    --volume /srv/docker/gitlab/redis:/var/lib/redis \
    sameersbn/redis:latest
{% endhighlight %}

Step 3. Launch the gitlab container

{% highlight bash %}
docker run --name gitlab -d \
    --link gitlab-postgresql:postgresql --link gitlab-redis:redisio \
    --publish 10022:22 --publish 10080:80 \
    --env 'GITLAB_PORT=10080' --env 'GITLAB_SSH_PORT=10022' \
    --env 'GITLAB_SECRETS_DB_KEY_BASE=long-and-random-alpha-numeric-string' \
    --volume /srv/docker/gitlab/gitlab:/home/git/data \
    sameersbn/gitlab:8.4.4
{% endhighlight %}

两种方式各有优劣，第一种倾向于配置化，个人更喜欢一些，特别是有时候想知道当时启动docker的参数是如何设置的，看一下yml文件就清楚了。第二种适合你对docker有一定了解，或在测试、学习时比较方便。

#### 如何重置postgresql的用户密码与权限设置

如果你忘记了之前设置或使用哪个用户进行操作，可以用以下方式恢复:

`docker exec -it gitlab-postgresql sudo -u postgres psql`

`alter user gitlab with password 'password'`

修改用户权限:

`GRANT ALL PRIVILEGES ON DATABASE gitlabhq_production to gitlab;`

#### 注意目录权限

在官方示例中，我们把gitlab的数据放在了`/srv/docker/gitlab/`下，一开始我用`root`身份对整个目录进行`cp -R`备份，发现gitlab有时会出现无法显示（读取）gitlab库，以及有时个别操作（如恢复备份）会出现权限不足的情况，使用`cp -a`或者`cp -rp`或者`rsync -a`来保持复制后的文件具有原来的模样。
