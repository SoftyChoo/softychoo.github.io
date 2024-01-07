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

# [Android Jetpack Compose] Statefull & Stateless?

{:toc}

![jetpack_compose](../../../assets/img/blog/jetpack_compose.png)



**💡 remeber를 사용해서 statefull를 가져가게 된다면 Composable의 재사용성이 많이 떨어지게 되므로 `state hoisting pattern`을 사용해서 stateless 패턴으로 사용하자**



<br/>



## 📌 Stateful & Stateless Composable

- Composable의 두 가지 타입 :  상태를 가지고 있는 `Stateful Composable`, 상태를 가지지 않는 `Stateless Composable`
- `Stateful Composable` : `상태가 변하게 되면` 자기 자신과 자식의 Composable 을 `재구성`
- `Stateless Composable` : `상태가 없기 때문`에 스스로 재구성을 할수 없으며 `부모의 Composable이 재구성되어야 자신이 재구성`

