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

# [Kotlin] RecyclerView LayoutManager 사용



* toc
{:toc}








## 📌  레이아웃 매니저(LayoutManager)란?

- 레이아웃 매니저는 데이터나 아이템들이 리사이클러뷰 내부에서 배치되는 형태를 관리하는 역할을 한다.



## 🤔 레이아웃 매니저(LayoutManager)의 종류

- **LinearLayoutManager** : 수평,수직으로 배치시켜주는 레이아웃 매니저

- **GridLayoudManager** : 그리드 화면으로 배치(2단,3단진열 등)시켜주는 레이아웃 매니저

- **StaggeredGridLayoutManager** : 높이가 불규칙한 그리드 화면으로 배치시켜주는 레이아웃 매니저



## 1. LinearLayoutManager

- 가장 기본적으로 LinearLayoutManager의 방향을 수직으로 지정해주는 코드이다.

```kotlin
 binding.recycelrView.layoutManager = LinearLayoutManager(this)
```

##### 결과화면

![rv_mg0_out](../../../assets/img/blog/rv_mg0_out.gif)

- 다음으로 LinearLayoutManager의 방향을 수평으로 지정해주는 코드이다.
- Item을 역순으로 보여주려면 `true` 아니라면 `false`를 입력해준다.

```kotlin
binding.recycelrView.layoutManager = LinearLayoutManager(this,LinearLayoutManager.HORIZONTAL,false)
```

##### 결과화면

![rv_mg1_out](../../../assets/img/blog/rv_mg1_out.gif)



## 2. GridLayoutManager

- GridLayoutManager의 수직 방향으로 2개의 뷰홀더를 리스트를 보여주는 코드이다.

```kotlin
binding.recycelrView.layoutManager = GridLayoutManager(this,2)
```

##### 결과화면

![rv_mg3_out](../../../assets/img/blog/rv_mg3_out.gif)



- GridLayoutManager의 수평 방향으로 2개의 뷰홀더를 리스트를 보여주는 코드이다.

```kotlin
binding.recycelrView.layoutManager = GridLayoutManager(this,2,GridLayoutManager.HORIZONTAL,false)
```

##### 결과화면

![rv_mg4_out](../../../assets/img/blog/rv_mg4_out.gif)



## 3. StaggeredGridLayoutManager

- 불규칙한 Grid형식으로 리스트를 보여주는 StaggeredGridLayoutManager이다.
- 기본 수직방향 코드이고 수평방향은 `HORIZONTAL`로 변경해주면 된다.
- 숫자 3은 Grid의 열 수를 의미한다.
- 현재는 사진크기와 항목을 넣어준 크기가 일치해서 딱 맞춰줘 보이지만 각 항목의 크기가 다르면 불규칙한 Grid 형식으로 보이게 된다.

```kotlin
binding.recycelrView.layoutManager = StaggeredGridLayoutManager(3,LinearLayoutManager.VERTICAL)
```

##### 결과화면

![rv_mg5_out](../../../assets/img/blog/rv_mg5_out.gif)

 