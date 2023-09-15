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

# [Android/Kotlin] ViewModel Factory

* toc
{:toc}




[ListAtapter(Developer)](https://developer.android.com/reference/androidx/recyclerview/widget/ListAdapter)

## 📌 ViewModel Factory?

- ViewModel을 생성하는데 도움을 주는 Class이며 의존성 주입을 가능하게 한다.
- ViewModel인스턴스를 생성할 때 특정한 설정 및 초기화를 수행하는데 사용된다.



## 🤔 사용하는 이유?

ViewModel에 의존성을 주입할 수 있고 커스텀을 통해 ViewModel을 생성 할 때 다양한 초기 설정을 지정해 줄 수 있다.

이는 확장성, 유지보수성, 분리 면에서 다양한 이점을 가져갈 수 있게된다.



## 👨🏻‍💻 사용

나는 TodoList에서 id값을 넘겨주는 것으로 사용하였는데 코드는 다음과 같다.

```kotlin
class TodoViewModel(private val idGenerate: AtomicLong) : ViewModel() {
}
```

- ViewModel의 생성자에 넘겨줄 값을 선언해주었다.

```kotlin
class TodoViewModelFactory(private val idGenerate: AtomicLong) : ViewModelProvider.Factory {

    // ViewModelProvider.Factory 인터페이스를 구현하기 위해 create 메서드를 오버라이드
    // 이 메서드는 ViewModel 인스턴스를 생성하는 역할을 함
    override fun <T: ViewModel> create(modelClass: Class<T>): T {
    // create 메서드는 요청된 ViewModel 클래스 (modelClass)를 기반으로 ViewModel을 생성한다.

        if(modelClass.isAssignableFrom(TodoViewModel::class.java)){// 요청된 modelClass가 TodoViewModel Class와 호환 가능한지 확인
            return TodoViewModel(idGenerate) as T //호환되는 경우 생성된 ViewModel을 T타입으로 형변환 하여 반환
        }
        throw IllegalArgumentException("Not Found ViewModel class.")// 호환되지 않는 경우 알림
    }
}
```

- 그 이후 ViewModel Factory를 만든 이후

```kotlin
    private val viewModel: TodoViewModel by viewModels {TodoViewModelFactory(AtomicLong(1L))}
```

- Fragment의 ViewModel 과 연결해주었고 이를 통해 원하는 형태로 파라미터를 넘겨줄 수 있다.

