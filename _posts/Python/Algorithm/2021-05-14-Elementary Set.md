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

<br>

# 수열 정렬

- <https://www.acmicpc.net/problem/1015>

```python
n = int(input()) 
lst = list(map(int, input().split())) 
s_lst = sorted(t) 
ans = [] 
for i in range(n): 
    idx = s_lst.index(lst[i]) 
    ans.append(idx) 
    s_lst[idx] = -1 
print(ans)
```

<Br>

# 좌표압축

- <https://www.acmicpc.net/problem/18870>

```python
import sys
input = sys.stdin.readline

N = int(input())
lst = list(map(int,input().split()))
s_lst = sorted(list(set(lst)))
dic = dict(zip(s_lst,list(range(len(s_lst)))))
for i in lst:
    print(dic[i],end=' ')
```

<br>

