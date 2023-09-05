---
layout: post
title: Fix-It
accent_image: 
  background: url('/assets/img/change_img/book.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  fixNote
invert_sidebar: true
categories :
 - devlog
 - fix-it




---

# [Android/Kotlin] Serializable & Parcelable

{:toc}

## 상황

기존에 Activity끼리 데이터를 전달하며 intent를 통해 데이터를 전달해 주던 중 DataClass객체를 통째로 전달하고 싶어 객체를 **직렬화** 하는 방법을 찾아보았다.

> 여기서 직렬화란 객체 데이터를 전송이나 저장이 가능한 형태로 바꿔주는 것이다.
>
> 반대로 역 직렬화란 직렬화를 통해 변환된 객체를 다시 객체 형태로 읽어내기 위한 것이다. 

오늘은 navigation 라이브러리에서 지원하는 **Serializable**, **Parcelable** 두가지를 알아보고 Parcelable을 적용하는 방법까지 알아보도록 하자



## Serializable

Serializable는 직렬화를 가능하게 하는 자바 표준 인터페이스이다. 따라서 Android SDK에 포함되어있진 않다.

#### 장점

- **구현의 편리함** : Serializable인터페이스만 상속하면 바로 구현이되므로 편리하다.

#### 단점

- **속도가 매우 느림** : Reflection을 사용해 속도가 느리다.

> Reflection 은 프로세스 동작 중에 많은 추가 객체들을 생성한다. 
> 추가 객체 생성 후에 나온 Garbage들은 Garbage Collector의 타켓이 되고 과도한 동작으로 오버헤드가 발생한다.
> 따라서 정보가 많아질수록 성능에 부하를 준다는 의미이다.



## Parcelable

Parcelable은 Serializable과 달리 Android SDK에 포함되어있는 인터페이스이다.

#### 장점

- **빠른 속도** : Reflection을 사용하지 않기 때문에 Serializable에 비해서 매우 빠른 속도가 장점이다.

#### 단점

- **보일러플레이트 코드의 증가**



## 결론 및 해결 코드

Serializable은 인터페이스 상속만 하면 되기 때문에 개발자 입장에서 편하다는 점이 있지만 이는 사용자에게는 퍼포먼스 저하와 빠른 배터리 소모를 일으키는 단점이 있다고 한다. 따라서 Serializable보다는 Parcelable을 사용하는 습관을 들여야 겠다.

### Step 1 

- Grade(Module : app) plugins에 다음 코드를 추가해 준 후 sync를 해준다.

```kotlin
plugins {
    id 'kotlin-parcelize'
    id 'kotlin-android'
}
```

### Step 2

- 사용중인 data class에 `@Parcelize` 어노테이션을 달아준다.

```kotlin
import kotlinx.android.parcel.Parcelize

@Parcelize
data class Mydata(
    val name: String,
    val age: String,
    val image: Int,
) : Parcelable
```

**그럼 이제 객체를 Parcelize의 형태로 직렬화해 전송이 가능하다.**
