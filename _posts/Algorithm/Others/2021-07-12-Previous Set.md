---
title:  "미리 만들기"
excerpt: "값을 미리 만들기"
categories:
  - AL_Others
tags:
  - 1
last_modified_at: 2021-07-12

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 미리 만들기

- 어떤 문제들은 범위에 맞춰서 미리 '정답' 을 생성한 뒤에 푸는것이 더 효율적일 떄가 있다. 

<br>

# 베르트랑 공준

- <https://www.acmicpc.net/problem/4948>

- 베르트랑 공준은 임의의 자연수 n에 대하여, n보다 크고, 2n보다 작거나 같은 소수는 적어도 하나 존재한다는 내용을 담고 있다.
- 예를 들어, 10보다 크고, 20보다 작거나 같은 소수는 4개가 있다. (11, 13, 17, 19) 또, 14보다 크고, 28보다 작거나 같은 소수는 3개가 있다. (17,19, 23)
- 자연수 n이 주어졌을 때, n보다 크고, 2n보다 작거나 같은 소수의 개수를 구하는 프로그램을 작성하시오. 

```python
import math
dp = [0,1,1] + [0]*250000
def ch(x):
    for i in range(2,int(math.sqrt(x))+1) :
        if x % i == 0 :
            return(0) # 합성수일떄
    return(1) # 소수일떄
for i in range(250000):
    dp[i] = ch(i)
while True :
    val = int(input())
    if val == 0 :
        break
    ans = sum(dp[val+1:2*val+1])
    print(ans)
```

- 위처럼 미리 '소수' 인 행렬을 25만개까지 만든 뒤에, 그 뒤는 그저 input 에 따라 sum 만 하면 된다.
- 이를 각각에 대해 Input 을 받고 소수의 갯수를 출력하려 하면 시간 초과가 뜬다. 
