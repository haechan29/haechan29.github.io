---
title: Backing Field/Property
layout: default
parent: Basic
grand_parent: Java, Kotlin
nav_order: 2
---

## Backing Field/Properties란?
### Backing Field
- Property<sup>1</sup>가 Getter, Setter을 통해 접근하는 내부 Field<sup>2</sup>.<br/>
- Getter, Setter 내부에서 ``field`` 키워드를 통해 접근할 수 있다.<br/>
    ```kotlin
    var count = 0
        get() = field * 2
        set(value) {
            if (value >= field) field = value
        } 
    ```

### Backing Properties
- Property가 Getter, Setter을 통해 접근하는 내부 Property.<br/>
- Property에 접근하는 방식을 제어한다.<br/>
    ```kotlin
    private val _count = MutableLiveData<Int>(0)
    val count: LiveData<Int> get() = _count
    ```

### Backing Properties vs private set
- Private Setter을 통해 내부 Property에 접근하는 방식을 제어할 수 있다. [이 경우 변수를 var로 선언하기 때문에 변수가 재할당될 수 있어 권장되지 않는다.] [1]<br/>
    ```kotlin
    var count = MutableLiveData<Int>(0)
        private set
    ```

<br/>

<sup>1</sup>Property: Field와 Getter, Setter을 추상화한 것. Field에 접근하는 방식을 제어한다. Kotlin에서는 Getter와 Setter을 자동으로 생성한다.<br/>
<sup>2</sup>Field: 클래스 내에 선언된 변수.<br/>

[1]: https://everyday-develop-myself.tistory.com/m/344