---
title: 인텐트
layout: default
parent: Basic
grand_parent: Android
date: 2025-02-11
nav_order: 12
---

## 인텐트란?
### 인텐트
- 액티비티, 서비스 등의 컴포넌트를 실행할 때 사용한다.<br/>
- 클래스나 패키지 이름을 사용하는 명시적 인텐트, 인텐트 필터를 사용하는 암시적 인텐트로 분류된다.<br/>

### 암시적 인텐트
- 조건을 제시하고, 이를 처리할 수 있는 인텐트를 찾는 방식.<br/>
- 인텐트에 카테고리를 설정하지 않을 경우 기본 값으로 Intent.category.default 가 설정된다<sup>1</sup>.<br/>
- 처리할 수 있는 인텐트가 없는 경우 ActivityNotFound 예외가 발생한다. (예외 처리 필수)<br/>

Ex. 인텐트 필터<br/>
```xml
<activity
    android:name="com.example.ExampleActivity" >
    <intent-filter android:label="@string/filter_view_example_gizmos">
    <action android:name="android.intent.action.VIEW" />
    <category android:name="android.intent.category.DEFAULT" />
    <category android:name="android.intent.category.BROWSABLE" />
    <data
        android:scheme="example"
        android:host="example" />
    </intent-filter>
</activity>
```

Ex. 인텐트 스킴<br/>
```kotlin
val url = "intent://..."
val intent = Intent.parse(url, Intent.URI_INTENT_SCHEME)
startActivity(intent)
```

<sup>1</sup>암시적 인텐트를 처리하는 Activity의 경우 인텐트 필터에 intent.category.default를 반드시 추가해야 한다.<br/>
