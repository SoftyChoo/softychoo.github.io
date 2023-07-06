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

# [Flutter] TextField 거꾸로 입력될 때

플러터 앱개발 중 textField에 타자기로 입력할 때 거꾸로 입력되는 문제점을 발견했다.

기존 코드

```dart
TextField(
              controller: contentController,
              maxLines: 5,
              decoration: InputDecoration(
                border: OutlineInputBorder(
                  borderRadius: BorderRadius.circular(10.0),
                ),
                hintText: '내용을 입력해주세요',
                filled: true,
                fillColor: Colors.white,
              ),
              onChanged: (value) {
                contentController.text = value;
              },
            ),
```



수정코드

```dart
TextField(
              controller: contentController,
              maxLines: 5,
              decoration: InputDecoration(
                border: OutlineInputBorder(
                  borderRadius: BorderRadius.circular(10.0),
                ),
                hintText: '내용을 입력해주세요',
                filled: true,
                fillColor: Colors.white,
              ),
            ),
```



Onchange를 사용해야 하는줄 알았는데 상관 없었다..

그냥 OnChange를 제거하면 된다.
