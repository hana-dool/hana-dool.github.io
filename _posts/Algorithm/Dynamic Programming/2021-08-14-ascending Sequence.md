---
title:  "긴 증가하는 부분수열"
excerpt: "매우 유명한 유형"
categories:
  - AL_Dynamic_Programming
tags:
  - 1
last_modified_at: 2021-08-14

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 가장 큰 증가 부분수열 (LIS)

![png](/assets/images/Python/9.png)

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

# 알고리즘 설명 : $O(N^2)$

- 새로운 배열 D를 정의하자. D[i]의 정의는 다음과 같다.
- D[i] : A[i]를 마지막 값으로 가지는 가장 긴 증가부분수열의 길이
- A[i]가 어떤 증가부분수열의 마지막 값이 되기 위해서는 A[i]가 추가되기 전 증가부분수열의 마지막 값이 A[i]보다 작은 값이여야 한다.
- 따라서 A[i]를 마지막 값으로 가지는 '가장 긴' 증가부분수열의 길이는 A[i]가 추가될 수 있는 증가부분수열 중 가장 긴 수열의 길이에 1을 더한 값이 된다.
- 수열 A = **3 5 7 9 2 1 4 8**을 예로 들어 알고리즘을 살펴보자.
  (알고리즘의 규칙성을 위해 i = 0일 때를 추가하자. i = 0일 때 A[i] = 0, D[i] = 0이다.)

| i    | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| A    | 0    | 3    | 5    | 7    | 9    | 2    | 1    | 4    | 8    |
| D    | 0    |      |      |      |      |      |      |      |      |

- i = 1일 때를 살펴보자.
- A[1] = 3이다. 3은 A[0] = 0 뒤에 붙을 수 있다. 따라서 D[1] = D[0] + 1 = 1이다.

| i    | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| A    | 0    | 3    | 5    | 7    | 9    | 2    | 1    | 4    | 8    |
| D    | 0    | 1    |      |      |      |      |      |      |      |

- i = 2일 때를 살펴보자.
- A[2] = 5이다. 5는 A[0] = 0, A[1] = 3 뒤에 붙을 수 있다. 이 때 D[0] = 0, D[1] = 1에서 D[1]이 가장 크다. 
- 이 말은 A[1] = 3을 가장 마지막 값으로 가지는 증가부분수열의 길이가 가장 길다는 뜻이다. A[2]가 가장 긴 증가부분수열 뒤에 붙는 게 더 긴 증가부분수열을 만들 수 있다. 따라서 D[2] = D[1] + 1 = 2이다.

| i    | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| A    | 0    | 3    | 5    | 7    | 9    | 2    | 1    | 4    | 8    |
| D    | 0    | 1    | 2    |      |      |      |      |      |      |

- i = 3일 때를 살펴보자.
- A[3] = 7이다. 7는 A[0] = 0, A[1] = 3, A[2] = 5 뒤에 붙을 수 있다. 이 때 D[0] = 0, D[1] = 1, D[2] = 2에서 D[2]가 가장 크다. 따라서 D[3] = D[2] + 1 = 3이다.

| i    | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| A    | 0    | 3    | 5    | 7    | 9    | 2    | 1    | 4    | 8    |
| D    | 0    | 1    | 2    | 3    |      |      |      |      |      |

- i = 4일 때를 살펴보자.
- A[4] = 9이다. 9는 A[0] = 0, A[1] = 3, A[2] = 5, A[3] = 7 뒤에 붙을 수 있다. 이 때 D[0] = 0, D[1] = 1, D[2] = 2, D[3] = 3에서 D[3]이 가장 크다. 따라서 D[4] = D[3] + 1 = 4이다.

| i    | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| A    | 0    | 3    | 5    | 7    | 9    | 2    | 1    | 4    | 8    |
| D    | 0    | 1    | 2    | 3    | 4    |      |      |      |      |

- i = 5일 때를 살펴보자.
- A[5] = 2이다. 2는 A[0] = 0 뒤에 붙을 수 있다. 따라서 D[5] = D[0] + 1 = 1이다.

| i    | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| A    | 0    | 3    | 5    | 7    | 9    | 2    | 1    | 4    | 8    |
| D    | 0    | 1    | 2    | 3    | 4    | 1    |      |      |      |

- i = 6일 때를 살펴보자.
- A[6] = 1이다. 2는 A[0] = 0 뒤에 붙을 수 있다. 따라서 D[6] = D[0] + 1 = 1이다.

| i    | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| A    | 0    | 3    | 5    | 7    | 9    | 2    | 1    | 4    | 8    |
| D    | 0    | 1    | 2    | 3    | 4    | 1    | 1    |      |      |

- i = 7일 때를 살펴보자.
- A[7] = 4이다. 4는 A[0] = 0, A[1] = 3, A[5] = 2, A[6] = 1 뒤에 붙을 수 있다. 이 때 D[0] = 0, D[1] = 1, D[5] = 1, D[6] = 1에서 D[1] = D[5] = D[6] = 1이 가장 크다. 따라서 D[4] = D[1] + 1 = 2이다.

| i    | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| A    | 0    | 3    | 5    | 7    | 9    | 2    | 1    | 4    | 8    |
| D    | 0    | 1    | 2    | 3    | 4    | 1    | 1    | 2    |      |

- i = 8일 때를 살펴보자.
- A[8] = 8이다. 8는 A[0] = 0, A[1] = 3, A[2] = 5, A[3] = 7, A[5] = 2, A[6] = 1, A[7] = 4 뒤에 붙을 수 있다. 이 때 D[0] = 0, D[1] = 1, D[2] = 2, D[3] = 3, D[5] = 1, D[6] = 1, D[7] = 2에서 D[3] = 3이 가장 크다. 따라서 D[4] = D[3] + 1 = 4이다.

| i    | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| A    | 0    | 3    | 5    | 7    | 9    | 2    | 1    | 4    | 8    |
| D    | 0    | 1    | 2    | 3    | 4    | 1    | 1    | 2    | 4    |

- 이렇게 해서 배열 D를 다 완성했다. D의 값들 중 가장 큰 값(D[4] = D[8] = 4)가 수열 A = **3 5 7 9 2 1 4 8**의 LIS의 길이다.
- 해당 길이를 가지는 부분수열을 찾는 방법은 여러 개가 있지만, 가장 간단한 것은 해당 값을 가지는 값부터 거꾸로 이어나가는 것이다. 0부터 순서대로 이어나가는 경우 해당 값을 마지막에 가진다는 보장이 없기 때문이다.
- 이 알고리즘은 N개의 수들에 대해 자기 자신 전의 모든 수를 다 훑어봐야 하므로 O(N2)의 시간복잡도를 가지는 알고리즘이 된다.

<br>

#  응용 : 가장 큰 증가 부분 수열

![png](/assets/images/Python/10.png)

```python
import sys
input = sys.stdin.readline
N = int(input())

lst=  list(map(int,input().split()))
dp = lst.copy()
for end in range(N) :
    for search in range(end) :
        if lst[search] < lst[end] :
            dp[end] = max(lst[end]+dp[search], dp[end])
print(max(dp))
```
