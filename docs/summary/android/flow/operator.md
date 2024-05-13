---
title: Operator
layout: default
parent: Flow
grand_parent: Android
nav_order: 2
---

## 여러 가지 Flow Operator
### Terminal operator
first(), last(), single(), toList(), toCollection(), fold() 등.<br/>

### Intermediate operator
transform(), takeWhile(), dropWhile(), distinctUntilChanged() 등.<br/>

### collect() vs launchIn() vs asLiveData()
- collect(): ``suspend`` function. 연속적으로 호출하면 앞의 호출이 끝나고, 뒤의 호출이 시작된다.<br/>
- launchIn(): ``regular`` function. 연속적으로 호출하면 두 블럭이 동시에 실행된다.<br/>
- asLiveData(): Flow를 LiveData로 변환한다.<br/><br/>

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
