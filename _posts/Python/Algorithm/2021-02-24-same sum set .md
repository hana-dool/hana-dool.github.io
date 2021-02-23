---
title:  "합이 같은 부분집합"
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

N 개의 원소로 구성된 자연수 집합이 주어지면, 이 집합을 두개의 부부ㄴ집합으로 나누었을 때 두 부분집합의 원소의 합이 서로 같은 경우가 존재하면 YES 를 출력하고, 그렇지 않으면 NO 를 출력하는 프로그램을 작성하라

둘로 나뉘는 두 부분집합은 서로소 집합이며, 두 부분집합을 합하면 입력으로 주어진 원래의 집합이 되어야 한다.

**입력설명**

- 첫번째 줄에 자연수 N 이 주어진다.
- 두번째 줄에 집합의 원소 N 개가 주어진다. 각 원소는 중복되지 않는다.

**출력 설명**

- 첫 줄에 yes 또는 no 출력

**입력 예제**

6

1 3 5 6 7 10

**출력예제**

Yes

# 내 해답

- 이 경우에도, 내가 구현한 재귀식이, 아래의 예시처럼 잘 작동하지 않았기 때문에.. 답지의 방식을 보고, 나도 비슷하게 다시 구현해 본 것이다.

```python
import sys
sys.stdin=open("in5.txt", "r")

N = int(input())
lis = list(map(int,input().split()))

def DFS(L,s):
    if L >= N : # 조건부
        if s == sum(lis)/2: # 출력부
            print('YES') 
            sys.exit(0)
    else :
        DFS(L+1,s) # 적용부(s) 재귀부(L)
        DFS(L+1,s+lis[L])

DFS(0,0)
print('NO')
```



# 다른 답

```python
import sys
sys.stdin=open("input.txt", "r")
def DFS(L, sum): # L 은 깊이 , sum 은 합 
    if sum>total//2: # 이 부분은 사실 최적화 부분이다. 필수적이지는 않음
        return
    if L==n: # 조건부
        if sum==(total-sum): # 출력부
            print("YES")
            sys.exit(0)
    else:
        DFS(L+1, sum+a[L]) # 적용부 + 재귀부
        DFS(L+1, sum)

if __name__=="__main__":
    n=int(input())
    a=list(map(int, input().split()))
    total=sum(a)
    DFS(0, 0)
    print("NO")
```

- 배워야 할 점! DFS의 인자를 2개이상으로 구성하고있다.
  - Why?
  - DFS 의 인자를 1개만으로 구성하면, 다양하게 값을 비교할 수 없기 때문이다.
  - 아래의 예시를 보자.

```python
import sys
sys.stdin=open("in1.txt", "r")

N = int(input())
lis = list(map(int, input().split()))

# 각각 분기할때마다, 왼쪽집합에 속하던지/ 오른쪽 집합에 속하던지 둘중에 하나를 실행하도록 하였다.
# 즉 x N 을 초과하게 되면 멈추는것이 바람직
lis1 = [0]*N
lis2 = [0]*N
yes = 0

def DFS(x):
    if x >= N : # 조건부
        if sum(lis1) == sum(lis2) : # 출력부
            print('YES')
            print(lis1)
            print(lis2)
            sys.exit(0)

    else :
        lis1[x] = lis[x] # 적용부
        DFS(x+1) #재귀부
        lis2[x] = lis[x]
        DFS(x+1)
DFS(0)
print('NO')
```

- 이 경우 제대로 출력되지 않는다. 
- 이는 내가 lis 라는 global 함수를 이용해서 재귀함수를 짯는데, 이런 경우에 결국 하나의 global 함수를 가지고 여러 재귀함수들이 돌아가면서 바꾸는것이기 때문에, 생각보다 제어하기가 힘들기 때문이다.
- 그러므로 재귀함수에서 여러 함수에 대해서 여러 변수를 사용하게 함수를 짠다면, 각 함수마다 global 함수를 이용한게 아니라, 여러 변수를(x,y..) 이용하는 형식으로 함수를 짯기 떄문에 제어하기가 훨씬 쉽다. 

