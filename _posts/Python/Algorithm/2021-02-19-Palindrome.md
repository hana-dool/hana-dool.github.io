---
title:  "회문"
excerpt: "Algorithm"
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

- 문제 및 답 출처 : [링크](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/dashboard)

- 해당 링크에 가시면 훨씬 더 전문적인 해설 및 / 강의를 보실 수 있습니다. 

# 문제

**문제**  

- N 개의 문자열 데이터를 입력받아 앞에서 읽을때나, 뒤에서 읽을 때나 같은 경우이면 YES 를 출력, 그렇지 않으면 NO 를 출력하는 프로그램을 작성한다.
- 단 회문을 검사할 때 대소문자를 구분하지 않는다.

**입력설명**

- 첫 줄에 정수 N 이 주어지고, 그 다음 줄부터 N 개의 단어가 입력된다.
- 각 단어의 길이는 100을 넘지 않는다.

**출력 설명**

- 각 줄에 해당 문자열의 결과를 YES 또는 NO 로 출력한다.

**입력 예제**

5

level

moon

abcba

soon

gooG

**출력예제**

#1 YES

#2 NO

#3 YES

#4 NO

#5 YES



# 내 해답

```python
import sys
sys.stdin=open("in1.txt", "r")

N = int(input())
for repeat in range(N) :
    string = input()
    string = string.lower()
    if string == string[::-1] :
        ans = 'YES'
        print(f'#{repeat+1} {ans}')
    else :
        ans = 'NO'
        print(f'#{repeat+1} {ans}')
```



# 답지

```python
import sys
sys.stdin=open("input.txt", "r")
n=int(input())
for i in range(n):
    str=input()
    str=str.upper()
    if str==str[::-1]:
        print("#%d YES" %i)
    else:
        print("#%d NO" %i)
```

- 나와 거의 똑같은듯!