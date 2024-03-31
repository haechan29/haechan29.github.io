---
title: Exception Handling
layout: default
parent: Coroutines
grand_parent: Android
nav_order: 2.12
---

## Exception Handling이란?
### Exception Handling
코루틴에서 발생한 예외를 처리하는 메커니즘.<br/>

### 사용 방법
- Exception Handler는 Top Level Coroutine<sup>1</sup>에 설정해야 한다.<br/>
- 자식 코루틴이 처리하지 못한 에외는 부모 코루틴에게 전달된다. 단, async()의 경우 반환한 Deferred 객체가 실행되는 시점에 예외를 발생시킨다. 
- coroutineScope()는 동기적으로 실행되므로 부모 코루틴에서 try-catch를 통해 예외를 처리할 수 있다.
- SupervisorJob을 사용하면 자식 코루틴이 발생시킨 예외를 전파하지 않는다.<br/><br/>

<sup>1</sup>CoroutineScope()로부터 바로 생성된 Coroutine 또는 SupervisorJob의 자식.<br/>