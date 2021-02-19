---
title:  "평균에 가장 가까운 사람"
excerpt: "Algorithm"
categories:
  - Py_Algorithm
tags:
  - 3
last_modified_at: 2021-02-17

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

- N명의 학생의 수학 점수가 주어진다. N 명의 학생들의 평균(소수 첫째자리 만올림) 을 구하고 , N 명의 학생 중 평균에 가장 가까운 학생은 몇 번째 학생인지 출력하는 프로그램을 작성하라.
- 평균과  가장 가까운 점수가 여러개일 경우, 먼저 점수가 높은 학생의 답을 답으로 하고, 높은 점수를 가진 학생이 여러명일 경우 그 중 학생번호가 빠른 학생의 번호를 답으로 한다.

**입력설명**

- 첫 줄에 자연수 N(5~100) 이 주어진다.
- 두번째 줄에는 각 학생의 수학점수인 N 개의 자연수가 주어진다.
- 학생의 번호는 앞에서부터 1로 시작해 N 까지 이다

**출력 설명**

- 첫 줄에 평균과 평균에 가장 가까운 학생의 번호를 출력한다.
- 평균은 소수 첫째 자리에서 반올림한다.

**입력 예제**

10

45 73 66 87 92 67 75 79 75 80

**출력예제**

74 7

**설명**

현재 평균은 74점으로. 그에 가장 가까운 학생은 73(2번), 75(7번), 75(9번) 이다. 여기에서 점수가 높은 75 점이 우선 선택되고 그 이후 학생번호가 빠른 7번이 답이 된다.



# 내 풀이

1. 우선 input 을 받고, 거기에서 평균을 계산해 낸다.
2. list 에 대해서 mean 을 계산한다.
3. 그리고 계산한 mean 에 대해서 각 val

```python
import timeit
start = timeit.default_timer()

import sys
sys.stdin=open("in1.txt", "r")

n = int(input())
lis = list(map(int, input().split()))
mean = round(sum(lis)/n)

# 평균과 값의 차이에 대해서 '가장 작으면' 그 값이 평균과 제일 가까운것
# 우선 제일 작은 차이를 import 한다.
min = abs(lis[0] - mean)
for val in lis:
    if abs(val-mean) < min :
        min = abs(val-mean)

score = 0
pos_id = []
neg_id = []
pos_val = []
neg_val = []
for idx,value in enumerate(lis):
    dif = abs(value-mean) # 각 value 에 대해서 mean 을 뺴주고 abs
    if dif == min: # 만일 같다면 양수일때 우선시 + 빠른 idx 일떄 우선시 해야한다.
        if value-mean > 0 :
            pos_id.append(idx)
            pos_val.append(value)
        else :
            neg_id.append(idx)
            neg_val.append(value)
print(pos_id)
print(neg_id)
if pos_id:
    rst_id = pos_id[0]
    rst_val = pos_val[0]
else :
    rst_id = neg_id[0]
    rst_val = neg_val[0]

print(rst_val, rst_id+1)

stop = timeit.default_timer()
print(f'실행 시간 : {stop-start}')
```





# 답지

```python
import sys
#sys.stdin=open("input.txt", "r")
n=int(input())
a=list(map(int, input().split()))
ave=round(sum(a)/n)
min=2147000000
for idx, x in enumerate(a):
    tmp=abs(x-ave) # temp 를 통해 평균과의 차이 계산
    if tmp<min: # 만약 min 보다 작다면 
        min=tmp # 새로 업데이트
        score=x # 그 당시의 x(value) 도 업데이트
        res=idx+1 # res 는 idx가 ~번째가 되기에는 1 부족하므로
    elif tmp==min: # 만일 min 과 같다면
        if x>score: # value 가 score 보다 크다면 (value 는 양수, 기존것은 음수)
            score=x 
            res=idx+1 # residual 에 1을 더해준다. (위치)
print(ave, res) # 평균과 그 위치
```

- 내가 우선순위를 1.양수이거나 2.index 가 빠르거나 로 나누어서 일일히 비교하느라 힘들었는데 여기에서는 바로 그 과정을 단축시킴
- 우선 min 보다 작을때에는 min 을 업데이트 시키고 / min 과 같을때에는 양수여야지만 update 를 시킴 

- **즉 1 우선순위가 되는값을 먼저 if 문으로 써서 걔네만 추린 후에, 2 우선순위가 되는 애들은 elif 로 업데이트 해 줌으로서 자연스럽게 순위가 부여되고 있다.**

