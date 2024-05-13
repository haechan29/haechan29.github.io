---
title: 예외 처리, 취소
layout: default
parent: Flow
grand_parent: Android
nav_order: 3
---

## Flow의 예외 처리와 취소
### 예외 처리
- **Exception Transparency**<sup>1</sup>를 유지한다.<br/>
- [onEach(), catch()를 통해 예외를 효과적으로 처리할 수 있다] [1].<br/>
- retry(), retryWhen()을 통해 재시도할 수 있다.<br/>

### 취소
- 협력적 취소 모델<sup>2</sup>을 사용한다.<br/>
- Flow가 취소되어도 정상 동작으로 간주된다. 따라서 Flow#catch()에 검출되지 않고 onCompletion()으로 이동한다.<br/>

### 취소 상태 직접 확인하기
- CoroutineContext#ensureActive(): 코루틴이 취소되었다면 CancellationException를 발생시킨다.<br/>
- Job#isActive: onEach() 내부에서 코루틴의 상태를 확인.<br/>
- [cancellable()] [2]: onEach() 내부에서 isActive를 확인하는 것과 같다.<br/><br/>

<sup>1</sup>Exception Transparency: 예외는 Downstream으로 전달되어야 한다.<br/>
<sup>2</sup>협력적 취소 모델: 취소 요청이 발생했을 때 안전하게 작업을 중단하도록 "협력"하는 방식. 실행 중인 작업을 강제로 취소하는 대신, 작업을 실행하면서 취소 요청을 주기적으로(중단점마다) 확인한다.<br/>

[1]: https://simplecode.kr/42
[2]: https://kotlinlang.org/api/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.flow/cancellable.html