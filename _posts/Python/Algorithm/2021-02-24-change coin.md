---
title:  "동전 교환"
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

다음과 같이 여러 단위의 동전들이 주어져 있을때 거스름돈을 가장 적은 수의 동전으로 교환해주려면 어떻게 주면 되는가? 각 단위의 동전은 무한정 쓸 수 있다.

**입력설명**

- 첫번째 줄에는 동전의 종류 갯수 N 이 주어진다 
- 두번째 줄에는 N 개의 동전의 종류가 주어지고, 그 다음줄에 거슬러 줄 금액 M 이 주어진다. 
- 각 동전의 종류는 100원을 넘지 않는다.

**출력 설명**

- 첫 번째 줄에 거슬러 줄 동전의 최소개수를 출력한다.

**입력 예제**

3

1 2 5

15

**출력예제**

3

# 내 해답

```python
import sys
sys.stdin = open('in5.txt','r')

N = int(input())
lis = list(map(int,input().split()))
change = int(input())
min = 24000000
def DFS(m,c) : # m은 money 라는 뜻임
    global min
    if c > min :
        return
    if m < 0 : # 0보다 작으면 끝입니다.. 아무것도 하지마세요
        return
    if m == 0 : # 0 이면 이때다~!
        if min > c :
            min = c
    else : # m이 0보다 크면 아직 더 돈이 남아있다는 뜻!
        for i in lis:
            DFS(m-i,c+1) # update 가 변수에서 일어나서 특별한 조정이 필요없음 -> 편하다.

DFS(change,0)
print(min)
```

- 위대로 하면 답은 나온다.
- 하지만 그 Procedure 만 나와있을 뿐, 최적화가 되어있지 않아서 매우 느리다.
- 즉 최적화를 더 추가해야된다.

# 다른 답

```python
import sys
sys.stdin=open("input.txt", "r")
def DFS(L, sum):
    global res
    if L>=res:
        return
    if sum>m:
        return
    if sum==m:
        if L<res:
            res=L
    else:
        for i in range(n):
            DFS(L+1, sum+a[i])

if __name__=="__main__":
    n=int(input())
    a=list(map(int, input().split()))
    m=int(input())
    res=2147000000
    a.sort(reverse=True)
    DFS(0, 0)
    print(res)
```

- 주요했던점은 a.sort 였다. 
- 먼저 '큰 금액' 부터 처리하는게 더 효율적이다! 