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

# [Android/Kotlin] Scope Function(let, run, with, apply, also)이란?



* toc
{:toc}


##### 프로젝트를 진행할 때 let, with, apply등을 자주 쓰는데 오늘은 이러한 Scope function(범위지정 함수)에 대해서 공부해보겠다.



<br/>



먼저 코틀린 공홈에서 말하는 Scope function을 알아보자.

[[ Kotlin : Scope functions﻿ ]](https://kotlinlang.org/docs/scope-functions.html) 

> Kotlin 표준 라이브러리에는 객체 컨텍스트 내에서 코드 블록을 실행하는 것이 유일한 목적인 여러 함수가 포함되어 있습니다. 제공된 람다 식이 있는 개체에서 이러한 함수를 호출하면 임시 범위가 형성됩니다. 이 범위에서는 이름 없이 개체에 액세스할 수 있습니다. *이러한 함수를 범위 함수* 라고 합니다 . 종류로는 `let` , `run`, `with`, `apply`, `also`의 5개가 있습니다.
>
> 기본적으로 이러한 함수는 모두 동일한 작업을 수행합니다. 즉, 개체에서 코드 블록을 실행합니다. 다른 점은 이 객체가 블록 내에서 사용 가능해지는 방식과 전체 표현식의 결과가 무엇인지입니다.
>
> **Scope functions**를 사용하는 방법에 대한 일반적인 예는 다음과 같습니다.
>
> ```
> Person("Alice", 20, "Amsterdam").let {
>     println(it)
>     it.moveTo("London")
>     it.incrementAge()
>     println(it)
> }
> ```
>
>  `let` 없이 동일한 내용을 작성하는 경우, 새 변수를 도입하고 사용할 때마다 해당 이름을 반복해야 합니다.
>
> ```
> val alice = Person("Alice", 20, "Amsterdam")
> println(alice)
> alice.moveTo("London")
> alice.incrementAge()
> println(alice)
> ```
>
> **Scope functions**은 새로운 기술적 기능을 도입하지 않지만 코드를 더 간결하고 읽기 쉽게 만들 수 있습니다.
>
> 범위 기능 간의 많은 유사성으로 인해 사용 사례에 적합한 기능을 선택하는 것이 까다로울 수 있습니다. 선택은 주로 귀하의 의도와 프로젝트에서의 사용 일관성에 따라 달라집니다. 

위의 내용과 사이트에 적힌 추가적인 내용으로 정리를 해보겠다.



<br/>



## Scope functions이란?

- **객체의 범위 내**에서 **코드 블럭을 실행**하는 것이 목적인 함수이다.
- 종류로는 **`let, run, with, apply, also`** 총 5개가 있다.



#### Sealed Class의 장점

- 기술적 기능을 도입하지 않지만 코드를 더 **간결하고 읽기 쉽게** 만든다.

코틀린 공식 홈페이지엔 기능간의 많은 유사성으로 인해 사용 사례에 적합한 기능을 선택하는 것이 까다로울 수 있다고 나와있다.
그 이후 하단에 나와있는 scope function과 규칙간의 차이점에 대해 알아보도록 하자.



| function                                                     | 객체 참조 | 리턴 값        | 확장가능 여부                                                |
| ------------------------------------------------------------ | --------- | -------------- | ------------------------------------------------------------ |
| [`let`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/let.html) | `it`      | Lambda result  | Yes                                                          |
| [`run`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/run.html) | `this`    | Lambda result  | Yes                                                          |
| [`run`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/run.html) | -         | Lambda result  | No: called without the context object (context객체 없이 호출) |
| [`with`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/with.html) | `this`    | Lambda result  | No: takes the context object as an argument. (context 객체를 인수로 사용) |
| [`apply`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/apply.html) | `this`    | Context object | Yes                                                          |
| [`also`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/also.html) | `it`      | Context object | Yes                                                          |

위의 표를 보고 다음과 같이 차이를 정리해보았다.

**객체를 접근하는 방법**

- **`run, with, apply`** : 자기 자신을 블럭(**`this`**)으로 넘기고 **`this`**를 사용해 객체에 접근 

- **`let, also`** : 자기 자신을 (람다) 인자(**`it`**)으로 넘기고 **`it`**을 사용해 객체에 접근

**리턴 값**

- **`apply, also`** : Context Object를 리턴
- **`let, run, with`** : 람다식 결과를 리턴



**추가적으로 각각 Scope Function에 대해 알아보도록 하자.**



<br/>



## 1. `with()`

가장 먼저 **`with`**에 대해 알아보자. 매우 직관적으로 가용이 가능한데 with을 사용하게 되면 **점 표기법(dot notation)** 없이 바로 블럭을 사용해서 코드를 간략하게 사용할 수 있다. 

```kotlin
viewModel.addData(data)
viewModel.updateData(data)
viewModel.removeData(data)
```

- 먼저 **`with`**을 사용하지 않았을 때의 코드이다. **dot notation** 사용으로 코드상의 반복이 많아진 것을 볼 수 있다.

```kotlin
with(viewModel) {
    addData(data)
    updateData(data)
    removeData(data)
}
```

- 다음은 **`with`**을 사용한 코드이다. 코드상의 반복이 줄어들고 블럭으로 묶여있어 가독성 또한 올라간 것을 볼 수 있다.

```kotlin
fun initView() = with(binding) {
    ... 
}
fun inintViewModel() = with(binding){
  	with(viewModel){
      ...
		}
  	
  	with(sharedViewModel){
      ...
    }
}
```

- 마지막으로 프로젝트 할 때 응용해봤던 경우인데, 함수 자체를 **`with`**으로 묶어 **`viewBinding`**을 바로 적용시키고 추가적으로 **`viewModel`**과 **`sharedViewModel`** 또한 **`with`**으로 묶어 효율성을 극대화 시켜 보았다. ㅎㅎ :)
- 정리해보자면 with는 객체를 인자로 받기 때문에, 이미 생성된 객체에 여러 작업을 일괄적으로 해야할 때 유용하다.



<br/>



## 2. `let()`

**`let`** 또한 먼저 다뤘던 with처럼 사용이 가능하여 헷갈리지만 코드로 구현해보자면 다음과 같다.

```kotlin
viewModel.let {
    it.addData(data)
    it.addData(data)
    it.addData(data)
}
viewModel.let { mainList ->
    mainList.addData(data)
    mainList.addData(data)
    mainList.addData(data)
}
```

- 람다 함수이므로 명시하지 않으면 **`it`**으로 사용이 가능하고 이름을 람다식으로 명시해주면 **`mainList`** 와 같이 원하는 이름으로 사용 가능하다.
- 어찌됐든, **`let`**또한 **`with`**처럼 사용이 가능하지만, 매번 객체(it,mainList)를 표시해주어야 하기 때문에 나라면 with을 사용할 것 같다. 그렇다면 어떤 경우에 let을 사용하면 좋을지 코드로 알아보자

```kotlin
data?.let {
    viewModel.addData(it)
} ?: println("null")
```

- 위 코드는 null 체크를 하기 위한 코드이다. **`let`**을 사용하여 null이 아닐경우에만  **`let`**블럭 안의 코드가 실행되도록 할 수 있다. 이후 엘비스 연산자로 null 처리까지 해주었다.

```kotlin
val length = str?.let { it.length }
```

- 위와 같이 리시버 객체의 확장 함수로 사용이 가능하다.



<br/>



## 3. `apply`

apply 람다함수 블럭내에선, context object를 사용하므로, 객체는 this로 참조가 된다. 즉, with와 동일하게 블럭내에서 객체를 명시적으로 표시할 필요없이 다음 예제처럼 사용가능하다.

```kotlin
viewModel.apply { 
    addData(data)
    addData(data)
    addData(data)
}
```

- 하지만 **`with`**와는 달리 **`apply`**는 확장 함수의 형태이다.

```kotlin
val minsu = Person("Minsu").apply {
    age = 25
    city = "Seoul"
}
println(minsu)
```

- 확장함수의 장점은 위의 코드처럼 객체를 생성해서 할당하기 이전에 사용할 수 있다는 점이다.
- 그렇기 떄문에, 객체의 생성 시점에서 객체의 초기화에 많이 사용된다.



<br/>



## 4. also

**`also`**는 **`apply`**와 유사하게 확장함수로 정의되는 람다 함수이다. 

- **`apply`**와의 차이점은 **`also`**는 context 객체를 인자로 넘겨주기 때문에 **`it`**이나 다른 명시적인 이름을 통해 참조 가능하다.

- 이러한 **`this`**, **`it`**이 두개의 차이밖에 없는 것 같다고 생각하는 찰나 어떤 블로그의 글을 보고 깨닫게 되었다.

https://jaeyeong951.medium.com/kotlin-lambda-with-receiver-5c2cccd8265a

> ### it vs this
>
> **하지만 it과 this는 단순히 키워드의 차이가 아니다. 그 이상이다.**
>
> also 는 객체를 람다 아규먼트로 받기 때문에 객체에 접근할 때 it(혹은 내가 정의한 다른 이름)을 사용하며, 이는 코드가 **객체 외부에서 해당 객체에 접근한다는 인상**을 강하게 준다.
>
> 이에 반해 apply 는 객체를 람다 리시버로 받기 때문에 객체에 접근할 때 this(혹은 생략)을 사용하며, 코드가 해당 **객체의 외부가 아니라 객체 내부에 있는듯한 인상**을 준다.
>
> 이 차이 때문에 also 와 apply 는 그 쓰임새가 완전히 달라진다. 내가 작성하고자 하는 코드의 semactics 에 따라 also를 쓸지 apply를 쓸지 결정하는 것이다.
>
> apply 는 방금 말했듯이 코드 블록이 객체 내부에 있는 듯한 느낌을 주기 때문에 주로 객체를 초기화 하는 코드 혹은 객체의 상태를 변경하는 코드에 많이 사용된다.
>
> ```
> person.apply {
>     name = "steven"
>     age = 21
> }
> ```
>
> also 는 이와 달리 객체를 외부에서 접근하는 느낌을 주기 때문에 해당 객체와 더불어(혹은 이용해서) 어떠한 행위를 수행하고자 할 때 쓰인다.
>
> ```
> person.also {
>     println("my name is ${it.steven}")
> }
> ```
>
> 정말 말 그대로 apply와 also라는 단어 그 본연의 의미에 맞게 쓰는 것이다.



<br/>



## 5. run

run은 다른 얘들과는 달리 context object가 없이 단일 람다함수 R로 되어있는 것과, context object 의 extension funcion으로 정의된 두가지 버전이 있다. 둘 다, 리턴값은 람다함수의 리턴값을 사용한다.

- 사실상 with 와 동일하지만, 확장함수 형태라는 차이가 있다. 위에서 말했다시피 확장함수의 장점으로는 객체를 생성해서 할당하기 이전에 사용할 수 있다는 점이다.
- 추가적으로 run에서는 람다함수의 리턴값이 사용되므로 빌더 패턴에 적합하다고 할 수 있다.
- 

