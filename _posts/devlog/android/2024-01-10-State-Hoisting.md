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
 - android















---

# [Android Jetpack Compose] State Hoisting

{:toc}

![jetpack_compose](../../../assets/img/blog/jetpack_compose.png)

**💡 일반적으로 여러 함수에서 읽거나 수정하는 `상태`는 공통적인 상위항목에 있어야한다.**



<br/>



Stateful & Stateless를 알아볼 때 Codelabs에서 상태를 끌어올린다는 State Hoisting을 보았는데 조금 더 자세히 알아보자 :)



<br/>



먼저 코드랩과 Developer의 설명을 봐보자

[[ Codelabs ]](https://developer.android.com/codelabs/jetpack-compose-state?hl=ko&continue=https%3A%2F%2Fdeveloper.android.com%2Fcourses%2Fpathways%2Fcompose%3Fhl%3Dko%23codelab-https%3A%2F%2Fdeveloper.android.com%2Fcodelabs%2Fjetpack-compose-state#8) [[ Developer ]](https://developer.android.com/jetpack/compose/state?hl=ko)

> **`remember`**를 사용하여 객체를 저장하는 컴포저블에는 내부 상태가 포함되어 있어 컴포저블을 **스테이트풀(Stateful)**로 만듭니다. 이는 호출자가 상태를 제어할 필요가 없고 상태를 직접 관리하지 않아도 상태를 사용할 수 있는 경우에 유용합니다. 그러나 **내부 상태를 갖는 컴포저블은 재사용 가능성이 적고 테스트하기가 더 어려운 경향이 있습니다**.
>
> **상태를 보유하지 않는 컴포저블을 스테이트리스(Stateless) 컴포저블이라고 합니다**. 상태 호이스팅을 사용하면 **스테이트리스(Stateless)** 컴포저블을 쉽게 만들 수 있습니다.

> Compose에서 **상태 호이스팅은 컴포저블을 스테이트리스(Stateless)로 만들기 위해 상태를 컴포저블의 호출자로 옮기는 패턴**입니다. Jetpack Compose에서 상태 호이스팅을 위한 일반적 패턴은 상태 변수를 다음 두 개의 매개변수로 바꾸는 것입니다.
>
> - **value: T** - 표시할 현재 값입니다.
> - **onValueChange: (T) -> Unit** - 값을 변경하도록 요청하는 이벤트입니다. 여기서 T는 제안된 새 값입니다.
>
> 여기서 이 값은 수정할 수 있는 모든 상태를 나타냅니다.
>
> 상태가 내려가고 이벤트가 올라가는 패턴을 단방향 데이터 흐름(UDF)이라고 하며, 상태 호이스팅은 이 아키텍처를 Compose에서 구현하는 방법입니다. 자세한 내용은 [Compose 아키텍처 문서](https://developer.android.com/jetpack/compose/architecture?hl=ko#udf-compose)를 참고하세요.
>
> 이러한 방식으로 끌어올린 상태에는 중요한 속성이 몇 가지 있습니다.
>
> - **단일 소스 저장소:** 상태를 복제하는 대신 옮겼기 때문에 소스 저장소가 하나만 있습니다. 버그 방지에 도움이 됩니다.
> - **공유 가능함:** 끌어올린 상태를 여러 컴포저블과 공유할 수 있습니다.
> - **가로채기 가능함:** 스테이트리스(Stateless) 컴포저블의 호출자는 상태를 변경하기 전에 이벤트를 무시할지 수정할지 결정할 수 있습니다.
> - **분리됨**: 구성 가능한 스테이트리스(Stateless) 함수의 상태는 어디에든(예: ViewModel) 저장할 수 있습니다.

추가적인 내용을 공식 사이트를 참고해보자



<br/>



위의 데이터를 바탕으로 State Hoisting을 정리해보자면

- State Hoisting 은 자신이 가지고 있는 상태를 부모 Composable 로 넘겨주어 자기 자신을 Stateless Composable로 바꾼다는 뜻
- remember을 사용하여 Stateful을 사용하면 재사용성 및 테스트 문제가 있어, 상태 호이스팅을 통해 stateless 형태로 사용하는것을 권장한다.

**State Hoisting 를 사용하는 목적은 `**단반향 데이터 흐름 구조**` 를 가지는 것**

- `Caller가 Composable 함수의 상태를 알필요가 없다면 Hosting할 필요 없음`

<img src = "https://developer.android.com/static/images/jetpack/compose/state-unidirectional-flow.png?hl=ko" width = 50%>

**`단반향 데이터 흐름 구조` 는 아래 매커니즘으로 동작한다.**

- 단방향 데이터 흐름을 사용하는 앱의 

  업데이트 루프

  - 이벤트 : UI 일부가 이벤트를 만들어 위쪽으로 전달, 앱의 다른 레이어에서 이벤트 전달
  - 상태 업데이트 : 이벤트 핸들러가 상태를 바꿀 수도 있다
  - 상태 표시 : 상태 홀더가 상태를 아래로 전달하고 UI가 상태를 표시한다

- `자식 Composable` 이 이벤트를 수신하여 `부모 Composable` 에게 전달

- `부모 Composable` 은 `자식 Composable`로 부터 전달받은 이벤트를 처리하고 상태를 업데이트하여 `자기 자신`과 `자식 Composable` 을 `재구성`하여 UI 업데이트

**`단반향 데이터 흐름 구조` 를 사용함으로서 얻는 이점**

- `테스트 가능성` : 상태를 관리하는 코드와 상태를 이용하여 화면을 구성하는 코드를 `분리`함으로써 `테스트 용의성` 증가
- `상태 캡슐화` : 상태를 관리하는 코드를 한 곳에서 `관리`함으로써 UI가 복잡해진다 하여도 `버그가 발생할 확률` 감소
- `UI 일관성` : 관찰 가능한 상태를 사용하여 상태가 변경하게 되면 그 `즉시 UI가 업데이트` 됩니다.

