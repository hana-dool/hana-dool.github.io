---
title:  "송아지 찾기(BFS)"
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

현수는 송아지를 잃어버렸다. 다행이 송아지에는 위치추적기가 달려있다. 현수의 위치와 송아지의 위치가 직선상의 좌표점으로 주어지면 현수는 현재 위치에서 송아지의 위치까지 다음과 같은 방법으로 이동한다.

현수는 스카이 콩콩을 타고 가는데, 한 번의 점프로 앞으로1/ 뒤로1/ 앞으로5 를 이동할 수 있다. 최소 몇 번의 점프로 현수가 송아지의 위치까지 갈 수 있는지 구하는프로그램을 작성하세요.

**입력설명**

- 첫 번째 줄에 현수의 위치 S 와 송아지의 위치 E 가 주어진다. 
- 직선의 좌표 점은 1 부터 10000까지이다.

**출력 설명**

- 점프의 최소횟수를 구한다.

**입력 예제**

5 14

**출력예제**

3

# 내 해답

- 일단 BFS 에 익숙해 지기 위해 다른 답을 참고하고 풀었다 
- 나중에 다시 도전해바야겠다.

```python
import sys
sys.stdin = open('in3.txt','r')

N,M = map(int,input().split())
from collections import deque

num = [0]*10001 # 이 num 에다가 계속 집어넣을거임
num[N] = 0
dq = deque()
dq.append(N)
while dq :
    val = dq.popleft()
    if val == M :
        print(num[val])
    for next in (val-1,val+1,val+5):
        if next < 10001 :
            if num[next] == 0 :
                num[next] = num[val] +1
                dq.append(next) # 그 다음이 되는 값을 append
# 이렇게 하면 dq 에 계속 쌓이게 된다.
# 계~속 쌓여서 적체를 해결하지 못한다고 생각할 수 있다,
# 하지만 계~속 쌓이는건 아니다. if 조건에 맞아야 쌓이므로, 어느순간부터는 popleft 에서 적체가 풀리는게 더 빨라짐.

```



# 다른 답

```python
import sys
from collections import deque
sys.stdin = open('input.txt','r')
# 좌표의 maximum 이 만 이므로
MAX = 10000
ch = [0] * (MAX+1) # 0번부터 생기니까 MAX + 1
dis = [0] * (MAX+1)
# 목적은 n 에서 출발 -> m 에 도착
n,m = map(int,input().split())
ch[n] = 1 # 처음에 n에서 출발
dis[n] = 0 # 그 지점은 첫 단계부터 가능하므로 0
dq = deque()
dq.append(n)
while dq : # dq 가 비어있으면 멈춘다.
    now = dq.popleft() # q에서 하나 꺼낸다.
    if now == m :
        break
    for next in (now-1,now+1,now+5) : # next 가 다음 값으로 이동
        if 0 < next <= MAX :
            if ch[next] == 0 : # 방문 안했을때에만 넣는다.
                dq.append(next)
                ch[next] = 1
                dis[next] = dis[now]+1
```

- While 문과 deque / for문을 통해서 BFS 를 구현할 수 있다.
- 먼저 Whilw 문을 넣어 계속 탐색하려는 의지를 보여준다. 
- 그 이후 위 식과 같이 for 문을 통해서 now-1/now+1/now+5 로 깊어진다.
- dis[next] 를 for 문이 돌아가면서 update 한다.

- append 를 통해서, 시로 업데이트 