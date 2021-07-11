---
title:  "Brute Force"
excerpt: "다~ 해보기"
categories:
  - AL_Others
tags:
  - 1
last_modified_at: 2021-05-19

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# <center><font size="15"> Brute Force </font></center>

- **무차별 대입 공격**(brute-force attack) 이다.
- 이는 모든 경우의 수를 직접 다 적용해보는, 한마디로 '노가다' 방법이다.
  - 거의 무조건적으로 시간이 더 걸린다고 보면 됩니다. 
- 진짜 단순하게 1씩 더해보는게 논리의 핵심? 입니다.
  - 이런 단순함이란게 사실 생각나지 않을떄가 있습니다.

<br>

<br>

# EX1

![png](/assets/images/Py_Algorithm/2_1.png)

```python
N = int(input())
movie = 666
while N:
    if "666" in str(movie):
        N -= 1
    movie += 1
print(movie - 1)
```

- 위와같이 Brute Force 법으로 간단하게 구현할 수 있다.
- 위 방법을 소개해 보자면, 666부터 시작하여 1씩 늘려가며 '모두 경우의 수를' 노가다로 구하고 있다.
- 일반적으로 최적화 없이 작동하게 되면 시간 초과에 걸리기가 쉽디ㅏ.

# EX2

<https://www.acmicpc.net/problem/1052>

```python
n, k = map(int, input().split())
num = 0
while True:
    b = bin(n)
    c = b.count('1')
    if c <= k:
        break
    else:
        n += 1
        num += 1
print(num)
```

- 진짜 징그럽다... 

