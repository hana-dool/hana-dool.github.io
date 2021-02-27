---
title:  "사과나무"
excerpt: "Algorithm"
categories:
  - Py_Algorithm
tags:
  - 3
last_modified_at: 2021-02-25

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

![png](/assets/images/{Algorithm}/31_1.JPG)

**입력설명**

- 첫째 줄에 자연수 N(홀수) 가 주어진다.
- 둘째 줄부터 N 줄에 걸쳐 각 줄에 N개의 자연수가 주어진다.
- 이 자연수는 각 격자안에 있는 사과나무에 열린 사과의 갯수이다.
- 각 격자안 사과의 갯수는 100을 넘지 않는다.

**출력 설명**

- 수확한 사과의 총 갯수를 출력

**예제**

![png](/assets/images/{Algorithm}/31_2.JPG)

# 내 해답

- BFS 로 풀수 있는지는 감이 안잡혀서 그냥 FOR문으로 풀었다.

```python
import sys
from collections import deque
sys.stdin = open('in2.txt','r')

N = int(input())
mat = []
for row in range(N) :
    val = list(map(int, input().split()))
    val.append(0) # 0을 맨 오른쪽에 더 넣는다. (index 문제떄문에)
    mat.append(val)
# 위 변환을 통해서 N*N 의 매트릭스가 생긴다.
mid = int((N-1)/2)
sm = 0
i = -1
for v in range(N):
    if v <= mid:
        i += 1
        sm += sum(mat[v][ mid-i:mid+i+1 ])
    else :
        i -= 1
        sm += sum(mat[v][mid-i : mid+i+1])
print(sm)
```



# 다른 답

```python
import sys
from collections import deque
sys.stdin=open("input.txt", "r")

# 방향을 정의하기 위한 좌표를 생성한다.
dx=[-1, 0, 1, 0]
dy=[0, 1, 0, -1]
n=int(input())
# a 는 매트릭스임
a=[list(map(int, input().split())) for _ in range(n)]
# 사용한값을 담는 같은 매트릭스 형성(check)
ch=[[0]*n for _ in range(n)]
sum=0
Q=deque()
#첫 시작지 이므로, 무조건 check 는 1 
ch[n//2][n//2]=1 
sum+=a[n//2][n//2]
Q.append((n//2, n//2)) # Q 에 좌표를 넣는다.
L=0
while True:
    if L==n//2: # 사이즈는 n//2 까지여야한다.
        break
    size=len(Q) # 
    for i in range(size): # size 만큼 for문이 돈다.
        tmp=Q.popleft() # 하나를 꺼내면
        for j in range(4): # 뭄조건 4가닥이 퍼진다. 
            x=tmp[0]+dx[j]
            y=tmp[1]+dy[j]
            if ch[x][y]==0: # 체크하고
                sum+=a[x][y] # sum 에 누적하고
                ch[x][y]=1 # ch에 표시하고
                Q.append((x, y)) # q 에 append
    L+=1 # level 증가
print(sum)
```

- 격자의 중심에서 출발한다.(여기에서 상태트리가 커진다.)

- (2,2) 가 상하좌우로 커지면서 상태트리를 업데이트한다.

  

