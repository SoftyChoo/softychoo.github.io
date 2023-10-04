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

# [TIL] (2023/10/04) Custom Dialog 적용

{:toc}



## Start!

팀 프로젝트 제출까지 하루를 두고 오늘은 간단한 Custom Dialog를 구현해보았다. 밋밋한 Dialog보다 앱의 퀄리티에 맞는 Dialog를 만들고 싶어 Custom으로 제작해보았다 !



## Custem Dialog

결과적으론 앱과 어울리는 Dialog가 완성되어 꽤 만족스러웠다! CustomDialog를 만드는 링크는 다음의 링크에 정리해 두었다 :)

[[Custom Dialog 링크!!]](https://softychoo.github.io/devlog/kotlin/2023-10-04-customdialog)

#### 결과!!

<img src = "../../../assets/img/blog/image-20231004212435087.png" width = "33.333%"><img src = "../../../assets/img/blog/image-20231004212530154.png" width = "33.333%"><img src = "../../../assets/img/blog/image-20231004212607682.png" width = "33.333%">



## DialogFragment로 변경 예정

내가 구현했던 방식은 Dialog 클래스를 상속받는 Class를 만들어 Callback이벤트를 넘겨주는 방식으로 구현하였는데 이렇게 하면 MVVM을 효율적으로 적용할 수 없게 된다는 것을 알게 되었다. 따라서 시간이 남는다면 Dialog Fragement로 변경해서 작업해볼 생각이다!



## 느낀점

어느덧 프로젝트 제출까지 하루가 남았다. 중간 쯤엔 진행도가 좀 아쉬운가? 라는 생각도 했지만 생각없이 구현하다보니 여유있게 잘 마무리된 것 같다. 🙂



## End!

이제 이번 프로젝트가 끝나면 최종 프로젝트 인데 최종 프로젝트에선 내가 알고 적용할 수 있는 효율적인 모든 것을 쏟아부어봐야겠다!