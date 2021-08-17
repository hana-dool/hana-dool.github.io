---
title:  "Floyd Warshall 알고리즘"
excerpt: "플로이드 와셜 알고리즘"
categories:
  - AL_Graph_Tree
tags:
  - 1
last_modified_at: 2021-07-31

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 플로이드 워셜 알고리즘

- 다익스트라 알고리즘은 한 지점에서 다른 특정 지점까지의 최단 경로를 구해야 하는 경우에 사용되는 알고리즘이다.
- 그에 반해서 플로이드 워셜을 모든 지점에서 다른 모든 지점까지의 최단 경로를 모두 구해야 하는 경우에 사용됩니다.

> $D_{a,b}$  = $min(D_{ab}, D_{akb})$ 를 이용해 업데이트 하는 방식

![png](/assets/images/Python/10_1.png)

![png](/assets/images/Python/10_2.png)

![png](/assets/images/Python/10_3.png)

![png](/assets/images/Python/10_4.png)

- 위와 같이, 각 노드마다 계속 업데이트를 한 뒤에 마지막 매트릭스를 출력하면 됩니다.
- 시간복잡도는 $O(N^3)$ 입니다. 

<br>

```python
import sys
input = sys.stdin.readline

inf = 10**9
n = int(input())
m = int(input())

# 거리를 담을 그래프 만들기
graph = [[inf]*(n+1) for _ in range(n+1)]
for i in range(n+1):
    for j in range(n+1):
        if i == j :
            graph[i][j] = 0

# 그래프에다가 거리 정보 넣기
for _ in range(m):
    a,b,c = map(int,input().split())
    graph[a][b] =  c

# 점화식 업데이트 (여기가 중심인데 정말 짧다.)
for k in range(1,n+1):
    for i in range(1,n+1):
        for j in range(1,n+1):
            graph[i][j] = min(graph[i][j], graph[i][k]+graph[k][j])

# 출력 부분 
for i in range(1,n+1):
    for j in range(1,n+1):
        if graph[i][j] == inf :
            print('0',end = ' ')
        else :
            print(graph[i][j], end = ' ')
    print()
```

<br>

## 실전 사용

- <https://www.acmicpc.net/problem/11404>

```python
#
import sys 
input = sys.stdin.readline
n = int(input())
m = int(input())
inf = 10**9

graph = [[inf] * (n+1) for _ in range(n+1)]

for i in range(n+1) :
    graph[i][i] = 0
 
for _ in range(m):
    start,end,cost = map(int,input().split())
    if graph[start][end] > cost :
        graph[start][end] = cost

for k in range(1,n+1) :
    for i in range(1,n+1):
        for j in range(1,n+1) :
            graph[i][j] = min(graph[i][j], graph[i][k] + graph[k][j])

for i in range(1,n+1) :
    for j in graph[i][1:] :
        if j == inf :
            print(0, end = ' ')
        else :
            print(j, end = ' ')
    print()
```

<br>

# 순환을 포함하는 문제

```python
import sys 
input = sys.stdin.readline 

V,E = map(int,input().split())
inf = 10** 9
mat = [[inf] * (V+1) for _ in range(V+1)]

for _ in range(E) :
    start, end , length = map(int,input().split())
    mat[start][end] = length

for mid in range(1,V+1) :
    for i in range(1, V+1) :
        for j in range(1,V+1) :
            mat[i][j] = min(mat[i][j],mat[i][mid] + mat[mid][j])

mn = 10**9
for i in range(1,V+1) :
    mn = min(mn,mat[i][i])
if mn == 10**9 :
    print(-1)
else :
    print(mn)
```

- 위와 같이 mat(i)(i) 를 0으로 초기화하는 부분을 없앤다면, 순환하는 Cycle 까지 고려하게 됩니다.

