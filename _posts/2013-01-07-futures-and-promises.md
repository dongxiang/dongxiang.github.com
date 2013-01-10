---
layout: post
title: Futures and Promises 
category : functional_prograrmming
tags : [scala]
---
{% include JB/setup %}

参见[FUTURES AND PROMISES - A NEW TAKE ON CONCURRENCY IN SCALA 2.10](http://v.youku.com/v_show/id_XNDk5MzU0MTMy.html) 和 [SIP-14 - Futures and Promises](http://docs.scala-lang.org/sips/pending/futures-promises.html)。讲座的[slides链接](https://speakerdeck.com/heathermiller/futures-and-promises-in-scala-2-dot-10)。

Scala 2.10实现了SIP-14,也算是对现状清理： 现在五法八门的Future轮子太多了，SIP-14里面就列举了一大堆。比如Scala自己的，Akka的，twitter的，scalaz的。

Java里面的Future没有callback，用户只能调用future.isDone来确认状态。Scala就友好多了：

{% highlight scala linenos %}

val f: Future[List[String]] = future {
  session.getRecentPosts
}

f onComplete {
  case Right(posts) => for (post <- posts) render(post)
  case Left(t)  => render("An error has occured: " + t.getMessage)
}

{% endhighlight %}

这感觉不是在写scala，是在写javascrit嘛。 

通过combinators，代码可以更加简洁。 

{% highlight scala linenos %}
val rateQuote = future {
  connection.getCurrentValue(USD)
}
rateQuote onSuccess { case quote =>
  val purchase = future {
    if (isProfitable(quote)) connection.buy(amount, quote)
    else throw new Exception("not profitable")
  }
  
  purchase onSuccess {
    case _ => println("Purchased " + amount + " USD")
  }
}

{% endhighlight %}

可以写成

{% highlight scala linenos %}

val rateQuote = future {
  connection.getCurrentValue(USD)
}
val purchase = rateQuote map {
  quote => if (isProfitable(quote)) connection.buy(amount, quote)
           else throw new Exception("not profitable")
}
purchase onSuccess {
  case _ => println("Purchased " + amount + " USD")
}

{% endhighlight %}

其他combinator有map，filter，fallbackTo，fut，andThen，revocer，recoverWith， either等。

video的下半部分是讲execution context。通过implicit，可以指定不同的execution model，比如single thread execution pool。
