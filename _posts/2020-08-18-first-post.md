---
title: "LBS 프로젝트 개발 정리(Android)"
date: 2020-08-18
categories: jekyll update
---


## LBS 프로젝트 개발 정리(Android) 

### 1. 전체로직

1. 주기적 위치추적(Foreground service start) -> 실시간 위치추적을 통한 간접적 진입 확인(Geofence)
2. 실시간 위치추적을 통한 직접적 진입 확인(JTS Library)
3. 기기 내 측정을 통한 정확성 확보(WiFi scanning)

### 2. 이슈사항

1. 비콘(Beacon) 사용 불가
개발 시 Bluetooth 사용 불가능하여 정밀한 위치추적이 불가능
2. 지속적인 안드로이드 정책 변경으로 인한 Background service 사용 불가
3. Google 사 제공 Geofence API 는 원형 도형 드로잉만 제공 

### 3. 해결방안

1번 이슈는 WiFi의 2.4G와 5G를 혼합 사용하는 방안과 JTS 라이브러리 사용으로 대체
2번 이슈는 Foreground Service 사용(상단바 아이콘은 해결 불가) Foreground service에서 상단 notification 을 지속적으로 날리고, 사용자에게 보여지는 단을 Kill.
3번 이슈는 1번 이슈와 동일하게 JTS 라이브러리를 활용하는 방안으로 대체 *1)

*1) Geofence API 를 임의로 조절하더라도, 다각형의 모양이 복잡할 경우 이슈가 발생할 가능성이 있음. 現 프로젝트에서는 경계선 내부로 진입했을 시에만(Within) 작동하도록 되어있으나, 경계선 포함 시 Ray-casting algorithm 을 사용해야 함.

* Ray-casting(광선투사) 알고리즘 참고[https://woowabros.github.io/experience/2018/03/31/hello-geofence.html](https://woowabros.github.io/experience/2018/03/31/hello-geofence.html)

참고: 백준 지민이의 테러 문제(Ray-casting algorithm)
[https://velog.io/@skyepodium/%EB%B0%B1%EC%A4%80-1688-%EC%A7%80%EB%AF%BC%EC%9D%B4%EC%9D%98-%ED%85%8C%EB%9F%AC-%EB%A0%88%EC%9D%B4-%EC%BA%90%EC%8A%A4%ED%8C%85-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%8B%A4%EA%B0%81%ED%98%95-%EB%82%B4%EB%B6%80-%EC%99%B8%EB%B6%80-%ED%8C%90%EB%B3%84](https://velog.io/@skyepodium/%EB%B0%B1%EC%A4%80-1688-%EC%A7%80%EB%AF%BC%EC%9D%B4%EC%9D%98-%ED%85%8C%EB%9F%AC-%EB%A0%88%EC%9D%B4-%EC%BA%90%EC%8A%A4%ED%8C%85-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%8B%A4%EA%B0%81%ED%98%95-%EB%82%B4%EB%B6%80-%EC%99%B8%EB%B6%80-%ED%8C%90%EB%B3%84)