---
title: 재귀 없이 이진 트리 순회하기 
layout: default
parent: Post
date: 2024-05-22
---

## 재귀 없이 이진 트리 순회하기
### 문제
[프로그래머스, 월간 코드 챌린지 시즌2 - 모두 0으로 만들기] [1]

### 상황
- 이진 트리를 순회해야 한다.<br/>
- 자식 노드를 부모 노드보다 먼저 방문해야 한다.<br/><br/>

### 제한
- 트리의 사이즈가 커서 기존의 재귀 방식은 사용할 수 없다.<br/><br/>

### 해결 <sub>[View Code] [Repository Link]</sub>
- 리프 노드부터 순회를 시작한다.<br/>
- 리프 노드를 순회할 때 부모의 모든 리프 노드를 방문했는지 확인한다.<br/>
- 만약 부모의 리프 노트를 모두 방문했다면 부모 노드를 순회한다.<br/><br/>

[1]: https://school.programmers.co.kr/learn/courses/30/lessons/76503?language=kotlin
[Repository Link]: https://github.com/haechan29/problem-solving/blob/main/src/main/kotlin/programmers/MakeValuesZero.kt