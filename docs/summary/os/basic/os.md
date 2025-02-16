---
title: OS
layout: default
parent: Basic
grand_parent: OS
nav_order: 1
---

## OS란?
### OS
[컴퓨터의 하드웨어] [1]와 응용 프로그램의 상호작용을 관리하는 소프트웨어.

### OS의 구조
[커널(Kernel)] [2], 시스템 콜(System Call), 인터페이스로 구성됩니다.

### 커널
아래와 같은 기능을 통해 하드웨어와 소프트웨어 리소스를 관리합니다.<br/>
- 프로세스 상태 관리.<br/>
- 메모리 관리.<br/>
- I/O 디바이스 관리.<br/>
- 디스크 파일 관리.<br/>
- 인터페이스(시스템 콜) 제공.<br/>

### 시스템 콜
- 사용자 프로그램이 커널의 기능을 사용하기 위한 인터페이스.<br/>
- 모드빗<sup>1</sup>을 통해 커널 모드<sup>2</sup>와 사용자 모드<sup>3</sup>를 구분하여 시스템의 보안을 유지합니다.<br/>

### 인터페이스
- 사용자와 시스템의 상호작용을 담당한다.<br/>
- Ex. GUI(Graphical User Interface), CLI(Command Line Interface).<br/>

<br/>

<sup>1</sup>모드빗(Modebit): 시스템콜의 모드를 결정하는 플래그 변수.<br/>
<sup>2</sup>커널 모드(Kernel mode): 커널 영역의 코드를 실행할 수 있는 모드. 모드빗이 0인 상태.<br/>
<sup>3</sup>사용자 모드(User mode): 커널 영역의 코드를 실행할 수 없는 모드. 모드빗이 1인 상태.<br/>

[1]: /docs/summary/os/basic/computer%20hardware.html
[2]: https://minkwon4.tistory.com/295