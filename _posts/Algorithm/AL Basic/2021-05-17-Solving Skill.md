---
title:  "7.Solving Stratige"
excerpt: "모든 방법"
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

# 1. 기초

## 완전 탐색(Brute-force Search)

- 기본적으로 '모든 경우의 수를' 구현합니다.

```python
# lst 의 모든 구간을 탐색 , 길이를 N 이라 하자.
for start in range(N) : 
    for end in range(start+1,N+1) :
        lst[start:end]
```



```python
# lst 의 모든 값들을 탐색, 
for start in range(N) : 
    for end in range(start+1,N) : 
        lst[start], lst[end]
```

## 탐욕적 기법(Greedy)

- Greedy 는 제일 많이 사용되는 방법으로, 최적의 선택만 하는 방법을 이야기합니다.
  - 하지만 그리디 알고리즘은 모든 문제에 적용가능한것은 아닙니다.
  - 왜냐하면 Local minimal 이 Global 한 답이 되지는 않기 때문닙니다.

## 이분 탐색 (Binary Search)

- 탐색 시간이 $Log(N)$ 이기 떄문에 탐색의 길이가 엄청나게 길때에 사용합니다. 
- 길이가 0<= x <= 10**9 가 되는 경우, 일반적인 Search 로 진행시에는 무조건 시간에 걸리게 됩니다.
- 크게 몇가지 유형으로 나뉠 수 있습니다.

> 단순한 값 찾기 

- 단순히 값을 찾는 유형입니다. 

```python
N개의 정수 A[1], A[2], …, A[N]이 주어져 있을 때, 이 안에 X라는 정수가 존재하는지 알아내는 프로그램을 작성하시오.
```

- 위와 같이, 단순히 어디에 위치하는지만 찾으면 되므로 매우 쉽게 구현 가능합니다.

> 함수와 연계 

- 문제를 함수로 만든뒤, 값을 연계해서 값을 찾는 방법입니다. 
  - https://www.acmicpc.net/problem/2805
- 이때에 중요한것은 F(input) 에 대해서 , 단조증가 / 단조감소 여야 합니다.

> 만족하는 최대 / 최소

```python
설정할수 있는 높이의 최댓값을 구하시오..
만족하는 최소값을 구하시오 ...
```

- 위와 같이 , 
  - '만족하는 값의 최소 / 최대' 값을 요구
  - 주어진 조건을 함수로 만들 수 있음 
  - F(input) 에 대해서 단조증가 / 감소

## 넓이 우선 탐색 (BFS)

- 넓이 우선 탐색은 먼저 '넓게' 탐색합니다. 
  - 이로부터 '최소 거리/가짓수' 와 연관되어서 많이 나온다는것을 알 수 있습니다.

> 최소 Count/경로

```python
정수 A를 B로 바꾸려고 한다. 가능한 연산은 다음과 같은 두 가지이다.
2를 곱한다.
1을 수의 가장 오른쪽에 추가한다. 
A를 B로 바꾸는데 필요한 연산의 최솟값을 구해보자.
- https://www.acmicpc.net/problem/16953
```

```python
체스판 위에 한 나이트가 놓여져 있다. 나이트가 한 번에 이동할 수 있는 칸은 아래 그림에 나와있다. 나이트가 이동하려고 하는 칸이 주어진다. 나이트는 몇 번 움직이면 이 칸으로 이동할 수 있을까?
- https://www.acmicpc.net/problem/7562
```

- 위와 같이 '최소' Count 를 세기 위한 방법으로 BFS 가 이용됩니다. 
- (x,y,cnt) 를 Queue 에 넣으면서 구현하고, 조건에 맞으면 바로 break 하면 됩니다.

> Matrix 에서 연결된 영역의 수

- https://www.acmicpc.net/problem/2667
- https://www.acmicpc.net/problem/2606

- 위와 같이 Matrix 을 순회하면서 연결된 요소를 세는데에 BFS 를 쓸 수 있습니다.
  - dx , dy 를 정의하고 순회하면서 cnt 하는게 포인트입니다.

## 깊이 우선 탐색(DFS)

> Matrix 에서 연결된 영역의 수

- 이 부분은 BFS 와 겹칩니다. 
- '인접한 부분' 만 세면 되므로 BFS ,DFS 모두 가능합니다.

## 정렬 (Sorting)

- 일반적으로 파이썬의 sort 는 $NlogN$ 의 복잡도를 가집니다. 
- 이러한 경우, sorted 함수에 대해서 잘 알아두는것이 중요합니다. 

## 탐색 (Search)

- 탐색의 경우, 시간 복잡도와 관련된 경우가 많습니다. 

```python
x in list # O(N)
x in set # O(1)
x in dict.keys() # O(1)
x in str # O(N)
x in tuple # O(N)
```

- 위와 같은 시간복잡도를 가집니다. 
- 즉 '빠른 Search' 를 원하는 경우 Set / Dict 로 구현하는것이 좋습니다.

- 문자열
- 재귀
  - 프렉탈 구조일떄의 구현

## 수학 ( MAth)



<br>

# 2. 자료구조

## List

## Stack

## Deque

## Tree

## Heap

# 3. 알고리즘

## Union Find

- 부분 집합 알고리즘

## Two Pointer

## Dynamic Programing

- 점화식
  - 모두 쪼개기
- 2차원 DP

## 위상 정렬(Topological Sort)

- 우선순위가 있는 시간표 짜기 

##플로이드 와샬

- 모든 정점에 대해 최소거리 

## 다익스트라

- 특정한 정점에 대해 최소거리

## 크루스칼 

- 모든 정점을 잇는 최단 경로

# 4. 외부 모듈 활용

## itertools

