---
title: 프로세스 생명주기
layout: default
parent: Basic
grand_parent: Android
date: 2025-02-16
nav_order: 13
---

## 프로세스 생명주기란?
### 프로세스 생명주기
- 메모리가 부족할때 종료할 프로세스를 결정하기 위해 프로세스를 중요도에 따라 분류한다.<br/>
- 앱 구성요소의 중요도 중 가장 높은 중요도를 따른다.<br/>
- 포그라운드 프로세스, 가시적 프로세스, 서비스 프로세스, 캐시된 프로세스<sup>1</sup>로 나뉜다.<br/>

|                    | 포그라운드 프로세스     | 가시적 프로세스      | 서비스 프로세스     | 캐시된 프로세스<sup>1</sup>        |
|--------------------|----------------|---------------|--------------|-----------------------------|
| Activity           | onResume 호출 이후 | onPause 호출 이후 | onStop 호출 이후 | onDestory 호출 이후             |
| Service            | 주요 메서드 호출 중    | 포그라운드 서비스 실행중 | 일반 서비스 실행중   | 서비스 종료 이후<sup>2</sup>       |
| Broadcast Receiver | onReceive 호출 중 |               |              | onReceive 호출 이후<sup>3</sup> |

<sup>1</sup>비활성 상태로 인식되어 시스템에 의해 강제로 프로세스가 종료될 수 있다. 이 경우 Activity#onDestory()가 호출되지 않는 등 종료 동작이 감지되지 않을 수 있다.<br/>
<sup>2</sup>장기 작업을 실행하고 싶은 경우 Service#setForeground()를 사용해 포그라운드 서비스로 전환한다.<br/>
<sup>3</sup>장기 작업을 실행하고 싶은 경우 Workmanager, JobService, AlarmManager 등을 사용해 백그라운드 작업을 예약한다.<br/>
