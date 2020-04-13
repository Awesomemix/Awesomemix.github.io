---
title: "안드로이드 HandlerThread 스레드"
date: 2017-10-20 08:26:28 -0400
categories: jekyll update
---

HandlerThread 는 UI와 관련없지만 단일스레드에서 순차적인 작업이 필요할 때 사용한다.
(ex. 상태가 바뀔 때 마다 스레드를 생성해서 DB에 반영할 경우, 해당 작업의 순서가 중요)

Example code

​```
HandlerThread handlerThread = new HandlerThread("ht");
handlerThread.start();
Looper looper = handlerThread.getLooper();
Handler handler = new Handler(looper);
context.registerReceiver(receiver, filter, null, handler);
​```

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
