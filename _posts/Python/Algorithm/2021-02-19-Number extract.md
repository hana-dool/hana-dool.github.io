---
title:  "숫자만 추출하기"
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

- 문자와 숫자가 섞여있는 문자열이 주어지면 그 중 숫자만 추출하여 그 순서대로 자연수를 만든다. 
- 담들어진 자연수와 그 자연수의 약수 개수를 출력한다.
- 만약 't0e0a1c2h0er' 에서 숫자만 추출하면 00120 이다. 이것을 자연수로 만들면 120 이다. 즉 첫 자리 자연수 0 은 자연수화 할 때에 무시가 된다.
- 출력은 120을 출력한다.
- 다음 줄에는 120의 약수의 갯수를 출력하면 된다.

**입력설명**

- 첫줄에 숫자가 섞인 문자열이 주어진다. 문자열의 길이는 50을 넘지 않는다.

**출력 설명**

- 첫줄에 자연수를 출력하고, 두 번째 줄에 약수의 갯수를 출력한다.

**입력 예제**

g0en2Ts8eSoft

**출력예제**

28

6

# 내 답

```python
import sys
sys.stdin=open("in2.txt", "r")

string = input()
number = ''
for val in string :
    if val.isdigit():
        number += val
# 이때 0016 -> 16 으로 바뀐다.
number = int(number)
ans = 0
for divisor in range(1,number+1):
    if number % divisor == 0 :
        ans += 1
print(number)
print(ans)
```



# 해답

```python
import sys
sys.stdin=open("input.txt", "r")
s=input()
res=0
for x in s:
    if x.isdecimal():
        res=res*10+int(x)
print(res)
cnt=0
for i in range(1, res+1):
    if res%i==0:
        cnt+=1
print(cnt)
```

- 이때 isdecimal 을 사용한것을 주의깊게 보아야 한다.
- isdecimal 은 0~9만 인식하기떄문에 훨씬 정확함.(물론 여기에서는 numeric 만 해도 되긴 한다.)