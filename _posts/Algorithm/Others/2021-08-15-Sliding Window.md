---
title:  "Sliding Window"
excerpt: "슬라이딩 윈도우"
categories:
  - AL_Others
tags:
  - 1
last_modified_at: 2021-08-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

- 슬라이딩 윈도우는, 기본적으로 아래 아이디어를 따릅니다.

![png](/assets/images/Python/26_1.png)

- 위와 같이, 같은 길이를 가지는 '윈도우' 를 순회하는 방식입니다.
- 이때에, 각 합을 구할때에는 sum(lst[start:end]) 방식으로 구현하는게 아니라, 각 단계마다 lst[start] 를 뺴도 lst[end] 를 더해서 계산합니다.
  - lst[start:end] 를 이용하게 된다면, lst 의 인덱싱이 큰 시간이 걸리기 떄문입니다.
  - 그러므로 value 로만 접근하여 시간을 줄이는 방법입니다.
- 주로 '연속된 K 개의 arr element 가 조건을 만족하도록' 하려면 어떻게 해야하는가? 와 관련됩니다.

# EX : 게으른 백곰

![png](/assets/images/Python/26_2.png)

```python
import sys
input = sys.stdin.readline

arr = [0] * 1000001

N, K = map(int, input().split())
for _ in range(N):
    g, x = map(int, input().split())
    arr[x] = g

step = K * 2 + 1
tmp = sum(arr[:step])
result = tmp

for i in range(step, 1000001):
    tmp += arr[i] - arr[i-step]
    result = max(result, tmp)
print(result)
```

- 위와 같이 슬라이딩 윈도우를 이용하여 풀 수 있습니다.
- 이 떄에 초깃값을 먼저 계산해야 그 뒤는 슬라이딩으로 계속 풀 수 있음을 기억합시다!

<br>

# 신호등 수리

![png](/assets/images/Python/26_3.png)

```python
N,K,B = map(int,input().split())
road = [0]*N
for _ in range(B) :
    a = int(input())
    road[a-1] = 1
init = sum(road[:K])
mn = init
for i in range(K, N) :
    init += road[i]-road[i-K]
    mn = min(init,mn)
print(mn)
# 연속한 K 개 존재하도록
```

<br>

# DNA 비밀번호

- https://www.acmicpc.net/problem/12891

```python
import sys
input = sys.stdin.readline
S,P = map(int,input().split())
dna = input()
a,c,g,t = map(int,input().split())
cnt = 0

def check(dic) :
    if dic['A'] >= a and dic['C'] >= c and dic['G'] >= g and dic['T'] >= t :
        return 1
    else :
        return 0

dic = {'A':dna[:P].count('A'),
       'C':dna[:P].count('C'),
       'G':dna[:P].count('G'),
       'T':dna[:P].count('T')}
cnt += check(dic)

for i in range(P,S) :
    if dna[i] in ('A','C','G','T') :
        dic[dna[i]] += 1
    if dna[i] in ('A','C','G','T') :
        dic[dna[i-P]] -= 1
    cnt += check(dic)
print(cnt)
```

- 어려워 보이지만 '비밀번호의 길이' 가 주어진다는 점에서 그냥 슬라이딩 윈도우를 쓰면 된다~!

