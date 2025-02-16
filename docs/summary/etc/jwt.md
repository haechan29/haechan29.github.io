---
title: JWT
layout: default
parent: Etc
grand_parent: Summary
nav_order: 15
---

## JWT란?
### JWT
- JSON<sup>1</sup> Web Token.<br/>
- 자가 수용적<sup>2</sup>이다.<br/>
- 일반적으로 Access Token과 Refresh Token<sup>3</sup>으로 구분하여 사용한다.<br/>

### 구성 요소
1. 헤더<sup>Header</sup>: 토큰의 유형(JWT)과 사용된 알고리즘(Ex. RSA, HMAC SHA256)을 설명한다.<br/>
2. 페이로드<sup>Payload</sup>: 전달할 데이터를 담고 있는 JSON 객체. 사용자 정보, 권한 등을 포함할 수 있다.<br/>
3. 서명<sup>Signature</sup>: 헤더와 페이로드를 합쳐 [암호화] [1]한 것. 메시지의 무결성을 보장한다.<br/>

### 동작 원리
- 사용자가 로그인하면, 서버는 사용자의 정보를 기반으로 JWT를 생성하고, 사용자에게 전송한다.<br/>
- 사용자는 모든 요청에 JWT를 포함시켜 서버에 전송하고, 서버는 요청을 받을 때마다 JWT의 서명을 확인한다.<br/><br/>

<sup>1</sup>JavaScript Object Notation. 키와 값의 쌍(클레임)으로 객체를 표현하는 방식.<br/>
<sup>2</sup>Self-contained. 그 자체로 필요한 모든 정보를 담고 있다. 토큰을 검증하기 위해 별도의 데이터베이스 탐색 등의 추가 과정이 필요 없다는 의미.<br/>
<sup>3</sup>유효 기간이 짧은 Access Token을 통해 자원에 접근하고, 유효 기간이 긴 Refresh Token을 통해 Access Token을 재발급한다. Refresh 토큰이 유효하지 않으면 로그인 등을 통해 사용자를 검증한다.<br/>

[1]: encryption.html