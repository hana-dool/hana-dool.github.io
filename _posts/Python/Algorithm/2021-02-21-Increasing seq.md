---
title:  "증가수열 만들기(Greedy)"
excerpt: "Algorithm"
categories:
  - Py_Algorithm
tags:
  - 3
last_modified_at: 2021-02-22

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

1~N 까지의 모든 자연수로 구성된 길이 N 의 수열이 주어진다. 

이 수열의 왼쪽 맨 끝 숫자 또는 오른쪽 맨 끝 숫자 중 하나를 가져와 나열하여 가장 긴 증가수열을 만든다. 이 때에 수열에서 가져온 숫자(왼쪽 맨 끝 또는 오른쪽 맨 끝)은 그 수열에서 제거된다.

예를 들어 2 4 5 1 3 이 주어지면 만들 수 있는 가장 긴 증가수열의 길이는 4이다. 

맨 처음 왼쪽 끝에서 2를 가져오고, 그 다음 오른쪽 끝에서 3을 가져오고, 왼쪽 끝에서 4, 왼쪽 끝에서 5 를 가져와 2345 를 만들 수 있다.

**입력설명**

- 첫째 줄에 자연수 N 이 주어진다.
- 두번째 줄에 N 개로 구성된 수열이 주어진다.

**출력 설명**

- 첫째 줄에 최대 증가수열의 길이를 출력한다.
- 두번째 줄에 가져간 순서대로 왼쪽 끝에서 가져갔으면 L, 오른쪽 끝에서 가져갔으면 R 을 써간 문자열을 출력한다. ( 단 마지막에 남은 값은 왼쪽 끝으로 생각한다.)

**입력 예제**

5

2 4 5 1 3

**출력예제**

4

LRLL

# 내 해답

```python
import sys
sys.stdin=open("in4.txt", "r")

N = int(input())
lis = list(map(int,input().split()))

from collections import deque
dq = deque(lis)

# [2 4 5 1] 의 경우를 생각해보자.
# 뽑아낼 때에는 제일 '끝' 부분의 값을 뽑아내야 한다.

LR_str = ''
val = [0]

while True :
    if (val[-1] > dq[0]) & (val[-1] > dq[-1])  :
        break
    # 위 if 를 통해서 맨 마지막 값보다 높은값이 있음을 알았다.
    # 즉 이를 참고한다면 맨 왼쪽 / 맨 오른쪽 값중 작은값을 추가하면 될 것이다.
    if  (dq[0] < dq[-1]) :
        if val[-1] < dq[0] :
            LR_str += 'L'
            val.append(dq.popleft())
        else :
            LR_str += 'R'
            val.append(dq.pop())
    else :
        if val[-1] < dq[-1] :
            LR_str += 'R'
            val.append(dq.pop())
        else :
            LR_str += 'L'
            val.append(dq.popleft())
print(len(val)-1)
print(LR_str)
```



# 다른 답

```python
import sys
sys.stdin=open("input.txt", "r")
n=int(input())
a=list(map(int, input().split()))
lt=0
rt=n-1
last=0
res=""
tmp=[]
while lt<=rt:
    if a[lt]>last:
        tmp.append((a[lt], 'L'))
    if a[rt]>last:
        tmp.append((a[rt], 'R'))
    tmp.sort()
    if len(tmp)==0:
        break;
    else:
        res=res+tmp[0][1]
        last=tmp[0][0]
        if tmp[0][1]=='L':
            lt=lt+1
        else:
            rt=rt-1
    tmp.clear()

print(len(res))
print(res)
```

- 나랑 어느정도 비슷한듯. 크게 아이디어가 들어가지는 않았다.
- tuple 로 list 에 append 함으로서, 다중 정보가 들어간 element 를 특정 기준으로 정렬할 수 있었다.

- 같은 element 에 대해서 많은 정보가 겹쳐있을 때에는 위처럼 append 를 tuple 로 하는것이 좋다!