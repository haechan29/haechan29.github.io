---
title: Cancellation
layout: default
parent: Coroutines
grand_parent: Android
nav_order: 2.11
---

## Cancellation이란?
### Cancellation
- 코루틴을 취소하는 메커니즘.<br/>
- CancellationException을 발생시킨다.<br/>

### 사용 방법
- 코루틴이 취소되었을 때 작업을 중지하려면 아래의 방법을 사용한다.<br/>
    - yield()와 같은 Suspend Function을 호출한다.
    - CoroutineScope.isActive를 통해 상태를 확인한다.<br/>
    - CoroutineScope.ensureActive()를 호출한다.<br/><br/>

- Cancel 할 수 없게 하려면 withContext(NonCancellable)을 사용한다.<br/>