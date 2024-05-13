---
title: Suspend function
layout: default
parent: Coroutines
grand_parent: Android
nav_order: 1.2
---

## Suspend Function이란?
### Suspend Function
- 코틀린의 코루틴에서 사용되는 특별한 종류의 함수.<br/>
- 코루틴 스코프 내부 또는 다른 Suspend Function에서만 호출될 수 있습니다.<br/>
- 함수의 실행을 일시 중단(Suspend)할 수 있습니다.<br/>
- 비동기 코드를 동기 코드처럼 읽히게 하여 코드의 가독성과 유지보수성을 크게 향상시킵니다.<br/><br/>

Ex<br/>

```kotlin
fun main() {
    // 코루틴 스코프 생성
    val scope = CoroutineScope(EmptyCoroutineContext)

    scope.launch { // 이 코드 블럭이 코루틴 스코프 내부입니다.
        val response = fetchData() // suspend function이므로 코루틴 스코프 내부에서만 호출될 수 있습니다.
        
        /*
        일반적으로 서버 통신을 할때 Response를 처리하는 코드는 CallBack 형태로 전달합니다.
        그러나 Coroutine을 사용하면 response가 전달되기 전까지는 다음 코드를 실행하지 않고 있다가
        response를 전달받으면 다음 코드를 실행하므로 request를 보내는 코드와 reponse를 처리하는 코드를 같은 곳에 작성할 수 있습니다.
        */
        if (response.isSuccessful()) { 
            // reponse를 처리하는 코드
        }
    }
}

suspend fun fetchData() {
    // 서버와 통신하는 코드 (시간이 오래 걸리는 작업)
} 
```