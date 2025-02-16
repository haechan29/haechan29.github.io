---
title: Internet Layer
layout: default
parent: Network Model
grand_parent: Network
nav_order: 5
---

## 인터넷 계층이란?
### 인터넷 계층
데이터 패킷을 목적지까지 라우팅하는 계층<br/>

### 사용되는 프로토콜
1. IP<br/>
    - Internet Protocol.<br/>
    - 데이터 패킷을 전송하는 메커니즘.<br/>
    - 각 네트워크 기기에 고유한 주소(IP 주소)를 할당한다. 이 주소를 사용하여 인터넷 상의 다른 기기와 통신할 수 있다.<br/>
    <br/>
   
2. ICMP<br/>
    - Internet Control Message Protocol.<br/>
    - 네트워크 장비간의 통신 상태를 진단하고, 오류 메시지를 전달.<br/>
    <br/>

3. ARP<br/>
    - Address Resolution Protocol.<br/>
    - 논리적 주소인 IP 주소를 물리적 주소인 MAC 주소로 변환하는 과정.<br/>
    - 브로드캐스팅을 통해 요청을 보내고, IP 주소가 일치하는 네트워크로부터 MAC 주소를 전달받는다.<br/>
    <br/>

### 사용되는 기술
1. NAT<br/>
    - Network Address Translation.<br/>
    - IP 주소를 변경하여 네트워크 내부의 여러 장치가 하나의 공인 IP를 공유하는 방법.<br/>
    - IP 부족 문제를 해결하고, 네트워크 보안성을 높인다.<br/>
    <br/>
