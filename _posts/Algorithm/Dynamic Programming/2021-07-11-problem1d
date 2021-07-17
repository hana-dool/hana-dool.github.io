---
title:  "점화식과 dp"
excerpt: "다이나믹 프로그래밍"
categories:
  - AL_Dynamic_Programming
tags:
  - 1
last_modified_at: 2021-07-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 점화식과 DP

## Ex1

- https://www.acmicpc.net/problem/1463
- 위 문제의 경우, 점화식은 $a_i = min(a_{i-1}, a_{i/2}, a_{i/3})+1 $ 이 됩니다.
- 이렇게 문제가 점화식으로 표현이 될경우, 바텀업 dp 와 list 로 구현이 가능합니다. 

```python
n = int(input())
dp = [ 0 for _ in range(n+1)] # 각 index 가 바르게 표현되어야 해서, n+1 까지! 

for i in range(2,n+1):
    lst = []
    if i > 0 :
        lst.append(dp[i-1])
    if i % 2 == 0 :
        lst.append(dp[i//2])
    if i % 3 == 0 :
        lst.append(dp[i//3])
    dp[i] = min(lst) + 1
print(dp[-1])
```

## Ex2

- 리스트가 주어지고, 인접해서 리스트의 원소를 선택할 수 없을때 얻을 수 있는 최댓값 

```python
4
[1,3,1,5] 
```

```python
8
```

- 위 문제의 경우 $a_n = max(a_{n-1},a_{n-2} + l_n)$ 이다. ($l_n$ 은 리스트의 n 번째 원소)

```python
def(n,arr):
    dp = [0]*n
    dp[0] = arr[0]
    dp[1] = max(arr[0],arr[1])
    for i in range(2,n):
        dp[i] = max(dp[i-1],dp[i-2]+arr[i])
    return(dp[-1])
```

## Ex3

<https://www.acmicpc.net/problem/11727>

- 위 문제의 경우 점화식은 다음과 같다. 
- $a_i = a_{i-1} + 2a_{i-2} $

```python
n = int(input())
dp = [0]*(n+1)

dp[1] = 1
dp[2] = 3
for i in range(3,n+1):
    dp[i] = dp[i-1] + dp[i-2] * 2
print(dp[-1] % 10007)
```

# 좀 더 잘게 쪼개기

- 위처럼 일반적인 점화식으로 나오면 좋겠지만, 문제의 조건에 따라서는 일반적으로 나오기 힘들 수 있다.
- 이 경우 각 경우의 수를 '더 잘게 쪼개서' 현제 Step 을 이전 Step 으로 표현할 수 있으면 된다. 

## Ex4 

- <https://www.acmicpc.net/problem/10844>
- 항상 마음에 가질것 : '복잡하더라도, 이전 Step 으로 쪼갤수만 있다면 DP 가 가능하다.'

```python
N = int(input())
dp = [[0,0,0,0,0,0,0,0,0,0] for _ in range(101)]
# 높은 자릿수 (1~9) 에 대한 경우의 수로 쪼갰다. 
dp[0] = [0,1,1,1,1,1,1,1,1,1] 
dp[1] = [0,2,2,2,2,2,2,2,2,1]

for i in range(2,101):
    dp[i][1] = dp[i-2][1] + dp[i-1][2]
    dp[i][2] = dp[i-1][1] + dp[i-1][3]
    dp[i][3] = dp[i-1][2] + dp[i-1][4]
    dp[i][4] = dp[i-1][3] + dp[i-1][5]
    dp[i][5] = dp[i-1][4] + dp[i-1][6]
    dp[i][6] = dp[i-1][5] + dp[i-1][7]
    dp[i][7] = dp[i-1][6] + dp[i-1][8]
    dp[i][8] = dp[i-1][7] + dp[i-1][9]
    dp[i][9] = dp[i-1][8]
print(sum(dp[N-1])%1000000000)
```

<br>

# EX 

- <https://www.acmicpc.net/problem/1912>
- n개의 정수로 이루어진 임의의 수열이 주어진다. 우리는 이 중 연속된 몇 개의 수를 선택해서 구할 수 있는 합 중 가장 큰 합을 구하려고 한다. 단, 수는 한 개 이상 선택해야 한다.
- 예를 들어서 10, -4, 3, 1, 5, 6, -35, 12, 21, -1 이라는 수열이 주어졌다고 하자. 여기서 정답은 12+21인 33이 정답이 된다.

```python
import sys
input = sys.stdin.readline
n = int(input())
lst = list(map(int,input().split()))
dp = [0] * n
dp[0] = lst[0]
for i in range(1,n):
    dp[i] = max(lst[i],lst[i] + dp[i-1])
print(max(dp))
```

- 위와 같이 dp[i]  는 i 를 선택한 경우의, maximum 값 이라는 조건을 걸어서 풀었다. 

# 복잡한 DP

## 가장 긴 증가하는 부분수열

<https://www.acmicpc.net/problem/11053>

```python
n = int(input())
lst = list(map(int,input().split()))
dp = [1] * n
for i in range(n):
    for j in range(i):
        if lst[j] < lst[i] :
            dp[i] = max(dp[i], dp[j]+1)
print(max(dp))
```



