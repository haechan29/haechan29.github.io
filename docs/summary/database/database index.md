---
title: Index
layout: default
parent: Database
grand_parent: Summary
nav_order: 2
---

## 인덱스란?
### 인덱스
데이터의 검색 속도를 향상시키기 위해 사용되는 데이터 구조.<br/>
대표적으로 [B-트리] [1], 해시 테이블 등을 사용합니다.<br/>

### 인덱스의 장점
- 검색 속도 향상.<br/>

### 인덱스의 단점
- 추가적인 저장 공간 사용.<br/>
- 인덱스를 관리하기 위해 추가 작업이 필요.<br/>

### 인덱스를 사용하기 적절한 경우
- INSERT, UPDATE, DELETE가 자주 발생하지 않는 컬럼.<br/>
- JOIN이나 WHERE 또는 ORDER BY에 자주 사용되는 컬럼.<br/>
- 데이터의 중복도가 낮은 컬럼.<br/><br/>

[1]: b%20tree.html