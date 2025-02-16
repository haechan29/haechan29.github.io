---
title: 대칭키 암호화 vs 비대칭키 암호화
layout: default
parent: Etc
grand_parent: Summary
nav_order: 5
---

## 대칭키 암호화 vs 비대칭키 암호화
### 대칭키 암호화(비밀키 암호화)
- 암호화와 복호화에 같은 키(비밀키)를 사용한다.<br/> 
- 처리 속도가 빠르지만 보안성이 떨어진다.<br/>
- Ex. HMAC.<br/>

### 비대칭키 암호화(공개 키 암호화)<sup>1</sup>
- 암호화와 복호화에 공개 키와 비밀 키를 사용한다. 한 키로 암호화된 데이터는 반대 키로만 복호화할 수 있다.<br/>
- 보안성이 뛰어나지만 처리 속도가 느리다.<br/>
- Ex. RSA, ECC<sup>Elliptic Curve Cryptography</sup>, DSA<sup>Digital Signature Algorithm</sup>.<br/>

### 하이브리드 암호화
- 비대칭키 암호화를 사용하여 개인키를 안전하게 교환한 다음, 나머지 데이터 전송에는 대칭키 암호화를 사용한다.<br/>
- 대칭키 암호화와 비대칭키 암호화의 절충 방식.<br/><br/>

<sup>1</sup>1976년에 화이트필드 디피<sup>Whitfield Diffie</sup>와 마틴 헬먼<sup>Martin Hellman</sup>이 [비대칭키 암호화 개념] [1]을 최초로 발표했다.<br/>

[1]: https://www.scirp.org/reference/referencespapers?referenceid=1940218