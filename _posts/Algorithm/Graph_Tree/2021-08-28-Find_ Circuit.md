---
title:  "순횐 찾기"
excerpt: "무향 / 유향 그래프"
categories:
  - AL_Graph_Tree
tags:
  - 1
last_modified_at: 2021-08-28

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 순열 사이클 

- 위 문제는, 아주 쉬운버전으로, 재귀를 이용해 사이클의 유무를 판단하는것이 핵심입니다.
  - 이런 아이디어가 뒤에서도 사용되므로 잘 익히도록합시다.
- https://www.acmicpc.net/problem/10451

```python
import sys
input = sys.stdin.readline
sys.setrecursionlimit(10**9)
T = int(input())
for _ in range(T) :
    N = int(input())
    visited = [0]*(N+1)
    cycle = [0] + list(map(int,input().split()))

    def dfs(x) :
        # 이미 visited 가 아닌 수열로 접어들었다고 판단.
        visited[x] = 1
        if visited[cycle[x]] == 0 :
            dfs(cycle[x])
    cnt = 0
    for i in range(1,N+1) :
        if visited[i] == 0 :
            dfs(i)
            cnt += 1
    print(cnt)
```

# 무향 그래프

- 기본적으로 Union Find 를 통해 가능합니다. 



<Br>

# 유향 그래프 

```python
# 방문한 정점을 기록하면서, 방문한 정점을 또 방문하면 사이클이 존재

V, E = map(int,input().split())
visited = [0] * (V+1) # 방문한 정점 정보를 담을 stack 생성
graph = [[] for i in range(V+1)] # 빈 인접 리스트 그래프 생성

# 그래프 생성
for i in range(E):
    a, b = map(int,input().split()) # 간선 정보 받아오기
    graph[a].append(b)
    graph[b].append(a)
    
# dfs 탐색 함수 생성
def dfs(i):
    visited[i] = 1 # 방문한 정점 정보 갱신
    node = graph[i] # 방문할 정점 받아오기
    if not node in visited: # 방문하지 않은 정점이면 dfs 진행
        dfs(node)
    elif node in visited: # 다음에 방문할 정점이 visitied에 존재하면 순환이 존재
        return True
    return False # 순환이 존재하지 않으면 False

result = False
for i in range(1, V+1): # 모든 정점 호출
    if visited[i] == 0: # 방문하지 않은 정점이면, 탐색 진행
        if dfs(i):
            result = True

print(result) # 순환이 존재하면 True 반환
```

- 기본적으로 위와 같이 구현이 됩니다.
