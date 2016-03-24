---
layout: post
title: '使用OpenCV简易实现how-old.net'
description: "OpenCV"
keywords: "OpenCV"
category: 图像识别
tags: [OpenCV, Python]
---

[HowOldRobot](http://www.how-old.net) 是微软推出的一个小服务，实现识别图片中的人脸以及预测图片中人的年龄，预测模型可能比较复杂，但是想做一个简单的人脸轮廓的识别还是比较简单的，下面记录使用Opencv工具包里的`haarcascade`进行识别的过程。

![]({{ site.qiniudn }}/images/2016012702.png)

<!-- more -->

{% highlight python %}
import matplotlib.pyplot as plt
%matplotlib inline
{% endhighlight %}

{% highlight python %}
import sys, cv2
imagePath = '3jpg.jpg'
image = cv2.imread(imagePath)
# plt.imshow(image)
# plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
{% endhighlight %}


{% highlight python %}
faceCascade = cv2.CascadeClassifier('F:\BaiduYunDownload\opencv\sources\data\haarcascades\haarcascade_frontalface_default.xml')

gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
# plt.imshow(gray)
faces = faceCascade.detectMultiScale(
    gray,
    scaleFactor=1.1,
    minNeighbors=5,
    minSize=(30,30),
    flags=cv2.CASCADE_SCALE_IMAGE)
print faces

{% endhighlight %}

    [[401  26  91  91]
     [ 47  26 108 108]
     [238  44  60  60]]
    


{% highlight python %}
import random
font = cv2.FONT_HERSHEY_SIMPLEX
for (x, y, w, h) in faces:
    cv2.rectangle(image, (x, y), (x+w, y+h), (14, 201, 255), 2)
    cv2.putText(image, str(random.randrange(20, 30)), (x+(w/2)-18, y-10), font, 1,(14, 201, 255), 2)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
{% endhighlight %}



![]({{ site.qiniudn }}/images/2016012701.png)

