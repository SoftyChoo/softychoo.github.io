---
layout: post
title: kotlin
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

# [Android] constraint layout의 장점

* toc
{:toc}






##### 오늘은 기술면접에서 가볍게 말할 constraint layout에 대해 알아보자



<br/>



## Constraint Layout?

- 안드로이드에서 제공하는 뷰 레이아웃 중, 뷰를 배치할때 제약조건을 사용해 제어한다.
- 예를들어 **`LinearLayout`**에는 뷰를 **Vertical, Horizontal** 하게 배치할 수 있고 **`RelativeLayout`**은 뷰를 상대적으로 배치하는데
- **`ConstraintLayout`**은 뷰간의 관계를 **제약조건(Constraint)**으로 지정하여 비교적 쉽게 뷰의 위치를 지정해 다양한 레이아웃을 구성할 수있다.

## 💡**장점**

- 제약 조건을 통해 뷰를 배치하면 뷰의 깊이를 줄일 수 있는데

1. 성능 최적화
   - 1depth 만으로도 복잡한 화면 구성가능
2. 가독성 증대
   - 뷰 구조가 깊지 않기 때문에 훨씬 간결하고 가독성이 좋다.