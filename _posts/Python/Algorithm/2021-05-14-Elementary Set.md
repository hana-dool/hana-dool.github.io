---
title:  "5.기초 필수문제"
excerpt: "자주 쓰이는 문제"
categories:
  - Py_Algorithm
tags:
  - 1
last_modified_at: 2021-07-04

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 문자열 세기

<https://www.acmicpc.net/problem/2941>

```python
Input=input()
Dict=['c=','c-','dz=','d-','lj','nj','s=','z=']
for key in Dict:
    Input=Input.replace(key,'_')
print(len(Input))
```

<br>

# BFS 

<https://www.acmicpc.net/problem/1697>

```python
from collections import deque

n,k = map(int,input().split())

Max = 100001
visited = [0]*Max

need_visit = deque([n])
while need_visit:
    node = need_visit.popleft()
    if node == k:
        print(visited[node])
    for next_node in (node-1, node+1, node*2):
        if 0<=next_node < Max and not visited[next_node]:
            visited[next_node] = visited[node]+1
            need_visit.append(next_node)
```



# 회의실 배정

<https://www.acmicpc.net/problem/1931>

```

```

