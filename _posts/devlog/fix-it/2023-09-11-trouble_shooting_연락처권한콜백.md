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

# [Android/Kotlin],[TroubleShooting] registerForActivityResult 권한 콜백

{:toc}

## 상황

실제 기기의 연락처를 어플로 받아오는 코드 구현 중 연락처를 받아올 때 
**권한이 이미 허용된 경우에는 정상적**으로 받아와 지지만 
앱 설치 후 가장 **처음 권한을 허용할 때 연락처가 바로 받아지지 않는 문제**가 발생함



## 시도

권한 허용 창과 동시에 동작을 하는 함수를 구현해 시도했으나 권한 요청과 동시에 실행돼버려 문제가 해결되지 않음 그래서 어떤방식이 있을까 서칭과 질문을 통해 문제파악



## 결론 및 해결 코드

registerForActivityResult의 권한을 콜백으로 받아서 해결완료

```kotlin
private val permissionLauncher = registerForActivityResult(ActivityResultContracts.RequestPermission()) { isGranted ->
    if (isGranted) {
        Toast.makeText(context,"권한 허용",Toast.LENGTH_SHORT).show()
        getContact()
    } else {
        Toast.makeText(context,"권한 거부",Toast.LENGTH_SHORT).show()
    }
}

private fun requestPermission() {
    val readContactsPermission = Manifest.permission.READ_CONTACTS
    if (ActivityCompat.shouldShowRequestPermissionRationale(requireActivity(), 			  
    readContactsPermission)) {
        getContact() 
    } else {
        permissionLauncher.launch(readContactsPermission)
    }
}
```



## 알게된 점

registerForActivityResult는 이전에 데이터 콜백 시 사용했던 기능인데 권한을 콜백으로 받아온다는 생각을 못하였다. 따라서 무작정 새로운 기능이라고 생각하지말고 내가 아는 선에서 해결이 가능한지 먼저 생각을 해보고 차근차근 나아가는 것이 필요하다고 생각하였다.

