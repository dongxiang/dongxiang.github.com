---
layout: post
title: The Actor Model 
category : functional_prograrmming
tags : [actor]
---
{% include JB/setup %}

这篇文章是观看Channel 9 这个[Hewitt, Meijer and Szyperski: The Actor Model ](http://channel9.msdn.com/Shows/Going+Deep/Hewitt-Meijer-and-Szyperski-The-Actor-Model-everything-you-wanted-to-know-but-were-afraid-to-ask)视频以后的笔记。

视频是以Meijer采访Hewitt的模式进行的。Hewitt首先提出了actor是包含的下列3个要素的基本计算单元：

1. process
2. storage
3. communication

然后开始讨论上诉3个要素如何fit into mail box， message queue， concurrency等和Actor model紧密相关的概念。 这里讲了个笑话everything is an actor，then an actor has a mail box, while a mail box is an actor. Then a mail box needs a mail box. Kind of jumpping into the rabbit hole. 然后又扯到Axum。。。 

Hewitt定义了Actor收到message以后的行为

1. 创建新的actor
2. send message to actor with known address
3. designate what to do with next message 

Meijer 问第3点和continuation有么关系。答案是no。 

然后谈到actor处理message的模型，conceptually 1 message at 1 time，但是implementation可以做优化。 Meijer的下一个问题是actor发给自己的message能造成dead lock么？ no。这里提到了Future的概念，然后Future是种特殊的actor。 

Szyperski 问了第3点相关的问题，designate what to do with next message和创建一个新actor的区别。 解释很直白，designate what to do with next message是指当前actor的。

下面一个问题是address和actor的关系，他们是多对多的关系。然后address和identity是不同的。根据address无法知道underlay 有多少actor。举了google.com和背后server的例子。 

然后讨论了address如何获得的问题, 原则是必须保证address的integrity，不能随便把一个integer之类的cast成一个addrss。 Hewitt举例inside CLR和crosss machine如何做。Szyperski comment address等同于某种capability。 

理论上，在actor之间没有channel的概念，因为channel很heavy。message deliver的order不保证，所以message deliver at most once。 

然后讨论了nondeterminism和indeterminism。nondeterminism图灵模型没法子支持indeterminism。actor model是一个更加powerful的模型。 

然后讨论patri net和actor model的异同。 这时有人乱入，问了actor model里面synchronization的问题，actor model的语义就是同时只能处理一个message。 

接着讨论[arbiter](http://en.wikipedia.org/wiki/Arbiter_(electronics)). arbiter和仍硬币的方式不一样的地方是arbiter的输出是没有时间限制的，其产生输出的时间是依照概率曲线来的。 后面一个问题扯的更远了。。。

下一个问题是address如何被discover的问题。 

然后终于轮到Szyperski，问题是software component和actor model关系，是否complement之类的问题。然后扯到actor model的意义之类的问题，就扯到Godel's famous last words. 唉，几位牛又扯远了。

Hewitt提到了一个有意思的观点，assignment consider harmful, 尤其是many cores system。 

然后讨论inconsistence。 

最后一个问题是tail call。 

这个video太理论了。。 做了一半笔记不想做了，最后还是坚持下来了。 















