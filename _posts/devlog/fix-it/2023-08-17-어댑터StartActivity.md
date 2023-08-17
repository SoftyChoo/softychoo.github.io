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

# [Kotlin] Adaptor,ViewHolder에서 StartActivity 실행하는 방법

{:toc}

개발을 하던 중 RecyclerView Adaptor내에서 StartActivity를 사용할 상황이 생겼는데 Activity에서 사용하는 방법대로 하니 오류가 나서 다른형식을 알아보았다.

## Code!!

it을 매개체로 받아오기 때문에 startActivity앞에 `it.context`를 추가해준다.

```kotlin
class ViewHolder(view: View) : RecyclerView.ViewHolder(view) {
        val imageButton : ImageButton
        init {
           
            imageButton.setOnClickListener {
                val intentToProfile = Intent(it.context,ProfileActivity::class.java)
                intentToProfile.putExtra("name",textView.text.toString())
                it.context.startActivity(intentToProfile)
            }
        }
    }
```


