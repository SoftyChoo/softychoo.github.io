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

# [Android/Kotlin] Sealed Class란?



* toc
{:toc}
##### 오늘은 자바엔 없고 Kotlin만 있는 Sealed Class에 대해 알아보겠다. 



먼저 코틀린 공홈에서 말하는 Sealed Class를 알아보자.

[[ Kotlin : Sealed classes and interfaces ]](https://kotlinlang.org/docs/sealed-classes.html) 

> - sealed class와 인터페이스는 상속에 대한 더 많은 제어를 제공하는 제한된 클래스 계층을 나타낸다. 
> - sealed class의 모든 직접 하위 클래스는 컴파일 시간에 알려진다. 
> - sealed class가 있는 모듈이 컴파일된 후에는 다른 하위 클래스가 나타날 수 없다. 
> - 예를 들어 타사 클라이언트는 코드에서 sealed class를 확장할 수 없다. 
> - 따라서 sealed class의 각 인스턴스에는 이 클래스가 컴파일될 때 알려진 제한된 집합의 유형이 있다. 
> - sealed interface와 그 구현에 대해서도 동일하게 작동한다. 
> - sealed interface가 있는 모듈이 컴파일되면 새 구현이 나타날 수 없다. 
> - 어떤 의미에서 sealed class는 enum class와 유사하다. 
> - 열거형 유형에 대한 값 집합도 제한되지만 각 열거형 상수는 단일 인스턴스로만 존재하는 반면 sealed class의 하위 클래스에는 각각 고유한 속성이 있는 여러 인스턴스가 있을 수 있다.

위의 내용과 추가적으로 조사하고 사용한 경험을 바탕으로 정리를 해보겠다.



<br/>



## Sealed Class란?

- **`Sealed Class`**는 다른 클래스가 상속을 받지 못하도록 제한한다.
  - 따라서 **`sealed class`**의 하위 클래스는 **`sealed class`**의 내부에서 정의되어야 한다.

  - 상속을 제한하기 때문에 유한한 개수의 하위 클래스를 가지게 된다.

- 클래스 계층 구조에서 제한된 개수의 클래스를 나타낼때 사용한다.

- **`enum class`**를 확장한 개념으로 볼 수 있으며, **`enum class`**와 달리 인스턴스를 여러 개 생성할 수 있다.



<br/>



## Sealed Class의 장점

- 코드 안정성 향상
  - 컴파일 타임에 모든 하위 클래스를 확인하고 사용할 수 있기 때문에 런타임에서 예상치 못한 동작을 방지하여 코드 안정성을 향상시킨다.

- 가독성 향상
  - sealed class를 사용하면 클래스 계층 구조가 명확해 지기 떄문에 코드의 가독성이 향상되고 유지보수성이 향상된다.

- 패턴 매칭
  - 패턴 매칭은 일반적으로 타입이 서로 다른 값들을 패턴으로 지정하고, 해당 값이 각각 어떤 타입인지 판별하는 기능이다. 이를 통해 코드를 간결하고 가독성 높게 작성할 수 있다.
  - 일반적인 클래스나 인터페이스일 경우 패턴 매칭을 진행할 때, 패턴 추가 후 타입에 대한 분기를 추가해주어야 하지만 `sealed class`를 활용한 경우에는 상속계층 내부에서 패턴 매칭이 가능하기 때문에 모든 하위 클래스에 대한 분기를 명시적으로 작성하지 않아도 된다. 

