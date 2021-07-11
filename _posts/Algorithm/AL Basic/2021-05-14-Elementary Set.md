---
title:  "5.기초 필수문제"
excerpt: "자주 쓰이는 문제"
categories:
  - AL_Basic
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

# Windowing

- <https://www.acmicpc.net/problem/1018>
- 좌표를 순회하면서, 내가 정한 모양에 부합하는지 검사합니다. 

```python
import sys
input = sys.stdin.readline

n,m = map(int,input().split())
mat = []
mat = [list(input().strip()) for _ in range(n)]

# 내가 정한 모양
window_1 = [['W','B']*4,['B','W']*4]*4
window_2 = [['B','W']*4,['W','B']*4]*4
ans = []
for i in range(n):
    for j in range(m):
        # index 를 벗어나지 않도록
        if i+8 <= n and j+8 <= m :
            val1,val2 = 0,0
            for x in range(8):
                for y in range(8):
                    # 검사하는 부분
                    if mat[i+x][j+y] != window_1[x][y] :
                        val1 += 1
                    if mat[i+x][j+y] != window_2[x][y] :
                        val2 += 1
            ans.extend([val1,val2])
print(min(ans))
```

<br>

# 원형큐 구현

- <https://www.acmicpc.net/problem/1158>

```python
N, K = map(int,input().strip().split())
lst = list(range(1,N+1))
ans = []  # 제거된 사람들을 넣을 배열
idx = 0  # 제거될 사람의 인덱스 번호

for t in range(N):
    idx += K - 1
    if idx >= len(lst):  # 한바퀴를 돌고 그다음으로 돌아올때를 대비해 값을 나머지로 바꿈
        idx = idx % len(lst)
    ans.append(lst.pop(idx))
print('<',end = '')
print(', '.join(map(str,ans)),end = '')
print('>')
```

<br>

# 전화번호 목록

- <https://programmers.co.kr/learn/courses/30/lessons/42577>

```python
def solution(phoneBook):
    phoneBook = sorted(phoneBook)
    for p1, p2 in zip(phoneBook, phoneBook[1:]):
        if p2.startswith(p1):
            return False
    return True
```

<br>

- 

```python
def whatFlavors(cost, money):
    dic = {}
    for idx,val in enumerate(cost):
        if money - val in dic :
            print(f'{dic[money-val]+1} {idx+1}')
        else :
            dic[val] = idx
```

