---
title: JVM의 구성 요소
layout: default
parent: Basic
grand_parent: Java, Kotlin
nav_order: 6.1
---

## JVM은 어떻게 구성될까?
### JVM의 구성 요소
1. 클래스 로더
    - [바이트 코드(.class 파일)를 묶어서 Runtime Data 영역에 적재한다.] [1]<br/>
    - 클래스가 처음 참조될 때 로딩한다.<br/><br/>
   
2. 실행 엔진
    - 클래스 로더가 메모리에 로딩한 바이트 코드를 실행한다.<br/> 
    - [인터프리터] [2] 또는 [JIT 컴파일러] [3]를 이용한다.<br/><br/>
   
3. [GC] [4]
    - 사용되지 않는 메모리를 자동으로 회수한다.<br/>
    - 동적으로 할당된 객체 중에서 참조되지 않은 객체를 탐색 후 제거한다.<br/><br/>

4. 런타임 데이터 영역
    - 힙, 메서드<sup>1</sup>, 스택 영역과 PC 레지스터, 네이티브 메서드 스택<sup>2</sup>으로 구성된다.<br/>
    - 힙, 메서드 영역은 모든 스레드가 공유하고, 스택 영역, PC 레지스터, 네이티브 메서드 스택은 스레드마다 독립적으로 할당받는다.<br/><br/>

<sup>1</sup>메서드 영역: 클래스 수준의 정보(클래스 메타데이터, 정적 변수 등)를 저장한다. Static 영역이라고도 불린다.<br/>
<sup>2</sup>네이티브 메서드 스택: Java 이외의 언어(C, C++, 어셈블리 등)로 작성된 네이티브 코드를 실행할 때 사용되는 메모리 영역.<br/>

[1]: class%20loading.html
[2]: /docs/summary/etc/compiler%20vs%20interpreter.html
[3]: /docs/summary/etc/jit%20vs%20aot.html
[4]: /docs/summary/etc/garbage%20collection.html