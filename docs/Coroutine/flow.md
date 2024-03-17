---
title: Flow
layout: default
parent: Coroutine
nav_order: 1
---

## Flow
### Flow 란?
비동기적으로 계산되는 데이터의 흐름
<br/>

<details>
  <summary>동작 원리</summary>

<br/>

1. Flow 빌더 함수는 FlowCollector 컨텍스트를 제공한다.<br/>

        fun <T> flow(
          block: suspend FlowCollector<T>.() -> Unit
        ): Flow<T>
<br/>

2. Flow.collect()를 호출하면 FlowCollector 객체를 생성한다.<br/>

        public interface Flow<out T> {
          public suspend fun collect(collector: FlowCollector<T>)
        }
        
        public suspend inline fun <T> Flow<T>.collect(crossinline action: suspend (value: T) -> Unit): Unit =
          collect(object : FlowCollector<T> {
            override suspend fun emit(value: T) = action(value)
          })
<br/>

3. Flow 빌더 함수에서 emit()을 호출하면 collect()를 통해 전달된 람다 함수가 실행된다.<br/>

</details>
<details>
  <summary>예시</summary>

<br/>

아래의 두 코드는 같은 코드이다.

    val myFlow = flow {
      emit(1)
      emit(2)
    }
    
    myFlow.collect {
      println(it)
    }
<br/>

    println(1)
    println(2)
</details>

### Flow Builder
- flow()
- flowOf()
- Collection#asFlow()

### Flow Operator
- terminal operator: first(), last(), single(), toList(), toCollection(), fold() 등<br/>
- intermediate operator: transform(), takeWhile(), dropWhile(), distinctUntilChanged() 등<br/>

### collect() vs launchIn() vs asLiveData()
- collect(): ``suspend`` function. 연속적으로 호출하면 앞의 호출이 끝나고, 뒤의 호출이 시작된다.
- launchIn(): ``regular`` function. 연속적으로 호출하면 두 블럭이 동시에 실행된다.
- asLiveData(): Flow를 LiveData로 변환한다.
<details>
  <summary>예시</summary>

<br/>

    val flow = flow {
      emit(1)
      delay(100)
      emit(2)
    }
    
    scope.launch {
      flow.collect {
        println("1: " + it)
      }
      flow.collect {
        println("2: " + it)
      }
    }
    // 실행 결과
    // 1: 1
    // 1: 2
    // 2: 1
    // 2: 2
<br/>

    val flow = flow {
      emit(1)
      delay(100)
      emit(2)
    }
    
    flow.onEach {
      println("1: " + it)
    }.launchIn(scope)
    
    flow.onEach {
        println("2: " + it)
    }.launchIn(scope)
    // 실행 결과
    // 1: 1
    // 2: 1
    // 1: 2
    // 2: 2
</details>
