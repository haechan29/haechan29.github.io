---
title: 프로그램의 빌드 과정
layout: default
parent: Basic
grand_parent: OS
nav_order: 3
---

## 프로그램은 어떻게 빌드되나요?
### 프로그램의 빌드 과정
1. 소스 코드 작성<br/>
    - 프로그래머가 프로그래밍 언어(C, C++, Java 등)를 사용하여 소스 코드를 작성합니다.<br/>
    <br/>

2. 전처리(Preprocessing)<br/>
    - 전처리기(Preprocessor)는 #include, #define과 같은 지시어를 처리합니다.<br/>
    - 지시어에 의해 포함된 파일이 소스 코드에 삽입되거나, 매크로가 확장되는 등의 작업이 수행됩니다.<br/>
    <br/>

3. 컴파일(Compiling)<br/>
    - 문법 오류 검증 단계를 거칩니다.<br/>
    - 플랫폼(OS, HW 등)에 독립적인 중간 코드(Intermediate Code)를 생성합니다.<br/>
    - 중간 코드를 최적화하고, 목적 코드(Target Code)<sup>1</sup>로 변환합니다.<br/>
    <br/>

4. 링킹(Linking)<br/>
    - 컴파일 단계에서 생성된 하나 이상의 목적 파일(.o 또는 .obj)을 하나의 실행 파일로 결합됩니다.<br/>
    - 이 과정에서 다른 라이브러리 함수들과 함께 연결되거나(동적 링킹<sup>2</sup>), 필요한 라이브러리 코드가 포함됩니다(정적 링킹<sup>3</sup>).<br/>
    <br/>

<sup>1</sup>목적 코드: 대상 플랫폼(운영체제, 하드웨어 등)의 기계어 코드.<br/>
<sup>2</sup>[정적 링킹] [1]: 필요한 모든 코드(라이브러리 코드 포함)를 실행 파일 안에 포함시키는 방식입니다.<br/>
<sup>3</sup>[동적 링킹] [1]: 실행 파일이 실행될 때 라이브러리 코드를 메모리로 로드하는 방식입니다.<br/>

[1]: static%20linking%20vs%20dynamic%20linking.html
