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

1. Flow 빌더 함수는 FlowCollector 컨텍스트를 제공한다.<br/>
```kotlin
fun <T> flow(
  block: suspend FlowCollector<T>.() -> Unit
): Flow<T>
```
<br/>