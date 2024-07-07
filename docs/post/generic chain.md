---
title: 제네릭 무한 연쇄 없애기 
layout: default
parent: Post
date: 2024-05-15
---

## 제네릭 무한 연쇄 없애기 <sub>[Youtube] [Youtube Link]</sub>
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
    suspend fun save(token: T)
    suspend fun load(): T?
}

// 제네릭 인터페이스를 래핑하는 인터페이스
// 역할이 명확하면서도 구현할 때는 제네릭 클래스처럼 타입이 정해진다 
abstract class AccessTokenRepository: Repository<AccessToken>
```
<br/>

### 문제 2
- 제네릭을 사용하지 않아 구현 클래스에 코드 중복이 많아진다.<br/>

Ex

```kotlin
class AccessTokenRepositoryImpl : AccessTokenRepository() {
    private var accessToken: AccessToken? = null

    override suspend fun save(accessToken: AccessToken) {
        this.accessToken = accessToken
    }

    override suspend fun load(): AccessToken? {
        return accessToken
    }
}

// AccessTokenRepositoryImpl과 구현 사항이 거의 똑같다
class RefreshTokenRepositoryImpl : RefreshTokenRepository() {
    private var refreshToken: RefreshToken? = null

    override suspend fun save(refreshToken: RefreshToken) {
        this.refreshToken = refreshToken
    }

    override suspend fun load(): RefreshToken? {
        return refreshToken
    }
}
```
<br/>

### 해결 2
- 상위 타입의 구현 클래스를 만들고, 구현 사항을 위임한다.<br/>

Ex
```kotlin
// 기존에 했던 것과 같은 방식으로
// 상위 타입의 제네릭 인터페이스를 래핑하는 인터페이스를 만든다.
abstract class SuperTokenRepository: Repository<Token>

// 이후 제네릭 인터페이스의 구현 클래스를 만든다
class SuperTokenRepositoryImpl: SuperTokenRepository() {
    private var token: Token? = null
    
    override suspend fun save(token: Token) {
        this.token = token
    }
    
    override suspend fun load(): Token? {
        return token
    }
}

// 기존의 구현 클래스에서는 상위 타입의 구현 클래스에게 구현을 위임한다
class AccessTokenRepositoryImpl : AccessTokenRepository() {
    private var delegate = SuperTokenRepositoryImpl()

    override suspend fun save(accessToken: AccessToken) {
        delegate.save(accessToken)
    }

    override suspend fun load(): AccessToken? {
        // delegate.load()는 Token? 타입을 반환하므로
        // AccessToken? 타입으로 변환해야 한다
        return delegate.load()?.let { reify(it) }
    }
}

// 런타임에 추상 타입인 Token을 구체 타입인
// AccessToken 또는 RefreshToken으로 변환한다
inline fun <reified T: Token> reify(token: Token): T {
    return token as T
}
```
<br/>

[Youtube Link]: https://www.youtube.com/watch?v=I7kxH8AXqwQ