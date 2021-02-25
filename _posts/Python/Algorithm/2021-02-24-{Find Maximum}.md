---
title:  "최대 점수 구하기"
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

이번 정보올림피아드 대회에서 좋은 성적을 내기 위해서 현수는 선생님이 주신 N 개의 문제를 풀려고 한다. 각 문제는 그것을 풀었을 떄 얻는 점수와 푸는데 걸리는 시간이 주어지게 됩니다. 제한시간 M 안에 N 개의 문제 중 최대점수를 얻을 수 있도록 해야합니다. (해당 문제는 해당 시간이 걸리면 푸는것으로 간주합니다. 한 유형당 한개만 풀 수 있습니다.)

**입력설명**

- 첫 번째 줄에 문제의 개수 N 과 제한시간 M 이 주어집니다.

**출력 설명**

- 첫 번째 줄에 제한 시간안에 얻을 수 있는 최대 점수를 출력합니다.

**입력 예제**

5 20

10 5

25 12

15 8

6 3

7 4

**출력예제**

41

# 내 해답

```python
import sys
sys.stdin = open('in3.txt','r')

N,M = map(int,input().split())
lis = []
for _ in range(N) :
    val = list(map(int,input().split()))
    lis.append(val)


# 그냥 for 문으로는 구현이 어려울거같고.. 역시나 DFS!
dup = [0] * N
max = 0
def DFS(T,sum,s) :
    global max
    if max < sum :
        max = sum
    for i in range(s+1,N): # i 값을 주우욱 훑으면서!
        # 중복을 없애기 위해서!
        if (M>=T+lis[i][1]) :
            DFS(T+lis[i][1],sum + lis[i][0],i)
DFS(0,0,-1)
print(max)
```

- 조합이기 때문에, start index 인 s 를 넣어서 구하기로 하였다

- 그리고 DFS(0,0,-1) 을 넣은 이유는, range(s+1,N) 으로 하기로 해서 첫 DFS(0,0,0) 을 넣게 되면 처음값 (인덱스가 0 이므로) 은 무시하게되기 때문

  

# 다른 답

```python
import sys
sys.stdin=open("input.txt", "r")
def DFS(L, sum, time): 
    global res
    if time>m: # 시간이 m 넘으면 말짝 도루묵
        return
    if L==n: # n 과 같은 길이가 되면 
        if sum>res: # 만약 res 보다 크면
            res=sum # 최대값
    else:
        # pv 는 점수고/ pt는 시간이고
        DFS(L+1, sum+pv[L], time+pt[L])
        DFS(L+1, sum, time)

if __name__=="__main__":
    n, m=map(int, input().split())
    pv=list()
    pt=list()
    for i in range(n):
        a, b=map(int, input().split())
        pv.append(a)
        pt.append(b)
    res=-2147000000
    DFS(0, 0, 0)
    print(res)

```

- 너무 '조합' 이라는 사실에 얽매여서 했던거같다.
- DFS 로 넣고/ 안넣고 를 그냥 위처럼 스~~윽 실행시켜주면 되는것이다! 

if ....return 

if .... print

else  DFS DFS .....

의 구문이다. DFS 가 깊어짐에 따라서 점점 분기하고, 그에 따라서 if 가 촉!촉! 조건에 맞는녀석을 추리는것! 