---
layout: post
title: "Android简易对讲机的设计与实现"
description: "Android简易对讲机的设计与实现"
keywords: "android, programing"
category: 程序开发
tags: [Android, Programing]
---

近日猎奇于Android，卒造简易对讲机以练手，以此文存载。

这里主要分析一下对讲机的设计思路。读者也可先自行思索一下这个问题，如何设计一个对讲机。

####功能

本简易对讲机的功能简单有两：

- 登录
- 多人对讲

####交互模型

各个终端通过网络，与服务器通讯：

<!-- more -->

- ![Main]({{ site.qiniudn }}/images/2014/01/speaker1.png)

####前、后端

- 服务器

	1. 登录
	2. 上传音频
	3. 下载音频
	4. 群发音频

- Android端

	1. 登录
	2. 上传音频
	3. 下载音频
	4. 录音、播放

- 由上可看出，前后端交互的主要环节在于登录与上传下载。

####Socket与Http

在Android的网络通讯中，通常会使用Socket进行设备间数的数据通讯，使用Http来对网络数据进行请求。

对Socket与Http的描述有很多，可参见[Http和Socket连接区别](http://pan.baidu.com/s/11TOv0)、[TCP/IP、Http、Socket的区别](http://jingyan.baidu.com/article/08b6a591e07ecc14a80922f1.html)

有两个比较有意思的比喻，

- 如果Socket比喻成一台发动机（提供网络通讯的能力），那么Http就是一部轿车（提供了封装或者显示数据的具体形式）。
- 另外一个是，Socket，就是“插座”的意思，理解为，终端和服务器之间有一个“电源线”连接，传输你想要的东西，一直存在这个连接。直到你不要连接才去切断那根线。而Http就是连接一次就得插一次电源，传输完毕连接自动断开。

####协议

此Toycode采用的是TCP+UDP，用到的一些消息定义如下图s：

- 登录：

![Login]({{ site.qiniudn }}/images/2014/01/login.png)

- 下载：

![Get]({{ site.qiniudn }}/images/2014/01/get.png)

- 上传与群发：

![Multisend]({{ site.qiniudn }}/images/2014/01/multisend.png)

####功能截图

- ![login_layout]({{ site.qiniudn }}/images/2014/01/login_layout.png) &nbsp;&nbsp;&nbsp; ![message_layout]({{ site.qiniudn }}/images/2014/01/message_layout.png)

####源码下载

Git: <a href="https://github.com/atomatrix/android-simple-radio" target="_blank">shsfoolish/android-simple-radio</a>

Enjoy it!

















