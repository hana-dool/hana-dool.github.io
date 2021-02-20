---
title:  "격자판 회문"
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

![png](/assets/images/{Algorithm}/7_1.JPG)

# 내 해답

- 우선 5자리 수를 모두 추출하자. (list 형식으로 append)
- 그 이후 5자리 수에 대해서 회문인지 아닌지를 검사하는 함수를 def 한다.
- 그 함수에 대해서 list 의 모든 구성요서에 대해 회문검사하면 될듯!

```python
import sys
sys.stdin=open("in5.txt", "r")

mat = [list(map(int,input().split())) for repeat in range(7)]

# row 5자리수 추출
all_lis = []
for row in range(7) :
    for i in range(3):
        all_lis.append(mat[row][0+i:5+i])

# col 5자리 수 추출
for col in range(7) : # 어느 columns 에서 뽑을지 고정
    for i in range(3): # 그 columns 내에서 어디에서 시작할지 결정
        lis = []
        for row in range(0+i,5+i):
            lis.append(mat[row][col])
        all_lis.append(lis) # list 를 넣는다.

# 이제 모든 5자리 수들을 뽑아내었으므로, 각각의 list 가 회문인지 검사하는 프로그램을 만든다.
rst = 0
for i in all_lis:
    if i == i[::-1] :
        rst += 1
print(rst)
```



# 다른 답

```python
import sys
sys.stdin=open("input.txt", "r")
board=[list(map(int, input().split())) for _ in range(7)]
cnt=0
for i in range(3):
    for j in range(7):
        tmp=board[j][i:i+5]
        if tmp==tmp[::-1]:
            cnt+=1
        for k in range(2):
            if board[i+k][j]!=board[i+5-k-1][j]:
                break;
        else:
            cnt+=1
        
print(cnt)
```

- row 의 회문검사는 나랑 같은데, col 의 회문검사를 여기에서는 바로 수행한게 다른점!
- for else + breaks 구문을 사용하여, 앞의 for 문을 모두 break 없이 잘 통과해야 cnt 를 늘려주는 방식을 사용