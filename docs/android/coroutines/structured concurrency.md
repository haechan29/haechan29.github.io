---
title: Structured Concurrency
layout: default
parent: Coroutines
grand_parent: Android
nav_order: 2.1
---

## Structured Concurrency란?
### Structured Concurrency
코루틴의 생명 주기를 효율적으로 관리하기 위한 시스템.<br/>

- 모든 자식 코루틴이 일을 끝내기 전까지 부모 코루틴 끝나지 않는다.(launch(), async() 제외)<br/>
- **[취소] [1]는 아래**로 전파된다(옆이나 위로는 전파되지 않는다).<br/>
- **[예외] [2]는 위로** 전파된다. 이로 인해 한 코루틴이 취소되면 그 자식 코루틴 또한 취소된다.<br/><br/>

[1]: cancellation.html
[2]: exception%20handling.html