---
title: Kotest를 사용할 때 주의할 점 (2)
layout: default
parent: Kotest
grand_parent: Android
nav_order: 1.2
---

## Kotest를 사용할 때 주의할 점 (2)
### 숨겨야 할 것을 공개하지 않는다
예를 들어 로그인 요청을 서버로 전송하는 메서드가 있다고 해보자.<br/>
```kotlin
suspend fun login(id: String, password: String) {
    val request = LoginRequest(id, password)
    server.send(request)
}
```
<br/>

이 메서드를 테스트하기 위해 아래와 같은 테스트를 작성했다고 해보자.<br/>
- 로그인하면 서버로 로그인 요청을 전송한다<br/><br/>

해당 테스트를 MockK을 이용해서 작성하면 아래와 같다.
```kotlin
when("로그인하면") {
    repository.login(id, password)
        
    then("서버로 로그인 요청을 전송한다") {
        val request = LoginRequest(id, password)
        
        coVerify { server.send(request) }
    }
}
```
<br/>

이러한 테스트는 작성되어선 안된다. 왜냐하면 로그인 요청이 무엇을 포함하는지 겉으로 드러나기 때문이다. 로그인 정보는 숨겨야 하는 내용이다.<br/><br/>

따라서 서버로 로그인 요청이 전송되었는지는 아래와 같이 확인한다.<br/>
```kotlin
when("로그인하면") {
    repository.login(id, password)

    then("서버로 로그인 요청을 전송한다") {
        // 요청의 타입을 밝히지 않는 경우
        coVerify { server.send(any()) }
    }

    then("서버로 로그인 요청을 전송한다") {
        // 요청의 타입을 밝히는 경우
        coVerify { server.send(ofType<LoginRequest>()) }
    }
}
```
<br/>

Kotest의 ``ofType()`` 메서드를 활용하면 검증 과정에서 메서드의 인자로 전달되는 정보를 숨길 수 있다.<br/> 