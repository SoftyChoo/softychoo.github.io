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

# [Android/Kotlin] lateinit vs by lazy 확실히 알고가기

* toc
{:toc}


**💡 Java에선 초기화 없이 선언만 하게되면 변수에 기본적으로 값이 들어가게 된다. 만약 초기화를 해주지 않는다면 자동으로 null값이 들어가게 된다.**



<br/>



**💡 하지만, 코틀린에선 초기화를 필수로 해야하기 때문에 값을 넣어주지 않으면 바로 오류가 뜨는것을 확인할 수 있다. 그래서 이런 상황엔 늦은 초기화를 사용해서 해결할 수 있다.**



<br/>



## 지연 초기화란?

- 지연 초기화란 말 그대로 객체를 늦게 초기화 하는것을 의미한다.
- 선언할 당시 초기화가 어려울 경우에 사용한다.
- 늦은 초기화는 **`lateinit`**과 **`by lazy`**로 나뉜다.



<br/>



## 📌 lateinit

- `lateinit`은 처음 선언 당시에 타입만을 설정하면 된다.
- 변수를 선언할때는 `var`로 선언이 가능하다.
- lateinit을 사용 후 초기화 없이 값을 사용하려 한다면 컴파일 단계에서 다음과 같은 오류가 뜨게된다.

```kotlin
Exception in thread "main" kotlin.UninitializedPropertyAccessException: lateinit property test has not been initialized
```

📌 **lateinit의 경우 무조건 `var`을 사용해야 하며, Primitive Type (Int, Float, Double, Long 등) 에는 사용할 수 없다.**



<br/>



## 📌 by lazy

- `by lazy`는 의존하는 값이 초기화 된 이후에 값을 채워넣고 싶을때 사용한다. 
- 어떤 말인지 코드를 통해 알아보자

```kotlin
lateinit var text: String
val textLength: Int by lazy {
    text.length
}

text = "by_lazy_test"
println(textLength)
```

- 위의 코드를 보게되면 textlength를 당장 초기화 할 수 없기 때문에 by lazy를 통해 늦은 초기화를 선언해두고 text가 초기화 된 이후에 초기화가 진행되도록 하였다.
- **즉, 그 변수가 호출될 시점에 초기화가 되도록 한다.**



<br/>



- 추가적으로 by lazy를 사용했던 코드를 하나만 더 살펴보자면

```kotlin
private val listAdapter by lazy {
    BookmarkListAdapter { position, item ->
        viewModel.removeBookmarkItem(position)
        sharedViewModel.updateTodoItem(item)
    }
}
```

- listAdapter가 BookmarkListAdapter로부터 이벤트가 발생했을 경우에 listAdapter를 초기화 하도록 구현하였다.



<br/>



#### 마지막으로 정리를 해보자

- 공통적으로는 `lateinit`과 `by lazy` 모두 늦은 초기화를 위해 사용한다.
- 차이점으론
  - lateinit : 값 변경 가능 (`var`) - 초기화 이후 값을 변경해서 사용하려 할 때
  - by lazy : 값 변경 불가능(`val`) - 초기화 이후 읽기 전용으로 사용하려 할 때



<br/>



최근 lateinit과 bylazy의 차이를 말 할 상황이 생겼었다. 간단한 개념이였지만 갑자기 말하려니 늦은 초기환데.. 라고만 머릿속에 맴돌아서 결국 확실하게 대답하지 못했다.. ㅋㅋㅋ

이제 쉬운 개념들도 하나씩 개념정리를 해가며 완전한 내것으로 만들어야겠다 ㅎㅎ :)