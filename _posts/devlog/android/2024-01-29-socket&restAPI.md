---
layout: post
title: kotlin
accent_image: 
  background: url('/assets/img/change_img/book.jpg') center/cover
  overlay: false
accent_color: '#fff'
theme_color: '#fff'
description: >
  kotlin
invert_sidebar: true
categories :
 - devlog	
 - android








---

# [Network] 소켓 통신과 rest API의 차이점



* toc
{:toc}




##### 오늘은 소켓통신과 rest API의 차이점에 대해 가볍게 알아보도록 하겠다.



<br/>



## Rest API와 소켓통의 차이



### 1) rest API(HTTP) 통신

- Rest API는 HTTP 통신으로 Client가 요청할때만 Server가 응답하여 데이터를 전송한다.
- 전송후엔 연결이 바로 종료된다.
- 따라서 HTTP 통신은 Client가 요청을 하는 경우에만 Sever가 응답하기 때문에 **`단방향 통신`** 이라고 할 수 있다.

#### 사용 및 장점

- 실시간 연결이 아니기 때문에 요청을 보내고 응답을 기다리는 어플리케이션 개발에 주로 사용된다.
- 비용 및 유지보수의 장점이 있다. 

HTTP 통신은 다음과 같은 **`HTTP 메서드`**를 사용하여 데이터를 통신한다. 

| METHOD | 역할 |
| ------ | ------------- |
| POST   | 리소스를 **`생성`**한다. |
| GET    | 리소스를 **`조회`**하고 해당 도큐먼트에 대한 **상세정보를 가져온다**. |
| PUT    | 리소스를 **`수정`**한다. |
| DELETE | 리소스를 **`삭제`**한다. |



<br/>



### 2) Socket 통신

- Server와 Client가 특정 포트를 통해 **실시간**으로 통신하는 방법이다.
- **`양방향 통신`**으로 서버에서도 클라이언트에 메시지를 보낼 수 있다.

#### 사용 및 장점

-  Http 통신과 달리 계속 연결을 유지하는 연결 지향형 통신이기 때문에 실시간 통신이 필요한 경우에 주로 사용된다.
-  실시간 채팅, 스트리밍 등에 용이하다.
