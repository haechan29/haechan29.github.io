---
title: Init Block
layout: default
parent: Basic
grand_parent: Java, Kotlin
nav_order: 3
---

## Init Block은 어떤 역할을 할까?
### Init Block
- 객체가 생성될 때 초기화하는 역할.<br/>
- 필드를 초기화한 이후에 실행된다<sup>1</sup>.<br/>

### Java의 Static, Instance Block 대체하기
1. Static Block.<br/>
    - [클래스가 메모리에 로드될 때] [1] 실행된다.<br/>
    - Companion Object 내부에서 Init Block을 호출한다.<sup>2</sup><br/><br/>

2. Instance Block.<br/>
    - 객체가 생성될 때마다 실행된다.<br/>
    - 클래스 내부에서 Init Block을 호출한다.<br/><br/>

<sup>1</sup>필드가 초기화되는 순서는 다음과 같다. Static 변수 초기화 -> Static Block 실행 -> Instance 변수 초기화 -> Instance Block 실행 -> Constructor 실행<br/>
<sup>2</sup>[Companion Object] [2]는 Singleton 패턴과 유사한 방식으로 구현된다. 클래스 내부에 Companion 클래스를 선언하고, Companion 객체를 생성한다. 따라서 Companion Object를 포함하는 클래스가 로딩될 때 Companion Object 내부의 Init Block이 실행된다.<br/> 

[1]: class%20loading.html
[2]: companion%20object.html