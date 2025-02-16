---
title: Coroutine
layout: default
parent: Coroutines
grand_parent: Android
nav_order: 1
---

## Coroutine이란?
### Coroutine
- 동시성 프로그래밍을 지원하는 경량화 Thread.<br/>
- [비선점적 멀티태스킹을 위한 서브 루틴을 일반화한 컴퓨터 프로그램 구성요소] [1].<br/>

### 특징
- 중단과 재개: 코루틴은 실행 중인 위치를 기억하고 중단했다가 나중에 다시 그 지점부터 실행을 재개할 수 있습니다. 이를 통해 복잡한 비동기 코드를 동기 코드처럼 간결하게 작성할 수 있습니다.
- 컨텍스트 전환 비용 절감: 스레드보다 컨텍스트 전환 비용이 훨씬 적습니다. 이로 인해 많은 수의 동시 작업을 생성하고 관리할 수 있습니다.

[1]: https://dev.gmarket.com/82
