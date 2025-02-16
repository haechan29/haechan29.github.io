---
title: Buffer
layout: default
parent: Flow
grand_parent: Android
nav_order: 7
---

## Buffer란?
### Buffer
- Back Pressure<sup>1</sup>을 관리한다.<br/>
- buffer()을 통해 사용할 수 있다. Capacity<sup>2</sup>, Buffer Overflow 관리 전략<sup>3</sup>을 인자로 갖는다.<br/><br/>

Ex<br/>
```kotlin
// Buffer을 사용하지 않은 경우
// 값을 방출한 후에 수집되기 전까지 다음 값을 방출하지 않는다. 
val flow = flow {
  repeat(5) {
    println("Emitter: start cooking pancake: $it")
    delay(100) // time spent to cook pancake
    println("Emitter: finish cooking pancake: $it")
    emit(it)
  }
}

flow.collect {
  println("Collector: start eating pancake: $it")
  delay(300) // time spent to eat pancake
  println("Collector: finish eating pancake: $it")
}
// 출력
// Emitter: start cooking pancake: 0
// Emitter: finish cooking pancake: 0
// Collector: start eating pancake: 0
// Collector: finish eating pancake: 0
// Emitter: start cooking pancake: 1
// Emitter: finish cooking pancake: 1
// Collector: start eating pancake: 1
// Collector: finish eating pancake: 1
// …

// Buffer을 사용한 경우 
val flow = flow {
    repeat(5) {
        println("Emitter: start cooking pancake: $it")
        delay(100) // time spent to cook pancake
        println("Emitter: finish cooking pancake: $it")
        emit(it)
    }.buffer()
}

flow.collect {
    println("Collector: start eating pancake: $it")
    delay(300) // time spent to eat pancake
    println("Collector: finish eating pancake: $it")
}
// 출력
// Emitter: start cooking pancake: 0
// Emitter: finish cooking pancake: 0
// Collector: start eating pancake: 0
// Emitter: start cooking pancake: 1
// Emitter: finish cooking pancake: 1
// Emitter: start cooking pancake: 2
// Emitter: finish cooking pancake: 2
// Emitter: start cooking pancake: 3
// Collector: finish eating pancake: 0
// …
```
<br/><br/>

<sup>1</sup>Back Pressure: 데이터를 생산하는 속도가 소비하는 속도보다 빠를 떄, 이로 인해 발생할 수 있는 데이터 손실.<br/>
<sup>2</sup>기본 값은 64이다. UNLIMITED를 설정할 수 있다.<br/>
<sup>3</sup>SUSPEND(기본 값), DROP_OLDEST, DROP_LATEST 중에서 선택할 수 있다.<br/> 