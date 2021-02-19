---
title:  "격자판 최대합"
excerpt: "Algorithm"
categories:
  - Py_Algorithm
tags:
  - 3
last_modified_at: 2021-02-19

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

​	![png](/assets/images/{Algorithm}/2_1.JPG)

**입력설명**

- 첫 줄에 자연수 N 이 주어진다.
- 두번째 줄부터 N 줄에 걸쳐 각 줄에 N 개의 자연수가 주어진다. 각 자연수는 100을 넘지 않는다.

**출력 설명**

- 최대합을 출력한다.

**입력 예제**

5

10 13 10 12 15

12 39 30 23 11

11 25 50 53 15

19 27 29 37 27 

19 13 30 13 19

**출력예제**

155

**설명**



# 내 해답

```python
import sys
sys.stdin=open("in5.txt", "r")


N = int(input())
lis = []
for row in range(N):
    lis.append(list(map(int,input().split())))

lis_ans=[]
for i in range(N): # rowsum
    lis_ans.append(sum(lis[i]))


for i in range(N): # colsum
    val = 0
    for j in range(N):
        val += lis[j][i]
    lis_ans.append(val)

val = 0
for i in range(N): # diagonal sum
    val += lis[i][i]
    lis_ans.append(val)

val = 0
for i in range(N): # diagonal sum
    val += lis[i][N-i-1]
    lis_ans.append(val)

print(max(lis_ans))
```

- 2차원으로 구성하기 위해, list 를 2차원으로 사용하는 ide 말고는 어려운게 없었다.



# 다른 답

```python
import sys
sys.stdin = open("input.txt", 'r')
n=int(input())
a=[list(map(int, input().split())) for _ in range(n)]
largest=-2147000000
for i in range(n):
    sum1=sum2=0
    for j in range(n):
        sum1+=a[i][j]
        sum2+=a[j][i]
    if sum1>largest:
        largest=sum1
    if sum2>largest:
        largest=sum2
sum1=sum2=0
for i in range(n):
    sum1+=a[i][i]
    sum2+=a[i][n-i-1]
if sum1>largest:
    largest=sum1
if sum2>largest:
    largest=sum2
print(largest)
```

- 나는 append 한다음에 마지막에 max 를 넣는데, 여기에서는 계속 도중에 업데이트를 한다. 
- list comprehension 을 통해서 나보다 훨씬 matrix 를 효율적으로 생성하였다.

