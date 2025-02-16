---
title: SharedFlow vs StateFlow
layout: default
parent: Flow
grand_parent: Android
nav_order: 6
---

## SharedFlow vs StateFlow
### SharedFlow
- [Cold Flow] [1]를 [Hot Flow] [1]로 변환한 것.<br/>
- MutableSharedFlow() 또는 shareIn()을 통해 생성한다.<br/>
- SharingStarted<sup>1</sup>, 캐시 용량<sup>2</sup>를 설정할 수 있다.<br/>
- 기본적으로 캐싱하지 않으며, BufferOverflow의 기본 값은 SUSPEND.<br/> 

### StateFlow
- 초기값을 갖고 캐시를 제공하도록 커스텀된 SharedFlow.<br/> 
- MutableStateFlow() 또는 stateIn()을 통해 생성한다.<br/>
- [Replay 캐시 용량의 기본값은 1이고, BufferOverflow는 DROP_OLDEST로 기본 설정되어 있다. 방출된 값이 같다면 생략한다.] [2]<br/>
- MutableStateFlow#value를 통해 현재 값에 접근 가능하지만, Thread-safe하지 않다.<br/><br/>
    ```kotlin
    // value를 통해 직접 접근하는 경우
    val flow1 = MutableStateFlow(0)
    
    repeat(10000) {
        flow1.value = flow1.value + 1
    }
    println(flow1.value) // 7812 (1000이 나오지 않는다)
  
    // update()을 통해 접근하는 경우
    val flow2 = MutableStateFlow(0)
    repeat(10000) {
        flow2.update { currentValue ->
            currentValue + 1
        }
    }
    println(flow2.value) // 10000
    ```
    <br/><br/>

<sup>1</sup>[SharingStarted] [3]: 실행 시점을 결정한다. Eagerly, Lazily, WhileSubscribed가 있다.<br/>
<sup>2</sup>Replay 캐시와 Extra Buffer(Replay에 사용되지 않는 캐시)의 용량. Replay 캐시는 새로 Collect하기 시작할 때 몇 번 Re-emit할 지 결정한다. 0으로 설정하면 Configuration 등으로 인해 액티비티가 재생성될때 emit()이 호출되기 전까지 뷰에 아무 것도 표시되지 않을 수 있다. 따라서 0으로 설정하는 것은 권장되지 않는다.<br/>


[1]: cold%20flow%20vs%20hot%20flow.html
[2]: https://kotlinlang.org/api/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.flow/-state-flow/
[3]: https://kotlinlang.org/api/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.flow/-sharing-started/