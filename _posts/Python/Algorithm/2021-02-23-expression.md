---
title:  "후위표기식"
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

 ![png](/assets/images/{Algorithm}/13_1.JPG)

**입력설명**

- 첫 줄에 중위 표기식이 주어진다. 
- 식은 1~9 의 숫자와 +,-,*,/,(,) 연산자로만 이루어진다.

**출력 설명**

- 후위표기식을 출력한다.

**입력 예제**

3 + 5 * 2 /(7-2)

**출력예제**

352*72-/+

**설명**

3 5 2 * 7 2 - / + 

3 10 7 2 - / + 

3 10 5 / +

3 2 +

5

# 내 해답

- 어려워서 풀지 못하였다 ㅜㅜ
- 나중에 재도전해서 다시 풀어보아야할듯!

# 다른 답

```python
import sys
sys.stdin=open("input.txt", "r")
a=input()
stack=[]
res=''
for x in a:
    if x.isdecimal():
        res+=x
    else:
        if x=='(':
            stack.append(x)
        elif x=='*' or x=='/':
            while stack and (stack[-1]=='*' or stack[-1]=='/'):
                res+=stack.pop()
            stack.append(x)
        elif x=='+' or x=='-':
            while stack and stack[-1]!='(':
                res+=stack.pop()
            stack.append(x)
        elif x==')':
            while stack and stack[-1]!='(':
                res+=stack.pop()
            stack.pop()
while stack:
    res+=stack.pop()
print(res)
```

