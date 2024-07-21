---
title: Call by value
layout: default
parent: Post
date: 2024-07-21
---

## Call by value vs Call by reference
Call by value와 Call by reference가 이해하기 어려운 이유는 여러 가지가 있다.<br/>
첫째, 이해하지 못했는데 이해했다고 착각하기가 쉽다.<br/>
둘째, 이해하지 못해도 문제가 되는 경우가 잘 없다. (하지만 문제가 생기면 크게 문제가 된다)<br/><br/>

이 글에서는 Call by value와 Call by reference의 차이를 이론적으로, 또 실제적으로 이해하려고 해볼 것이다.<br/><br/>  

### Call by value와 Call by reference의 의미 이해하기
1. Call이란?<br/>
   **저장된 값을 읽어낸다**는 의미이다. 기본적으로 Java의 프로그램은 main()을 시작으로, [Stack 영역] [1]의 함수를 실행/종료시킨다.
   따라서 프로그램의 명령을 실행하기 위해서는 Stack 영역에 값을 저장하고, 읽어내는 작업이 필요하다.<br/><br/>

   해당 과정이 어떻게 이루어지는지 예시를 통해 간단히 알아보자.<br/>

   ```kotlin
   var a = 0           // Primitive type
   var b = Object()    // Reference type
   ```
   <br/>

   첫째 줄의 코드는 Stack 영역에 a라는 메모리 공간을 할당하고, 해당 메모리 공간에 0이라는 값을 저장한다.<br/>
   둘째 줄의 코드도 비슷한 기능을 하는데, 약간 다르다. Object는 Primitive 타입이 아니라 Reference 타입이므로, 해당 값을 Stack 영역에 직접 저장하지 않는다. 대신, 런타임에 해당 인스턴스의 크기를 계산하여 Heap 영역에 메모리 공간을 할당하고, 값을 저장한다. 그리고 Stack 영역에는 해당 메모리 주소(Heap 영역의 메모리 공간의 주소)를 전달한다.<br/>
   이렇게 저장된 값을 읽어오는 것을 Call이라고 한다.<br/><br/>

2. value, reference<br/>
   value는 **값 자체**를 의미한다. 그리고 reference는 **값이 저장되는 메모리 주소**를 의미한다. 예를 들어 아래와 같은 코드를 보자.<br/>
   
   ```kotlin
   var a = 0
   var b = a
   ```
   <br/>
   
   여기서 변수 b가 가리키는 메모리 공간은 무엇을 저장하고 있을까?<br/>
   (1) 변수 a가 가리키는 메모리 공간에 저장된 값(0)<br/>
   (2) 변수 a가 가리키는 메모리 주소<br/><br/>
   
   정답은 (1)이다. 둘째 줄의 코드는 단순히 a가 가리키는 메모리 공간에 저장된 값을 새로운 메모리 공간(b)에 할당한다.<br/>
   따라서 b의 값을 변경한다고 해서 a의 값은 변경되지 않는다. 두 변수가 가리키는 메모리 주소가 다르기 때문이다. (이것은 Primitive 타입이든 Reference 타입이든 마찬가지다)<br/>
   여기서 저장되는 값(0)이 value이다. 반면에 값이 저장되는 메모리 주소(a와 b)가 reference다.<br/>
   위의 예시에서 두 변수의 reference는 다르고, value는 같다.<br/><br/>

3. Call by value, Call by reference<br/>
   1번과 2번을 이해했다면, 이제는 Call by value와 Call by reference를 이해할 준비가 됐다.<br/><br/>

   Call by value와 Call by reference는 **저장되어 있는 값을 읽어내는(call) 방식의 차이**이다. **읽어내는 대상이 메모리 공간에 저장된 값(value)인지 아니면 메모리 주소(reference)인지에 따라 구분**되는 것이다.<br/>
   위의 2에서 살펴봤듯 **Java는 Call by value**이고, 포인터 개념을 지원하는 C++은 Call by reference이다.<br/><br/>

### Call by value와 Call by reference를 구분하여 오류 코드 방지하기
Call by value와 Call by reference를 구분하지 못하면 의도하지 않은 문제가 발생할 수 있다. 예시를 통해 확인해보자.<br/><br/>

```kotlin
fun main() {
    val room = Room(24)
    
    AirConditioner.lowerTemperatureOfRoom(room)
    println(room.temperature) // #1
    
    AirConditioner.lowerTemperature(room.temperature)
    println(room.temperature) // #2
}

object AirConditioner {
    fun lowerTemperatureOfRoom(room: Room) {
        room.temparature--
    }
    
    fun lowerTemperature(temperature: Int) {
        temperature--
    }
}

data class Room(var temperature: Int)
```

에어컨을 통해 방 안의 온도를 낮추고 있다. #1과 #2에서 어떤 값이 출력될지 예상해보자.<br/>
정답은 #1 - <span style="color: white;">23</span>, #2 - <span style="color: white;">23</span>이다.<br/><br/>

room의 temparature 값이 왜 #1에서는 낮아지고, #2에서는 낮아지지 않았을까?<br/>
두 경우 메서드를 통해 인자를 전달할 때 Call by value가 일어난다. 즉, 값이 복사되어 전달되는데, #1에서는 복사하는 값이 Reference 타입이므로 Heap 영역의 메모리 주소가 복사된다. 따라서 main()과 lowerTemperatureOfRoom()은 같은 Room 인스턴스를 가리킨다.<br/>
하지만 #2에서 복사하는 값은 Primitive 타입이다. 따라서 Int 값 자체가 복사된다. 따라서 main()과 lowerTemperature()은 서로 다른 메모리 공간을 기리킨다. 그러므로 lowerTemperature()에서 값을 감소시켜도 room 변수의 temperature 값은 변하지 않는 것이다.<br/><br/> 

만약 위의 문제의 정답을 맞혔다면 다음 문제도 풀어보자.<br/>
다음 문제는 Flow를 사용할때 발생할 수 있는 조금 더 교묘한 오류다.<br/><br/>

```kotlin
import kotlinx.coroutines.*
import kotlinx.coroutines.flow.*

fun main() {
   val numberBox = NumberBox()
   val numberBoxUtil = NumberBoxUtil(numberBox)

   val numberUsingFlow = numberBoxUtil.numberUsingFlow()
   val numberUsingFlowOf = numberBoxUtil.numberUsingFlowOf()
   
   runBlocking {
      numberUsingFlow.collect {
         println("#numberUsingFlow - $it")  // #1
      }

      numberUsingFlowOf.collect {
         println("numberUsingFlowOf - $it") // #2
      }

      numberBox.i = 1

      numberUsingFlow.collect {
         println("numberUsingFlow - $it")   // #3
      }

      numberUsingFlowOf.collect {
         println("numberUsingFlowOf - $it") // #4
      }
   }
}

class NumberBoxUtil(val numberBox: NumberBox) {
   fun numberUsingFlow() = flow {
      emit(numberBox.i)
   }

   fun numberUsingFlowOf() = flowOf(
      numberBox.i
   )
}

class NumberBox {
   var i = 0
}
```
<br/>

약간의 설명을 덧붙이자면 위 코드는 다음과 같다. `NumberBox`는 하나의 값을 가지는 클래스다. `NumberBoxUtil`은 NumberBox의 값을 Flow로 가져오는 클래스다.<br/>
여기에 flow()와 flowOf()를 사용하는 두 가지 함수가 있는데, flowOf()는 단순히 flow()를 랩핑하는 함수이다. 소스 코드는 정확히 아래와 같다.<br/><br/>

```kotlin
fun <T> flowOf(value: T) = flow {
    emit(value)
}
```
<br/>

두 함수를 통해 flow를 받아온 후, 플로우가 방출하는 값을 변경했다. #3과 #4에서는 변경된 값을 방출할까 아니면 변경되기 이전의 값을 방출할까?<br/>
정답은 #1 - <span style="color: white;">0</span>, #2 - <span style="color: white;">0</span>, #3 - <span style="color: white;">1</span>, #4 - <span style="color: white;">0</span>이다.<br/><br/>

#4가 <span style="color: white;">0</span>이라는 것은 맞히지 쉽지 않았을 것이다. 그러나 상황은 위의 예시와 정확히 같다.<br/>
flowOf()에 인자로 넘겨준 값이 Int였기 때문에 flowOf()가 가리키는 값과 numberBox 변수의 i 값은 다르다.<br/><br/>

만약 numberBox 내부의 값이 Int같은 Primitive 타입이 아니라 Reference 타입이었다면 어떨까? 그 떄는 #3과 #4가 똑같이 동작한다.<br/>
실제 동작은 [Kotlin Playground] [2]에 위의 코드를 복붙하여 간단히 확인할 수 있다.<br/><br/>

### 정리
1. Call by value는 값 자체를 복사하는 것, Call by reference는 메모리 주소를 복사하는 것.<br/>
2. Java는 Call by value.<br/>
3. 웬만하면 글을 다 읽어보시는 걸 추천드립니다..!<br/><br/>

### 참고자료
[[ JAVA ] 참조란?](https://gyubgyub.tistory.com/83)<br/>
[[ JAVA ] 자바는 call by value? call by reference?](https://gyubgyub.tistory.com/84)<br/>

[1]: /docs/summary/os/process%20and%20thread.html
[2]: https://play.kotlinlang.org