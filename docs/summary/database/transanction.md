---
title: Transaction
layout: default
parent: Database
grand_parent: Summary
nav_order: 10
---

## Transaction이란?
### Transaction
- 모두 실행되거나 전혀 실행되지 않아야 하는 작업 묶음. Ex. 쇼핑몰 결제.<br/>
- 기본 속성(ACID)을 만족해야 한다.<br/>

### ACID 
1. 원자성<sup>Atomicity</sup>: 분할할 수 없다. 모든 연산이 성공적으로 실행되거나, 전혀 실행되지 않아야 한다.<br/>
2. 일관성<sup>Consistency</sup>: 트랜잭션 실행이 완료된 후에는 데이터베이스가 일관된 상태를 유지해야 한다<sup>1</sup>.<br/>
3. 독립성<sup>Isolation</sup>: 동시에 실행되는 여러 트랜잭션이 서로에게 영향을 주지 않아야 한다.<br/>
4. 지속성<sup>Durability</sup>: 트랜잭션이 성공적으로 완료되면, 그 결과는 시스템이 고장 나더라도 영구적으로 데이터베이스에 반영되어야 한다.<br/><br/>

<sup>1</sup>무결성 제약 조건을 위반하지 않는다.<br/>