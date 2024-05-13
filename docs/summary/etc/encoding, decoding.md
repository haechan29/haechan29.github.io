---
title: Encoding, Decoding
layout: default
parent: Etc
grand_parent: Summary
nav_order: 9
---

## Encoding, Decoding이란?
### Encoding과 Decoding
- Encoding: 문자, 사진 등의 데이터를 이진 데이터로 변환하는 과정.<br/>
- Decoding: Encoding의 역과정.<br/>

### 종류
1. ASCII
    - American Standard Code for Information Interchange.<br/>
    - ASCII 문자<sup>1</sup>를 사용한다.<br/>
    - 문자당 **1바이트**를 사용하여 저장한다.<br/>
    - 128개의 문자를 저장한다. 원래는 1비트는 오류 검출용이었으나, 국가 별로 확장하여 사용한다.<br/>
    <br/>

2. UTF-8
    - Unicode Transformation Format - 8bit.<br/>
    - 전 세계의 모든 문자를 다루도록 설계되었다.<br/>
    - 문자당 **1 ~ 4바이트**를 사용하여 저장한다(한글은 3바이트).<br/>
    <br/>

3. Base64
    - 64개의 ASCII 문자를 사용한다.<br/>
    - 문자당 **6비트**를 사용하여 저장한다.<br/>
    - 제어 문자 등의 형식이 달라 통신 과정에서 원본 데이터가 훼손되는 일을 방지하는 목적.<br/>
    - 데이터의 용량이 약 1/3만큼 증가한다.<br/>
    <br/>

<br/>

<sup>1</sup>ASCII 문자: 알파벳, 숫자 등 문자 코드에 영향을 받지 않는 공통 문자.<br/>