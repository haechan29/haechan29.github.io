---
title: Scope, Context
layout: default
parent: Coroutines
grand_parent: Android
nav_order: 2
---

## Scope와 Context
### Scope
- Context만을 가지는 인터페이스.<br/>
- [Structured Concurrency] [1]를 지원한다.<br/>

### Context
- Map과 유사한 구조.<br/>
- [Job] [2], [Dispatcher] [3], [ExceptionHandler] [4], Name 등 Coroutine의 다양한 요소를 포함한다.<br/>

### ViewModelScope
- ViewModel에 의해 제공되는 Scope.<br/>
- ViewModel의 Lifecycle과 연동된다(onCleared() 호출시 취소된다).<br/>
- SupervisorJob<sup>1</sup>을 가진다.<br/>
- [Dispatcher.Main.immediate] [5]을 사용한다.<br/>

### LifecycleScope
- LifecycleOwner의 Lifecycle과 연결된다.<br/>
- Activity, Fragment와 연결할 경우 화면 회전과 같은 Configuration 변경 시에 취소된다.<br/><br/>

<sup>1</sup>SupervisorJob: 자식 코루틴이 발생시킨 예외를 전파하지 않는다.<br/>

[1]: structured%20concurrency.html
[2]: job%20and%20lifecycle.html
[3]: dispatcher.html
[4]: exception%20handling.html
[5]: https://jisungbin.medium.com/dispatchers-main-immediate-의-대한-이해-9f073be21e5a