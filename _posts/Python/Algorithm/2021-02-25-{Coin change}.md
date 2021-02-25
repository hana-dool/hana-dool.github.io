---
title:  "동전 바꾸기"
excerpt: "Algorithm"
categories:
  - Py_Algorithm
tags:
  - 3
last_modified_at: 2021-02-25

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

![png](/assets/images/{Algorithm}/29_1.JPG)

**입력설명**

- 첫째 줄에는 지폐의 금액 T
- 둘째 줄에는 동전의 가지 수 K
- 셋째줄부터 마지막 줄 까지는 각 줄에 동전의 금액 p 와 갯수 n 이 주어진다.

**출력 설명**

- 첫번째 줄에 동전의 교환 방법의 가지 수를 출력한다. (교환할 수 없는 경우는 존재하지 않음)

**입력 예제**

20

3

5 3

10 2

1 5

**출력예제**

4

# 내 해답

- 답지 아이디어를 이해한 이후 구현한거라 상당히 비슷하다. 
- 나중에 다시한번 구현해야한다.

```python
import sys
sys.stdin = open('in2.txt','r')

T = int(input())
K = int(input())

money = []
num = []

for _ in range(K):
    a,b = map(int,input().split())
    money.append(a)
    num.append(b)

# 이제 DFS 를 Construct
# tot : 최대값
# T : 내가 채우고자 하는금액
# l : 내가 사용한 동전의 가짓수, 예제 1 에서는 [5,10,1] 로 3이 된다.
cnt = 0
def DFS(l,sum):
    global cnt
    if sum > T : # 최적화부분
        return
    if (l == K) :
        if sum == T :
            cnt += 1
    else :
        for i in range(num[l]+1): # l번째 동전의 총 갯수
            DFS(l+1,sum+(i*money[l])) # l번째 동전의 액수 * 갯수
# l 은 0 ~ K-1
DFS(0,0)
print(cnt)
```



# 다른 답

```python
import sys
sys.stdin=open("input.txt", "r")
def DFS(L, sum):
    global cnt
    if sum>m:
        return
    if L==n:
        if sum==m:
            cnt+=1
    else:
        # DFS 가 
        for i in range(cn[L]+1):
            DFS(L+1, sum+(cv[L]*i))

m=int(input()) # 환전해야 하는 금액
n=int(input()) # 동전의 가짓수
cv=list() # 금액의 list
cn=list() # 갯수의 list
for i in range(n): 
    a, b=map(int, input().split()) 
    cv.append(a)
    cn.append(b)
cnt=0
DFS(0, 0)
print(cnt)
```

- ![png](/assets/images/{Algorithm}/29_2.JPG)

- 위의 그림처럼 DFS에서 L을 '사용하는 동전의 금액' 으로 잡는다. 
- 이렇게 기준을 잡고나서, dfs 가 1씩 늘어나는 단계에서, for문을 돌리는데 for문은 각 동전의 수 만큼 돌린다. 
- 그러면 DFS 를 깔끔하게 구현 가능하다! (조합에서의 구현이 깔끔해진다.)
- DFS에서 '조합'을 어떻게 구현할까에 대한 좋은 예시이다.