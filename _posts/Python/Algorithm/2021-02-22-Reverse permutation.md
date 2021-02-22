---
title:  "역수열(Greedy)"
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

![png](/assets/images/{Algorithm}/11_1.JPG)

**입력설명**

- 첫번째 줄에 자연수 N 이 주어지고, 두번째 줄에는 역수열이 숫자 사이에 한 칸의 공백을 두고 주어진다.

**출력 설명**

- 원래 수열을 출력한다.

**입력 예제**

8

5 3 4 0 2 1 1 0

**출력예제**

4 8 6 2 5 1 3 7

# 내 해답

```python
import sys
sys.stdin=open("in2.txt", "r")

N = int(input())
lis = list(map(int,input().split()))
ans = [0]*N
br = True

# list 의 1 ~ N 값 탐색하기
for i in range(N):
    # list 에서 정한 1~N 값 각각에 대해 맞는 위치 탐색하기
    print(ans)
    br = True
    for j in range(N):
        # for 문을 통해 적절한 위치로 들어간다.
        if ans[:j].count(0) == lis[i] :
            print(lis[i])
            # 가장 가까운 0에다가 값 부여
            for k in range(j,N):
                print(k)
                if ans[k] == 0 :
                    ans[k] = i+1 # list[i] 는 i+1이라는 수의 역수열값이므로!
                    br = False
                    break
        if br == False :
            break
print(ans)
```

- 먼저 작은 수 부터 차례차례 넣기로 하였다.
- [0] * N 을 통해서 N 길이의 0 을 생성
- 그이후 1 은 lis[0] 의 자리, 2 는 앞에 0이 lis[1] 만큼 있는자리 ..... 

```
# 00000000
# 00000100 
# 00020100 
# 00020130 .....
```

- 이 순서대로 넣으려 하였다. 

- 너무 어렵게 풀은 느낌..

# 다른 답

```python
import sys
sys.stdin=open("input.txt", "r")
n=int(input())
a=list(map(int, input().split()))
seq=[0]*n
for i in range(n):
    for j in range(n):
        if(a[i]==0 and seq[j]==0):
            seq[j]=i+1
            break
        elif seq[j]==0:
            a[i]-=1

for x in seq:
    print(x, end=' ')
```

- 우선 [0] 을 N 개의 길이만큼 list 로 생성한다는 아이디어는 같다.
- 그런데 나는 문제의 조건을 곧이 곧대로 풀었고, 이 풀이는 그 조건을 좀 더 알고리즘이 분석하기 쉽게 만들엇다. 그래서 더욱 효과적인건 덤