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

# [Andorid/Kotlin] binding = null처리를 onDestroyView에서 해주는 이유

{:toc}



## 기존의 코드와 변경된 코드

- 기존의 코드는 **onDestroy()**에서 binding을 null처리 해주었는데

```kotlin
override fun onDestroy() {
    super.onDestroy()
    _binding = null
}
```



- 바뀐 코드는 다음과 같이 **onDestroyView()**때 binding을 null처리 해주는 것을 알 수 있다.

```kotlin
override fun onDestroyView() {
    super.onDestroyView()
    _binding = null
}
```



- 그 이유는 다음의 Fragment LifeCycle, View LifeCycle을 보면 알 수 있다.



## Fragment View LifeCycle

<img src = "../../../assets/img/blog/images_evergreen_tree_post_cc753569-a1c8-44c6-ab88-67dc9152a243_image.png" width = "60%">



- view에 대한 처리를 다뤄야하기 때문에 **프래그먼트와 연결된 View Layer가 제거되는 중일 때 호출**되는 **onDestroyView()** 때 bindig을 null 처리 해주어야 한다. :)