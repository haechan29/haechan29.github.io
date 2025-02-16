---
title: Dispatcher
layout: default
parent: Coroutines
grand_parent: Android
nav_order: 2.2
---

## Dispatcher이란?
### Dispatcher
Coroutine을 실행할 스레드를 결정한다.<br/>

1. Main<br/>
    - Main 스레드(=UI 스레드)를 이용한다.<br/>
    - UI에 접근하는 경우 반드시 이용해야 한다.<br/><br/>

2. IO<br/>
    - 네트워크 작업을 진행할 때 이용한다.<br/>
    - 내부의 **공유 스레드풀**을 이용한다.(스레드 최대 64개)<br/><br/>

3. Default<br/>
    - 이름 그대로 Dispatcher를 설정하지 않았을 때 설정되는 기본 Dispatcher.<br/>
    - CPU 집약적인 작업에 적합하다.<br/>
    - 최대 CPU 갯수만큼의 스레드가 할당된다.<br/> 

### 설정 방법
- Coroutine Builder를 통해 설정할 수 있다. ``+`` 연산자를 이용한다.<br/>
- 명시하지 않으면 부모 코루틴의 Dispatcher을 상속받는다.<br/>
- withContext(): 코드 블럭이 다른 Dispatcher를 통해 수행되도록 한다.<br/>

