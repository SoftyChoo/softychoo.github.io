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

# [Android/Kotlin] Youtube Player

{:toc}

## Youtube Video Player 

동영상을 재생시켜주는 Youtube Video Player Library

 [[android-youtube-player] ⬅︎ 클릭 시 이동!!](https://github.com/PierfrancescoSoffritti/android-youtube-player#android-youtube-player) 



#### 종속성 추가

- 코드를 작성하기 전 gradle 파일에 종속성을 추가한다.

```kotlin
implementation("com.pierfrancescosoffritti.androidyoutubeplayer:core:11.0.1")
```



#### Xml 구성

- 종속성을 추가해주면 `YouTubePlayerView`를 사용할 수 있게 된다.

```kotlin
<com.pierfrancescosoffritti.androidyoutubeplayer.core.player.views.YouTubePlayerView
    android:id="@+id/detail_player"
    android:layout_width="match_parent"
    android:layout_height="200dp" />
```



#### 코드 추가

- 플레이어가 준비되면 호출되는 코드를 작성해주고
- ID값은 다음 링크에서 `=`와 `&` 사이의 값이 아이디로 설정된다. 
- **42fmMP81EvA** : https://www.youtube.com/watch?v=42fmMP81EvA&t=2296s

```kotlin
private fun initPlayer() = with(binding) {
    detailPlayer.addYouTubePlayerListener(object :
        AbstractYouTubePlayerListener() {
        override fun onReady(youTubePlayer: YouTubePlayer) {
            super.onReady(youTubePlayer)
            val videoId = "42fmMP81EvA"
            youTubePlayer.cueVideo(videoId, 0f) // loadVideo로 변경 시 바로 재생
        }
    })
}
```



## 동작

<img src = "../../../assets/img/blog/image-20230928011307138.png" width = "50%"><img src = "../../../assets/img/blog/image-20230928011709232.png" width = "50%">

