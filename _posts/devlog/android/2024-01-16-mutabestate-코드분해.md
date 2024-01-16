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

# [Android Jetpack Compose] MutableState + 코드분해

{:toc}

![jetpack_compose](../../../assets/img/blog/jetpack_compose.png)

**💡 Recomposition : 컴포즈가 계속 다시 그려지는 것**



<br/>



**오늘은 MutableState와 코드분해에 대해서 알아보자**



<br/>



- State는 읽기만 가능한 값(value)하나를 가지고있고

```kotlin
@Stable
interface State<out T> { 
    val value: T
}
```

- MutableState는 읽기 쓰기가 가능한 형태의 값을 가지고 있다.
- 또한 Operator로 getter/setter의 역할을 하는 component가 있다.

```kotlin
@Stable
interface MutableState<T> : State<T> {
    override var value: T // 값
    operator fun component1(): T // 보통 value가 return
    operator fun component2(): (T) -> Unit // value의 setter
}
```

- mutableStateOf

```kotlin
fun <T> mutableStateOf(
    value: T,
    policy: SnapshotMutationPolicy<T> = structuralEqualityPolicy()
): MutableState<T> = createSnapshotMutableState(value, policy)
```

- `onValueChange` 가 일어날때 마다 setText가 되며  컴포즈가 다시 그려지는 Recomposition이 일어난다.

```kotlin
@Composable
fun HomeScreen(viewModel : MainViewModel = viewModel()){
    val (text, setText) = remember {
        mutableStateOf("Hello world")
    }

    Column {
        Text(text = text)
        TextField(value = text, onValueChange = setText)
        Button(onClick = {}) {
            Text(text = "클릭")
        }
    }
}
```

### 코드분해

- 들어가보면 다음과 같은 형식으로 지정되있는 것을 볼 수 있다.
- 보통 아래와 같은 형식으로 이루어진 친구들은 특별한 함수이기 때문에 `구조분해 기법`이 사용가능하다.

```kotlin
 operator fun component1(): T
 operator fun component2(): (T) -> Unit
```

- 다음과 같이 코드변경이 가능하다.

```kotlin
val textValue = rememberSaveable {
    mutableStateOf("")
}

TextField(
    modifier = Modifier.fillMaxSize(),
    value = **textValue.value**,
    onValueChange = { **textValue.value** = it },
)
```

### ➡︎

- **text**에는 component1의 value가, **setValue**에는 setter가 위치된다.

```kotlin
val (text, setValue) = rememberSaveable { // text
    mutableStateOf("")
}

TextField(
    modifier = Modifier.fillMaxSize(),
    value = **text**,
    onValueChange = **setValue**
)
```

### Additional

- 기존의 코드는 text : MutableState<String>의 형식을 갖는다.
- 사용할 때는 MutableState.value의 형태로 사용해야한다.

```kotlin
val text = remember {  
    mutableStateOf("Hello world")
}
Text(text = text.value) // 사용
```

- by를 사용하면 Text : String의 형식을 갖기 때문에 바로 값을 참조하게 되어 value를 생략하여 사용 가능하다.

```kotlin
val text by remember {  
    mutableStateOf("Hello world")
}
Text(text = text) // 사용
```