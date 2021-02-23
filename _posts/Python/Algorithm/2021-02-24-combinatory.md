---
title:  "중복순열"
excerpt: "Algorithm"
categories:
  - Py_Algorithm
tags:
  - 3
last_modified_at: 2021-02-24

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

1부터 N까지의 번호가 적힌 구슬이 있다. 이 중 중복을 허락하여 M번을 뽑아 일렬로 나열하는 방법을 모두 출력하라

**입력설명**

- 첫 번째 줄에 자연수 N 과 M 이 주어진다. 

**출력 설명**

- 첫 번째 줄에 결과를 출력한다.

- 맨 마지막 총 경우의 수를 출력한다.

- 출력 순서는 사전순으로 오름차순으로 출력 

**입력 예제**

3 2

**출력예제**

1 1

1 2

1 3

2 1

2 2

2 3

3 1

3 2

3 3

9

# 내 해답

```python
import sys
sys.stdin = open('in5.txt','r')

N,M = map(int,input().split())
lis = [0]*M
cnt = 0
def DFS(l):
    global cnt
    if l == M : # 0 부터 시작하니까요!
        for i in lis:
            print(i,end=' ')
        cnt += 1
        print()
    else :
        for i in range(N):
            lis[l] = i+1
            DFS(l+1)
DFS(0)
print(cnt)
```

- list 는 처음 만들때 append 할 생각 없고, index 로 업데이트 하려면 꼭 [0]*M 형식으로 만들어야함을 기억하자! 

# 다른 답

```python
import sys
sys.stdin=open("input.txt", "r")
def DFS(L):
    global cnt
    if L==m:
        for i in range(m):
            print(res[i], end=' ')
        print()
        cnt+=1
    else:
        for i in range(1, n+1):
            res[L]=i
            DFS(L+1)

if __name__=="__main__":
    n, m=map(int, input().split())
    res=[0]*n
    cnt=0
    DFS(0)
    print(cnt)
```

- 나랑 거의 비슷하다.
- 리뷰할게 없음