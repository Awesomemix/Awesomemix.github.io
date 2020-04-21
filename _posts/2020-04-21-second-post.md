---
title: "Using Firestore"
date: 2020-04-21
categories: jekyll update
---

### 1. 개요

<hr>
<br>

시간 리스너를 통해 클라이언트 애플리케이션 간에 데이터의 동기화를 유지하고 모바일 및 웹에 대한 오프라인 지원을 제공해 네트워크 
지연 시간이나 인터넷 연결에 상관없이 원활하게 반응하는 앱을 개발할 때 사용하는 NoSql이라고 firestore 공식 문서에 기재되어있다.

<br>

일반적으로 다음과 같이 불러서 사용한다.

{% highlight java %}

collection(Collection 이름).document().
set(입력할데이터).addOnCompleteListener{
// TODO: Write your code here.
}

{% endhighlight %}

<br>
<br>
<br>

_the end_
