---
title:  "조합"
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

1부터 N 까지 번호가 적힌 구슬이 있습니다. 이 중 M 개를 뽑는 방법의 수를 출력하는 프로그램을 작성하세요

**입력설명**

- 첫번째 줄에 자연수 N 과 M 이 주어집니다.

**출력 설명**

- 첫 번째 줄에 결과를 출력합니다. 맨 마지막 총 경우의 수를 출력합니다.
- 출력 순서는 사전순으로 오름차순으로 출력합니다.

**입력 예제**

4 2

**출력예제**

1 2

1 3

1 4

2 3

2 4

3 4

6

# 내 해답

```python
import sys
sys.stdin = open('in1.txt','r')

N,M = map(int,input().split())
# N : 번호가 적힌 구슬의 수
# M : M 개를 뽑는 방법의 수

li = [0] * (N+1)
check = []
cnt = 0

def DFS(l,ans):
    global cnt
    if l >= M : # 당연히 M+1 개 이상 뽑으면 안되니까 M 이상이면 중지
        if set(ans) not in check:
            for i in ans :
                print(i, end = ' ')
            check.append(set(ans))
            print()
            cnt += 1
    else :
        for i in range(1,N+1): # 1 ~ N 의 값 중에서!
            if li[i] == 0: # 즉 비어있다는 소리!
                li[i] = 1
                ans.append(i)
                DFS(l+1,ans)
                li[i] = 0
                ans.pop()
DFS(0,[])
print(cnt)
```

- set 과 not in 을 활용하여, 겹치지 않도록 하였다.

# 다른 답

```python
import sys
sys.stdin=open("input.txt", "r")
def DFS(L, s):
    global cnt
    if L==m:
        for i in range(m):
            print(res[i], end=' ')
        print()
        cnt+=1
    else:
        for i in range(s, n+1):
            res[L]=i
            # 깊이가 늘고. 시작점이 늘어남!
            DFS(L+1, i+1)

n, m=map(int, input().split())
res=[0]*(n+1)
cnt=0
DFS(0, 1)
print(cnt)
```

