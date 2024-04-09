---
title: 위임
layout: default
parent: 객체 지향
grand_parent: Java, Kotlin
nav_order: 2.1
---

## 위임이란?
### 위임
- [구성] [1]의 한 방법으로, 객체가 특정 작업을 처리하기 위해 다른 객체의 메서드를 호출하는 것.<br/>
- 상속하지 않으면서 상속하는 것처럼 코드를 재사용할 수 있다.<br/>
- 위임 객체를 호출하는 보일러 플레이트가 발생한다. ([Kotlin에서는 by 키워드를 통해 보일러 플레이트를 없앨 수 있다.] [2])<br/><br/>

<sup>1</sup>클래스의 내부 구현을 알 수 없다.<br/>
<sup>2</sup>한 클래스가 수정되어도 다른 클래스를 수정해야 할 가능성이 적다.<br/>
<sup>3</sup>클래스의 내부 구현을 알 수 있다.<br/>

[1]: composition%20vs%20inheritance.html
[2]: by.html