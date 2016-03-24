---
layout: post
title: '"Large Scale Deep Learning for Predictive Tasks" from Jeff Dean'
description: "Large Scale Deep Learning for Predictive Tasks"
keywords: "Jeff, ML, Google, DL, NLP, word2vec"
category: 机器学习
tags: [Jeff, ML, Google, DL, NLP, word2vec]
---

Video Link：[http://www.56.com/u86/v_MTI4NzUyOTYz.html](http://www.56.com/u86/v_MTI4NzUyOTYz.html) .  

Deep Learning已经火了很久，其中Google开源的word2vec的出现使得NLP在DL上又有了新了突破，Jeff Dean的这个讲座更多是分享这方面的内容，讲的是一些目前Google在文本处理上在预测、推荐上的一些大致框架，从中了解一下现在的研究状况跟巨头里的运用。

#### What is a Recommendation?

**Broad View**: Anything a computer can suggest to help a user.

#### What is Required for Good Recommendations?

- Context  
It's really important to understand what the user is doing for providing user what informations or what service at the particular time.  

<!-- more -->

- Understanding a user's surroundings  
![]({{ site.qiniudn }}/images/2014/11/3.jpg)

- Previous behavior of the user  

- Previous agrregatied behavior of many other users  
![]({{ site.qiniudn }}/images/2014/11/4.png)

- Textual understanding  
E.g.*A masterpiece of genre film-making. I felt like I was watching a long-lost Hitchcock classic (but one with all the sex and violence Hitch was only allowed to hint at). No spoilers. The less you know about the story going in, the more you'll enjoy it. Fans of the novel are in for an impeccable and precise adaptation of the source material. Fincher nails the tone and sustains it effortlessly for the entire running time.*

#### General Machine Learning Approaches

- Learning by labeled example: *supervised learning*  
	* e.g. An email spam detector
	* amazingly effective if you have lots of examples

- Discovering patterns: *unsupervised learning*  
	* e.g. data clustering
	* difficult in practice, but useful if you lack labeled examples

- Feedback right/wrong: reinforcement learning  
	* e.g. learning to play chess with "partial/implicit information"
	* works well in some domains, ad system / black jack agent

#### Machine Learning

* For many of these these problems, we havd lots of data
* Want techniques that minimize software engineering effort  
	* simple alogrithms, teach computer how to learn from data
	* don't spend time hand-engineering algorithms or high-level features from the raw data

#### What is Deep Learning

* The modern reicarnation of Artificial Neural Networks from the 1980s and 90s.
* A collection of simple trainable mathematical units, which collaborate to compute a complicated function.
* Compatible with supervised, unsupervised, and reinforcement learning.
* Loosely inspired by what (little) we know about the biological brain.
* Higher layers form higher levels of abstraction.  
![]({{ site.qiniudn }}/images/2014/11/5.jpg)

#### Neural Networks

* Learn a complicated function from data.
* Different weights compute different functions.

$$y_i= \left ( \sum_{i} w_ix_i\right )$$

![]({{ site.qiniudn }}/images/2014/11/7.jpg)  
![]({{ site.qiniudn }}/images/2014/11/8.png)

* While not done  
	* pick a random training case **(x, y)**  
	* run neural network on input **x**  
	* modify connection weight to make prediction closer to **y**

#### How to modify connections?

* Follow the gradient of the error w.r.t. the connections  
![]({{ site.qiniudn }}/images/2014/11/9.png)  

#### What can neural nets compute?

* Human perception is very fast (0.1 second)  
	* Recognize objects ("see")
	* Recognize speech ("hear")
	* Recognize emotion
	* Instantly see how to solve different problems
	* And many more!

* **Anything humans can do in 0.1 sec, the right big 10-layer network can do too**

#### Functions Artificial Neural Nets Can Learn

* Image recognition
* Speech recognition
* Recommendation
* Translations

#### Research Objective: Minimizing Time to Results

* We want results of experiments quickly
* "**Patience threshold**": No one wants to wait more than a few days or a week for a result  
	* Significantly affects scale of problems that can be tackled
	* We sometimes **optimize for experiment turnaround time**, rather than absolute minimal system resources for performing the experiment
* Train in a day what takes a single GPU card 6 weeks

#### How Can We Train Big Nets Quickly?

* Exploit many kinds of parallelism  
	* Model parallelism
	* Data parallelism

* Model Parallelism: Partition model across machines

![]({{ site.qiniudn }}/images/2014/11/10.png) 

* Data Parallelism: Asynchronous Distributed Stochastic Gradient Descent

![]({{ site.qiniudn }}/images/2014/11/11.png) 

#### Plenty of Data

* **Text**: trillions of words of English + other languages
* **Visual**:billions of images and videos
* **Audio**:thousands of hours of speech per day
* **User activity**: queries, result page cliks,, map requests, etc.
* **Knowledge graph**:billions of labelled relation triples
* ...

#### Applications

* Acoustic Modeling for Speech Recognition  
![]({{ site.qiniudn }}/images/2014/11/12.png)

* Convolutional Models for Object Recognition  
![]({{ site.qiniudn }}/images/2014/11/13.png)

* Deep Nets: Learning by exampe.  
![]({{ site.qiniudn }}/images/2014/11/14.png)  

* Works in practice  
![]({{ site.qiniudn }}/images/2014/11/17.png)  
![]({{ site.qiniudn }}/images/2014/11/18.png) 

#### What do I mean by sparse input data?

* **One version: Unstructured**  
10 million dimensional vector with a handful of non-zeros  
|0|0|0|0.2|0|0.7|0|0|0|...|...|  
`query = "palo alto restaurants"`  
A bag of tokens, possibly with scalar weights

* **Reality is often richer: Structured**  
A collection of strings, bags, one-hot encodings, tuples  
`query = "recommendation systems"`  
`keywords = {machine, learning, jobs}`  
`language = EN-US`  
`previous queries = ...`  

#### How can DNNs Possibly deal with sparse data?

**Answer: Embeddings**

~1000-D joint embedding space  
![]({{ site.qiniudn }}/images/2014/11/19.png) 

#### How Can We Learn the Embeddings?

![]({{ site.qiniudn }}/images/2014/11/20.png) 

#### Nearest neighbors in language embeddings space are closely related semantically.

* Trained skip-gram model on Wikipedia corpus.

![]({{ site.qiniudn }}/images/2014/11/21.png) 

#### Solving Analogies

* Embedding vectors trained for the language modeling task have very interesting properties (especially the skip-gram model_.

$$E(hotter) - E(hot) + E(bigger) \approx  E(big)$$

$$E(Rome) - E(Italy) + E(Germany) \approx E(Berlin)$$

Skip-gram model w/ 640 dimensions trained experiments achieves 57% accuracy for analogy-solving.

#### Visulizing the Embedding Space

![]({{ site.qiniudn }}/images/2014/11/22.png)  
![]({{ site.qiniudn }}/images/2014/11/23.png) 

#### Can We Embed Longer Pieces of Text?

![]({{ site.qiniudn }}/images/2014/11/24.png)

* Query similarity
* Machine translation
* Question answering
* Natural language understanding

![]({{ site.qiniudn }}/images/2014/11/25.png)  
![]({{ site.qiniudn }}/images/2014/11/26.png)

#### Paragraph Vectors: Embeddings for long chunks of text.

![]({{ site.qiniudn }}/images/2014/11/27.png)

#### Paragrap Vector Model

![]({{ site.qiniudn }}/images/2014/11/28.png)  
*Details in* [Distributed Representations of Sentences and Documents](http://jmlr.org/proceedings/papers/v32/le14.pdf)

#### More:

[Deep Learning（深度学习）学习笔记](http://blog.csdn.net/zouxy09/article/details/14222605)  
[Google 开源项目 word2vec 的分析](http://www.zhihu.com/question/21661274)  
[深度学习word2vec笔记之基础篇](http://blog.csdn.net/mytestmy/article/details/26961315)  
[Deep Learning实战之word2vec](http://techblog.youdao.com/?p=915)


