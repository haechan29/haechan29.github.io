---
title: TransformLatest vs Conflate
layout: default
parent: Flow
grand_parent: Android
nav_order: 8
---

## TransformLatest vs Conflate
### TransformLatest
- 수집된 데이터를 모두 처리하기 전에 새로운 값이 방출되면 **기존에 진행하던 작업을 취소**하고 새로운 작업을 시작한다.<br/>
- mapLatest(), collectLatest()도 내부적으로 transformLatest()를 호출한다.<br/>

### Conflate
- 수집된 데이터를 모두 처리하기 전에 새로운 값이 방출되면 **방출된 값을 무시**하고 기존의 작업을 마무리한다.<br/>
- 내부적으로 buffer(0, DROP_OLDEST)를 사용한다.<br/>
