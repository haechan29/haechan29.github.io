---
title: 제네릭 무한 연쇄 없애기 
layout: default
parent: Post
date: 2024-05-15
---

## 제네릭 무한 연쇄 없애기
### 문제 1
- 한 클래스가 제네릭을 사용하기 시작하면, 이를 사용하는 클래스에서도 제네릭을 사용하게 된다.<br/>
- 이로 인해 가독성이 떨어지고, 클래스의 역할을 알아보기가 어려워진다.<br/>

Ex
```kotlin
// AccessToken을 담을 DTO를 반환하는 API를 호출하는 Repository
val repository = Repository<Api<Dto<AccessToken>>>()
```
<br/>

### 해결 1
- 제네릭을 사용하는 인터페이스를 만든다.<br/>
- 제네릭 인터페이스를 래핑하는 인터페이스를 만든다.<br/>

Ex
```kotlin
// 제네릭 인터페이스
private interface Repository<T: Token> {
    // Repository의 공통 사항
}

// 제네릭 인터페이스를 래핑하는 인터페이스
// 역할이 명확하면서도 구현할 때는 제네릭 클래스처럼 타입이 정해진다 
abstract class AccessTokenRepository: Repository<AccessToken>
```
<br/>

### 문제 2
- AccessTokenRepository와 RefreshTokenRepository의 구현이 거의 똑같다.<br/>
- 위임을 통해 코드의 중복을 없애고 싶다.<br/>