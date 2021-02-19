---
title:  "격자 모양 합"
excerpt: "Algorithm"
categories:
  - Py_Algorithm
tags:
  - 3
last_modified_at: 2021-02-20

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

​	![png](/assets/images/{Algorithm}/3_1.JPG)

**입력설명**

- 첫 줄에 자연수 N(홀수) 가 주어진다.
- 두번째 줄부터 N 줄에 걸쳐 각 줄에 N 개의 자연수가 주어진다.
- 이 자연수는 격자안에 있는 사과나무에 열린 사과의 갯수이다.
- 각 격자 안의 사과의 갯수는 100을 넘지 않는다.

**출력 설명**

- 수확한 사과의 총 갯수를 출력

**입력 예제**

5

10 13 10 12 15

12 39 30 23 11

11 25 50 53 15

19 27 29 37 27

19 13 30 13 19

**출력예제**

379



# 내 풀이

```python
import sys
sys.stdin=open("in5.txt", "r")

N = int(input())
mat = [list(map(int, input().split())) for repeat in range(N)]
i = int((N-1)/2)
j = int((N-1)/2)
lis = []

rst = 0
for n in range(N):
    val=sum(mat[n][abs(i):(N-abs(j))])
    rst += val
    i -= 1
    j -= 1

print(rst)
```

- 주요 쟁점은 for 문으로 어떻게 늘어나다가 줄어드는 마름모를 표현할지였다.
- 하지만 for 문에 너무 집착하지 말고, 외부 변수로 i 와 j 를 이용하면 위 고민을 해결할 수 있다. 
- i, j 를 이용하여 한쪽은 줄고, 한쪽은 늘어나는 경향을 반영하였다.

# 다른 풀이

```python
import sys
sys.stdin = open("input.txt", 'r')
n=int(input())
a=[list(map(int, input().split())) for _ in range(n)]
res=0
s=e=n//2
for i in range(n):
    for j in range(s, e+1):
        res+=a[i][j]
    if i<n//2:
        s-=1
        e+=1
    else:
        s+=1
        e-=1
print(res)
```

- 이 역시 쟁점은 matrix 를 구성한다기 보다는 마름모의 경향을 잘 반영하는지였다.
- if / else 를 같이 써줌으로서 end 과 start 의 업데이트 방식을 아예 바꿈으로서 다양한 모양을 표현할 수 있을것이다! 

# 고친 풀이

- 아래와 같이 if 와 else 를 이용해 'Update' 의 방식을 바꿈으로서 더 간결하고 쉬운 풀이가 가능합니다!

```python
import sys
sys.stdin=open("in5.txt", "r")

N = int(input())
mat = [list(map(int, input().split())) for repeat in range(N)]
i = int((N-1)/2)
j = int((N+1)/2)
rst = 0
for n in range(N):
    val = sum(mat[n][i:j])
    rst += val
    if n >= (N-1)/2 :
        i += 1
        j -= 1
    else :
        i -= 1
        j += 1
print(rst)
```