---
title: 예외 처리, 취소
layout: default
parent: Coroutines
grand_parent: Android
nav_order: 2.11
---

## Coroutine은 예외를 어떻게 처리할까?
### 예외 처리
- Exception Handler를 Top Level Coroutine<sup>1</sup>에 설정 한다.<br/>
- SupervisorJob을 사용하면 자식 코루틴이 발생시킨 예외를 전파하지 않는다.<br/>
- coroutineScope()는 동기적으로 실행되므로 부모 코루틴에서 try-catch를 통해 예외를 처리할 수 있다.<br/>

### 취소
- 협력적 취소 모델<sup>2</sup>을 사용한다.<br/>
- CancellationException은 코루틴의 상태를 제어하는 데만 사용된다. ExceptonHandler에 의해 검출되지 않는다.<br/>
- Job#isActive를 통해 코루틴의 상태를 직접 확인할 수 있다.<br/>
- Cancel 할 수 없게 하려면 withContext(NonCancellable)을 사용한다.<br/><br/>

<sup>1</sup>CoroutineScope()로부터 바로 생성된 Coroutine 또는 SupervisorJob의 자식.<br/>
<sup>2</sup>협력적 취소 모델: 취소 요청이 발생했을 때 안전하게 작업을 중단하도록 "협력"하는 방식. 실행 중인 작업을 강제로 취소하는 대신, 작업을 실행하면서 취소 요청을 주기적으로(중단점마다) 확인한다.<br/>