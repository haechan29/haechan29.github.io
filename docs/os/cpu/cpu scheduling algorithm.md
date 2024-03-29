---
title: CPU 스케쥴링 알고리즘
layout: default
parent: CPU
grand_parent: OS
nav_order: 2
---

## CPU는 어떻게 스케쥴링될까?
### CPU 스케쥴링 알고리즘
1. 비선점형(Non-preemptive): 프로세스가 스스로 CPU 소유권을 포기하는 방식.<br/>
    - FCFS(First Come, First Served): 먼저 요청된 작업을 먼저 처리하는 알고리즘. 호위 효과<sup>1</sup>가 발생하는 단점이 있다.<br/>
    - SJF(Shortest Job First): 실행 시간이 짧은 순서대로 실행하는 알고리즘. 평균 대기 시간이 가장 짧다. 하지만 기아 현상<sup>2</sup>이 일어날 수 있다. 실행 시간은 과거 이력을 토대로 추측한다.<br/>
    - 우선 순위: SJF에 에이징<sup>3</sup>을 적용한 알고리즘.<br/>
    <br/>

2. 선점형(Preemptive): CPU 소유권을 강제로 할당할 수 있는 방식. 현대 운영체제가 쓰는 방식.
    - RR(Round Robin): 준비 큐(Ready queue)를 이용하여 각 프로세스에 순차적으로 동일한 시간을 할당하는 알고리즘. 전체 작업 시간은 길어지지만 평균 응답 시간은 짧아진다.<br/>
    - SRTF(Shortest Remaining Time First): SJF의 선점형 버전. 현재 진행 중인 프로세스보다 더 짧은 작업이 추가되면 수행하던 프로세스를 중지하고 해당 프로세스를 수행한다.<br/>
    <br/>

3. 혼합형
    - 다단계 큐: RR이나 FCFS 등 여러 스케줄링 알고리즘을 이용하는 것. 우선 순위가 다른 준비 큐 여러 개를 사용한다. 우선 순위가 낮은 큐에서 기아 현상이 발생할 수 있다.<br/>
    <br/>

<sup>1</sup>호위 효과(Convoy effect): 길게 수행되는 프로세스 때문에 준비 큐에서 오래 기다리는 현상.<br/>
<sup>2</sup>기아 현상(Starvation): 프로세스가 계속해서 자원을 할당받지 못하는 현상.<br/>
<sup>3</sup>에이징(Aging): 프로세스의 대기 시간이 길어질수록 우선 순위를 높이는 방법.<br/>