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
