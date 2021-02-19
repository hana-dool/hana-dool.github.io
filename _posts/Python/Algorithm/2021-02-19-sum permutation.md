---
title:  "수열의 합"
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

- N 개의 수로 된 수열 A[1] .... A[N] 이 있다. 이 수열의 i번째 수부터 j 번째 수 까지의 합 A[i] + A[i+1] .... +A[j] 가 M 이 되는 경우의 수를 구하는 프로그램을 작성해라.

**입력설명**

- 첫째 줄에 N, M 이 주어진다.
- 다음 줄에는 A[1] .... A[N] 이 공백으로 분리되어 주어진다.
- 각각의 A[x] 는 30000 을 넘지 않는 자연수이다.

**출력 설명**

- 첫째 줄에 경우의 수를 출력한다.

**입력 예제**

8 3

1 2 1 3 1 1 1 2

**출력예제**

5



# 내 해답

```python
import sys
sys.stdin=open("in2.txt", "r")

N,M = map(int,input().split())
lis = list(map(int,input().split()))

ans = 0
for i in range(N): # 시작지점 i 를 정한다.
    for j in range(i,N): # 끝나는 지점 j 를 정한다.
        tot = 0
        for k in range(i,j+1):
            tot += lis[k]
        if tot == M : # 만약 그 합이 M 이라면
            ans += 1 #경우의 수에 1을 더한다.
print(ans)
```

- 사실 for 문을 너무 무지막지하게 돌려서 효율성 측면에서 매우 안좋을듯 하다.

# 답지

```python
import sys
sys.stdin = open("input.txt", 'r')
n, m=map(int, input().split())
a=list(map(int, input().split()))
lt=0 # lt 로서 시작하는 left indtx
rt=1 # rt 로서 끝나는 right index
tot=a[0] # 첫 시작값
cnt=0 
while True: 
    if tot<m: # tot 이 m 이 아니라면
        if rt<n: # rt(오른쪽 index) 가 n보다 작으면
            tot+=a[rt] # 
            rt+=1
        else: # else , 즉 오른쪽 index 가 n 보다 같거나 크면 while 터트림
            break
    elif tot==m: # total 이 m 과 같다면
        cnt+=1 # count 에 1을 추가
        tot-=a[lt] # 그리고 total 에서 왼쪽 index 값을 뺴고
        lt+=1 #왼쪽의 index가 1 올라간다.
    else: # 즉 tot > m 일때에
        tot-=a[lt] # 인쪽 인덱스를 뺴고
        lt+=1 # 왼쪽 인덱스를 1 올린다
print(cnt)
```

- 탐색 과정을 보면 합리적이고 정말 tricky 한거 같다.
- 최적화가 많이 진행되어 있어, 내가 한 for 문 겹친거보다 훨~씬 효율적!
- 이 코드는 경험과 공부를 많이 해야 따라할 수 있을듯 하다..