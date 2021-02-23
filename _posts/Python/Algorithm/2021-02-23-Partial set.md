---
title:  "부분집합 구하기(DFS)"
excerpt: "Algorithm"
categories:
  - Py_Algorithm
tags:
  - 3
last_modified_at: 2021-02-23

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

- 문제 및 답 출처 : [링크](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/dashboard)

- 해당 링크에 가시면 훨씬 더 전문적인 해설 및 / 강의를 보실 수 있습니다. 

# 문제

**문제**  

자연수 N 이 주어지면 1부터 N 까지의 원소를 갖는 집합의 부분집합을 모두 출력하는 프로그램을 작성하라.

**입력설명**

첫 줄에 자연수 N이 주어진다. 

**출력 설명**

- 첫 번째 줄부터 각 줄에 하나씩 부분집합을 아래와 출력 예제와 같은 순서로 출력한다. 단 공집합은 출력하지 않습니다.

**입력 예제**

3

**출력예제**

1 2 3

1 2 

1 3

1

2 3

2

3

# 내 답

- 재귀에 대한 이해가 많지 않아 답을 한번 본 후에 비슷하게 구현해 보았다.
- 그래서 답이랑 비슷하다.. 나중에 한번 더 풀어볼것!

```python
import sys
sys.stdin=open("in1.txt", "r")

# 중단부
# 재귀부
# 적용부
# 출력부
N = int(input())
# x 는 기준으로 길이를 잡을것이다. 즉 중단부는
ch = [0]*N
def DFS(x) :
    if x >= N :
        for i in range(N) :
            if ch[i] == 1:
                print(i+1 , end = ' ')
        print()
    else :
        ch[x] = 1 # 포함 경우의 수
        DFS(x+1)
        ch[x] = 0 # 미포함 경우의수
        DFS(x+1)
DFS(0)
```



# 해답

```python
import sys
sys.stdin=open("input.txt", "r")
def DFS(v):
    if v==n+1: # 중단부
        for i in range(1, n+1): # 츨력부
            if ch[i]==1: 
                print(i, end=' ')
        print()
    else: 
        ch[v]=1 # 적용부
        DFS(v+1) # 재귀부
        ch[v]=0
        DFS(v+1)

if __name__=="__main__":
    n=int(input())
    # 집합의 틀이 되는 list = ch
    ch=[0]*(n+1)
    DFS(1)
   
```

- DFS 의 구현은 크게 중단부 /적용부 / 출력부 / 재귀부 이다.
  - 중단부 : 어떤 조건에 의해 중단되는 구간. 즉 내가 어느정도까지 탐색하고 싶느냐를 나타낸다.
  - 적용부 : 깊어지면서 어떠한 처리를 하고싶을것이다. 이 문제의 경우 ch[v] = 1 이였다. 그러한 부분을 적용부라 하겠다.
  - 출력부 : 모든 함수를 재귀부를 통해서 적용시킨 뒤에, 중단부에 의해 중단된 이후 답을 출력하는 부분이다. 
  - 재귀부 : 점점 깊어지는 구간이다. 적용부와 한 몸으로 움직인다.

