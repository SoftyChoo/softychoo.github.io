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

# [Android/Kotlin] ContentProvider, ContentResolver 이용해서 연락처 가져오기



* toc
{:toc}


## Menifest에 permission 추가

```kotlin
<uses-permission android:name="android.permission.READ_CONTACTS"/>
```











