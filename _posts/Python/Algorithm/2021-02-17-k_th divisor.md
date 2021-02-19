---
title:  "k번째 약수"
excerpt: "파이썬 Algorithm"
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

```python
#k 번째 약수
#어떤 자연수 p와 q 가 있을때에 p를 q 로나누었을때 나머지가 0 이면 p는 p의 약수이다.
#n,k 가 주어졌을 때 n 의 약수들 중 k 번째로 작은수를 출력하는 프로그램
```

```python
# 입력예제 6 3
# 출력예제 3
```

- 아래의 답은 내가 직접 해본 답 

```python
import sys
sys.stdin = open("in3.txt", "rt")
n, k = map(int,input().split()) #n,k 를 integer 로 받고

lis = []
for i in range(1,n+1): # 1~n 에 대하여
    if n % i == 0 : # i 로 나누어 떨어지면
        lis.append(i) # 작은순으로 append
if len(lis) < k : # 만약 list 의 lenth 보다 k 가 크다면, 이는 에러
    print(-1) # 그런 경우 -1 을 출력 
else :
    print(lis[k - 1]) # length 보다 작거나 같은경우는 출력가능
```

- 다음은 답지의 해설이다.

```python
import sys
sys.stdin=open("input.txt", "r")
n, k=map(int, input().split())
cnt=0 # cnt = 0 을 지정해줌
for i in range(1, n+1): # 1~n 에 대해서
    if n%i==0: # i 로 잘 나누어지면 cnt 에 1을 더한다.
        cnt+=1
    if cnt==k: # 만약 cnt 가 k가 된다면, 그때 i 를 출력
        print(i)
        break # 이후 for문을 벗어난다.
else:
    print(-1)
```

- 이때에 잘 봐야할것은 for 문과 else 문의 결합이다. 
- for ~ else 문 : for 문이 중간에 break 으로 인해 끊기지 않고 끝까지 수행되었을 때 else 를 출력하는 코드
  - 즉 break 가 한번도 걸리지 않고, (즉 cnt == k 인 순간이 없었음) 수해되었다면 else 의 print(-1) 을 출력하게 된다.

