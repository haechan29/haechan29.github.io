---
title: Application Layer
layout: default
parent: Network Model
grand_parent: Network
nav_order: 2
---

## 애플리케이션 계층이란?
### 애플리케이션 계층
웹, 이메일 등 서비스를 실질적으로 사람들에게 제공하는 계층.<br/>

### 역할
- 인코딩과 디코딩: 데이터를 네트워크를 통해 전송할 수 있는 형태로 인코딩하고, 수신한 데이터를 사용자가 이해할 수 있는 형태로 디코딩합니다.<br/>
- 세션 관리: 응용 프로그램 간의 세션을 설정, 관리, 종료하는 기능을 담당합니다.<br/>
- 인증 및 권한 부여: 인증 절차를 수행하고, 데이터 접근 권한을 부여합니다.<br/>

### 사용하는 프로토콜
1. [HTTP] [1]: Hypertext Transfer Protocol. 브라우저 또는 서버 간의 통신에 주로 이용되는 프로토콜.<br/>
2. SMTP: Simple Mail Transfer Protocol. 메일을 전송하는데 사용되는 프로토콜.<br/>
3. SSH: Secure SHell Protocol. 보안을 위한 암호화 네트워크 프로토콜.<br/>
4. FTP: File Transfer Protocol. 파일을 전송하는데 사용되는 프로토콜.
   지금은 파일을 암호화해서 전송하는 FTPS 또는 SFTP로 대체되고 있습니다.<br/>

### 사용하는 서비스
1. DNS
    - Domain Name System.
    - 도메인 이름을 IP 주소로 변환하는 서비스. 예를 들어, 사용자가 웹 브라우저에 도메인 이름을 입력할 때, DNS 서버는 해당 도메인 이름에 해당하는 IP 주소를 조회하여 반환합니다.

[1]: /docs/summary/network/http/http.html