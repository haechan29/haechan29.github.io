---
title: Dependency Injection
layout: default
parent: 객체 지향
grand_parent: Java, Kotlin
nav_order: 1.41
---

## Dependency Injection이란?
### Dependency Injection(DI)
- 의존성<sup>1</sup>을 직접 생성하는 대신 전달받는 것.<br/>
- 객체의 생성과 사용의 관심을 분리한다.<br/>
- 주로 생성자를 통해 의존성을 전달받는다.<br/>
- [역제어] [1]의 한 형태이다.<br/>

### [Service Locator] [2]
- 객체를 제공하는 책임을 가지는 클래스.<br/>
- DI에 비해 의존성이 불명확하다.<br/><br/>

<sup>1</sup>의존성: 한 객체가 다른 객체를 참조하는 것.<br/>

[1]: /docs/summary/etc/inversion%20of%20control.html
[2]: https://velog.io/@tco0427/DIDependency-Injection와-서비스-로케이터