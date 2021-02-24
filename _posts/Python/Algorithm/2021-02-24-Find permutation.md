---
title:  "순열 구하기"
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

1 부터 N 까지 번호가 적힌 구슬이 있습니다. 이 중 M 개를 뽑아 일렬로 나열하는 방법을 모두 출력하라

**입력설명**

- 첫줄에 자연수 N 과 M 이 주어진다.

**출력 설명**

- 첫 번째 줄에 결과를 출력한다. 맨 마지막 총 경우의 수를 출력한다.
- 출력 순서는 사전순으로 오름차순으로 출력

**입력 예제**

3 2

**출력예제**

1 2

1 3

2 1

2 3

3 1

3 2

6

# 내 해답

```python
import sys
sys.stdin = open('in2.txt','r')

n,m = map(int,input().split())

# m = 뽑아야 하는 카드의 수
# n = 카드의 종류
lis = [i+1 for i in range(n)]
# M 개를 뽑아서 일렬로 나열!

ans = []
cnt = 0
def DFS(l) :
    global cnt
    if l >= m : # 조건부
        for i in ans :
            print(i, end = ' ')
        print()
        cnt += 1
    else :
        for val in lis :
            if val not in ans : # 없어야한다(중복금지)
                ans.append(val)
                DFS(l+1) # 재귀부
                ans.pop() # 복구부
DFS(0)
print(cnt)
```

- 이 부분에서 다른점은 DFS 이후에 '복구하는 부분' 이 있다는 것이다.
- 왜냐하면, DFS 에서, 각 함수들은 global 변수들에 대해서 수정하기 때문에, 그에 따라서 그대로 두게 된다면 뒤죽박죽이 되기 떄문! 그래서 dfs 뒤에 내가 global 변수에게 행했던 수정을 되돌리는 연산을 추가한다면 좀 더 컨트롤 하기가 쉽다.

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
            if ch[i]==0:
                ch[i]=1
                res[L]=i
                DFS(L+1)
                ch[i]=0 # 이 부분을 통해 원상복구

if __name__=="__main__":
    n, m=map(int, input().split())
    res=[0]*n
    ch=[0]*(n+1)
    cnt=0
    DFS(0)
    print(cnt)
```

- DFS 다음 부분이 눈에 띈다. 
- 다시 돌아올 때, ch[i] = 0 을 통해서 원상복구 시키는 부분이 있다.