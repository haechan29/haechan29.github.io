---
title: JVM, JRE, JDK
layout: default
parent: Basic
grand_parent: Java, Kotlin
nav_order: 6
---

## JVM, JRE, JDK란?
### JVM
- Java Virtual Machine.<br/>
- Java 바이트코드(.class 파일)를 실행하는 추상적인 연산 장치.<br/>
- 운영 체제와 독립적이다<sup>1</sup>.<br/>

### JRE
- Java Runtime Environment.<br/>
- JVM을 포함하는 소프트웨어 패키지. Java 프로그램을 실행하는 데 필요한 환경을 제공한다.<br/>
- Java 라이브러리와 JVM과 같은 기타 파일들을 포함하고 있다.<br/>

### JDK
- Java Development Kit.<br/>
- Java 프로그램을 개발할 때 필요한 소프트웨어 개발 키트.<br/>
- JRE, 컴파일러(javac), 자바 문서 생성기(javadoc), 디버거와 같은 개발 도구를 포함한다.<br/>

<sup>1</sup>Write Once, Read Anywhere.<br/>
<sup>2</sup>메서드 영역: 클래스 수준의 정보(클래스 메타데이터, 정적 변수 등)를 저장한다. Static 영역이라고도 불린다.<br/>
<sup>3</sup>네이티브 메서드 스택: Java 이외의 언어(C, C++, 어셈블리 등)로 작성된 네이티브 코드를 실행할 때 사용되는 메모리 영역.<br/>