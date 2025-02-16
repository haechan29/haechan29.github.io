---
title: Parcelable
layout: default
parent: Basic
grand_parent: Android
nav_order: 8
---

## Parcelable이란?
### Parcelable
객체를 빠르게 직렬화하고 역직렬화하기 위한 메커니즘을 제공하는 인터페이스
- 안드로이드 플랫폼 최적화: Parcelable은 안드로이드 플랫폼에 특화되어 설계되었습니다. 안드로이드의 Intent와 Bundle 객체를 통한 데이터 전송에 최적화되어 있어, 이러한 메커니즘을 사용할 때 더 빠르게 작동합니다.
- 명시적 직렬화: 개발자가 객체를 직렬화하는 방법을 명시적으로 정의합니다(writeToParcel 메소드에서 직접 구현). 이는 직렬화 과정에서 불필요한 작업을 최소화하고, 메모리 사용을 최적화할 수 있도록 합니다.
- Serializable과의 차이: Serializable에서는 객체의 상태 뿐만 아니라 메타데이터까지 직렬화하는 것과는 달리, 객체의 상태만을 저장합니다.

