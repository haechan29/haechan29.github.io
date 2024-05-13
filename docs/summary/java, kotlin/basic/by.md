---
title: by 키워드
layout: default
parent: Basic
grand_parent: Java, Kotlin
nav_order: 9
---

## by 키워드를 사용하여 위임하기
### 위임의 여러 가지 방법
1. 클래스 위임<br/>
    - Class를 선언할 때 ``by`` 키워드를 사용하여 위임할 수 있다.<br/>
    - 구현되지 않은 내용만 위임 객체에 의해 구현된다.<br/>
    - [위임 객체는 내부적으로 필드로 선언되어 사용된다.] [1]<br/>
        ```kotlin
        interface ExampleInterface {
            fun exampleMethod()
        }

        class Delegator(delegatee: ExampleInterface): ExampleInterface by delegatee
        // 내부적으로 위임 객체를 저장할 필드가 선언된다. 실제 구현은 해당 필드를 통해 이루어진다.
  
        fun main() {
            val exampleInterfaceImpl = object: ExampleInterface {
                override fun exampleMethod() { 
                    println("Example method executed.")
                } 
            }

            val delegator = Delegator(exampleInterfaceImpl)
            delegator.exampleMethod() // "Example method executed."가 출력된다.
        }
        ```
        <br/>

2. 프로퍼티 위임<br/>
    - [필드를 선언할 때 ``by`` 키워드를 사용하여 위임할 수 있다.] [2]<br/>
    - 필드에 접근하는 방식을 제어한다.<br/><br/>
    
3. 기타<br/>
    - [Lazy 프로퍼티] [3]<br/>
    - [Observable 프로퍼티] [4]<br/>
    - [Map에 프로퍼티 저장하기] [5]<br/><br/>

[1]: https://medium.com/til-kotlin-ko/kotlin의-클래스-위임은-어떻게-동작하는가-c14dcbbb08ad
[2]: https://readystory.tistory.com/204
[3]: https://kotlinlang.org/docs/delegated-properties.html#lazy-properties
[4]: https://kotlinlang.org/docs/delegated-properties.html#observable-properties
[5]: https://kotlinlang.org/docs/delegated-properties.html#storing-properties-in-a-map