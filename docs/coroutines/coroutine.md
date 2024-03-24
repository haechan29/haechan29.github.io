---
title: Coroutine
layout: default
parent: Coroutine
grand_parent: Android
nav_order: 1
---

## Coroutine이란?
### Coroutine
- 동시성 프로그래밍을 지원하는 경량화 Thread<br/>
- [비선점적 멀티태스킹을 위한 서브 루틴을 일반화한 컴퓨터 프로그램 구성요소] [1]<br/>

### 특징
- 중단과 재개: 코루틴은 실행 중인 위치를 기억하고 중단했다가 나중에 다시 그 지점부터 실행을 재개할 수 있습니다. 이를 통해 복잡한 비동기 코드를 동기 코드처럼 간결하게 작성할 수 있습니다.
- 컨텍스트 전환 비용 절감: 스레드보다 컨텍스트 전환 비용이 훨씬 적습니다. 이로 인해 많은 수의 동시 작업을 생성하고 관리할 수 있습니다.

### Coroutine Builder
1. runBlocking()<br/>
   - 현재 스레드를 차단(blocking)하여 코루틴을 실행합니다.<br/>
   - 주로 테스트 환경에서 사용되며, 다른 목적으로 사용하는 것은 권장되지 않습니다.<br/>
   
   Ex
   ```kotlin
   fun main() { 
       println("1")
       // runBlocking 코드 블럭이 실행 완료될 때까지 메인 스레드를 block함
       runBlocking {
           delay(1000)
           println("2")
       }
       println("3")
   }
   // 실행 순서: 1 - 2 - 3
   ```
   
   <br/>

2. launch()
   - [Suspend function] [2]<br/>
   - Job 객체를 반환합니다. Job 객체는 작업 상태를 관리하는 데에 사용됩니다.<br/>

   Ex
   ```kotlin
   fun main() { 
     println("1")
     GlobalScope.launch {
       delay(1000)
       println("2")
     }
     println("3")
   }
   // 실행 순서: 1 - 3 - 2
   ```
   
   <br/>

3. async()
   - Suspend function<br/>
   - Deferred 객체를 반환합니다. Deferred 객체는 작업 결과를 전달하는 데에 사용됩니다.<br/>
   
   <br/>
   
4. coroutineScope()
   - 현재 스레드를 차단(blocking)하여 코루틴을 실행합니다.<br/>
   - Suspend function<br/>
   
   Ex
   ```kotlin
   fun main() = runBlocking { 
       println("1")
       coroutineScope {
           delay(1000)
           println("2")
       }
       launch {
           delay(100)
           println("3")
       }
       println("4")
   }
   // 실행 순서: 1 - 2 - 4 - 3
   ```

[1]: https://dev.gmarket.com/82
[2]: suspend%20function.html
