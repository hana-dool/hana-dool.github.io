---
title:  "k 번쨰 수"
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

- 문제 

  - N개의 숫자로 이루어진 숫자열이 주어지면 해당 숫자열중, s번째부터 e 번째 까지의 수를 오름차순 정렬하였을 때 k 번째로 나타나는 숫자를 출력하는 프로그램을 작성하라

- 입력 

  -  첫째줄에 테스트 케이스 T 가 주어짐

  - 각각 케이스별 
    - 첫쨰줄은 자연수 N,s,e,k 가 차례로 주어짐
    - 두번째 줄에 N 개의 숫자가 차례로 주어진다.

- EX)

  입력

  2

  6 2 5 3

  5 2 7 3 8 9 

  15 3 10 3 

  4 15 8 16 6 6 17 3 10 11 18 7 14 7 15

  출력

  #1 7

  #2 6

- 출력설명(#1)
  - 2~5번째는 2738 을 의미한다.
  - 2738 을 오름차순정렬하면 2378이다.
  - 여기에서 3번째 숫자는 7이다.

# 내 풀이

1. 우선 N ,e, s, k 를 각각 map(int,input().split()) 으로 받고 
2. 두번째 줄의 값은 list 로 받아야하므로  lis = list(map(int,input().split())) 으로받음
3. lis = lis[s-1:e] 를 통해서 s번째 ~ e 번째 선택
4. lis.sort() 를 통해서 list sorting
5. lis[k-1] 을 통해서 k 번째 뽑아내기

```python
import sys
sys.stdin=open("in2.txt", "r")
T= int(input())
for i in range(1,T+1):
    N,s,e,k = map(int,input().split())
    lis = list(map(int,input().split()))
    lis = lis[s-1:e]
    lis.sort()
    rst = lis[k-1]
    print(f'#{i} {rst}')
```



# 답지의 풀이

```python
import sys
sys.stdin=open("input.txt", "r")
T=int(input())
for t in range(T):
    n, s, e, k=map(int, input().split())
    a=list(map(int, input().split()))
    a=a[s-1:e]
    a.sort()
    print("#%d %d" %(t+1, a[k-1]))
```

- 나와 거의 비슷하다. 
- 이 부분에서는 특별히 할 코멘트 없음!

