---
title: Garbage Collection
layout: default
parent: Etc
grand_parent: Summary
nav_order: 3
---

## Garbage Collection이란?
### Garbage Collection
- 프로그램이 동적으로 할당한 메모리 중에서 더 이상 사용되지 않는 부분을 자동으로 찾아서 해제하는 프로세스.<br/>
- 메모리 공간을 효율적으로 관리하고 메모리 누수를 방지한다.<br/>
- [Serial GC, Parallel GC, Parallel Old GC, CMS GC] [1], [G1 GC] [2] 등이 있다.<br/>

### 동작 원리
1. 도달 가능성 분석: Garbage Collector가 루트 집합<sup>1</sup>에서 시작하여 접근할 수 있는 모든 객체를 추적한다.<br/>
2. 메모리 회수: 프로그램에서 접근할 수 없는 객체를 메모리에서 제거한다.<br/>

### 전략
- 마크 앤 스위프(Mark and Sweep): 객체가 살아있는지 여부를 마킹하고 쓸모없는 객체를 메모리에서 제거한다.<br/>
- 참조 카운팅(Reference Counting): 객체에 대한 참조 횟수를 센다. 참조 카운트가 0이 되면 메모리에서 제거한다.<br/>
- 복사 수집(Copying Collection): 메모리를 두 영역으로 나누고, 사용 중인 객체만 새 영역으로 복사한 다음, 이전 영역을 통째로 비운다.<br/>
- 세대별 수집(Generational Collection): 객체를 세대로 나누어 관리한다. 젊은 세대에서 오래된 세대로 확장하는 방식으로 GC을 수행한다. 대부분의 객체가 짧은 시간 내에 사용되지 않게 된다는 가설에 기반한다.<br/><br/>

<sup>1</sup>루트 집합: 전역 변수와 스택 프레임에서 참조되는 객체 등 프로그램이 직접 접근할 수 있는 변수.<br/>

[1]: https://mangkyu.tistory.com/119
[2]: garbage%20first%20garbage%20collection.html