---
title: OSI 7계층
layout: default
parent: Network Model
grand_parent: Network
nav_order: 8
---

## OSI 7계층이란?
### OSI 7계층
- 네트워크의 구성 요소를 역할에 따라 7가지 계층으로 나눈 것.<br/>
- [TCP/IP 모델은 오늘날 대부분의 인터넷과 상용 네트워크에서 사용되는 실용적인 모델입니다. 반면 OSI 모델은 이론적인 네트워크 모델입니다.] [1]<br/>

1. 응용 계층(Application Layer): 최종 사용자의 응용 프로그램과 직접 상호작용합니다.<br/>
2. 표현 계층(Presentation Layer): 데이터의 표현, 암호화, 압축을 담당합니다.<br/>
3. 세션 계층(Session Layer): [세션] [2]<sup>1</sup>의 설정, 관리, 종료를 담당합니다.<br/>
4. 전송 계층(Transport Layer): 두 호스트 간의 데이터 전송을 관리합니다.<br/>
5. 네트워크 계층(Network Layer): 다양한 네트워크를 통한 패킷 전송과 라우팅을 담당합니다.<br/>
6. 데이터 링크 계층(Data Link Layer): 두 장치 간의 신뢰성 있는 링크를 생성하고 프레임에 주소를 부여합니다.<br/>
7. 물리 계층(Physical Layer): 물리적 매체를 통한 비트 전송을 담당합니다.<br/>

<sup>1</sup>세션: 클라이언트와 서버 간의 연결 상태

[1]: https://easyitwanner.tistory.com/373
[2]: https://fomaios.tistory.com/entry/Network-세션Session이란-What-is-a-Session