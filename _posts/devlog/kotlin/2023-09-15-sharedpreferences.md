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

# [Android/Kotlin] SharedPreferences

* toc
{:toc}


## 📌 Preference?

- 프로그램의 설정 정보 (사용자의 옵션 선택 사항 이나 프로그램의 구성 정보)를 영구적으로 저장하는 용도로 사용
- XML 포맷의 텍스트 파일에 키-값 세트로 정보를 저장.
- SharedPreferences 클래스
  - Preferences의 데이터(키-값 세트)를 관리하는 클래스
  - 응용 프로그램 내의 액티비티 간에 공유하며, 한쪽 액티비티에서 수정 시 다른 액티비티에서도 수정된 값을 읽을 수 있다.
  - 응용 프로그램의 고유한 정보이므로 외부에서는 읽을 수 없다.



## **공유 환경설정의 핸들 가져오기**

- ```
  getSharedPreferences
  ```

   (name, mode)

  - 여러개의 Shared Preference파일들을 사용하는 경우
  - name : 프레퍼런스 데이터를 저장할 XML 파일의 이름이다.
  - mode : 파일의 공유 모드
    - MODE_PRIVATE: 생성된 XML 파일은 호출한 애플리케이션 내에서만 읽기 쓰기가 가능
    - MODE_WORLD_READABLE, MODE_WORLD_WRITEABLE은 보안상 이유로 API level 17에서 deprecated됨

```kotlin
val sharedPref = activity?.getSharedPreferences(
        getString(R.string.preference_file_key), Context.MODE_PRIVATE)
```

- 사용 가능한 데이터 타입

  ![img](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fd8886449-c473-4f6e-8559-606a3c7d4f23%2FUntitled.png?table=block&id=691ce0ae-32a4-49e1-8cfd-04c8dfc8b913&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=2000&userId=&cache=v2)

- SharedPreferences 클래스

  - 프레퍼런스의 데이터(키-값 세트)를 관리하는 클래스
  - 응용 프로그램 내의 액티비티 간에 공유하며, 한쪽 액티비티에서 수정 시 다른 액티비티에서도 수정된 값을 읽을 수 있다.
  - 응용 프로그램의 고유한 정보이므로 외부에서는 읽을 수 없다.

- XML 포맷의 텍스트 파일에 키-값 세트로 정보를 저장.

- 프로그램의 설정 정보 (사용자의 옵션 선택 사항 이나 프로그램의 구성 정보)를 영구적으로 저장하는 용도로 사용

- `getPreferences`
  - 한개의 Shared Preference 파일을 사용하는 경우
  - Activity 클래스에 정의된 메소드 이므로, Activity 인스턴스를 통해 접근 가능
  - 생성한 액티비티 전용이므로 같은 패키지의 다른 액티비티는 읽을 수 없다.
  - 액티비티와 동일한 이름의 XML 파일 생성

```kotlin
val sharedPref = activity?.getPreferences(Context.MODE_PRIVATE)
```



