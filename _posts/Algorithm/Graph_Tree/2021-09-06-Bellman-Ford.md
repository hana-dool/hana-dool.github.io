---
title:  "벨만 포드 알고리즘"
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

# 개요

![png](/assets/images/Algorithm/15.png)

- 벨만포드 알고리즘은 간선을 최대 1개 사용 / 2개 사용... 의 방식으로 간선을 최대 n-1 개까지 사용하는 최단경로를 구합니다.
  - 1) 최단 거리 테이블 초기화
  - 2) 모든 간선을 한번 돌면서 최단거리 테이블 갱신
  - 3) 2 과정을 1~V-1 반복

![png](/assets/images/Algorithm/13.png)

![png](/assets/images/Algorithm/14.png)

# 구현

```python
import sys
input = sys.stdin.readline
inf = 10**9
n,m = map(int,input().split())
edges = []
dist = [inf]*(n+1)

# 간선정보 입력받기
for _ in range(m) :
    a,b,c = map(int,input().split())
    edges.append((a,b,c))


def bf(start) :
    dist[start] = 0
    for i in range(n) :
        for j in range(m) :
            now,next,cost = edges[j]
            # 현재 간선을 거쳐 다른 노드로 이동하는 거리가 더 짧을때
            if dist[now] != inf and dist[next] > dist[now] + cost :
                dist[next] = dist[now] + cost
                # n 번쨰 라운드에서도 값이 계속 갱신... ? : 음수 순환이 존재한다는것
                if i == n-1 :
                    return True
    # 다행히 음수 순환은 없다는것
    return False

cycle = bf(1)
if cycle :
    print(-1)
else :
    print(dist[1:])
```

