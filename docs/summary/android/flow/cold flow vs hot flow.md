---
title: Cold Flow vs Hot Flow
layout: default
parent: Flow
grand_parent: Android
nav_order: 5
---

## Cold Flow vs Hot Flow
### Cold Flow
- Collect하기 전까지는 활성화되지 않는다.<br/>
- Collect하면 활성화되고, Collect하는 코루틴이 취소되면 비활성화된다.<br/>
- 각각의 Collector가 각각의 Stream을 갖는다.<br/>
- Ex. Flow Builder을 통해 생성되는 Flow.<br/> 

### Hot Flow
- Collector가 없어도 활성화될 수 있다.<br/>
- Emit하는 데이터를 모든 Collector가 공유한다.<br/>
- Ex. SharedFlow, StateFlow.<br/>