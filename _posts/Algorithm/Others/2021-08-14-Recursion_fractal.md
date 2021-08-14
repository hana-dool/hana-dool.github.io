---
title:  "Dived And Conquor"
excerpt: "프렉탈 구조의 Recursion"
categories:
  - AL_Others
tags:
  - 1
last_modified_at: 2021-08-14

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# Fractal?

- 프랙탈이란 자기닮음을 가지고 있다는 뜻입니다.
- 이러한 문제는 '재귀로' 쉽게 풀 수 있는 유형이기떄문에 잘 알아두어야 합니다.

# 색종이 자르기

![png](/assets/images/Algorithm/8.png)

<br>

```python
import sys
input = sys.stdin.readline
N = int(input())
mat = [list(map(int,input().split())) for _ in range(N)]

blue = 0
red = 0
def recur(l,a,b) :
    global blue
    global red
    cnt = 0
    for i in range(a,a+l) :
        for j in range(b,b+l):
            if mat[i][j] == 1 :
                cnt += 1
    if cnt == l*l  :
        blue += 1
        return
    elif cnt == 0 :
        red += 1
        return
    else :
        recur(l//2,a,b)
        recur(l//2,a+l//2,b)
        recur(l//2,a,b+l//2)
        recur(l//2,a+l//2,b+l//2)
recur(N,0,0)
print(red)
print(blue)
```

- recursion 함수를 사용할때에 중요한것은 ' 재귀적으로 어떻게 나누어 보  것인가' 입니다.
- 저는 위의 문제에서 길이 l 과, 시작점 (왼쪽위) 의 x,y 좌표를 활용해 Recursion 을 진행하였습니다.

