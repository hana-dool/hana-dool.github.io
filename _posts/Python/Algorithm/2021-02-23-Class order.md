---
title:  "교육과정 설계"
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

7![png](/assets/images/{Algorithm}/17_1.JPG)

**입력설명**

- 첫 줄에 한 줄에 필수과목의 순서가 주어진다.
  - 모든 가목은 영문 대문자이다.
- 두 번째 줄에 N 이 주어딘다.
- 세 번째 줄부터 현수가 짠 N 개의 수업설계가 주어진다.(길이는 30 이하)
- 수업설계는 같은 과목을 여러번 이수하도록 설계해도 된다.

**출력 설명**

- 수업 설계가 잘된것이면 'Yes', 잘못된 것이면 'NO' 를 출력한다.

**입력 예제**

CBA

3

CBDAGE

FGCDAB

CTSBDEA

**출력예제**

#1 YES

#2 NO

#3 YES

# 내 해답

- 입력 첫재줄에 내가 들어야 되는 과목들이 나온다. 이 과목을 LIST 로 쪼갠다. (CBA -> [C,B,A])
- 그 이후 각 수업설계를 앞에서부터 훑는다.
  - 이 때에 List 에 있을때에만 Stack 에 넣는다.
- 이후 Stack 에 넣어진 값이 List 와 같은지 비교한다.
- 넣을 과목이 이미 stack 에 있으면 넣지 않는다.

```python
import sys
sys.stdin=open("in2.txt", "r")


Class = input()
lis = list(Class)
N = int(input())

for _ in range(N):
    stack = []
    Clas = input()
    for val in list(Clas):
        if (val in lis) & (val not in stack) :
            stack.append(val)
    if stack == lis :
        print(f'#{_+1} YES')
    else :
        print(f'#{_+1} NO')
```



# 다른 답

- 필요한 과목을 need 로 정의한다.
- 그 이후 '충족시킬때 마다' need 에서 제외시킴으로서 효율적인 코드를 짤 수 있다.
- 나는 need 에서 제외시키는게 아니라, need 에서 '없을 때' 라는 조건을 달아서 좀 더 지저분해짐..

```python
import sys
from collections import deque
sys.stdin=open("input.txt", "r")
need=input()
n=int(input())
for i in range(n):
    plan=input()
    dq=deque(need)
    for x in plan:
        if x in dq:
            if x!=dq.popleft():
                print("#%d NO" %(i+1))
                break
    else:
        if len(dq)==0:
            print("#%d YES" %(i+1))
        else:
            print("#%d NO" %(i+1))
```

