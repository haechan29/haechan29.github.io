---
title: 테스트 원칙(2)
layout: default
parent: Test
grand_parent: Summary
nav_order: 1.2
---

## 테스트 원칙(2)
### 공개하지 않아야 않아야 하는 데이터를 검증하는 테스트 작성하지 않기
- 로그인 정보와 같이 숨겨야 하는 데이터를 이용하는 테스트는 작성하지 않아야 한다.<br/>
- ofType(), beInstanceOf()와 같은 메서드를 활용하여 데이터를 드러내지 않는 테스트를 작성하자.<br/><br/>

### 예시
- 테스트 대상<br/>
```kotlin
suspend fun login(id: String, password: String) {
    val request = LoginRequest(id, password)
    server.send(request)
}
```
<br/>

- 잘못된 테스트<sup>1</sup><br/>
```kotlin
context("로그인하면") {
    repository.login(id, password)
        
    test("서버로 로그인 요청을 전송한다") {
        // 로그인 요청이 아이디와 비밀번호를 포함한다는 것을 알 수 있다
        val request = LoginRequest(id, password)
        
        coVerify { server.send(request) }
    }
}
```
<br/>

- 괜찮은 테스트<br/>
```kotlin
context("로그인하면") {
    repository.login(id, password)

    test("서버로 로그인 요청을 전송한다") {
        // 요청의 타입을 밝히지 않는 경우
        coVerify { server.send(any()) }
    }

    test("서버로 로그인 요청을 전송한다") {
        // 요청의 타입을 밝히는 경우
        coVerify { server.send(ofType<LoginRequest>()) }
    }
}
```
<br/><br/>

<sup>1</sup>로그인 요청이 포함하는 정보를 공개한다.<br/>