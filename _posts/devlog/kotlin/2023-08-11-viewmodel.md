---
layout: post
title: kotlin
image: /assets/img/kotlin_img/kotlin.png
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
 - kotlin






---

# [Android JetPack] View ßModel



* toc
{:toc}


먼저 ViewModel은 **MVVM ViewModel**과 **ACC ViewModel**로 나뉜다.



## MVVM ViewModel 이란?

#### 	MVVM패턴

- Design 패턴인 **MVVM** 패턴은 MVP 패턴에서 파생된 패턴으로 비즈니스 로직과 프레젠테이션 로직을 UI로 부터 **분리**시켜 **테스트, 유지보수, 재사용등을 용이**하게 하는것이 주 목적이다.
- **MVVM** 패턴에는 **모델, 뷰 및 뷰 모델**의 세 가지 핵심 구성 요소가 있다. 각 구성 요소는 다른 용도로 사용된다.



![MVVM 패턴](https://learn.microsoft.com/ko-kr/dotnet/architecture/maui/media/mvvm-pattern.png)

- 세 구성 요소 간의 관계를 보여 주는 다이어그램

#### 	View Model

- MVVM 패턴의 구성요소 중 ViewModel은 공통 속성 및 명령을 표시하는 뷰의 추상화 이다. 다르게 말하면 View와 Data Binder 사이의 통신을 조정한다.



## AAC ViewModel 이란?

- 공식 문서에 적혀있길 AAC ViewModel 클래스는 수명 주기를 고려하여 UI 관련 데이터를 저장하고 관리하도록 설계되었다고 한다. 
- AAC ViewModel 클래스를 사용하면 화면 회전과 같이 구성을 변경하는 경우에도 데이터를 유지할 수 있다.

![활동 상태 변경에 따른 ViewModel의 수명 주기를 나타내는 그림](https://developer.android.com/static/images/topic/libraries/architecture/viewmodel-lifecycle.png?hl=ko)

- 결론적으로 APP 의 LifeCycle을 고려하여 UI관련 데이터를 저장하고 관리하는 역할을 한다.

- AAC ViewModel 객체의 범위는 ViewModel을 가져오는 경우 ViewModel Provider에 전달되는 생명주기로 지정된다. 
- 그러므로 ViewModel은 생명주기가 영구적으로 종료되는 시점까지 메모리에 남아있게 된다.