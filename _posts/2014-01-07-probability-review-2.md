---
layout: post
title: "迷のProbability Review·续"
description: "Review the Probability class."
keywords: "math, probability"
category: 数学奥义
tags: [Math, Probability]
---

由于篇幅关系，此Review拆分为两部分，第一部分：<a href="http://yabuhoo.com/probability-review.html" target="_blank">迷のProbability Review</a>。

####大数法则

- 根据大数法则，

$$\lim_{N\rightarrow \infty}\frac{N_x}{N}=P_X(x)\Rightarrow \lim_{N\rightarrow \infty}mean=\lim_{N\rightarrow \infty }\sum_{x=1}^{n}x\frac{N_x}{N}=\sum_{x=1}^nx\cdot P_X(x)$$

<!-- more -->

####离散分布の期望值(Expectation)及方差(Variance)

- 对离散随机变量X而言，定义其期望值

$$E[X]=\mu _X=\sum_{x=-\infty }^\infty x\cdot P_X(x)$$

- 对于任一离散随机变量X而言，其任意函数$$g(X)$$亦是一随机变量，亦有期望值

$$E[g(X)]=\sum_{x=-\infty }^\infty g(x)\cdot P_X(x)$$

- 性质

$$E[\alpha g(X)+\beta h(X)=\alpha \cdot E[g(X)] + \beta \cdot E[h(X)]$$

$$E[\alpha ]=\alpha $$

- $$X$$的$$n^{th}$$moment:

$$E[X^n]=\sum_{x=-\infty }^\infty x^n\cdot P_X(x)$$

- Variance通常符号表示为$$\sigma _X^2=E[(X-\mu _X)^2]$$

- 方差（变异数）隐含关于随机变量X多“乱”的信息。

![Variance]({{ site.qiniudn }}/images/2014/01/variance.png)

- 标准差定义为方差的平方根：$$\sigma _X$$

- 两个常用公式

$$\sigma _X^2=E[(X-\mu _X)^2]=E[X^2]-\mu _X^2$$

$$E[X^2]=\sigma _X^2+\mu _X^2$$

- 常见离散分布的期望与方差

$$X\sim Bernouli(p): \mu _X=p; \sigma _X^2=p(1-p)$$

$$X\sim BIN(n,p): \mu _X=np; \sigma _X^2=np(1-p)$$

$$X\sim GEO(p): \mu _X=\frac{1}{p}; \sigma _X^2=\frac{1-p}{p^2}$$

$$X\sim PASKAL(k,p): \mu _X=\frac{k}{p}; \sigma _X^2=\frac{k(1-p)}{p^2}$$

$$X\sim POI(\alpha ): \mu _X=\alpha ;\sigma _X^2=\alpha $$

$$X\sim UNIF(a,b): \mu _X=\frac{a+b}{2}; \sigma _X^2=\frac{1}{12}(b-a)(b-a+2)$$

####连续分布の期望值(Expectation)及方差(Variance)

- 对于连续随机变量$$X$$，其期望定义为

$$E[X]=\int _{-\infty }^\infty xf_X(x)dx$$

- 对于任一连续随机变量X而言，其任意函数$$g(X)$$亦是一随机变量，亦有$$g(X)$$期望值

$$E[g(X)]=\int _{-\infty }^\infty g(x)f_X(x)dx$$

- 性质

$$E[\alpha g(X)+\beta h(X)=\alpha \cdot E[g(X)] + \beta \cdot E[h(X)]$$

- $$X$$的$$n^{th}$$moment:

$$E[X^n]=\int _{-\infty }^\infty x^nf_X(x)dx$$

- Variance

$$\sigma _X^2=E[(X-\mu )^2]=\int _{-\infty }^\infty (x-\mu _x)^2f_X(x)dx$$

- 方差（变异数）隐含关于随机变量X多“乱”的信息。

![Variance]({{ site.qiniudn }}/images/2014/01/variance2.png)

- 标准差定义为方差的平方根：$$\sigma _X$$

- 两个常用公式

$$\sigma _X^2=E[(X-\mu _X)^2]=E[X^2]-\mu _X^2$$

$$E[X^2]=\sigma _X^2+\mu _X^2$$

- 常见连续分布的期望与方差

$$X\sim Exponential(\lambda ): \mu _X=\frac{1}{\lambda }; \sigma _X^2=\frac{1}{\lambda ^2}$$

$$X\sim Erlang(n,\lambda ): \mu _X=\frac{n}{\lambda }; \sigma _X^2=\frac{n}{\lambda ^2}$$

$$X\sim Gaussian(\mu ,\sigma ): \mu _X=\mu ; \sigma _X^2=\sigma ^2$$

$$X\sim UNIF(a,b): \mu _X=\frac{a+b}{2}; \sigma _X^2=\frac{1}{12}(b-a)^2$$

####随机变量X的函数分布

- 随机变量$$X$$的任意函数$$g(X)$$也是一个随机变量，通常称之为Derived Random Variable。

- 若$$X$$为离散：直接推$$Y=g(X)$$的PMF

$$p_{g(X)}(y)=\sum_{x,g(x)=y}p_X(x)$$

- 若$$X$$为连续：先推$$Y=g(X)$$的CDF，再微分得PDF

$$F_{g(x)}(y)=P[g(X)\leqslant y]$$

$$f_{g(X)}(y)=\frac{d}{dy}F_{g(X)}(y)$$

####条件概率

- 若$$X$$是一离散随机变量，其PMF为$$p_X(x)$$。若已知某事件B已发生，则在此情况下的条件概率分布为：

$$
PMF:p_{X\mid B}(x)=\begin{cases}
x\in B:&\frac{p_X(x)}{P(B)} ,\\ 
x\notin B:&0. 
\end{cases}
$$

- 若$$X$$是一连续随机变量，其PDF为$$f_X(x)$$。若已知某事件B已发生，则在此情况下的条件概率分布为：

$$
PDF:f_{X\mid B}(x)=\begin{cases}
x\in B:&\frac{f_X(x)}{P(B)} \\ 
x\notin B: & 0
\end{cases}
$$

$$
CDF:F_{X\mid B}(x)=\int_{-\infty}^xf_{X\mid B}(u)du=\int_{-\infty \leqslant u \leqslant x,u\in B} \frac{f_X(x)}{P(B)}du
$$

- 关于条件概率的期望、方差都可在此基础上推出。

####联合概率分布

- 同时考虑多个随机变量的概率分布称之为联合概率分布(joint probability distribution)

$$PMF:p_{X,Y}(x,y)=P(X=x,Y=y)$$

$$CDF:F_{X,Y}(x,y)=P(X\leqslant x,Y\leqslant y)$$

$$
\begin{aligned}
&f_{X,Y}(x,y)=\frac{\partial ^2F_{X,Y}(x,y)}{\partial x\partial y} \\
\Rightarrow &F_{X,Y}(x,y)=\int_{-\infty}^x\int_{-\infty}^yf_{X,Y}(u,v)dvdu
 \end{aligned}
$$

- 联合PDF的性质

$$f_{x,y}(x,y)\geqslant 0$$

$$\int_{-\infty}^\infty f_{X,Y}(x,y)dxdy=1$$

$$if\ x,y\ independent\Rightarrow f_{X,Y}(x,y)=f_X(x)\cdot f_Y(y)$$

$$
\begin{aligned} 
for\ event\ B,&\\
&P(B)=\iint_{(x,y)\in B}f_{X,Y}(x,y)dxdy
\end{aligned}
$$

####边际概率分布

- 对于离散情形，$$X$$和$$Y$$的边际分布分别为：

$$p_X(x)=\sum_yp_{X,Y}(x,y)$$

$$p_Y(y)=\sum_xp_{X,Y}(x,y)$$

- 对于连续情形，$$X$$和$$Y$$的边际分布分别为：

$$f_X(x)=\int_{-\infty}^\infty f_{X,Y}(x,y)dy$$

$$f_X(y)=\int_{-\infty}^\infty f_{X,Y}(x,y)dx$$

- 期望值

$$PMF:E[h(X,Y)]=\sum_{x=-\infty}^{\infty}\sum_{y=-\infty}^{\infty}h(x,y)\cdot p_{X,Y} (x,y)$$

$$PDF:E[h(X,Y)]=\int_{-\infty}^\infty \int_{-\infty}^\infty h(x,y)\cdot f_{X,Y}(x,y)dxdy$$

$$if\ x,y\ independent\Rightarrow E[g(X)h(Y)]=E[g(X)]\cdot E[h(Y)]$$

- 方差

$$
\begin{aligned}
Var(X+Y)&=E[(X+Y-E[X+Y])^2] \\
&=E[(X-\mu _X)^2]+Var((Y-\mu _Y)^2)+2E[(X-\mu _X)(Y-\mu _Y)] \\
&=Var(x)+Var(y)+2Cov(X,Y) \\
\end{aligned}
$$

$$
if\ X,Y\ independent\Rightarrow Var(X+Y)=Var(X) + Var(Y)
$$

####随机变量之和

- 若$$X,Y$$独立

![Z]({{ site.qiniudn }}/images/2014/01/z.png)

- 考虑不只两个随机变量的情形，求和的分布的需要多次卷积（摺积）(convolution),很复杂。用MGF转换问题。

####MGF(Moment Generation Function)

- MGF$$\phi _X(s)$$定义：

$$\phi _X(s)=E[e^{sX}]=\begin{cases}
\sum_{x=-\infty}^\infty e^{sx}\cdot p_X(x) &(discreted)\\ 
\int_{-\infty}^\infty e^{sx}\cdot f_X(x)dx & (continue)
\end{cases}$$

- 逆转换通常靠查表

- Why named "Moment Generation Funtion"
	- Discreted case:  
![whymgf]({{ site.qiniudn }}/images/2014/01/whymgf.png)
	- Continue case:  
![whymgf]({{ site.qiniudn }}/images/2014/01/whymgf2.png)

- 性质

$$
\begin{aligned}
Y=aX+b \\
&\phi_Y(s)=E[e^{sY}]=E[e^{s(aX+b)}]=e^{sb}\cdot \phi_X(as)
\end{aligned}
$$

- 常见概率分布MGF及特征方程

![mgf]({{ site.qiniudn }}/images/2014/01/mgf.png)

####独立随机变量之和

- $$X_1,X_2,...$$独立且各自都有一模一样的概率分布，表示为

$$\left\{X_i\right\} \ I.I.D.\\
Independently\ and\ Identically\ Distributed$$

- $$X=X_1+X_2+\cdots +X_n$$,$$n$$为常数，求$$X$$的概率分布

$$\Phi_X(s)=[\phi_{X1}(s)]^n$$

- $$X_1,X_2,...I.I.D.$$，$$X=X_1+X_2+\cdots +X_N$$，若$$N$$本身也为随机变量

$$
N:p_N(n)\ given\\
\Rightarrow \phi _N(\widetilde{s})=\sum _{n=0}^\infty e^{\widehat{s}n}\cdot p_N(n)
$$

$$\Phi_X(s)=\phi_N(\ln(\phi _{x1}(s))))$$

####中央极限定理

- 若$$X_1,X_2,...，X_n$$为I.I.D.,则当$$n$$趋近于无穷大时:

$$X=X_1+X_2+\cdots +X_n \sim N(\mu _{X1+X2+\cdots +Xn}, \sigma _{X1+X2+\cdots +Xn}^2)$$

$$\mu _{X1+X2+\cdots +Xn}=\mu_{X1}+\mu_{X2}+\cdots +\mu_{Xn}$$

$$\sigma _{X1+X2+\cdots +Xn}^2=\sigma_{X1}^2+\sigma_{X2}^2+\cdots +\sigma_{Xn}^2$$

- CLT的应用
	- 当要处理多个独立的随机变数的和时，可以用CLT将其概率分布近似为正态分布后计算概率
	- 另若某概率分布等同于多个独立随机变量的和，此概率分布便可以用正态分布近似之，再计算概率 
	- Ex:$$X\sim BIN(100,0.3)\Rightarrow \left\{X_i\right\}I.I.D.,X_i\sim Bernoulli(0.3)$$

<br />

- De Moivre - Laplace Formula，结果更精确:

$$\begin{aligned} 
P(k_1\leqslant X\leqslant k_2)&\approx P(\frac{k_1-0.5-n\mu _{X1}}{\sqrt{n}\sigma_{X1}}\leqslant \frac{X-n\mu _{X1}}{\sqrt{n}\sigma_{X1}}\leqslant \frac{k_1+0.5-n\mu _{X1}}{\sqrt{n}\sigma_{X1}})\\
&\approx \Phi (\frac{k_2+0.5-n\mu _{X1}}{\sqrt{n}\sigma_{X1}})-\Phi (\frac{k_2-0.5-n\mu _{X1}}{\sqrt{n}\sigma_{X1}})
\end{aligned}$$

<center>■ 完 ■</center>
<center>lol</center>
-----
更详尽的课程内容还是回去复习吧：P

转载请注明出处：[迷のProbability Review·续](http://yabuhoo.com/probability-review-2.html)





