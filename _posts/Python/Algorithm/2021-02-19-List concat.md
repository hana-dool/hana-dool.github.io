---
title:  "두 리스트 합치기"
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

- 오름차순으로 정렬된 두 리스트가 주어지면 두 리스트를 오름차순으로 합쳐 출력하는 프로그램을 작성하라.

**입력설명**

- 첫번째 줄에 첫번째 리스트의 크기 N 이 주어진다.
- 두번째 줄에 N 개의 리스트 원소가 오름차순으로 주어지다.
- 세번째 줄에 두번째 리스트의 크기 M 이 주어진다.
- 네번쨰 줄에 M 개의 리스트 원소가 오름차순으로 주어지다.
- 각 리스트의 원소는 int 형 변수의 크기를 넣지 않는다.

**출력 설명**

- 오름차순으로 정렬된 리스트를 출력한다.

**입력 예제**

3

1 3 5 

5

2 3 6 7 9

**출력예제**

1 2 3 3 5 6 7 9



# 내 풀이

```
import sys
sys.stdin=open("in5.txt", "r")
N1 = int(input())
lis1 = list(map(int,input().split()))
N2 = int(input())
lis2 = list(map(int,input().split()))
lis_concat = lis1 + lis2
lis_concat.sort()
print(lis_concat)
```

- 딱히 설명할게 없을정도로 쉽다.

# 해답

```python
import sys
sys.stdin=open("input.txt", "r")
n=int(input())
a=list(map(int, input().split()))
m=int(input())
b=list(map(int, input().split()))
p1=p2=0
c=[]
while p1<n and p2<m:
    if a[p1]<b[p2]:
        c.append(a[p1])
        p1+=1
    else:
        c.append(b[p2])
        p2+=1
if p1<n:
    c=c+a[p1:]
if p2<m:
    c=c+b[p2:]
for x in c:
    print(x, end=' ')
```

- while 문을 통해서 직접 모두 추가하였다.
- 내 방법이 좀 더 간결해 보이긴 하나, 아래 방법을 익혀두어야 범용성 있게 적용할 수 있을것이다!