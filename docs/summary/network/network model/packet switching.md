---
title: TCP, UDP의 패킷 교환 방식
layout: default
parent: Network Model
grand_parent: Network
nav_order: 4
---

## TCP, UDP의 패킷 교환 방식
### 가상회선 패킷 교환 방식(TCP)
- ``3-way handshake``를 통해 연결을 맺고, ``4-way handshake``로 연결을 해제한다.<br/>
- 송신자와 수신자 사이에 가상의 연결(가상회선)을 설정하여 데이터를 전송한다. 가상회선은 데이터 전송이 끝날 때까지 유지된다.
- __패킷 순서가 유지된다.__
- __전달되지 않은 데이터는 재전송을 시도하고, 체크섬을 통해 데이터의 무결성을 확인한다.__
- 신뢰성이 중요하고 데이터 전송량이 많은 환경에서 유리하다. 예를 들어, 음성 통신이나 동영상 스트리밍과 같은 실시간 데이터 전송에 주로 사용된다.

### 3-way handshake
1. SYN 단계: 클라이언트는 서버에 자신의 ISN<sup>1</sup> 을 담아 SYN을 보낸다.<br/>
2. SYN + ACK 단계: 서버는 클라이언트의 SYN을 수신한다. 자신의 ISN을 담은 SYN과 승인번호를 클라이언트의 ISN + 1로 설정한 ACK를 보낸다.<br/>
3. ACK 단계: 클라이언트는 서버의 ACK를 수신한다. 승인번호를 서버의 ISN + 1로 설정하여 ACK를 서버에 보낸다.<br/>

<sup>1</sup> ISN: TCP/IP 통신은 시퀀스 번호를 이용하여 데이터의 순서를 보장한다. ISN은 그 시퀀스 번호의 초기 값이다.

### 4-way handshake
1. 먼저 클라이언트가 연결을 닫으려고 할 때 FIN으로 설정된 세그먼트를 보내고, FIN_WAIT_1 상태로 들어간다.
2. 서버는 클라이언트로 ACK라는 승인 세그먼트를 보내고 CLOSE_WAIT 상태에 들어간다.
   세그먼트를 받은 클라이언트는 FIN_WAIT_2 상태에 들어간다.
3. 서버는 LAST_ACK상태가 되며 일정 시간 이후에 클라이언트에 FIN이라는 세그먼트를 보낸다.
4. 클라이언트는 TIME_WAIT 상태가 되고 다시 서버로 ACK를 보낸다. 세그먼트를 받은 서버는 CLOSED 상태가 된다.
   클라이언트는 TIME_WAIT으로 설정된 시간을 대기한 후 연결이 닫힌다.

### 데이터그램 패킷 교환 방식(UDP)
- 각각의 패킷이 가상회선 없이 독립적인 경로를 통해 전달된다.<br/>
- 네트워크 내에서 혼잡이나 장애가 발생한 경우, 이를 우회하여 다른 경로를 통해 목적지에 도달할 수 있어 네트워크의 장애에 대해 높은 유연성을 가진다.<br/>
- 패킷이 목적지에 도착하는 순서가 발송된 순서와 다를 수 있다.<br/>
- 연결 설정과 해제에 필요한 오버헤드가 없다.<br/>