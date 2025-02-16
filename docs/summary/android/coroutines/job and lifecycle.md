---
title: Job and Lifecycle
layout: default
parent: Coroutines
grand_parent: Android
nav_order: 2.2
---

## Job and Lifecycle
### Job
- 작업의 실행<sup>1</sup>, 대기<sup>2</sup>, 취소<sup>3</sup>, 상태 관리<sup>4</sup>와 같은 기능을 제공한다.<br/>
- CoroutineBuilder를 통해 Coroutine이 생성될 때 자동으로 생성된다.<br/>

### [Lifecycle] [1]
                                          wait children
    +-----+ start  +--------+ complete   +-------------+  finish  +-----------+
    | New | -----> | Active | ---------> | Completing  | -------> | Completed |
    +-----+        +--------+            +-------------+          +-----------+
                     |  cancel / fail       |
                     |     +----------------+
                     |     |
                     V     V
                 +------------+                           finish  +-----------+
                 | Cancelling | --------------------------------> | Cancelled |
                 +------------+                                   +-----------+

- New: 생성 후 아직 실행되지 않는 상태. CoroutineStart를 ``LAZY``로 설정하면 이 상태가 된다.<br/>
- Active: 실행 중인 상태. 일시 중단된 Job도 활성 상태로 간주된다.<br/>
- Completing: 작업 완료 후 자식 코루틴의 작업 완료를 기다리는 상태.<br/>
- Completed: 자신과 자식 코루틴이 모두 작업을 완료한 상태.<br/>
- Canceling: 취소 완료 후 자식 코루틴의 취소를 기다리는 상태.<br/>
- Cancelled: 자신과 자식 코루틴이 모두 취소를 완료한 상태.<br/><br/>

<sup>1</sup>실행: ``start()``를 통해 생성 상태의 작업을 시작한다.<br/> 
<sup>2</sup>대기: ``join()``을 통해 실행 중인 작업이 완료될 때까지 대기한다.<br/>
<sup>3</sup>[취소] [2]: ``cancel()``을 통해 실행 중인 작업을 취소한다.<br/>
<sup>4</sup>상태 관리: ``isActive()``, ``isCompleted()``, ``isCancelled()`` 등.<br/>


[1]: https://myungpyo.medium.com/코루틴-내부-상태-관리-알아보기-26b3ac5b9e48
[2]: cancellation.html