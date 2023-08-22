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

# [Kotlin] 뷰 바인딩(View Binding)이란?



* toc
{:toc}






## 📌 View Binding이란?

- 뷰 바인딩을 사용하면 뷰와 상호작용하는 코드를 쉽게 작성할 수 있다. 
- 뷰 바인딩을 허용하면 각 Layout마다 바인딩 클래스를 자동으로 생성하는데, Layout에 ID가 있는 뷰에 직접 참조를 할 수 있다. 
- 대부분의 경우 뷰 바인딩은 **`findViewById`**를 대체한다.



## 👍🏻 View Binding의 장점

1. View를 직접 참조하기 때문에 **없는 id를 참조할 일이 없다.** 또한 이 과정에서 **Null Pointer Exception이 발생하지 않는다.**
2. View에 잘못된 타입을 지정할 때 생기는 **Class Cast Exception이 발생하지 않는다.**
3. 코드의 **가독성**이 올라간다.



## 🤔 `FindViewById`와의 차이점

### 1. 보일러 플레이트 코드 개선

- `findViewById`를 사용하면 뷰를 참조할 때 다음과 같은 코드를 사용한다.

```kotlin
val content = findViewById<TextView>(R.id.tv_content)
```

- 뷰의 개수가 적을 때는 못느꼈겠지만 개발을 진행하면서 뷰가 많아질 수록 코드가 너무 길어지는 단점이 있다.

- 하지만 **뷰 바인딩**을 사용하게 되면 **변수선언 없이 바로 뷰에 접근**할 수 있기 때문에 상당한 이점이 있다!

### 2. null 안정성

- `findViewById`를 사용할 개발자가 뷰의 id를 잘못작성해 **NPE(NullPointerException)**이 발생하는 단점이 있다.
- 하지만 **뷰 바인딩**의 경우에는 직접 뷰의 참조를 생성하므로  **NPE(NullPointerException)**이 **발생하지 않는다**는 이점이 있다!

### 3. 유형 안전

- 바인딩 클래스(ActivityMainBinding)의 필드 유형은 XML의 뷰와 완전히 일치한다. 그렇기 때문에 **Class Cast Exception** 이 발생할 위험이 없다는 장점이 있다.