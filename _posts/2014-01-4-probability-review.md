---
layout: post
title: "迷のProbability Review"
description: "Review the Probability class."
keywords: "math, probability"
category: 数学奥义
tags: [Math, Probability]
---

应该是年前挖下的坑了，赶在应用概率统计考试之前补一下。

以下内容多为<a href="http://weibo.com/yehbo" target="_blank">葉丙成_Benson</a>老师机率课上的一些笔记，略为基础，但却时不时会被遗忘，写下来做一次Review.

####概率与统计的不同
   
- 概率：概率模型已知，要学会怎么算某些事件的概率
- 统计：概率模型未知，要学会怎么从大量的实验结果中去建立概率模型

####De Morgan's Law

$$(A\cup B)^{c} = A^{c} \cap  B^{c}$$

<!-- more -->

####概率名词

- 实验：一个概率“实验”包含：步骤、模型、观察。
- 结果：“结果”是实验中可能的结果。
- 样本空间：“样本空间”是概率实验所有可能的结果的集合，通常用**S**来表示。
- 事件：“事件”指的是对于实验结果的某种叙述。在数学上，“事件”可以看成是“结果”的集合，亦即是“样本空间的子集。
- 事件空间：“事件空间”是包含所有事件的集合。
- 概率其实是一个函数，其自变量是事件！所以概率也可以看成是一个映射。

####公理

- 近代数学常以数条公理作为整套理论的基石。好处是，“头过身就过”。公理常是不能被证明的基本性质，也是非常基本的性质。

####概率三公理

- 公理1：对任何事件A而言，$$P(A)\geqslant 0$$.
- 公理2：$$P(S)=1$$.
- 公理3：$$事件A_{1},A_{2},...,A_{n}互斥\Rightarrow P(A_{1}\cup A_{2}\cup ...\cup A_{n}) = P(A_{1}) + P(A_{2}) + ... + P(A_{n})$$

####Bayes' Rule

- 若$$C_{1},C_{2},...,C_{n}$$互斥且$$C_{1}\cup C_{2}\cup ...\cup C_{n}=S$$，则对任意事件A，我们有：

$$P(C_{j}|A)=\frac{P(A|C_{j})P(C_{j})}{P(A|C_{1})P(C_{1})+P(A|C_{2})P(C_{2})+...+P(A|C_{n})P(C_{n})}$$
$$\Leftrightarrow$$
$$\frac{P(C_{j}\cap A)}{P(A)}=\frac{P(A|C_{j})P(C_{j})}{\sum_{i=1}^{n}P(A|C_{i})P(C_{i})}$$

- 这里有一个好玩的问题，有兴趣可参见我之前的一篇文章[Monty Hall problem](http://yabuhoo.com/monty-hall-problem.html "Monty Hall problem")。

####概率的独立性

$$P(A\cap B) = P(A)P(B)\Leftrightarrow \frac{P(A\cap B)}{P(B)}=P(A)\Leftrightarrow P(A│B)=P(A)$$

####二项式定理

$$(x+y)^{n}=\sum_{k=0}^{n}\binom{n}{k}x^{k}y^{n-k}$$

####数数算概率

- 如实验结果由事件A，B，C，D组成，且这4个事件相互独立，发生的概率分别为P(A)，P(B)，P(C），P(D)，问，如做10次实验，求出现2次A，4次B，3次C，1次D的概率。设所求事件为Z，则

$$P(Z)=\frac{10!}{2!4!3!1!}(P(A))^{2}(P(B))^{4}(P(C))^{3}P(D)$$

####随机变量R.V.

- 这是一个用来把实验结果（outcome）数字化的表示方式，目的是可以让概率的推导更数学、更简明。随机变数通常都是用大家的英文字母表示！
- 随机变量的本质不是一个变量，而是一个函数。
- Ex:X(今天下雨)=0；X(今天出太阳)=1；
- 数学上的表示法：$$X:S\rightarrow R$$

####可数与不可数

- 可数的：一个集合如果是“可数的”，这代表它包含的东西是可以一个个被数的。不管用什么文法数它里面的东西，它里面的任何一样东西，总是会被数到的！
- Ex:正偶数集合是可数的。
- 不可数的：一个集合若是“不可数的”，这代表它包含的东西是无法可以一个个被数的。不管用什么文法数它里面的东西，它里面一定有一样东西是你没数到的。
- Ex:0到1之间的所有数字的集合是不可数的！

####无穷多的世界里

- 正整数的集合跟正偶整数的集合相比，哪个集合里面东西比较多？
- 长度为一的线段上的点，与边长为一的正方形上的点，这两个集合，哪一个点的数量比较多?
- 都一样多，因为都可以找到一对一对应的方法。

####累积分布函数CDF(Cumulative Distribution Function)

- 对于任一个随机变量X，定义其CDF为函数：

$$F_X(x)\overset{\underset{\mathrm{def}}{}}{=}P(X\leqslant x)$$

- 最有用的用途：计算X落在某范围内的概率

$$P(a<X\leqslant b)=F_X(b)-F_X(a)$$

- CDF的分布呈梯形状，则它是一个离散随机变量

####概率质量函数PMF(Probability Mass Function)

- 对任一个整数值的**离散随机变量**X，定义其PMF为函数：

$$p_X(x)\overset{\underset{\mathrm{def}}{}}{=}P(X=x)$$

- 与CDF的关系是，对任何x：

$$F_X(x)=\sum_{n=-\infty }^{\left \lfloor x \right \rfloor}P_X(n)$$

####概率密度函数PDF(Probability Density Function)

- 连续随机变量每点发生的概率均是0.因此不能用PMF来计算。
- 如果我们想知道连续随机变数在各个点上的概率分布，可以用密度的方式来表示。
- 对随机变量X而言，其概率密度PDF：

$$f_X(x)=F'_X(x)$$

![PDF]({{ site.qiniudn }}/images/2014/01/cdf2pdf.png "PDF")

$$P(a<X\leqslant b)=F_X(b)-F_X(a)=\int _a^bf_X(x)dx$$

![PDF]({{ site.qiniudn }}/images/2014/01/pdf3.png "PDF")

- PDF有如下性质

$$f_X(x)=F'_X(x)$$

$$F_X(x)=\int_{-\infty }^{x}f_X(u)du$$

$$P(a\leqslant X\leqslant b)=\int_a^bf_X(x)dx$$

$$\int_{-\infty }^{\infty}f_X(x)dx=1$$

$$f_X(x)\geqslant 0$$

####离散概率分布のBernoulli Distribution

- 1次实验，2种结果。在意某结果发生与否。记作$$X\sim Bernoulli(p)$$

![Bernoulli]({{ site.qiniudn }}/images/2014/01/bernoulli.png "Bernoulli")

####离散概率分布のBinomial Distribution

- n次实验，1个概率。在意n次实验出现某结果k次的概率。记作$$X\sim BIN(n,p)$$

![BIN]({{ site.qiniudn }}/images/2014/01/bin.png "BIN")

####离散概率分布のUniform Distribution

- 1次实验，n种结果，各结果出现概率均等。在意某种结果发生与否。记作$$X\sim UNIF(a,b)$$

![Uniform]({{ site.qiniudn }}/images/2014/01/uniform.png "Uniform")

####离散概率分布のGeometric Distribution

- 实验中出现某种结果概率已知，重复操作实验至该结果出现为止。在意某结果是在第几次实验才首次出现。记作$$X\sim Geometric(p)$$

![Geometric]({{ site.qiniudn }}/images/2014/01/geometric1.png "Geometric")

![Geometric]({{ site.qiniudn }}/images/2014/01/geometric2.png "Geometric")

- Geometric Distribution有失忆性！失忆性是什么？我忘了=。=

- 段誉的六脉の神剑可以用几何分布来算他成功打出的概率T_T

####离散概率分布のPascal Distribution

- 实验中出现某种结果机率已知，重复操作实验至该结果出现第k次为止。在意到底在第几次实验才结束。记作$$X\sim Pascal(k,p)$$

![Pascal]({{ site.qiniudn }}/images/2014/01/pascal.png "Pascal")

####离散概率分布のPoisson Distribution

- 某结果出现之平均速率(rate:λ次数/时间)已知。问持续观察某时间长度T后，看到该结果出现k次的概率。记作$$X\sim POI(\lambda T)$$

- PMF:已知某事发生速率为每单位时间λ次，观察时间为T时间单位。X为该观察时间内发生该事件的总次数。则有：

![Poisson]({{ site.qiniudn }}/images/2014/01/poisson1.png "Poisson")

- CDF:

![Poisson]({{ site.qiniudn }}/images/2014/01/poisson.png "Poisson")

- **Poisson**别读成poison了（读：婆桑），其实就是法国佬泊松。

- Poisson可以用极限的思想看做Binomial分布，这也是它的推导由来。

####连续概率分布のUniform Distribution

- PDF：

$$
f_X(x)=\begin{cases}
\frac{1}{b-a}, &a\leqslant x\leqslant b \\ 
0, &otherwise
\end{cases}
$$

![Uniform]({{ site.qiniudn }}/images/2014/01/uniform0201.png "Uniform")

- CDF:

$$
F_X(x)=\int_{-\infty }^x f_X(u)du = \begin{cases}
0, &x\leqslant a, \\ 
\frac{x-a}{x-b},&a< x\leqslant b \\ 
1, &x>b 
\end{cases}
$$

![Uniform]({{ site.qiniudn }}/images/2014/01/uniform0202.png "Uniform")

####连续概率分布のExponential Distribution

- 如果一个随机变量X呈指数分布，则可以记作$$X\sim Exponential(\lambda )$$

- 其中$$\lambda >0$$是一个参数，常被称为率参数(rate parameter)。即每单位时间内发生某事件的次数。

- PDF

$$
f_X(x)=\begin{cases}
\lambda e^{\lambda x},&x\geqslant 0; \\ 
0,&otherwise
\end{cases}
$$

![Exponential]({{ site.qiniudn }}/images/2014/01/exponential.png)

- CDF
	- If $$x\geqslant 0$$:  
$$
F_X(x)=\int_{-\infty }^xf_X(u)du=\int_0^x\lambda e^{-\lambda u}du=-\int_0^xe^{-\lambda u}d(-\lambda u)=-[e^{-\lambda u}]_0^x=1-e^{-\lambda x}
$$  
	- If $$x<0$$:  
$$
F_X(x)=0
$$

- Exponential分布有失忆的性质(memoryless)，常被用来model有这种性质的事情
	- Ex:小美出门化妆所需的时间
	- Ex:某宅打LOL所花的时间

####连续概率分布のErlang Distribution

- $$Erlang(n,\lambda )$$常被用来model一件有n个关卡事情的总时间，而每个关卡所需时间都是关于$$\lambda $$的指数概率分布
	- Ex:打游戏过三关所需时间：$$Erlang(3,\lambda )$$
	- Ex:写五科作业所需时间：$$Erlang(5,\lambda )$$

-PDF

$$
f_X(x)=\begin{cases}
\frac{1}{(n-1)!}\lambda ^nx^{n-1}e^{-\lambda x},&x\geqslant 0; \\ 
0,&otherwise
\end{cases}
$$

![Erlang]({{ site.qiniudn }}/images/2014/01/erlang.png)

- CDF

$$
F_X(x)=\begin{cases}
1-\sum _{k=0}^{n-1}\frac{(\lambda x)^k}{k!}e^{-\lambda x},&x\geqslant 0;\\ 
0,&otherwise 
\end{cases}
$$

####连续概率分布のNormal Distribution

- 正态分布，亦常被称为高斯(Gaussian)分布。记作$$X\sim Gaussian(\mu ,\sigma )$$，也常有人用$$X\sim N(\mu ,\sigma ^2)$$来表示

- PDF

$$
f_X(x)=\frac{1}{\sqrt{2\pi }\sigma}e^{-\frac{(x-\mu )^2}{2\sigma ^2}}
$$

![Gaussian]({{ site.qiniudn }}/images/2014/01/gaussian.png)

- CDF
	- 很难算，积分根本算不出！
	- 办法：Gaussiaan ==> Standard Normal Distribution ==> 查表

- 标准正态分布
	- $$Z\sim N(0,1)$$，  

$$f_Z(z)=\frac{1}{\sqrt{2\pi }}e^{-\frac{z^2}{2}}$$

![SND]({{ site.qiniudn }}/images/2014/01/snd.png)

$$\Phi (z)=\int _{-\infty}^Z\frac{1}{\sqrt{2\pi }}e^{-\frac{u^2}{2}}du$$

![SND]({{ site.qiniudn }}/images/2014/01/snd2.png)

- $$\Phi (z)$$的性质：$$\Phi (-z)=1-\Phi (z)$$

- 对于任何$$X\sim N(\mu ,\sigma ^2)$$而言，$$\frac{X-\mu }{\sigma }\sim N(0,1)$$

- 对于任何$$X\sim N(\mu ,\sigma ^2)$$而言，$$F_X(x)=\Phi (\frac{x-\mu }{\sigma })$$

- 证明：

$$
\begin{aligned}
F_X(x)&=P(X\leqslant x) \\
&=P(X-\mu \leqslant x-\mu ) \\
&=P(\frac{X-\mu }{\sigma}\leqslant \frac{x-\mu }{\sigma }) \\
&=\Phi (\frac{x-\mu }{\sigma })
\end{aligned}
$$

<center><a href="http://pan.baidu.com/share/link?shareid=2338785072&uk=4130601504" target="_blank">[点击查看标准正态分布表]</a></center>

-------

由于篇幅关系，此Review拆分为两部分，第二部分：<a href="http://yabuhoo.com/probability-review-2.html" target="_blank">迷のProbability Review·续</a>。

转载请注明出处：[迷のProbability Review](http://yabuhoo.com/probability-review.html)