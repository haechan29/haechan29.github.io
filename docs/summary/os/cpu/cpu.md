---
title: CPU
layout: default
parent: CPU
grand_parent: OS
nav_order: 1
---

## CPU란?
### CPU
- Central Processing Unit.<br/>
- 주요 연산을 담당하는 컴퓨터의 제어 장치.<br/>

### 특징
- [스케쥴링 알고리즘] [1]에 따라 [인터럽트] [2]를 발생시켜 작업 순서를 결정한다. 이를 통해 여러 작업을 동시에 진행할 수 있다.<br/>
- [가상 메모리] [3]를 사용한다.<br/>

### 구성 요소
- 산술논리연산장치(ALU): 산술, 논리 연산을 하는 회로 장치.<br/>
- 제어 장치(Control Unit, CU): CPU 내의 명령어 실행 과정을 제어한다.<br/>
- 레지스터: CPU 안에 있는 매우 빠른 임시 기억 장치.<br/>

[1]: cpu%20scheduling%20algorithm.html
[2]: /docs/summary/os/process%20and%20thread/interrupt.html
[3]: /docs/summary/os/memory/virtual%20memory.html