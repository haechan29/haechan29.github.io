---
title: Object
layout: default
parent: Basic
grand_parent: Java, Kotlin
nav_order: 4
---

## Object란?
### Object
- ``class`` 키워드 대신 ``object`` 키워드를 사용하여 **Singleton**을 생성한다.<br/>
- 일반 클래스처럼 필드, 메서드, 초기화 블록을 가질 수 있지만 생성자는 가질 수 없다.<br/>
- Object 선언<sup>1</sup>, Object 식<sup>2</sup>, [Companion Object] [1]에 이용된다.<br/>
- 클래스를 상속 받을 수 있고, 여러 개의 인터페이스를 구현할 수 있다. 다른 클래스가 Object를 상속할 수는 없다.<br/>

### 원리
- 내부적으로 일반적인 Singleton 패턴과 같이 구현된다.<br/>
- Kotlin의 Object는 Java에서 아래와 같이 변환된다.<br/>
    ```kotlin
    // Kotlin 코드
    object ExampleObject {
        val exampleField = 0
        fun exampleFunction() {}
    }
    ```

    ```java
    // 위의 Kotlin 코드가 변환된 Java 코드
    public final class ExampleObject {
        // 객체를 상수로 선언한다. Kotlin에서 Object를 호출하면 이 객체를 전달한다.
        @NotNull
        public static final ExampleObject INSTANCE;
    
        // Object의 멤버는 위의 객체를 통해 접근한다.
        private static final int exampleField;
        public final int getExampleField() {
            return exampleField;
        }
       
        public final void method() {}
    
        // 생성자를 호출할 수 없다.
        private ExampleObject() {}
    
        // 객체는 정적 블럭을 통해 초기화된다.
        static {
            ExampleObject var0 = new ExampleObject();
            INSTANCE = var0;
        }
    }
    ```

<br/>

<sup>1</sup>클래스 내부에 선언할 경우 Java의 [Static Inner Class] [2], 메서드 내에서 선언할 경우 [Local Inner Class] [2]처럼 동작한다.<br/>
<sup>2</sup>Object를 반환하는 식. 익명 Object를 생성하는 경우 Java의 [Anonymous Inner Class] [2]처럼 동작한다.<br/>

[1]: companion%20object.html
[2]: https://hyunki99.tistory.com/13