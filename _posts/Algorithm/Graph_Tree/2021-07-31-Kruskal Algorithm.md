---
title:  "Kruskal 알고리즘"
excerpt: "크루스칼 알고리즘"
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

# 크루스칼 알고리즘

- 크루스칼 알고리즘은 "그래프를 최소 비용으로 모두 연결하고자 할 떄에" 사용되는 알고리즘입니다. 

![png](/assets/images/Python/18_1.png)

![png](/assets/images/Python/18_2.png)

![png](/assets/images/Python/18_3.png)

- https://www.youtube.com/watch?v=aOhhNFTIeFI&list=PLRx0vPvlEmdAghTr5mXQxGpHjWqSz0dgC&index=8

- 위와 같이, 간선의 길이가 작은경우 포함시키되, 사이클이 발생하면 제외하는 방식으로 그리디하게 구하는 방식입니다. 
- 간선의 갯수가 E 개일때에 $O(ElogE)$ 의 시간복잡도를 가집니다. 
  - 크루스칼 알고리즘에서 제일 오래 걸리는 부분은 간선 정렬 부분이고 E 개의 ㄷ이터를 정렬할떄의 시간 복잡도는 O(ElogE) 이기 때문입니다. 

# 구현

```python
def find_parent(parent,x):
    # 루트 노드가 아니라면, 루트 노드를 찾을떄까지 재귀적으로 호출된다.
    if parent[x] != x :
        parent[x] = find_parent(parent,parent[x])
    return parent[x]

# 두 원소가 속한 집합 합치기
# 작은값이면 루트가 된다.
def union_parent(parent,a,b) :
    a = find_parent(parent,a)
    b = find_parent(parent,b)
    if a<b :
        parent[b]=a
    else :
        parent[a]=b

# 노드의 개수와 간선(union 연산) 갯수 입력

v,e = map(int,input().split())
parent = [0] * (v+1)

# 모든 간선을 담을 리스트와 최종 비용 담을 변수
edges = []
result = 0

# 부모 테이블 상에서 부모를 자기 자신으로 초기화
for i in range(1,v+1) :
    parent[i] = i

# 모든 간선정보 입력받기
for _ in range(e) :
    a,b,cost = map(int,input().split())
    # 비용순으로 정렬하기 위해서 튜플의 첫번쨰 원소를 비용으로 결정
    edges.append((cost,a,b))

# 간선을 비용순으로 정렬
edges.sort()

# 간선을 하나씩 확인
for edge in edges :
    cost , a, b = edge
    # 사이클이 발생하지 않는 경우에만 포함
    if find_parent(parent,a) != find_parent(parent,b) :
        union_parent(parent,a,b)
        result += cost
print(result)
```



<br>

## 실전 사용

- <https://www.acmicpc.net/problem/1922>

```python
import sys
input = sys.stdin.readline
N = int(input())
M = int(input())

# 크루스칼 알고리즘
edge = []
for _ in range(M) :
    start,end,cost = map(int,input().split())
    edge.append((cost,start,end))

# 서로소 알고리즘
# 현재 부모는 늘 자식보다 작은 값을 가집니다.
def find_parent(parent,x) :
    if parent[x] != x :
        parent[x] = find_parent(parent,parent[x]) # parent[x] 에 기어이, 부모 노드를 넣음
    return parent[x]

def union_parent(parent,a,b) : # a와 b 를 합치는 연산
    a_p = find_parent(parent,a)
    b_p = find_parent(parent,b)
    if a_p > b_p :
        parent[a_p] = b_p
    else :
        parent[b_p] = a_p  # 다른 경우에는, b_p 의 부모는 a_p 가 됩니다.
parent = list(range(0,N+1))
# 각각의 노드는 , 자기 자신을 우선 부모로 가짐
# 첫번쨰 값인 0 은 사실 , 0임...
rst = 0
# 크루스칼 알고리즘 시작
edge.sort()
for e in edge :
    cost,start, end = e
    if find_parent(parent, start) != find_parent(parent, end) :
        union_parent(parent,start,end)
        rst += cost
print(rst)
```

