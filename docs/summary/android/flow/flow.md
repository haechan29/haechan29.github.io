---
title: Flow 
layout: default
parent: Flow
grand_parent: Android
nav_order: 1
---

## Flow란?
### Flow
- 비동기적으로 계산되는 데이터의 흐름<br/>
- flow(), flowOf(), Collection#asFlow() 등의 Builder을 통해 생성한다.<br/>

### 동작 원리
1. Flow 빌더 함수는 FlowCollector 컨텍스트를 제공한다.<br/>
    ```kotlin
    fun <T> flow(
      block: suspend FlowCollector<T>.() -> Unit
    ): Flow<T>
    ```

    <br/>

2. Flow.collect()를 호출하면 FlowCollector 객체를 생성한다.<br/>
    ```kotlin
    interface Flow<out T> {
      suspend fun collect(collector: FlowCollector<T>)
    }
    
    suspend inline fun <T> Flow<T>.collect(crossinline action: suspend (value: T) -> Unit): Unit =
      collect(object: FlowCollector<T> {
        override suspend fun emit(value: T) = action(value)
      })
    ```
    
    <br/>

3. Flow 빌더 함수에서 emit()을 호출하면 collect()를 통해 전달된 람다 함수가 실행된다.<br/><br/>

Ex
```kotlin
// 아래의 두 코드는 같은 코드이다.
// 1
val myFlow = flow {
  emit(1)
  emit(2)
}

myFlow.collect {
  println(it)
}

// 2
println(1)
println(2)
```