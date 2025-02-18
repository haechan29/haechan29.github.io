---
title: 잠자기 모드와 앱 대기 모드
layout: default
parent: Basic
grand_parent: Android
date: 2025-02-18
nav_order: 14
---

## 잠자기 모드와 앱 대기 모드란?
### 잠자기 모드<sub>Doze</sub>
- 핸드폰을 적은 전력으로 오래 사용할 수 있도록 일정 기간 사용하지 않으면 실행되는 모드.
- Doze 기간에는 일부 기능이 제한되고, 짧은 Maintenance Window 기간동안 제한이 해제된다. Doze 모드가 길어질수록 Doze 기간이 길어진다.
- Light Doze, Deep Doze로 구분된다.
- 진입 조건
  - Light Doze: Screen Off, On Battery
  - Deep Doze: Screen Off, On Battery, Stationary 
- [제약 사항][전력 관리 제한 사항]
  - Light Doze: Job 지연, 네트워크 불가능.
  - Deep Doze: Alarm 제한<sup>1</sup>, WakeLock 불가능.
- 테스트 방법
  ```
  // 설정
  adb shell dumpsys deviceidle force-idle
  
  // 해제
  adb shell dumpsys deviceidle unforce
  adb shell dumpsys battery reset 
  ```

### 앱 대기 모드<sub>App Standby</sub>
- 사용자가 앱을 활발히 사용하지 않으면 실행되는 모드.
- 앱 사용 빈도에 따라 앱을 여러 앱 대기 버킷<sup>2</sup>에 배치한다.
- `UsageStatsManager.getAppStandbyBucket()`을 통해 확인할 수 있다.
- [제약 사항][전력 관리 제한 사항]
  - 드물게 사용될수록 제약이 많아진다.
  - Job은 몇 시간에 10분, Alarm의 경우 1시간에 몇 번 꼴로 실행.
  - 드물게 사용 버킷부터는 네트워크 및 FCM<sup>3</sup> 을 사용할 수 없다.
- 테스트 방법
  ```
  // 설정
  adb shell dumpsys battery unplug
  adb shell am set-inactive <packageName> true
  
  adb shell am set-standby-bucket active|working_set|frequent|rare
  
  // 해제
  adb shell am set-inactive <packageName> false
  adb shell am get-inactive <packageName>
  ```

<sup>1</sup>set~AndAllowWhileIdle() 메서드가 부분적인 제약과 함께 동작한다.<br/>
<sup>2</sup>활성, 작업 세트, 자주 사용, 드물게 사용, 제한됨, 사용한 적 없음이 있다.<br/>
<sup>3</sup>[높은 우선순위의 메시지][메시지 우선순위 설정 및 관리]는 전송 가능하다.<br/>

[전력 관리 제한 사항]: https://developer.android.com/topic/performance/power/power-details?hl=ko
[메시지 우선순위 설정 및 관리]: https://firebase.google.com/docs/cloud-messaging/android/message-priority?hl=ko