---
title:  "분할정복"
excerpt: "나눠서 정복하기"
categories:
  - AL_Others
tags:
  - 1
last_modified_at: 2021-07-13

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 나눠서 정복하기

- 어떤 문제들은 한번에 풀기에는 메모리 및 시간초과가 나기때문에 분할정복이 필요한 경우가 있다. 

<br>

# 거듭제곱 구현

```python
def power(a,b):
    if b == 1:
        return a 
    else : 
        val = power(a,b//2)
        if b % 2 == 0 :
            return val * val
        else :
            return val * val * a 
```

# 거듭제곱의 나머지

- <https://www.acmicpc.net/problem/1629>

```python
a,b,C = map(int,input().split())
def power(a, b):
    if b == 1: # 출력부
        return a % C
    else:
        val = power(a, b // 2) # 깊어지는 재귀부
        if b % 2 == 0:
            return val * val % C # b가 짝수인 경우
        else:
            return val * val * a % C # b가 홀수인 경우
```

- 위와 같이, 하게되면 어떻게 될까
- power(2,10) -> power(2,5) -> power(2,2) -> power(2,1) 

<br>
