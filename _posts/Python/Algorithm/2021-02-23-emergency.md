---
title:  "응급실"
excerpt: "Algorithm"
categories:
  - Py_Algorithm
tags:
  - 3
last_modified_at: 2021-02-23

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

- 문제 및 답 출처 : [링크](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/dashboard)

- 해당 링크에 가시면 훨씬 더 전문적인 해설 및 / 강의를 보실 수 있습니다. 

# 문제

**문제**  

![png](/assets/images/{Algorithm}/16_1.JPG)

**입력설명**

- 첫 줄에 자연수 N , M 이 주어진다.
- 두번째 줄에 접수한 순서대로 환자의 위험도가 주어진다.
- 위험도는 값이 높을 수록 더 위험하다는 뜻이다. 같은 값의 위험도가 존재할 수 있다.

**출력 설명**

- M번째 환자의 몇번째로 진료받는지 출력하라.

**입력 예제**

5 2

60 50 70 80 90

**출력예제**

3

# 내 해답

- 큐 로 구성해서 풀어야 하는 문제이다.

```python
import sys
sys.stdin=open("in1.txt", "r")
from collections import deque

N, M = map(int,input().split())
lis = list(map(int,input().split()))
lis2 = list(enumerate(lis))

p = deque(lis2)
cnt = 0
while True :
    val = p.popleft() # val 의 첫번째는 순서/ 두번째는 값
    print([val[1] >= j[1] for j in p])
    if all([val[1] >= j[1] for j in p]) :
        # 내 앞에 사람이 잘 된다!
        cnt += 1
        if val[0] == M:
            break
    else :
        p.append(val)
print(cnt)
```



# 다른 답

```python
import sys
from collections import deque
sys.stdin=open("input.txt", "r")
n, m=map(int, input().split())
Q=[(pos, val) for pos, val in enumerate(list(map(int, input().split())))]
Q=deque(Q)
cnt=0
while True:
    cur=Q.popleft()
    if any(cur[1]<x[1] for x in Q):
        Q.append(cur)
    else:
        cnt+=1
        if cur[0]==m:
            print(cnt)
            break
```

