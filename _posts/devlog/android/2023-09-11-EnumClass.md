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
 - android








---

# [Android/Kotlin] Enum Class



* toc
{:toc}


## 📌 Enum Class?

> 열거형이라는 방식을 사용 (특정한 값을 0 ~ 끝까지 나열한다는 느낌)
>
> 내가 사용한 방식은 진입 타입을 설정할 때 사용하였다.





## 이해와 사용

- 다음과 같이 `title`과 `id`값을 주어주고 사용도 가능하고

```kotlin
enum class ContentType(val title: String, val id: Int) {
    ADD("저장",2), EDIT("수정",3), REMOVE("삭제",1)
}
```

```kotlin
fun test(){
  ContentType.EDIT.id
}
```

---

- `name`, `ordinal` 값으로도 사용이 가능한데 
  - `name`은 Enum Class의 이름인 **"ADD"**을
  - `ordinal`은 Enum Class의 index인 **"0"**을 가져오게 된다.

```kotlin
enum class TodoContentType {
    ADD, EDIT, REMOVE;
}
```

```kotlin
fun test(){
  contentType.ADD.name
  contentType.Add.ordinal
}
```

- 그 이후 `name`, `ordinal`로 뽑아온 값을 다시 **Enum Class**로 변환하는 작업이 필요하다.

```kotlin
enum class TodoContentType {
    ADD, EDIT, REMOVE;

    companion object {
        fun from(name: String?): TodoContentType? {
            return TodoContentType.values().find {
                it.name.uppercase() == name?.uppercase()
            }
        }
    }
}
```

- 다음은 `name` 값을 가지고 다시 EnumClass로 Converting 즉 변환하는 코드인데
- `TodoContentType.values().find` 로 Array Type을 순회하면서 클래스 상의 `name`과 들어온 `name`이 일치하는 경우 EnumType으로 Return 하는 코드이다.

⭐️⭐️⭐️

> 여기서 추가적으로 name 에 소문자가 들어오는 Case까지 보완해주기 위하여 모두 `uppercase(대문자)`처리를 해준 이후 비교해주는 코드이다.





## 참고용 진입타입 받아오는 방식

- intent

```kotlin
fun newIntentForEdit(
            context: Context,
            position: Int,
            todoModel: TodoModel
        ) = Intent(context, TodoContentActivity::class.java).apply {
            putExtra(EXTRA_TODO_ENTRY_TYPE, TodoContentType.EDIT.name)
            putExtra(EXTRA_TODO_POSITION, position)
            putExtra(EXTRA_TODO_MODEL, todoModel)
        }
```

- 지연초기화 사용해 EXTRA_TODO_ENTRY_TYPE 선언

```kotlin
private val entryType by lazy {
    TodoContentType.from(intent.getStringExtra(EXTRA_TODO_ENTRY_TYPE))
}
```

- 타입별 처리 예시

```kotlin
fun test(){
        when (entryType){
            TodoContentType.ADD -> 
            TodoContentType.EDIT -> 
            null -> 
        }
    }
```

