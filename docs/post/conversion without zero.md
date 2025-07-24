---
title: 124 나라의 숫자
layout: default
parent: Post
date: 2025-07-24
---

## 124 나라의 숫자
### 문제
[124 나라의 숫자] [1]<br/>
10진법을 3진법으로 변환하되, 0을 사용하지 않아야 한다.<br/>
(ex. 3 -> 10 이 아니라 3 -> 4)<br/>

### 나의 풀이
```
// 정답은 맞으나 시간 초과
def solution(n):
    digits = list(map(int, to_base3(n)))
    
    for i in range(0, len(digits) - 1):
        j = len(digits) - 1 - i
        if digits[j] <= 0:
            digits[j - 1] -= 1
            digits[j] += 3

    return ''.join(str(d) for d in digits).replace('0', '').replace('3', '4')

def to_base3(n: int) -> str:
    if n == 0:
        return "0"
    digits = []
    while n:
        digits.append(str(n % 3))
        n //= 3
    return ''.join(reversed(digits))
```

### 모범 답안
```
def solution(n):
    result = ''
    while (n >= 1):
        n -= 1
        n, mod = divmod(n, 3)
        result = '124'[mod] + result
    return result
```

### 생각해본 점
1. **진수 변환 문제도 결국 재귀 문제다**<sup>1</sup>.<br/>
맨 끝자리 하나를 변환하고, 변환된 숫자만큼 원래 숫자를 감소시키면 자리수만 하나 줄고 문제가 똑같이 때문이다.
그렇기 때문에 결국 한 자리수를 한 자리수로 변환하는 문제를 풀 수 있다면 이 문제를 풀 수 있다.<br/><br/>

2. [0, 1, 2]를 [1, 2, 4] 으로 매칭하기<br/>
이런 트릭은 가끔 쓰이곤 하는데, 1을 빼서 나눈 나머지에 1을 더해주면 된다.
다만 3이 아니라 4를 매칭해야 하므로 문자열 `124[i]`와 같이 문자열 기반 접근도 좋겠다.<br/><br/>

<sup>1</sup>문제를 재귀적으로 풀면 필요한 변수의 갯수가 줄기 떄문에 코드가 간결해지는 것 같다.

[1]: https://school.programmers.co.kr/learn/courses/30/lessons/12899