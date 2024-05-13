---
title: IP 주소
layout: default
parent: Network Model
grand_parent: Network
nav_order: 6
---

## IP 주소란?
### IP 주소
- 네트워크 기기를 식별하는 논리적 주소.<br/>
- ``네트워크 주소``와 ``호스트 주소``로 구성된다.<br/>

### IP 주소 체계
1. IPv4
    - 32비트 주소 체계(생성 가능한 IP 주소 약 43억개).<br/>
    - [NAT(Network Address Translation)] [1]을 사용한다.<br/>
    - 클래스 기반으로 주소 공간을 구분한다(classful<sup>1</sup>).<br/>
    - 체크섬 필드를 통해 오류를 검출한다.<br/>
    - 설계 초기에 보안을 고려하지 않아 추가적인 보안 조치가 필요.<br/>
    - 데이터 패킷의 크기가 MTU<sup>2</sup>를 초과할 경우 패킷을 분해한다(프래그먼테이션).<br/>
    <br/>

2. IPv6
    - 128비트 주소 체계.<br/>
    - 클래스 기반으로 주소 공간을 구분하지 않는다(classless<sup>3</sup>).
    - IPSec을 기본으로 내장하여 데이터의 무결성을 보장한다. 체크섬 필드는 없다.
    - 헤더 길이가 40바이트로 고정되어 있어 헤더 길이에 대한 정보가 없다.
    - 데이터 패킷의 크기가 MTU를 초과할 경우 송신자가 패킷을 쪼개서 다시 전송한다([PMTUD] [2]<sup>4</sup>).<br/><br/>

<sup>1</sup>클래스풀: IP 주소의 네트워크 주소 길이가 고정되어 있다. 클래스 A(8비트), B(16비트), C(27비트). D, E로 구분한다.<br/>
<sup>2</sup>MTU: Maximum Transmission Unit. 네트워크에 연결된 장치가 받아들일 수 있는 최대 데이터 패킷의 크기.<br/>
<sup>3</sup>클래스리스: ``서브넷 마스크``를 기준으로 네트워크 주소와 호스트 주소를 구분한다.<br/>
<sup>4</sup>PMTUD: Path MTU Discovery. 테스트 패킷의 크기를 낮추면서 MTU에 맞게끔 반복해서 보내는 과정.<br/>

[1]: internet%20layer.html
[2]: https://hoonheui.tistory.com/entry/PMTUD