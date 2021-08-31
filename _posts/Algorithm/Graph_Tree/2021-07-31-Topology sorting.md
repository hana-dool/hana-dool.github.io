---
title:  "위상 정렬 알고리즘"
excerpt: "위상정렬"
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

# 위상 정렬 알고리즘

![png](/assets/images/Python/20_1.png)

- 사이클이 없는 방향그래프에서, 모든 노드를 방향성에 거스르지 않게 배열하는 것입니다.

![png](/assets/images/Python/20_2.png)

![png](/assets/images/Python/20_3.png)

<br>

# 위상 정렬 예시

![png](/assets/images/Python/20_4.png)

![png](/assets/images/Python/20_5.png)

![png](/assets/images/Python/20_6.png)

- 위에서 , 2개의 노드가 큐에 들어갈 수 있습니다.
- 이때에 사실 어떤 순서로 들어가도 상관은 없습니다만, 여기에서는 작은 노드를 우선하겠습니다.

![png](/assets/images/Python/20_7.png)

![png](/assets/images/Python/20_8.png)

![png](/assets/images/Python/20_9.png)

![png](/assets/images/Python/20_10.png)

![png](/assets/images/Python/20_11.png)

![png](/assets/images/Python/20_12.png)

![png](/assets/images/Python/20_13.png)

![png](/assets/images/Python/20_14.png)

<br>

# 코드 구현

```python
from collections import deque
# 노드의 갯수와 간선 갯수 입력
v,e = map(int,input().split())

# 모든 노드에 대해 진입 차수는 0으로 초기화하기
indegree = [0] * (v+1)
graph = [[] for _ in range(v+1)]

# 방향 그래프의 모든 간선 정보 입력받기
for _ in range(e) :
    a,b = map(int,input().split())
    graph[a].append(b) # A  에서 B 로 이동 가능함을 나타냄
    indegree[b] += 1 # 진입차수 1 증가

# 위상 정렬 함수
def topology_sort():
    result = []
    q = deque()

    # 처음 시작할떄에는 진입 차수가 0인 노드를 큐에 삽입해야한다.
    for i in range(1,v+1):
        if indegree[i] == 0 :
            q.append(i)

    # 큐가 빌떄까지 반복
    while q :
        now = q.popleft()
        result.append(now)
        # 해당 원소와 연결된 노드들의 진입차수에서 1 뺴기기
        for i in graph[now] :
            indegree[i] -= 1
            # 새롭게 진입 차수가 0 이 되는 노드를 큐에 삽입
            if indegree[i] == 0 :
                q.append(i)
    # 결과 출력
    for i in result :
        print(i, end = ' ')

topology_sort()
```

<br>

# 실전

- <https://www.acmicpc.net/problem/1766>
- 아래의 경우는 heap 과 같이쓰인 특수한 경우입니다!

```python
import heapq
import sys
input = sys.stdin.readline

N,M = map(int,input().split())
graph = [[] for _ in range(N+1)]
indegree = [0]*(N+1) # N 은 문제의 수

for _ in range(M) :
    start , end = map(int,input().split())
    graph[start].append(end)
    indegree[end] += 1

q = []
rst = []
for i in range(1,N+1) :
    if indegree[i] == 0 :
        heapq.heappush(q,i)

while q :
    now = heapq.heappop(q)
    rst.append(now)
    for i in graph[now] :
        indegree[i] -= 1
        if indegree[i] == 0 :
            heapq.heappush(q,i)

print(*rst)
```

# 선수 과목

- https://www.acmicpc.net/problem/14567

```python
import sys
from collections import deque

input = sys.stdin.readline
N, M = map(int, input().split())
graph = [[] for _ in range(N+1)]
indegree = [0]*(N+1)
for _ in range(M):
    A, B = map(int, input().split())
    graph[A].append(B)
    indegree[B] += 1

ans = [0]*(N+1)

def topology() :
    q = deque()
    for idx in range(1,N+1) :
        if indegree[idx] == 0 :
            q.append((idx,1))
    while q :
        now ,cnt = q.popleft()
        ans[now] = cnt
        for end in graph[now] :
            indegree[end] -= 1
            if indegree[end] == 0 :
                q.append((end,cnt+1))
topology()
print(*ans[1:])
```



