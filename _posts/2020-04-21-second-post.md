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
<br>

#### 1) Document 임의 지정 방식

{% highlight python %}

collection(Collection 이름).document(Document 이름).
set(입력할데이터).addOnCompleteListener{
// TODO: Write your code here.
// 이 때 Document 이름을 지정하지 않으면 임의로 생성.
}

{% endhighlight %}

<br>

#### 2) runTransaction 방식

{% highlight python %}

runTransaction {
  transaction ->
    var result = transaction.get(database_path).toObject(datamodel)
    transaction.set(database_path, result)
}

fun runTransaction() {
        var tsDoc = firestore?.collection("User")?.document(
            "document1"
        )

        firestore?.runTransaction { transaction ->
            val userDTO = transaction.get(tsDoc!!).toObject(UserDTO::class.java)
            userDTO?.name - "ming"
            transaction.set(tsDoc, userDTO!!)
        }
    }

{% endhighlight %}
데이터 중복을 막기 위하여 경로를 미리 지정.

<br>

### 2. 이슈 사항

<hr>
<br>

프로젝트 진행 중 다음과 같이 코드를 작성하였을 때 그 리턴값이 들어오지 않았다. 다음은 해당 코드의 예시이다.


{% highlight java %}

for(QueryDocumentSnapshot document : task.getResult()){
//  TODO: test 시, 테스트 장소 내 비치된 wifi SSID 기입바람.
    value = document.getData().get("field").toString();
    value = "return_value";
}

{% endhighlight %}

<br>

<br>
<br>
<br>

_the end_
