---
title: Multidex
layout: default
parent: Basic
grand_parent: Android
nav_order: 9
---

## Multidex란?
### Multidex
[DEX] [1] 파일의 메서드가 64k(65536)개를 초과하지 않도록 여러 개로 쪼갠 것.<br/>

### 사용 방법 
- build.gradle 파일에 MultiDex 지원 라이브러리를 추가.<br/>
- Application 클래스에서 MultiDexApplication을 상속받거나 MultiDex.install(this)를 호출하여 초기화.<br/>
- Android 5.0 (API 레벨 21) 이상에서는 ART(Android Runtime)가 기본 런타임으로 사용되며, ART는 실행 시간에 자동으로 Multidex를 지원하기 때문에 추가 설정이 필요 없다.<br/>

[1]: build.html