---
title: ViewModel과 Lifecycle
layout: default
parent: Post
date: 2024-06-21
---

## ViewModel은 어떻게 Lifecycle을 인지할까?
### 공식 문서 살펴보기
공식 문서를 읽고 두 번 놀랐다. 소스 코드를 뒤져보며 어렵게 이해한 내용이 공식 문에 너무 간단하게 정리되어 있어서 놀랐고, 한국말인데도 너무 안 읽혀서 한 번 더 놀랐다.<br/><br/>
우선 공식 문서에 적힌 내용은 다음과 같다.<br/><br/>

> [ViewModel의 지속 범위] [1]
>
> <sup>1</sup>ViewModel을 인스턴스화할 때는 ViewModelStoreOwner 인터페이스를 구현하는 객체를 전달합니다.<br/>
> <sup>2</sup>이는 탐색 대상, 탐색 그래프, 액티비티, 프래그먼트 또는 인터페이스를 구현하는 다른 유형일 수 있습니다.<br/>
> <sup>3</sup>그러면 ViewModel의 범위가 ViewModelStoreOwner의 수명 주기로 지정됩니다.<br/>
> <sup>4</sup>이는 ViewModelStoreOwner가 영구적으로 사라질 때까지 메모리에 남아 있습니다.<br/>

<br/>
이게 무슨 소릴까? 한 문장씩 천천히 이해해보자.<br/><br/>

### 한 문장씩 천천히 이해해보기<br/>
<br/>

> <sup>1</sup>ViewModel을 인스턴스화할 때는 ViewModelStoreOwner 인터페이스를 구현하는 객체를 전달합니다.<br/>

<br/>
ViewModel을 인스턴스화하는 방법은 크게 두 가지이다. (1) ViewModelFactory를 사용하여 직접 생성할 수도 있고, (2) 간단하게 by viewModels()를 호출할 수도 있다.<br/><br/>
사실 이 두 방법은 크게 다르지 않다. 왜냐면 by viewModels()를 호출해도 내부적으로 ViewModelFactory를 사용하기 떄문이다. AppCompatActivity#viewModels의 내부 구현을 살펴보자.<br/><br/>

**androidx.activity.ActivityViewModelLazy.kt**
```kotlin
@MainThread
public inline fun <reified VM : ViewModel> ComponentActivity.viewModels(
    noinline extrasProducer: (() -> CreationExtras)? = null,
    noinline factoryProducer: (() -> Factory)? = null
): Lazy<VM> {
    val factoryPromise = factoryProducer ?: {
        defaultViewModelProviderFactory
    }

    return ViewModelLazy(
        VM::class,
        { viewModelStore },
        factoryPromise,
        { extrasProducer?.invoke() ?: this.defaultViewModelCreationExtras }
    )
}
```
<br/>
조금 복잡해 보이지만, 중요한 점은 ViewModelLazy는 생성자를 통해 ViewModelStore과 ViewModelFactory를 반환하는 람다식을 전달한다는 점이다. 특히 ViewModelStore의 경우 ComponentActivity의 필드를 그대로 전달하는데, 이를 통해 ViewModelStore은 Activity 별로 하나 씩만 존재한다는 것을 알 수 있다.<br/><br/>
ViewModelStoreOwner 인터페이스를 구현하는 객체를 전달한다는 말이 바로 이 뜻이다. ViewModelStoreOwner는 이름에서 알 수 있듯이 ViewModelStore를 저장하고 있음을 명시하는 인터페이스이다. 그리고 by viewModels()가 호출될 때 전달되는 ComponentActivity가 바로 ViewModelStoreOwner이다. 애초부터 Activity 별로 ViewModel을 하나 씩만 가지도록 하기 위해서 ComponentActivity를 ViewModelStoreOwner로 설정한 것이다.<br/>
<br/>

> <sup>2</sup>이는 탐색 대상, 탐색 그래프, 액티비티, 프래그먼트 또는 인터페이스를 구현하는 다른 유형일 수 있습니다.<br/>

<br/>
위에서는 Activity를 살펴봤지만 Fragment에서 ViewModel을 인스턴스화하는 경우도 크게 다르지 않다.<br/>
<br/>

> <sup>3</sup>그러면 ViewModel의 범위가 ViewModelStoreOwner의 수명 주기로 지정됩니다.<br/>

<br/>
앞서 ViewModelStoreOwner는 내부적으로 ViewModelStore를 저장하고 있는 ComponentActivity와 같은 것이라고 했다. 즉, ComponentActivity가 ViewModel에 수명 주기를 직접 지정한다는 것이다.<br/><br/>
ComponentActivity의 생성자를 보면 소스 코드를 직접 확인할 수 있다.<br/><br/>

**androidx.activity.ComponentActivity.java**
```java
public ComponentActivity() {
    Lifecycle lifecycle = getLifecycle();
    //noinspection ConstantConditions
    if (lifecycle == null) {
        throw new IllegalStateException("getLifecycle() returned null in ComponentActivity's "
                + "constructor. Please make sure you are lazily constructing your Lifecycle "
                + "in the first call to getLifecycle() rather than relying on field "
                + "initialization.");
    }
    getLifecycle().addObserver(new LifecycleEventObserver() {
        @Override
        public void onStateChanged(@NonNull LifecycleOwner source,
                @NonNull Lifecycle.Event event) {
            if (event == Lifecycle.Event.ON_DESTROY) {
                // Clear out the available context
                mContextAwareHelper.clearAvailableContext();
                // And clear the ViewModelStore
                if (!isChangingConfigurations()) {
                    getViewModelStore().clear();
                }
            }
        }
    });
}
```
<br/>
Activity가 파괴될 떄 ViewModelStore#clear()가 호출되는 것을 볼 수 있다.<br/>
<br/>

> <sup>4</sup>이는 ViewModelStoreOwner가 영구적으로 사라질 때까지 메모리에 남아 있습니다.<br/>

<br/>
위의 ComponentActivity의 생성자에서 확인한 것과 같은 내용이다.<br/><br/>

## 정리
1. Activity는 ViewModel 객체를 하나만 생성한다.<br/>
2. Activity가 파괴될 때 ViewModel 객체도 사라진다.<br/><br/>

[1]: https://developer.android.com/topic/libraries/architecture/viewmodel?hl=ko#scope