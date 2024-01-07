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

# [Android/Kotlin] Data Class



* toc
{:toc}


## **데이터 클래스(Data Class)**

- 코틀린의 **데이터 클래스(Data Class)는 데이터를 다루는데 최적화된 클래스**로 **데이터를 보관**하는 것이 주 목적인 클래스이다. 

- 데이터 클래스는 다양한 멤버함수가 자동으로 제공되는데 이는 개발자들이 매우 편리하게 쓸만한 메소드임으로 데이터클래스를 사용한다면 코드 양을 대폭 줄이고 클린 코드를 더욱 편리하게 구현할 수 있다는 장점이 있다.

#### Data Class 생성시 자동으로 제공되는 함수들

- `toString()`
- `equals()`/`hashCode()`
- `copy()`
- `componentsN()`

#### Data Class가 충족해야 할 요구사항

- 기본 생성자에는 최소한 하나의 매개변수가 있어야 한다.
- 모든 기본 생성자 매개변수는 `val`또는`var` 로 표시되어야 한다.
- 데이터 클래스는 `abstract`, `open`, `sealed`, `inner` 일 수 없다.

이 함수들은 코딩에서 캡슐화를 위해 필수적이지만 자바에서 사용할 때 코드를 생성해줘야하는 번거로움이 있다.



## Data Class 생성

```kotlin
data class Animals(
    val name: String,
    val age: Int
)
```

- 다음과 같은 형식으로만 적어주면 전에 자바에서 사용하던 `getName`, `setName`, `toString`구현 등을 건너뛰고 짧은 코드하나로 구현이 가능하다.

```kotlin
fun main() {
    val tiger = Animals("Ruru", 3)
    val cat = Animals("Mao", 2)
}
```

- 그리고 다음과 같이 데이터 클래스 객체를 생성해서 사용하면 된다.



## toString()

```kotlin
println(tiger)
```

```kotlin
//Animals(name=Ruru, age=3)
```



- 객체를 생성한 뒤 출력을 해보면 프로퍼티 값들이 바로 출력되는 것을 볼 수 있는데 이는 toString()이 구현되어있기 때문이다.



## hashCode() & equals()

##### hashCode()

```kotlin
val cat1 = Animals("Mao", 1)
val cat2 = Animals("Mao", 1)
println(cat1.hashCode())
println(cat1.hashCode())
```

```kotlin
2390566
2390566
```

- 두개의 객체를 프로퍼티값을 같게 만들고 hashCode()를 실행시키면  
- 일반 Class라면 다른 값을 갖게 되는 반면에  Data Class 는 두 객체의 해쉬코드 값이 같은 값을 출력하는것을 볼 수 있다.

##### equals()

```kotlin
val cat1 = Animals("Mao", 1)
val cat2 = Animals("Mao", 1)
val cat3 = Animals("Yeang",2)

println(cat1 == cat2) // 두 객체으 프로퍼티 완전히 같음
println(cat2 == cat3) // 두 객체의 메모리주소 다름

```

```kotlin
true
false
```

- `==` 연산자로 두 객체가 동일한 값을 가지고 있는지를 검사할 수 있다.



## copy()

```kotlin
val tiger2 = tiger.copy(name = "Meme")
println(tiger2)
```

```kotlin
//Animals(name=Meme, age=3)
```

- copy() 메소드를 바로 사용할 수 있는데 전체가 아닌 특정 필드값만 변경해주기 편리한 메소드이다.



## componentN()

Data Class 는 기본적으로 **`componentN()` 메소드가 생성** 되기 때문에, 각 프로퍼티에 번호가 붙어 다음과 같이 **구조 분해(Destructuring Declarations)가 가능하다.** 

```kotlin
val cat1 = Animals("Mao", 1)
val (name,age) = cat1
println(name)
println(age)
```

```kotlin
Mao
1
```

- 다음과 같이 cat1 객체의 프로퍼티를 편리하게 분해했다.
- 각 프로퍼티들은 선언 순서에 따라 번호를 갖게 되는데 분해 후 멤버를 확인해보면 메소드가 다음과 같이 생성되어 있는것을 확인할 수 있다.

```kotlin
val name = cat1.component1()
val age = cat1.component2()
```

- 따라서 `val (name,age) = cat1`이렇게만 적어도 위의 코드에 대한 동작을 구현해준다.

##### 

##### 따라서 Data Class는  보일러플레이트(boilerplate) Code도 줄일 수 있어 매우 편리하고 일반 클래스에 비해 다양한 장점을 가지고있어 데이터를 다루기 너무 좋은 클래스이기 때문에 다들 DataClass를 유용하게 잘 활용해보자! :)

