---
title: "AWS 활용 STUN, TURN 서버 구축"
date: 2020-04-21
categories: jekyll update
---

## 1. 개요

WebRTC 기반 다대다 화상 서비스 개발을 위한 STUN, TURN Server 구축

### 1) STUN Server

STUN Client이 자신의 공인 IP 주소 확인을 위해 STUN server 에 요청 STUN Server 가 응답하는 형태. STUN Server에서 클라이언트의 공인 주소와 클라이언트의 사설 주소를 비교하여 리턴(STUN Client 는 VoIP 시그널링 시 공인 IP주소 사용)

STUN Client(사설망 위) ⇒ 호스트 주소(단말 주소)
STUN Server(인터넷망 위) ⇒ Mapped Address 를 응답(Client 에서 SIP 과 RIP 에 사용)

### 2) TURN Server

TURN Server 는 미디어 릴레이 관련 문제 해결 시 사용(외부에 있는 사람들과 화상 통화를 하는 경우)
STUN 과 요청-응답 형태가 거의 유사하나 NAT 장비가 TURN 응답 메세지를 클라이언트의 사설 주소로 전송 가능
** 쉽게 생각해서 두 단말이 서로 다른 NAT 에 있을 경우, TURN 에게 권한 요청을 한다(바인딩)

#### * STUN SERVER 와 TURN SERVER 가 필요한 CASE

1. 서버 : 공인아이피 / 클라이언트1 : NAT / 클라이언트2 : NAT->  STUN 서버를 사용
  
2. 서버 : NAT / 클라이언트1 : NAT / 클라이언트2 : NAT  
-> TURN 서버를 사용 (복잡)  
  
3. 서버 : 로컬네트워크 / 클라이언트1 : 로컬네트워크 / 클라이언트2 : 로컬네트워크  
->  STUN / TURN 서버 필요 X
  
  **Example)
서버 위치 : 사설 IP (공유기를 통해 포트포워딩 하여 외부 접속 사용중)  
클라이언트1 : LTE 망 사용중  
클라이언트2 : 사설 IP (서버 위치와 다른 네트워크)
#### ※ ※ ※ NAT 환경의 Peer 주소 확인이 불가하므로 화상 통화 불가

### 3) ICE

두 단말이 서로 통신할 수 있는 최적의 경로를 찾는 프레임워크
STUN 과 TURN 프레임워크로 확보된 통신 가능 여러 IP와 포트넘버를 상대방에게 전송

