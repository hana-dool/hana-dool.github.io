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
- https://www.acmicpc.net/problem/20040

```python
import sys
input = sys.stdin.readline
N , M = map(int,input().split())
parent = list(range(N))

def find_parent(parent,x) :
    if parent[x] != x :
        parent[x] = find_parent(parent,parent[x])
    return parent[x]

def union_parent(parent,a,b) :
    a_p = find_parent(parent,a)
    b_p = find_parent(parent,b)
    if a_p != b_p :
        if a_p < b_p :
            parent[b_p] = a_p
        else :
            parent[a_p] = b_p
        return False
    else :
        return True
cnt = 0
for _ in range(M) :
    start, end = map(int,input().split())
    cnt += 1
    if union_parent(parent,start,end) :
        print(cnt)
        sys.exit(0)
print(0)
```

- 위처럼 union_parent 부분에 return True 를 넣으면 됩니다.
  - 왜냐하면, 이미 부모가 같은 상태에서 , 또 합쳐버리면 사이클이 되기 떄문

<Br>

# 유향 그래프 - 각 점에 대해서 판별

```python
from collections import defaultdict
N = 7
edges = [(1, 2), (2, 3), (3, 4), (4, 2), (5, 6), (6, 7)]
graph = defaultdict(list)
for edge in edges:
    v, w = edge
    graph[v].append(w)
visited = [0] * (N + 1)

ans = []
def dfs2(start,now) :
    if start == now : # 현재 지점과, dfs 로 도착한 지점이 같다?
        if visited[start] == 1: # 게다가 한번 방문했었음? 
            ans.append(start) # 그러면, 이건 사이클이다! 
            return # 끝내기
    for path in graph[now] :
        if visited[path] == 0 :
            visited[path] = 1
            dfs2(start,path)
dfs2(1,1) # 1->1 로 가는 사이클이 존재할까?
print(ans) 
```

- 위와 같이 , 구현하게 되면, 유향 그래프에서 사이클을 찾을 수 있습니다.
- 하지만 이떄에 모든 점에 대해서 사이클을 찾으려면 그 복잡도는 O(V(V+E)) 가 됩니다. 
  - V 는 정점의 수 
  - E 는 간선의 수 
- 각각의 정점에 대해서 사이클이 있는지 없는지를 검사한다는 의미는 있지만, 시간이 많이 걸리게 됩니다. 

# 유향 그래프 - 그래프에 대해서 판별

- https://hongl.tistory.com/60?category=922907

- 하지만 위의 경우, 복잡도가 너무 크기떄문에 (O(V+E)) 로 판별하는법이 필요합니다.
- 아래의 경우는, 복잡도가 O(V+E) 만에 체크하는 방법입니다.

```python
from collections import defaultdict
N = 7
edges = [(1, 2), (2, 3), (3, 4), (4, 2), (5, 6), (6, 7)]
graph = defaultdict(list)
for edge in edges:
    v, w = edge
    graph[v].append(w)
visited = [0] * (N + 1)

def dfs(here) :
    if visited[here] == -1 : # 어 이미 방문했어?
        return True
    if visited[here] == 1 :
        return False
    visited[here] = -1
    for node in graph[here] :
        if dfs(node) :
            return True
    visited[here] = 1
    return False
dfs(6)
```

