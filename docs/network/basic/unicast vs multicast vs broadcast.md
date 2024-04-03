---
title: Unicast vs Multicast vs Broadcast
layout: default
parent: Basic
grand_parent: Network
nav_order: 3
---

## Unicast vs Multicast vs BroadCast
### Unicast
- 1:1 통신(ex. HTTP). 가장 일반적인 통신 형태.

### Multicast
- 선택적인 1:N 통신. 특정 그룹에게만 데이터를 보낸다.
- [멀티캐스트용 IP 주소(224.0.0.0 ~ 239.255.255.255)를 사용한다.] [1]
- UDP를 사용한다.

### Broadcast
- 1 : N 통신. 연결되어있는 로컬 네트워크의 모든 노드에게 데이터를 보낸다.
- [브로드캐스트용 IP 주소로 네트워크 영역의 마지막 주소를 사용한다.] [2]
- 통신하고자 하는 시스템의 MAC 주소를 알지 못하거나, 네트워크에 있는 모든 시스템에게 알리거나, 새로운 라우터를 찾는 등의 경우에 사용된다.

[1]: https://blog.naver.com/wnrjsxo/221250742423
[2]: https://hasensprung.tistory.com/11