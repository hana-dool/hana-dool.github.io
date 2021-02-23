---
title:  "단어찾기"
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

현수는 영어로 시를 쓰는것을 좋아한다. 현수는 시를 쓰기 전에 시에 쓰일 단어를 미리 노트에 적어둔다. 이번에는 N 개의 단어를 노트에 적었는데, 시에 쓰지 않은 단어가 하나 있다고 한다. 우리들이 어떤 단어인지 찾아보자.

**입력설명**

- 첫 줄에 자연수 N 과 K 가 주어진다.
- 두 번째 줄부터 노트에 미리 적어놓은 N 개의 단어가 주어지고 이어 다음줄부터 시에 쓰인 N-1 개의 단어가 주어진다.

**출력 설명**

첫 번째 줄에 시에 쓰이지 않은 한개의 단어를 출력한다.

**입력 예제**

5

big

good

sky

blue

mouse

sky

good

mouse

big

**출력예제**

blue

# 내 해답

- 우선 deque 자료구조형을 쓰려고 노력해보자!
- 단어장의 N 개의 단어들을 쌓아 보관하자.
- 그리고 시에 쓰인 단어들을 deque 로 저장하자.
- 그 이후 deque 에서 pop 으로 하나씩 꺼내보면서 단어장에 있다면 deque 에서 pop 시키고 단어장에 없으면 append 시킨다.

```python
import sys
sys.stdin=open("in3.txt", "r")

N = int(input())
lis = []
for _ in range(N):
    lis.append(input())

word = []
for _ in range(N-1):
    word.append(input())

from collections import deque
deq = deque(lis)

while True :
    val = deq.pop()
    if val not in word :
        ans = val
        break
print(ans)
```



# 다른 답

- 해쉬(딕셔너리) 를 이용하여 풀었다!
- 활실히 내 방법보다 훨씬 빠를듯

```python
import sys
sys.stdin=open("input.txt", "r")
n=int(input())
p=dict()
for i in range(n):
    word=input()
    p[word]=1
for i in range(n-1):
    word=input()
    p[word]=0
for key, val in p.items():
    if val==1:
        print(key)
        break
```



# 내 해답2

- 해쉬를 이용하여 다시 풀어보았다.

```python
import sys
sys.stdin=open("in1.txt", "r")

N = int(input())

lis = []
val = [0]*N
for _ in range(N):
    lis.append(input())
dic = dict(zip(lis,val)) # 이름, value 가 같이 들어가있음!

for _ in range(N-1):
    val = input()
    dic[val] = 1

for val in dic.items() :
    if val[1] == 0:
        print(val[0])
```