---
title:  "k 번째 큰 수"
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

- 현수는 1~100 사이의 자연수가 적힌 N 장의 카드를 가지고 있다. 같은 숫자의 카드는 여러장 있을 수 있다. 현수는 이 중 3장을 뽑아 각 카드에 적힌 수를 합한 값을 기록하려고 한다. 3장을 뽑을 수 있는 모든 경우를 기록한다. 기록한 값 중 k 번째로 큰 수를 출력하는 프로그램을 작성하라

- note) 만약 큰 수 부터 만들어진 수가 25 25 23 23 22 20 19... 이고 k 가 3 이라면 k 번째 큰 값은 22 이다.

- **입력**

  - 첫 줄에 자연수 N(3~100) 과 K(1~50) 이 입력되고 그 다음줄에 N 개의 카드값이 입력된다.

- **출력**

  - 첫 줄에 K 번째 수를 출력. K 번째 수는 반드시 존재

- **입력예제**

  10 3

  13 15 34 23 45 65 33 11 26 42

- **출력예제**

  143

- **설명**

  3장을 뽑았을 때에, 얻은 카드들의 합에 대해서 3번째로 큰것이 143이다.

  (65+45+42, 65+45+34 ...)

# 내 풀이

1. 우선 N과 k를 받는다. N,k = map(int,input().split())

2. 그 이후 3장의 sum 에 대해서 k번쨰로 큰 값을 찾으면 된다.

   - 모든 조합별로 3을 하면 너무 계산량이 많다.
   - '큰' 값이 궁금하므로 set 을 활용하면 될거같다.

   - set 을 이용해서 모든 조합의 값을 써 넣는다.

3. 그 이후 그 set 을 list 로 고친 후 sort 하고 거기서 k번째를 출력

```python
import timeit
start = timeit.default_timer()
import sys
sys.stdin=open("in2.txt", "r")

n,k = map(int,input().split())
lis = list(map(int,input().split()))

# 조합별 덧셈을 수행하는 구간
set = set()
for i in range(0,n):
    for j in range(0,n):
        for r in range(0,n):
            if (i!= j) & (j!=r) & (i!=r): # 다른 조합게 하려고 
                set.add(lis[i]+lis[j]+lis[r])
                
# list 를 만들어 sort,reverse 한 뒤에 index 추출               
sum_lis = list(set)
sum_lis.sort()
sum_lis.reverse()
print(sum_lis[k-1])

stop = timeit.default_timer()
print(f'실행 시간 : {stop-start}')
```



# 답지 풀이

```python
import sys
sys.stdin=open("input.txt", "r")
n, k=map(int, input().split())
a=list(map(int, input().split()))
res=set()
# 조합을 더하는 구간이 다르다.
for i in range(n):
    for j in range(i+1, n):
        for m in range(j+1, n):
            res.add(a[i]+a[j]+a[m])
res=list(res)
res.sort(reverse=True)
print(res[k-1])
```

- 대부분 나와 비슷하지만, 조합을 구하는 부분에서 차이점이 있다.
- 나는 if 문을 써서 계산량이 늘어났지만, 여기에서는 indexing 만으로 조합을 구현해 내었다.

- sort 의 경우에도 reverse = True 인자를 함께 넣어서 만든게 인상깊음.

