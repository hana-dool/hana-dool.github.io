---
title:  "[알고리즘] DFS"
excerpt: "Algorithm"
categories:
  - Py_Basic
tags:
  - 3
last_modified_at: 2021-02-27

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# DFS

- 깊이 우선 탐색이라고 불리며, 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘

- DFS 는  스택/재귀 를 이용한다.

- 동작 순서는 다음과 같다.

  1. 탐색 시작 노드를 스택에 삽입하고 방문 처리를 한다.
  2. 스택의 최상단 노드에 방문하지 않은 인접한 노드가 하나라도 있으면 그 노드를 스택에 넣고 방문처리를 한다. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다.
  3. 더이상 2번 과정을 할 수 없을때까지 반복한다.

- EX) 그래프가 있을때, 1번부터 탐색을 진행한다. 

  ![png](/assets/images/{Py_Basic}/2_1.JPG)

  ![png](/assets/images/{Py_Basic}/2_2.JPG)

  ![png](/assets/images/{Py_Basic}/2_3.JPG)

  ![png](/assets/images/{Py_Basic}/2_4.JPG)

  ![png](/assets/images/{Py_Basic}/2_5.JPG)

  ![png](/assets/images/{Py_Basic}/2_6.JPG)

  ![png](/assets/images/{Py_Basic}/2_7.JPG)

  ![png](/assets/images/{Py_Basic}/2_8.JPG)

# Graph

![png](/assets/images/{Algorithm}/33_1.JPG)

- https://www.acmicpc.net/problem/2606
- 문제를 무작정 DFS 로 풀게 되면 시간초과로 에러가 나게 된다.

1. Graph 의 연결정보를 구현한다.(list 또는 dict)
2. visit 했었음을 나타낼 객체를 구현한다.
3. DFS 를 이용해서 훑어본다.

- 아래와 같이 효율적으로 코드를 사용하는것이 좋다.

```python
# https://www.acmicpc.net/problem/2606

# N : 컴퓨터의 수
# M : 연결되어있는 컴퓨터 쌍의 수
import sys
read = sys.stdin.readline

N = int(read())
M = int(read())
lis = [[] for _ in range(N+1)]

# Visit 을 나타내주기 위한 list
position = [0]*(N+1)

# 연결 정보를 생성하기 위한 리스트
for _ in range(M):
    start , end =map(int,read().split())
    lis[start].append(end)
    lis[end].append(start)
# 그러면 [[],[2,3],[4,2,5] ... ] 의 연결정보가 뜬다.

def DFS(l,cur) :
    global position
    for i in lis[cur] : # i 는 갈 수 있는 위치
        if position[i] == 0  : # 중복되서 가기 싫다는 뜻
           position[i] = 1 # 1로 갔었음을 표시
           DFS(l+1,i)
DFS(0,1)
print(sum(position)-1)
```



# Reference

- https://www.youtube.com/watch?v=PqzyFDUnbrY