---
title:  "후위식 연산"
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

  ![png](/assets/images/{Algorithm}/2_1.JPG)

**입력설명**

- 첫 줄에 후위 연산식이 주어진다. 
- 연산식의 길이는 50을 넘지 않는다.
- 식은 1~9 의 숫자와 +,-,*,/,(,) 연산자로 이루어진다.

**출력 설명**

- 연산한 결과를 출력한다.

**입력 예제**

352+*9-

**출력예제**

12

# 내 해답

- 설명할건 크게 없다. 
- stack 을 이미 문제에서 제시해 주었기 때문에, 그에 맞추어서 연산 기호를 만날때마다 차례로 앞 두 숫자에 대해 계산만 하면 되어서 매우 쉬웠다.

```python
import sys
sys.stdin=open("in1.txt", "r")

exp = input()
ans = []
for val in exp :
    if val.isdigit() :
        ans.append(val)
    elif val == '+' :
        num1 = float(ans.pop())
        num2 = float(ans.pop())
        num = num2 + num1
        ans.append(num)
    elif val == '-' :
        num1 = float(ans.pop())
        num2 = float(ans.pop())
        num = num2 - num1
        ans.append(num)
    elif val == '*' :
        num1 = float(ans.pop())
        num2 = float(ans.pop())
        num = num2 * num1
        ans.append(num)
    elif val == '/' :
        num1 = float(ans.pop())
        num2 = float(ans.pop())
        num = num2 / num1
        ans.append(num)
print(ans[0])
```

# 다른 답

```python
import sys
sys.stdin=open("input.txt", "r")
a=input()
stack=[]
for x in a:
    if x.isdecimal():
        stack.append(int(x))
    else:
        if x=='+':
            n1=stack.pop()
            n2=stack.pop()
            stack.append(n2+n1)
        elif x=='-':
            n1=stack.pop()
            n2=stack.pop()
            stack.append(n2-n1)
        elif x=='*':
            n1=stack.pop()
            n2=stack.pop()
            stack.append(n2*n1)
        elif x=='/':
            n1=stack.pop()
            n2=stack.pop()
            stack.append(n2/n1)
print(stack[0])
```

- 네... 똑같습니다~