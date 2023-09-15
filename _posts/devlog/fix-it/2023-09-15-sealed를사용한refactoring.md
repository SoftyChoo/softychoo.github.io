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

# [Android/Kotlin],[TroubleShooting] sealed Class를 사용한 viewModel 상태관리

{:toc}

## 상황

Activity ViewModel을 사용하여 데이터를 전달하는 과정 중 데이터가 꼬여 아이템의 이름이 마구잡이로 바뀌고 이전 상태로 변하는 등 심각한 문제 발생...ㅠㅠ



## 이유 & 기존의 코드

- 기존의 데이터를 전송하는 방식은 각각 동작별 LiveDataItem을 선언해 두고 데이터를 받아올 프래그먼트에서 모두 관찰해 데이터를 가져오는 방식이였는데 관찰하는 곳에서 불필요하게 데이터를 관찰하게되는 코드가 남발하게 되는 상황 

```
class SharedViewModel : ViewModel() {
    val modifyBookmarkItem: MutableLiveData<BookmarkModel> = MutableLiveData()
    val addBookmarkItem : MutableLiveData<BookmarkModel> = MutableLiveData()
    val removeBookmarkItem: MutableLiveData<BookmarkModel> = MutableLiveData()
}
```

```kotlin
sharedViewModel.addBookmarkItem.value = item.toBookmarkModel()
```

- 값을 넣어주는 부분에서도 함수를 통해 넘겨주는 방법이 더 좋다고 한다.  -> 리팩토링 예정



## 결론 및 해결 코드

- Sealed Class를 통한 상태관리를 통해 확장성 있는 코드로 개선

> Sealed Class를 통해 상태관리를 하면 코드 안정성 향상, 가독성 향상 등 다양한 장점이 있다. 

```kotlin
class SharedViewModel : ViewModel() {
    val bookmarkState : MutableLiveData<BookmarkState> = MutableLiveData()
}
sealed interface BookmarkState{
    data class AddBookmark(val bookmarkModel: BookmarkModel) : BookmarkState
    data class RemoveBookmark(val bookmarkModel: BookmarkModel) : BookmarkState
    data class ModifyBookmark(val bookmarkModel: BookmarkModel) : BookmarkState
}
```

- 값을 넣어주는 부분에서는 다음과 같이 Sealed클래스의 하위 클래스를 통해 값을 넣어준다.

```kotlin
sharedViewModel.bookmarkState.value = BookmarkState.AddBookmark(item.toBookmarkModel())
```

- 마지막으로 값을 받아오는 부분에서 다음과 같이 상태 변화에 따라 데이터를 수신해주면 된다.

```kotlin
//데이터를 관찰해 데이터 수신
sharedViewModel.bookmarkState.observe(viewLifecycleOwner, Observer { state ->
    when(state){
        is BookmarkState.AddBookmark -> addItem(state.bookmarkModel)
        is BookmarkState.ModifyBookmark -> Unit
        is BookmarkState.RemoveBookmark -> removeItem(state.bookmarkModel)
    }
})
```

> 여기서 Unit은 Void와 같이 아무 행동도 하지 않을 때 작성하면 된다.



## 느낀 점

공부하면 할수록 마르지 않고 계속계속 더 나은 코드와 방향이 나오는게 코딩인 것 같다.

ViewModel을 공부하면서 며칠간 막막하다는 느낌을 많이 받았었는데 막상 부딪혀 보니 하나씩 이해가고 해결되가는게 너무 재밌는 것 같다.

Sealed Class도 듣기만 해보고 이번에 처음 사용해봤는데 여러모로 앞으로 함께갈 친구인 것 같아서 열심히 공부해봐야 겠다.

