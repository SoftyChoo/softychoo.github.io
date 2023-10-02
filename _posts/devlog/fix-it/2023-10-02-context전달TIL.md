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

# [TIL] (2023/10/02) 공유기능 Context 전달, 제네릭 사용

{:toc}



## Start!

오늘은 팀 프로젝트 제출 이틀 전이다. 실질적인 시간이 없었기 때문에 오늘은 거의 하루종일 코딩만 하였다..!! ViewModel을 자주 다루며 데이터를 전달하던 중 제네릭을 적용해보았고 Util Object안에 공유기능을 넣으면서 Context를 전달한 것에 대해 가볍게 적어보려고 한다 🙂 



## 다른앱으로 데이터 공유 Context 전달

이번 팀 프로젝트를 진행하며 Youtube URL을 다른 앱으로 전송하는 기능을 구현하였는데 기능을 따로 Util Object로 빼주기 위해 다음과 같이 함수에 Context를 넘겨줄 일이 생겼다.

- Contex를 넘겨주는 방식에 있어서 고민을 좀 했는데
- 기존엔 생각 없이 `requireContext`나 `activity as MainActivity`로 액티비티 캐스팅을 때려넣어주는 방식을 사용했는데

```kotlin
1. Util.shareUrl(requireContext(), detailItem.imgUrl)

2. Util.shareUrl(activity as MainActivity, detailItem.imgUrl)
```

- 좀 더 생각을 하다보니 `requireContext()`는 context가 null일 경우 IllegalStateException 발생한다는 것을 알게되었고

- `activity as MainActivity` 이 방식 또한 생명주기 등으로 인해 안정성에서 문제가 있다는 것을 알게 됐다.

```kotlin
public final Context requireContext() {
        Context context = getContext();
        if (context == null) {
            throw new IllegalStateException("Fragment " + this + " not attached to a context.");
        }
        return context;
    }
```

##### 최종코드

- 그래서  context를 넣어줄 때 activity를 널체를 통해 안정성을 보장하는 방식으로 구현하였다 :)

```kotlin
final public FragmentActivity getActivity() {
    return mHost == null ? null : (FragmentActivity) mHost.getActivity();
}
```

```kotlin
activity?.let { context ->
    viewModel.detailItem.value?.let { detailItem ->
        Util.shareUrl(context, detailItem.imgUrl)
    }
}
```

##### [클릭!!](https://softychoo.github.io/devlog/fix-it/2023-10-02-sendDataOtherApp/)  ⬅︎ 기능에 대한 설명은 여기 링크에 작성해놓았다 !!



## 제네릭

다음은 제네릭인데 사실 제네릭을 알고만 있고 제대로 사용해본 적이 거의 없었는데 이번에 처음 사용함으로서 그 편리함을 알아버렸다..!

- 다음은 MainSharedViewModel에서 `_homeEvent` LiveData를 다루는 코드이다.
- updateHomeItems는 Detail,Bookmark Fragment 두 곳에서 사용하는데 각각 DetailModel, BookmarkModel을 파라미터로 넘겨주고 `toHomeModel()`확장함수를 통해 HomeModel로 매핑하게 된다.

##### 기존의 코드

- 기존의 코드는 각각 Fragment에서 데이터를 전달할 때 다른 Fragment에 해당하는 Model엔 null을 집어넣어 비효율적으로 파라미터를 넘겨줬지만

```kotlin
// DetailFragment
updateHomeItems(detailModel = detailModel, bookmarkModel = null)
// BookmarkFragment
updateHomeItems(detailModel = null, bookmarkModel = bookmarkModel)
```

```kotlin
fun updateHomeItems(detailModel: DetailModel?, bookmarkModel: BookmarkModel?) {
    val detailModel = when {
        DetailModel != null -> detailModel.toHomeModel()
        BookmarkModel != null -> bookmarkModel.toHomeModel()
        else -> return // 모든 변수가 null인 경우     
    }
    _detailEvent.value = MainSharedEventForDetail.UpdateDetailItem(detailModel)
}
```

##### 제네릭을 사용한 코드

- 제네릭을 사용해 판단만 ViewModel 내부에서 처리하여 좀 더 간결하고 보기 편한 코드가 되었다 :)

```kotlin
// DetailFragment
updateHomeItems(detailModel)
// BookmarkFragment
updateHomeItems(bookmarkModel)
```

```kotlin
fun <T> updateHomeItems(updateModel: T?) {
    val homeModel = when (updateModel) {
        is DetailModel -> updateModel.toHomeModel()
        is BookmarkModel -> updateModel.toHomeModel()
        else -> return
    }
    _homeEvent.value = MainSharedEventForHome.UpdateHomeItem(homeModel)
}
```



## 느낀점

요즘 계속해서 어떻게 하면 보기좋은, 효율적인 클린코드일까를 많이 고민하는것 같다.

물론 내 코드들보다 훨씬 더 좋은 코드들이 많겠지만 차근차근 리팩토링 해가며 발전하는 재미가 있는 것 같다 :)



## End!

얼마 안남았으니까 더 열심히 해야겠다 끝 ~!!