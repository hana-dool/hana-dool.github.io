---
title:  "[DFS] 조합과 수열"
excerpt: "조합의 수 출력"
categories:
  - AL_DFS_BFS
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

# 문제

- 자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 '수열'을 모두 구하는 프로그램을 작성하시오.
  - 1부터 N까지 자연수 중에서 중복 없이 M개를 고른 수열

- <https://www.acmicpc.net/problem/15649>

```python
n,m = map(int,input().split())
# 1~n 까지의 자연수 중에서 중복없이 M 개를고른 수열
visit = [0] * (n+1)
ans = []
def dfs(depth):
    if depth == m : # 조건부
        print(*ans) # 출력부
        return
    else :
        for i in range(1,n+1): # 조건부
            if visit[i] == 0 :
                visit[i] = 1
                ans.append(i)
                dfs(depth+1) # 재귀부
                visit[i] = 0 # 원상 복귀부
                ans.pop()
dfs(0)
```

<br>

# 문제

- <https://www.acmicpc.net/problem/15650>
- 위와는 다르게, 중복되는 수열을 여러개 출력하면 안된다. 

![png](/assets/images/Algorithm/2_1.png)

```python
n,m = map(int,input().split())
visit = [0]*(n+1)
ans = []
ch = []
def dfs(depth):
    if depth == m :
        print(*ans)
        return
    else :
        for i in range(1,n+1):
            if visit[i] == 0 :
                for j in range(i+1):
                visit[j] = 1
                ans.append(i)
                dfs(depth+1)
                ans.pop()
                for j in range(i+1):
                visit[j] = 0 
dfs(0)
```

- 위처럼 출력부에 새로 조건을 만들거나 

```python
n,m = map(int,input().split())
visit = [0]*(n+1)
ans = []
ch = []
def dfs(depth):
    if depth == m :
        print(*ans)
        return
    else :
        for i in range(1,n+1):
            if visit[i] == 0 :
                for j in range(i+1): # Visited 처리
                    visit[j] = 1
                ans.append(i)
                dfs(depth+1)
                ans.pop()
                for j in range(i+1):
                    visit[j] = 0
dfs(0)
```

- 위처럼 '깊어질떄에' 조건을 새로 달면 된다.

<br>
