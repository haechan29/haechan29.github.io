---
title: LiveData 대체하기
layout: default
parent: Flow
grand_parent: Android
nav_order: 4
---

## Flow로 LiveData를 어떻게 대체할 수 있을까?
### Flow와 LiveData의 차이점
- Flow는 collect할 때마다 새로 생성된다.<br/>
- Flow는 액티비티의 생명 주기를 고려하지 않는다(액티비티가 파괴되어도 계속 실행된다).<br/>

### 생명 주기 반영하기
1. 생명 주기 메서드 직접 이용하기.<br/>
    ```kotlin
    val job: Job? = null
    
    overide fun onStart() {
        super.onStart()
        job = exampleFlow.collect {
            // collect data
        }.launchIn(lifeCycleScope)
    }
    
    overide fun onStop() {
        super.onStop()
        job?.cancel()
    }
    ```
    <br/>

2. [repeatOnLifecycle()] [1] 이용하기.<br/>
- Suspend Function.<br/>
- Coroutine Scope 내부에서 호출할 수 있다.<br/>

    ```kotlin
    lifecycleScope.launch {
        repeatOnLifecycle(Lifecycle.State.STARTED) {
            exampleViewModel.exampleFlow
            // collect data
        }
    }
    ``` 
    <br/>

3. [flowWithLifecycle()] [2] 이용하기.<br/>
- NOT Suspend Function.<br/>
- Lifecycle과 연동되는 Flow를 반환한다. 별도의 Coroutine Scope를 통해 구독해야 한다.<br/>

    ```kotlin
    lifecycleScope.launch {
        exampleViewModel.exampleFlow
            .flowWithLifecycle(lifecycle, Lifecycle.State.STARTED)
            .collect { 
                // collect data 
            }
    }
    ```

[1]: https://developer.android.com/reference/kotlin/androidx/lifecycle/package-summary#repeatonlifecycle
[2]: https://developer.android.com/reference/kotlin/androidx/lifecycle/package-summary#(kotlinx.coroutines.flow.Flow).flowWithLifecycle(androidx.lifecycle.Lifecycle,androidx.lifecycle.Lifecycle.State)