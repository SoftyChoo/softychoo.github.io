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

# [Android/Kotlin] ListAdapter, DiffUtil

* toc
{:toc}


[ListAtapter(Developer)](https://developer.android.com/reference/androidx/recyclerview/widget/ListAdapter)

## 📌 ListAdapter?

- `AsyncListDiffer`를 더 쓰기 쉽게 랩핑한 클래스이다.

>  [`AsyncListDiffer`](https://developer.android.com/reference/androidx/recyclerview/widget/AsyncListDiffer)는 DiffUtil을 편하게 쓰기 위해서 만들어진 클래스로, DiffUtil에 대해 자체적으로 스레드 처리를 해준다.

- 즉, List를 관리하기 쉽게 DiffUtil을 비동기 처리해주는 기능이 들어간 Adapter라고 볼 수 있다.



## 📌 DiffUtil?

- 두 데이터셋을 받아서 그 차이를 계산해주는 클래스이다. 
- DiffUtil은 기존의 데이터와 새로 들어온 데이터를 비교해 그 중 변경점 만을 파악하여 Recyclerview에 반영해준다.



## 👨🏻‍💻 사용

- RecyclerView Adapter를 만들 때 ListAdapter를 상속한다.
- 다음으로 `DiffUtil.Callback` 추상 클래스를 받아준다.
- 이렇게 되면 `currentList`를 통해 현재 데이터를 불러오고 `submitList`를 통해 데이터를 갱신할 수 있게 된다.

```kotlin
class UserAdapter extends ListAdapter<User, UserViewHolder> {
    public UserAdapter() {
        super(User.DIFF_CALLBACK);
    }
    @Override
    public void onBindViewHolder(UserViewHolder holder, int position) {
        holder.bindTo(getItem(position));
    }
    public static final DiffUtil.ItemCallback<User> DIFF_CALLBACK =
            new DiffUtil.ItemCallback<User>() {
        @Override
        public boolean areItemsTheSame(
                @NonNull User oldUser, @NonNull User newUser) {
            // User properties may have changed if reloaded from the DB, but ID is fixed
            return oldUser.getId() == newUser.getId();
        }
        @Override
        public boolean areContentsTheSame(
                @NonNull User oldUser, @NonNull User newUser) {
            // NOTE: if you use equals, your object must properly override Object#equals()
            // Incorrectly returning false here will result in too many animations.
            return oldUser.equals(newUser);
        }
    }
}
```

- 다음과 같이 object를 통해서도 구현 가능하다.

```kotlin
class TodoListAdapter(
    private val onClickItem: (Int, TodoModel) -> Unit
) : ListAdapter<TodoModel, TodoListAdapter.ViewHolder>(
    object : DiffUtil.ItemCallback<TodoModel>() {
        override fun areItemsTheSame(
            oldItem: TodoModel,
            newItem: TodoModel
        ): Boolean {
            return  oldItem.id == newItem.id
        }

        override fun areContentsTheSame(
            oldItem: TodoModel,
            newItem: TodoModel
        ): Boolean {
            return oldItem == newItem
        }
    }
) {
  ...
}
```



#### 데이터 갱신 코드 예시

- ListAdapter는 기존에 사용하고 있던 리스트를 재활용하지 못하는데 그 이유는 기존에 들어왔던 ArrayList와 새로 들어온 ArrayList를 다르게 인식하기 때문이다
- 따라서 `submitList()`를 할 때 새로운 ArrayList의 인스턴스를 생성해서 넣어주어야 한다.

```kotlin
 fun addItem(todoModel: TodoModel?) {
        val list = currentList.toMutableList() //새로운 리스트 생성 기존의 데이터로 초기화
        list.add(todoModel) //새로 생성된 리스트에 객체 추가
        submitList(list) // submitList()를 통해 갱신
    }

```

