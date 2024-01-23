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

# [Android/Kotlin] Coroutine이란?



* toc
{:toc}


##### 오늘은 Coroutine에 대해서 알아보려고 한다.

- Coroutine은 co와 routine이 합쳐진 단어로서 해석 해보자면 특정한 일을 실행하기 위한 함께 작동하는 프로그램의 일부라고 해석이 된다.
- 아직까지는 확실히 감이 잘 오지 않기 때문에 Developer와 Kotlin공홈의 설명을 확인해보자.



[[ Developer : Kotlin Coroutine ]](https://developer.android.com/kotlin/coroutines?hl=ko)

> *코루틴*은 비동기적으로 실행되는 코드를 간소화하기 위해 Android에서 사용할 수 있는 동시 실행 설계 패턴입니다. [코루틴](https://kotlinlang.org/docs/coroutines-guide.html)은 Kotlin 버전 1.3에 추가되었으며 다른 언어에서 확립된 개념을 기반으로 합니다.
>
> Android에서 코루틴은 기본 스레드를 차단하여 앱이 응답하지 않게 만들 수도 있는 장기 실행 작업을 관리하는 데 도움이 됩니다. 코루틴을 사용하는 전문 개발자 중 50% 이상이 생산성이 향상되었다고 보고했습니다.
>
> 
>
> #### 기능
>
> 코루틴은 Android의 비동기 프로그래밍에 권장되는 솔루션입니다. 주목할 만한 기능은 다음과 같습니다.
>
> - **경량**: 코루틴을 실행 중인 스레드를 차단하지 않는 [*정지*](https://kotlinlang.org/docs/reference/coroutines/basics.html)를 지원하므로 단일 스레드에서 많은 코루틴을 실행할 수 있습니다. 정지는 많은 동시 작업을 지원하면서도 차단보다 메모리를 절약합니다.
> - **메모리 누수 감소**: [*구조화된 동시 실행*](https://kotlinlang.org/docs/reference/coroutines/basics.html#structured-concurrency)을 사용하여 범위 내에서 작업을 실행합니다.
> - **기본으로 제공되는 취소 지원**: 실행 중인 코루틴 계층 구조를 통해 자동으로 [취소](https://kotlinlang.org/docs/reference/coroutines/cancellation-and-timeouts.html)가 전달됩니다.
> - **Jetpack 통합**: 많은 Jetpack 라이브러리에 코루틴을 완전히 지원하는 [확장 프로그램](https://developer.android.com/kotlin/ktx?hl=ko)이 포함되어 있습니다. 일부 라이브러리는 구조화된 동시 실행에 사용할 수 있는 자체 [코루틴 범위](https://developer.android.com/topic/libraries/architecture/coroutines?hl=ko)도 제공합니다.

[[ Kotlin : Coroutines basics ]](https://kotlinlang.org/docs/coroutines-basics.html)

> Coroutine은 일시 중단 가능한 계산의 인스턴스입니다. 이는 나머지 코드와 동시에 작동하는 코드 블록을 실행해야 한다는 점에서 개념적으로 스레드와 유사합니다. 그러나 Coroutine은 특정 스레드에 바인딩되지 않습니다. 한 스레드에서 실행을 일시 중단하고 다른 스레드에서 다시 시작할 수 있습니다. Coroutine은 경량 스레드로 생각할 수 있지만 실제 사용법이 스레드와 매우 다르게 만드는 중요한 차이점이 많이 있습니다.



위의 내용을 바탕으로 정리를 해보자



<br/>



##  Coroutine이란?

- **`일시 중단`**이 가능한 계산의 인스턴스이다.
- 나머지 코드와 동시에 작동하는 코드 블록을 실행해야 한다는 점에서 스레드와 유사하지만, **Coroutine은 특정 스레드에 바인딩 되지 않는다**는 차이점이 있다.
- 한 스레드에서 실행을 **`정지`**하고 다른 스레드에서 **`재개`** 할 수 있다.

- **비동기적으로 실행되는 코드를 간소화**하기 위해 Android에서 사용할 수 있는 **동시 실행 설계 패턴**이다.

- 기본 스레드를 차단하여 앱이 응답하지 않게 만들 수도 있는 **장기 실행 작업을 관리**하는 데 도움이 된다.

- **생산성 향상**에 도움이 된다.

- 코루틴의 장점 중에 하나는 **비동기적**으로 실행된다는 점이다.

  - ***동기적(Synchronous)*** : 어떠한 작업을 요청했을 때 그 작업을 끝내고 다음 작업을 실행함
  - ***비동기적(Asynchronous)*** : 어떠한 작업을 요청했을 때 그 작업이 끝날 때 까지 기다리지 않고 다른 작업을 하다가 요청했던 작업이 끝나면 중단됐던 작업을 다시 수행함
  
  
  

### 기능

- **경량** : 실행중인 스레드를 차단하지 않는 **`정지`**를 지원 
  - 단일 스레드에서 많은 코루틴 실행 가능
  - 많은 동시작업 지원, 메모리 절약
- **메모리 누수 감소** : 구조화된 동시 실행을 사용하여 범위 내의 작업 실행
- **취소 지원** : 실행중인 코루틴 계층 구조를 통해 자동으로 취소 전달
- **Jetpack 통합** : Jetpack 라이브러리와의 호환성 좋음

<br/>



<br/>

 



- 추가적으로 공홈에 나와있는 코드를 통해 코루틴을 알아가는 Step을 밟아보자.

```kotlin
fun main () = runBlocking { // this: CoroutineScope
    launch { // launch a new coroutine and continue
        delay(1000L) // non-blocking delay for 1 second (default time unit is ms)
        println("World!") // print after delay
    }
    println("Hello") // main coroutine continues while a previous one is delayed
}

출력값
Hello
World!
```

**위의 코드를 분석해보자**

- **`launch`**는 비동기 작업을 수행하는데 사용되는 코루틴 빌더이다.
  - 나머지 코드와 동시에 새로운 코루틴을 시작하며 독립적으로 작동한다. 
  - 따라서 `Hello`가 먼저 출력된다.
- **`Delay`**는 특별한 중단 함수로, 일정시간동안 코루틴을 **`일시중단`**한다.
  - 코루틴을 중단시키지만 기본 스레드를 차단하지 않고 다른 코루틴이 실행되고 기본 스레드를 활용할 수 있게 한다.

- **`runBlocking`**은 일반적인 `fun main()`과 코루틴 내부의 코드를 연결하는 데 사용되는 코루틴 빌더이다.
  -  `runBlocking` 블록 내에서 코루틴이 실행되며, 이는 IDE에서 CoroutineScope 힌트로 강조 표시된다.

**만약 코드에서 `runBlocking`을 제거하거나 빠트리면 `launch` 호출에서 오류가 발생한다. 왜냐하면 `launch`는 CoroutineScope에서만 선언되기 때문이다.** 



<br/>



##  CoroutineScope란?

**`CoroutineScope`**는 코루틴을 실행하고 제어하는 데 사용되는 인터페이스이다. 코루틴은 비동기적인 작업을 처리하는 데 유용하며, **`CoroutineScope`**는 이러한 코루틴을 조직화하고 관리하기 위한 일종의 컨테이너 역할을 한다.

- ***글로벌 스코프(GlobalScope)***: **`앱의 생명주기와 함께 동작`**하므로 생명주기를 따로 관리해 줄 필요가 없다. **`앱이 시작할 때 부터 끝날 때 까지 긴 시간 실행되는 코루틴에 적합하다.`**
- ***코루틴 스코프(CoroutineScope)***: 서버에서 이미지를 가져오는 경우 같은 코루틴이 필요할 때만 사용하고 닫아주는 경우에 적합하다.



<br/>



## Coroutine Dispatcher란?

**`디스패처`**는 코루틴을 **적당한 스레드에 할당**하고 코루틴이 **정지하거나 다시 실행하는 것을 담당**한다. 

#### Dispatcher의 종류

- ***Dispatchers.Main*** : 메인 스레드에서 코루틴을 실행한다. **`UI와 상호작용에 최적화`** 되어있고 **`빠른 작업을 실행`**할 때 사용한다.
  - suspend 함수를 호출하고 안드로이드 UI 프레임워크 작업을 실행하며 LiveData 객체를 업데이트한다

- ***Dispatchers.Default*** : 메인 스레드 밖에서 코루틴을 실행한다. **`CPU를 많이 쓰는 데이터 정렬`**이나 **`복잡한 연산 같은 작업`**에 최적화 되어있다.
- ***Dispatchers.IO*** : 메인 스레드 밖에서 코루틴을 실행한다. **`이미지 다운로드, 파일 입출력 등 네트워크, 디스크, DB작업`**에 최적화 되어있다.
- ***Dispatchers.Unconfined*** : 호출한 context 를 기본으로 사용하는데 중단하고 다시 실행될 때 context가 바뀌면 바뀐 context로 따라간다.



<br/>



## Coroutine 상태관리 메서드

- ***cancel*** : 코루틴의 동작을 멈추게 하는 method이다. 하나의 스포크 안에 여러개의 코루틴이 존재할 때 하위 코루틴까지 모두 멈춘다.
- ***join*** : 코루틴 내부에 여러 launch 블록이 있을 경우 모두 새로운 코루틴으로 분기되어 동시에 실행되기 때문에 순서를 정할 수 없다. 순서를 정해야할때 join method 를 이용해서 코루틴이 순차적으로 실행할 수 있도록 할 수 있다.



<br/>



## Coroutine suspend 함수

**`suspend`**는 현재 코루틴 실행을 일시중지하고 모든 로컬 변수를 저장하기 때문에 스레드가 멈추지 않는 **효율적인 스레드 활용을 할 수 있게 된다**. 

1. 코루틴이 멈출 때 코틀린 런타임은 해당 코루틴이 실행되던 스레드에 다른 코루틴을 할당해 실행시킨다.

2. 멈춰있던 코루틴이 재개 될 때 사용 가능한 스레드에 할당해준다. 

3. 코루틴은 멈추면서 해당 루틴 상태를 저장하고 서브 루틴을 실행한 다음 저장한 부모루틴을 복원하는 방법으로 스레드에 영향을 주지 않는다.



<br/>



## 코루틴 withContext()

**suspend** 함수를 코루틴 스코프에서 사용할 때 **호출한 스코프와 다른 디스패쳐를 사용하는 경우**가 있다. 

- Kotlin은 가능한 한 스레드 전환을 방지하도록 **`Dispatchers.Default`**와 **`Dispatchers.IO`** 간의 전환을 최적화한다.
- 따라서, **`withContext()`**를 사용하여 스레드의 전환을 방지할 수 있다.
- 다음은 **`withContext()`**를 사용하여 디스패처를 전환하는 코드이다.

```kotlin
CoroutineScope(Dispatchers.Default).launch{ // Default 디스패쳐 사용
	val result = withContext(Dispatchers.IO){ // IO 디스패쳐로 변경
    	run()
    }
}
```



<br/>



## Coroutine 빌더

- **launch** : **비동기적으로 코루틴을 실행한다. 호출자에게 반환값이 없으며, 해당 코루틴이 완료될 때까지 대기하지 않는다.** 
  - 비동기적으로 작업을 실행하고 결과가 필요없는 경우에 적합하다.
- **async** : **비동기적으로 코루틴을 실행하며, 결과를 반환한다. `Deferred`를 반환하며, 결과에 접근하기 위해 `await()` 함수를 사용하여 결과값을 얻을 때까지 대기한다.**
  - 비동기 작업을 실행하고 결과값이 필요한 경우 사용한다.
  - **`suspend`** 함수 내부에서만 사용 가능하다.
- **withContext** : **부모 코루틴에 의해 사용되던 context와 다른 context에서 코루틴을 실행 할 수 있다.**
- **coroutineScope** : **다수의 코루틴을 사용하는 경우, `suspend` 함수가 시작하고 모든 코루틴이 완료될 때만 처리가 필요할 때 사용한다.**
  - 여러 코루틴 중에서 하나라도 실패하면 모든 코루틴이 취소된다.

- **supervisorScope** : **`coroutineScope`**와 비슷하지만 여러 코루틴 중에서 하나가 실패해도 다른 코루틴이 취소되지 않는다.
- **runBlocking** : **블록 내에서 코루틴을 실행하고 완료될 때까지 현재 스레드를 차단한다. 일반적으로 `main` 함수에서 사용된다.**
  - 애플리케이션의 진입점에서 비동기 코드를 시작하고 관리하는 데 사용한다.



<br/>



### 코루틴 suspend function

- ***withTimeout*** : 코루틴이 정해진 시간 안에 실행되지 않으면 예외를 발생시킨다.
- ***withTimeoutOrNull*** : 정해진 시간 안에 실행되지 않으면 null을 반환한다.
- ***awaitAll*** : 모든 작업의 성공을 기다리면서 작업중에 하나라도 실패하면 awaitAll 또한 실패한다.
- ***joinAll*** : 모든 작업이 끝날 때 까지 현재 작업을 일시 중단시킨다.

