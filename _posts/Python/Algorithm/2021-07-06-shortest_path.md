---
title:  "Dijkstra 최단경로"
excerpt: "다익스트라 최단경로문제"
categories:
  - Py_Algorithm
tags:
  - 1
last_modified_at: 2021-07-06

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 다익스트라 알고리즘

- 다익스트라 최단경로 알고리즘은, 그래프에서 여러개의 노드가 있을때, 특정한 노드에서 춟ㄹ해 다른 노드로 가는 각각의 최단 경로를 구해주는 알고리즘이다. 
- 다익스트라 최단 경로 알고리즘은 '음의 간선' 이 없을떄에 정상적으로 작동한다.
  - 실제 세계의 길은, 음의 간선으로 표현되지 않으므로 실제 gps 소프트웨어 기본 알고리즘으로 선택된다. 
- 다익스트라 최단 경로 알고리즘은 기본적으로 그리디 알고리즘이다. 

1. 출발 노드를 설정한다.
2. 최단거리 테이블을 초기화한다.
3. 방문하지 않는 노드중에서 최단거리가 가장 짧은 노드를 선택한다.
4. 해당 노드를 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블을 갱신한다.
5. 위 과정에서 3~4 를 반복한다. 

- 다익스트라 알고리즘은 각 노드에 대한 현재까지의 최단거리 정보를 항상 1차원 리스트에 저장하며 리스트를 갱신한다.
- 다익스트라 알고리즘을 구현하는 방법은 2가지이다. 

> 방법1 : 구현하기 쉽지만 느리게 작동하는 코드
>
> 방법2 : 구현하기 어렵지만 빠르게 작동하는 코드 

- 방법 2를 달달 외울떄까지 숙달하도록 하자. 

<BR>

# 다익스트라 알고리즘 구현

```python
import sys
input = sys.stdin.readline
INF = int(1e9)

# 노드의 갯수, 간선의 갯수를 입력받기
n,m = map(int,input().split())
# 시작 노드 번호를 입력받기
start = int(input())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트를 만들기
graph = [[] for i in range(n+1)]
# 방문한 적이 있는지 체크하는 목적의 리스트를 만들기
visited = [False] * (n+1)
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n+1)

# 모든 간선 입력받기
for _ in range(m):
    a,b,c = map(int,input().split())
    # a 번 노드에서 b 번 노드로 가는 비용이 c 라는 의미
    graph[a].append((b,c))

# 방문하지 않은 노드 중에서, 가장 최단 거리가 짧은 노드의 번호를 반환
def get_smallest_node():
    min_value = INF
    index = 0 # 가장 최단 거리가 짧은 노드(인덱스)
    for i in range(1,n+1):
        if distance[i] < min_value and not visited[i]:
            min_value = distance[i]
            index = i
    return index
# distance 는 [[],[(3,4),(4,3)]] ...] 

def dijkstra(start):
    distance[start] = 0
    visited[start] = True
    for j in graph[start]:
        # distance 를 업데이트
        distance[j[0]] = j[1]
    # 시작 노드를 제외한 전체 n-1 개의 노드에 대해 반복
    for _ in range(n-1):
        # 현재 최단 거리가 가장 짧은 노드를 꺼내서, 방문 처리
        now = get_smallest_node()
        visited[now] = True
        for j in graph[now]:
            cost = distance[now] + j[1]
            # 현재 노드를 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[j[0]]:
                distance[j[0]] = cost
                # 현재 노드를 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우


dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1,n+1):
    # 도달할 수 없는 경우 무한이라고 출력
    if distance[i] == INF :
        print('INF')
    else :
        print(distance[i])
```

- 위 시간 복잡도는 $O(V^2)$ 이다. 왜냐하면 총 $O(V)$ 에 걸쳐서 최단거리가 가장 짧은 노드를 매번 선형탐색해야 하기 떄문이다. 
- 그리고 현재 노드와 연결된 노드를 일일히 확인해야 한다. 

<br>

# 개선된 다익스트라 알고리즘

- 이 방법을 사용한다면, 최악의 경우에도 시간복잡도 $O(Elog V)$ 를 보장한다.  (V : 노드의 갯수, E : 간선의 갯수)
- 간단한 다익스트라 알고리즘은 최단거리가 가장 짧은 노드를 찾기 위해서 매번 최단 거리 테이블을 선형적으로 탐색해야 했다.
- 이러한 과정을 더욱 더 빠르게 찾을 수 있다면, 알고리즘의 시간 복잡도를 획기적으로 줄일 수 있을것이다. 
- 우리는 위와 같이, 더 빠르게 찾기 위하여, 우선순위 큐 를 사용하게 됩니다. 

```python
import sys
import heapq
input = sys.stdin.readline
INF = int(1e9)

# 노드의 갯수, 간선의 갯수를 입력받기
n,m = map(int,input().split())
# 시작 노드 번호를 입력받기
start = int(input())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트를 만들기
graph = [[] for i in range(n+1)]
# 방문한 적이 있는지 체크하는 목적의 리스트를 만들기
visited = [False] * (n+1)
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n+1)

# 모든 간선 입력받기
for _ in range(m):
    a,b,c = map(int,input().split())
    # a 번 노드에서 b 번 노드로 가는 비용이 c 라는 의미
    graph[a].append((b,c))


def dijkstra(start):
    q = []
    # 시작 노드로 가기 위한 최단 경로는 0으로 설정하여 큐에 삽입
    heapq.heappush(q,(0,start))
    distance[start] = 0
    while q : # 큐가 비어있지 앟다면
        # 가장 최단 거리가 짧은 노드에 대한 정보 꺼내기
        dist, now = heapq.heappop(q)
        # 현재 노드가 이미 처리된 적이 있는 노드라면 무시
        if distance[now] < dist :
            continue
        # 현재 노드와 연결된 다른 인접한 노드들을 확인
        for i in graph[now]:
            cost = dist + i[1]
            # 현재 노드를 거쳐 다른 노드로 이동하는 거리가 더 짧은경우
            if cost < distance[i[0]] :
                distance[i[0]] = cost
                heapq.heappush(q,(cost,i[0]))
dijkstra(start)
# 모든 노드로 가기 위한 최단 거리 출력

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1,n+1):
    # 도달할 수 없는 경우 무한이라고 출력
    if distance[i] == INF :
        print('INF')
    else :
        print(distance[i])
```

