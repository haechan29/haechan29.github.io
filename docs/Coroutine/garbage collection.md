---
title: Garbage Collection
layout: default
parent: etc
nav_order: 3
---

## Garbage Collection
### Garbage Collection이란?
프로그램이 동적으로 할당한 메모리 중에서 더 이상 사용되지 않는 부분을 자동으로 찾아서 해제하는 프로세스입니다. 프로그램이 사용하는 메모리 공간을 효율적으로 관리하고 메모리 누수를 방지하여, 프로그램의 안정성과 성능을 유지하는 데 도움을 줍니다.
모든 객체를 순회하며, 직접적으로 또는 간접적으로 접근할 수 있는 객체를 마킹하고, 마킹되지 않은 객체들을 메모리에서 해제합니다
