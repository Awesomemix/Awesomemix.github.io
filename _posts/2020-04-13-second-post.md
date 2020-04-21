---
title: "안드로이드 HandlerThread 스레드"
date: 2017-10-20 08:26:28 -0400
categories: jekyll update
---

HandlerThread 는 UI와 관련없지만 단일스레드에서 순차적인 작업이 필요할 때 사용한다.
(ex. 상태가 바뀔 때 마다 스레드를 생성해서 DB에 반영할 경우, 해당 작업의 순서가 중요)

####Example code

{% highlight js  linenos %}
HandlerThread handlerThread = new HandlerThread("ht");

handlerThread.start();

Looper looper = handlerThread.getLooper();

Handler handler = new Handler(looper);

context.registerReceiver(receiver, filter, null, handler);
{% endhighlight %}


_The end_
