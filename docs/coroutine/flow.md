---
title: Flow
layout: default
parent: Coroutine
nav_order: 1
---

# Flow
## Flow
### Flow 란?
비동기적으로 계산되는 데이터의 흐름
<br/>

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
      collect(object : FlowCollector<T> {
        override suspend fun emit(value: T) = action(value)
      })
    ```
    
    <br/>

3. Flow 빌더 함수에서 emit()을 호출하면 collect()를 통해 전달된 람다 함수가 실행된다.<br/>
<br/>

Ex. 아래의 두 코드는 같은 코드이다.

```kotlin
val myFlow = flow {
  emit(1)
  emit(2)
}

myFlow.collect {
  println(it)
}
```

<br/>

```kotlin
println(1)
println(2)
```

### Flow Builder
- flow()
- flowOf()
- Collection#asFlow()
<br/>

### Flow Operator
- terminal operator: first(), last(), single(), toList(), toCollection(), fold() 등<br/>
- intermediate operator: transform(), takeWhile(), dropWhile(), distinctUntilChanged() 등<br/>
<br/>

### collect() vs launchIn() vs asLiveData()
- collect(): ``suspend`` function. 연속적으로 호출하면 앞의 호출이 끝나고, 뒤의 호출이 시작된다.<br/>
- launchIn(): ``regular`` function. 연속적으로 호출하면 두 블럭이 동시에 실행된다.<br/>
- asLiveData(): Flow를 LiveData로 변환한다.<br/>
<br/>

Ex

```kotlin
val flow = flow {
  emit(1)
  delay(100)
  emit(2)
}
scope.launch {
  flow.collect {
    println("1: " + it)
  }
  flow.collect {
    println("2: " + it)
  }
}
// 실행 결과
// 1: 1
// 1: 2
// 2: 1
// 2: 2
```

<br/>

```kotlin
val flow = flow {
  emit(1)
  delay(100)
  emit(2)
}
flow.onEach {
  println("1: " + it)
}.launchIn(scope)
flow.onEach {
    println("2: " + it)
}.launchIn(scope)
// 실행 결과
// 1: 1
// 2: 1
// 1: 2
// 2: 2
```
