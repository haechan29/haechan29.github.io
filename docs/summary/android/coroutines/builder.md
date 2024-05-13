---
title: Builder
layout: default
parent: Coroutines
grand_parent: Android
nav_order: 1.1
---

## 여러 가지 Coroutine Builder
### Coroutine Builder
1. runBlocking()<br/>
   - 현재 스레드를 차단(Blocking)하여 코루틴을 실행합니다.<br/>
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
   - [Suspend function] [1].<br/>
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
   - Suspend function.<br/>
   - Deferred 객체를 반환합니다. Deferred 객체는 작업 결과를 전달하는 데에 사용됩니다.<br/>
   
   <br/>
   
4. coroutineScope()
   - Suspend function.<br/>
   - 현재 스레드를 차단(Blocking)하여 코루틴을 실행합니다.<br/>
   
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

[1]: suspend%20function.html