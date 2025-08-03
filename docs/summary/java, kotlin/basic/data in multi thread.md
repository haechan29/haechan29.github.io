---
title: 멀티 스레드에서 데이터 처리
layout: default
parent: Basic
grand_parent: Java, Kotlin
date: 2025-08-03
---

## 멀티 스레드에서 데이터 처리
### 데이터 경쟁
멀티 스레드 환경에서는 데이터 경쟁(= 데이터에 접근하는 순서에 따라 결과가 달라지는 현상)이 발생할 수 있다.
예를 들어 아래 함수를 두 스레드에서 호출한다고 해보자.<br/><br/>

```kotlin
var a = 0

fun foo() {
    a++
}

```
<br/>
이 함수는 변수 a에 저장된 값을 읽고(1), 그 값에 1을 더한 값을 구한 후에(2), 이 값을 다시 변수 a에 할당하는(3) 세 과정으로 이루어진다.
그런데 만약 두 스레드 A, B에서 해당 함수를 거의 동시에 호출하여 아래와 같은 순서로 코드가 실행된다면 어떨까?<br/><br/>

```text
A1: 스레드 A가 a를 읽음 (a: 0)
A2: 스레드 A가 a + 1 계산 (temp: 1)
B1: 스레드 B가 a를 읽음 (a: 0)
A3: 스레드 A가 a에 1 저장 (a: 1)
B2: 스레드 B가 a + 1 계산 (temp2: 1)
B3: 스레드 B가 a에 1 저장 (a: 1)
```
<br/>
a가 2만큼 증가할 것이라는 예상과 달리 B 스레드는 업데이트 이전의 값을 읽었기 때문에 결과적으로 a는 처음보다 1만큼만 커진다.<br/>
위 사례는 비교적 원인이 간단한 사례다. 하지만 더 무서운 사례도 있다.<br/><br/>

```kotlin
suspend fun foo() = coroutineScope {
    val worker = Worker()
    val job = launch(Dispatchers.Default) {
        worker.run()
    }
    delay(100)
    worker.stop()
    job.join() // worker#run()이 종료되면 job도 종료된다
}

class Worker {
    private var running = true

    fun run() {
        while (running) {}
    }

    fun stop() {
        running = false
    }
}
```
<br/>
이 함수는 영원히 종료되지 않을 수도 있다.<br/>
running의 값이 메인 스레드와 Default 스레드에 <b>각각</b> 캐싱되어 메인 스레드에서 running의 값을 false로 바꿔도 Default 스레드에서는 여전히 running의 값을 true로 인식해서 while문을 탈출하지 못하는 경우에 그렇다.<sup>1</sup><br/>

이와 같은 데이터 오염 문제를 방지하기 위해 **가시성**과 **원자성** 개념이 필요하다.<br/>
<u>가시성이란 여러 스레드에서 같은 값을 보는 것</u>이다.
<u>원자성이란 원자처럼 쪼개지지 않는 것</u>이다. 위의 a++는 사실 세 명령어로 나뉘고, 그렇기 때문에 한 스레드에서 명령어가 종료되기 전에 다른 스레드에서 명령어를 시작하는 것이 가능하다.
이것을 한 묶음으로 묶어 여러 스레드에서 동시에 접근할 수 없게 하는 것이다.<br/>

### 가시성과 원자성
<u>가시성을 보존하기 위해선 CPU 캐시를 사용하지 않고 메모리를 직접 참조</u>하게 하면 된다.
kotlin에서는 @Volatile 애너테이션을 통해 해당 기능을 사용할 수 있다.<br/>

원자성을 보존하기 위해선 크게 두 가지 방식이 있다.<br/>
첫째는 <u>접근 가능한 스레드의 수를 제한</u>하는 방법이다.
kotlin에서는 synchronized 블럭을 사용할 수도 있고, 뮤텍스나 세마포어를 사용할 수도 있다.
이 경우에 스레드가 차단되므로 성능 저하가 발생한다.<br/>

둘째는 <u>연산 후에 연산에 이용된 값이 오염되었는지 확인</u>하는 방법이다.<br/>
kotlin에서는 atomic 패키지를 사용하면 되는데, 위의 foo()를 다음과 같이 바꿀 수 있다.<br/><br/>

```kotlin
val a = AtomicInteger(0)

fun foo() {
    a.addAndGet(1)
}
```
<br/>

이 코드는 내부 연산 과정은 다음과 같다.
연산을 시작하기 전에 변수의 값을 저장해둔다.
물론 공유 자원이니 Valotile로 선언한다.
더하기 연산이 끝나면 변수의 값이 처음 값과 비교하여 동일한 경우에만 연산을 적용하고, 그렇지 않으면 루프를 돌며 재시도한다<sup>2</sup>.<br/><br/>

<sup>1</sup>Java에는 MESI와 같은 캐시 일관성 프로토콜이 런타임에 동작한다.
그러니 스레드에서 오래 걸리는 작업을 수행한다면 yield() 등을 호출하여 캐시 무효화나 메모리 동기화의 기회를 주자.<br/>
<sup>2</sup>Compare-And-Swap(CAS)이라고 한다.<br/>