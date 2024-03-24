---
title: Network Access Layer
layout: default
parent: Network Model
grand_parent: Network
nav_order: 7
---

## 네트워크 액세스 계층이란?
### 네트워크 액세스 계층
- 물리적 매체를 이용해 이더넷 프레임을 전송하고, 오류 검출 및 재전송, 네트워크 장치의 접근 제어를 담당하는 계층.<br/>
- OSI 7계층의 ``물리 계층``과 ``데이터 링크 계층``을 합친 게층.<br/>

### 사용하는 프로토콜
1. [이더넷] [1]
   - 물리 계층에서 신호 전송, 배선 등의 방식을 정의한다.<br/>
   - 데이터 링크 계층에서 MAC 주소<sup>1</sup>를 통해 이더넷 프레임을 목적지로 전송하고, ``CSMA/CD``, ``CSMA/CA`` 등의 알고리즘을 통해 네트워크 장치의 접근을 제어한다.<br/>

### CSMA/CD
- Carrier Sense Multiple Access with Collision Detection.<br/>
- 회선을 사용하는지를 파악한 후 사용하지 않는다면 데이터를 보내고 충돌이 발생한다면 일정 시간 이후 재전송하는 반이중화 통신 방식.<br/>
- Carrier Sense (캐리어 감지): 데이터를 전송하기 전에 통신 채널을 감지하여 다른 장치가 현재 데이터를 전송하고 있는지 확인하는 과정.<br/>
- Multiple Access (다중 접근): 여러 장치가 같은 네트워크 채널을 공유하여 데이터를 전송할 수 있음.<br/>
- Collision Detection (충돌 감지): 장치가 데이터를 전송하는 도중 다른 장치가 전송을 시작하여 데이터 충돌이 발생할 경우, 이를 감지하고 처리하는 기능.<br/>

### CSMA/CA
- Carrier Sense Multiple Access with Collision Avoidance.<br/>
- 데이터를 보내기 전에 일련의 과정을 기반으로 사전에 충돌을 방지하는 반이중화 통신 방식.<br/>
- Collision Avoidance (충돌 회피): 데이터 전송 과정에서 가능한 충돌을 미리 예방하는 것.<br/>

<sup>1</sup>MAC 주소: Media Access Control 주소로, 네트워크 인터페이스를 식별하기 위한 물리적 주소이다. 보통 장치의 NIC(=LAN 카드)에 할당된다. __24비트__ 의 ``OUI``(제조사 코드)와 __24비트__ 의 ``UAA``(시리얼 넘버)로 구성된다.<br/>
<sup>2</sup>반이중화 통신: 양쪽 장치 모두 통신할 수 있지만, 한 번에 한 방향만 통신할 수 있는 방식. ``전이중화 통신``과 반대되는 개념.<br/>

[1]: https://blue-shadow.tistory.com/37
