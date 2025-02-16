---
title: Companion Object
layout: default
parent: Basic
grand_parent: Java, Kotlin
nav_order: 4.1
---

## Companion Object란?
### Companion Object
- Kotlin에서 Static 변수를 선언하기 위해 사용된다.<br/> 
- [Object] [1]의 한 종류로, 특성을 공유한다.<br/>

### 원리
- 내부적으로 일반적인 Singleton 패턴과 유사하게 구현된다.<br/>
- Kotlin의 Companion Object는 Java에서 아래와 같이 변환된다.<br/>
    ```kotlin
    class ExampleClass {
        companion object {
            var exampleField = 3
            fun exampleMethod() {}
        }
    }
    ```

    ```java
    // 위의 Kotlin 코드가 변환된 Java 코드
    public final class ExampleClass {
        private static int exampleField = 3;
  
        // 객체를 상수로 선언한다.
        @NotNull
        public static final Companion Companion = new Companion();

        // 내부에 Inner Static Class를 선언한다. 
        public static final class Companion {
            // Companion Object의 멤버는 위의 인스턴스를 통해 접근한다.
            public final int getExampleField() {
                return ExampleClass.exampleField;
            }

            public final void setExampleField(int var1) {
                ExampleClass.exampleField = var1;
            }

            public final void exampleMethod() {
            }
            
            private Companion() {
            }
        }
    }
    ```
  
[1]: object.html
    