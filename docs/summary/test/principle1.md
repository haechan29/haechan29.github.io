---
title: 테스트 원칙(1)
layout: default
parent: Test
grand_parent: Summary
nav_order: 1.1
---

## 테스트 원칙(1)
### 요구 사항을 위반하는 테스트 작성하지 않기
- 프로그래머는 요구 사항을 준수하기 위해 특정 코드에 대한 접근을 제어할 수 있다.<br/>
- 하지만 테스트가 요구 사항을 위반하면, 실제 코드도 요구 사항을 위반할 수 있다.<br/>
- 따라서 테스트 또한 요구 사항을 준수해야 한다. 즉, 요구 사항을 위반하는 테스트는 작성하지 않아야 한다.<br/><br/>

### 예시
- 요구 사항<br/>
   1. 로그인 과정은 (1)아이디, 비밀번호의 유효성을 검사하고 (2)로그인 요청을 생성하는 단계를 포함한다.<br/>
   2. 두 단계는 분리되어선 안된다. 즉, 로그인 요청을 전송하기에 앞서 반드시 아이디, 비밀번호의 유효성을 검사해야 한다.<br/><br/>

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

- 요구 사항을 준수하는 테스트<br/>
   - 유효하지 않은 아이디를 입력하면 로그인이 실패한다.<br/>
   - 유효하지 않은 비밀번호를 입력하면 로그인이 실패한다.<br/>
   - 유효한 아이디와 비밀번호를 입력하면 로그인 요청을 생성한다.<br/><br/>

- 요구 사항을 위반하는 테스트
   - 로그인 요청을 생성하면 로그인 요청을 전송한다<sup>1</sup>.<br/><br/>

<sup>1</sup>아이디와 비밀번호의 유효성을 검사하지 않고 로그인 요청을 생성하는 코드를 작성할 수 있게 된다.<br/>