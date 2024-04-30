---
title: 테스트를 작성할 때 주의할 점
layout: default
parent: Kotest, MockK
grand_parent: Android
nav_order: 1
---

## 테스트를 작성할 때 주의할 점
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

### 원칙
{: .highlight }
프로그래머에 의해 구현되어서는 안되는 내용은 테스트도 이루어지면 안된다.<br/>
테스트 가능한 코드는 프로그래밍 가능한 코드이다. 즉, 에시와 함께 구체적인 내용을 살펴보자.<br/><br/>

### 예시 1. 트랜잭션을 쪼개지 않는다
예를 들어 로그인 과정에서 (1)아이디, 비밀번호의 유효성을 검사하고 (2)로그인 요청을 생성하는 단계가 있다고 해보자.<br/>
```kotlin
suspend fun login(id: String, password: String) {
    // 1. 아이디와 비밀번호의 유효성 검사
    if (!validator.isValid(id, password)) {
        // 로그인 실패 처리
    }
    
    // 2. 로그인 요청 생성
    val request = LoginRequestBuilder.build(id, password)
    
    // 로그인 요청 전송 처리
}
```
<br/>

여기서 두 단계는 분리되어선 안된다고 해보자. 즉, 로그인 요청을 전송하기에 앞서 반드시 아이디, 비밀번호의 유효성을 검사해야 한다고 해보자. 이 경우에 각각의 단계를 독립적으로 테스트할 수 없다.<br/><br/>

각 단계가 독립적으로 **테스트될 수 있다**는 이야기는 각 단계가 독립적으로 **프로그래밍될 수도 있다**는 이야기이다. 이로 인해 "로그인 요청을 생성하기에 앞서 반드시 아이디, 비밀번호의 유효성 검사가 진행되어야 한다"는 요구 사항이 꺠질 수 있다(아이디, 비밀번호의 유효성 검사를 깜빡하고 로그인 요청을 생성하는 불상사가 생길 수 있다).<br/><br/>

따라서 두 단계는 한 번에 테스트되어야 한다. 이와 관련하여 테스트 가능한 내역은 아래와 같다.<br/>
- 유효하지 않은 아이디를 입력하면 로그인이 실패한다<br/>
- 유효하지 않은 비밀번호를 입력하면 로그인이 실패한다<br/>
- 유효한 아이디와 비밀번호를 입력하면 로그인 요청을 생성한다<br/><br/>

반면에 이런 테스트는 나와선 안된다.<br/>
- 로그인 요청을 생성하면 로그인 요청을 전송한다<br/><br/>

이 내용을 테스트로 구현하려면 Given 부분에 로그인 요청을 생성하는 과정이 있어야 한다. 이를 위해서는 (아이디, 비밀번호의 유효성 검사를 진행하지 않고) 로그인 요청만을 생성하는 코드가 만들어져야 한다. 하지만 이 코드는 아이디, 비밀번호의 유효성 검사를 깜빡하고 로그인 요청을 생성하는 불상사를 낳을 수 있다. 따라서 이런 테스트는 애초부터 만들어지면 안된다.<br/><br/>

### 예시 2. 숨겨야 할 것을 공개하지 않는다
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

해당 테스트를 MockK을 이용해서 작성하면 아래와 같다.<br/>
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

Kotest의 ``ofType()`` 메서드를 활용하면 검증 과정에서 메서드의 인자로 전달되는 정보를 숨길 수 있다.<br/><br/>

### 결론
이와 같이 **테스트 가능한 코드는 프로그래밍 가능한 코드**라는 점을 이해하고, 테스트를 작성하도록 하자.<br/>