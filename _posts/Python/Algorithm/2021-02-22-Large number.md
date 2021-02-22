---
title:  "가장 큰 수"
excerpt: "Algorithm"
categories:
  - Py_Algorithm
tags:
  - 3
last_modified_at: 2021-02-22

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

선생님은 현수에게 숫자 하나를 주고, 해당 숫자의 자릿수들 중 m 개의 숫자를 제거하여 가장 큰 수를 만들라고 하엿다. 현수를 도와주세요! (단 숫자의 순서는 유지해야한다.)

즉 만약 5276823 이 주어지고 3개의 자릿수를 제거한다면 7823 이 가장 큰 숫자가 된다.

**입력설명**

- 첫째 줄에 숫자(길이는 1000을 넘지 않습니다.) 와 제거해야할 자릿수의 갯수가 주어집니다.

**출력 설명**

- 가장 큰 수를 출력합니다.

**입력 예제**

5276823 3

**출력예제**

7823

# 내 해답

- Stack 에 대해서 많이 익숙해진 후 도전해야겠다.

# 다른 답

```python
import sys
sys.stdin=open("input.txt", "rt")
num, m=map(int, input().split())
num=list(map(int, str(num)))
stack=[] # stack 을 만든다.
for x in num: 
    # stack 이 비어있거나
    # m > 0 으로 뺄게 남아있거나 
    # 현재 나보다(x) stack 의 맨 뒤 자료보다 더 크면 끄집어내!
    while stack and m>0 and stack[-1]<x: #앞의 자료가 x 보다 
        stack.pop() # 제일 뒤의 자료를 빼낸다.
        m-=1 # 하나 빼냈으니까 1을 줄여준다.  
    # 위의 조건을 통해 쳐낼건 다 쳐낸 후
    stack.append(x) # x 를 넣어준다.(자기가 들어감)
# 다 지워내도, m 이 남는다면
if m!=0:
    # 뒤쪽의 m 개 자료를 날리게 된다.
    stack=stack[:-m]
res=''.join(map(str, stack))
print(res)
```

- 자기 앞에 자기보다 작은수가 있다면 그것을 지우고 가야한다!
- 52768 이라고 하고, 3개를 지우고싶다고 하자
  - 5 입장에서는 자기 앞에 자기보다 작은애가 없으므로 52768
  - 2도 이하동문 52768
  - 7의 경우 2개가 자기보다 작으므로 768
  - 6의 경우는 그대로 768
  - 8 : 78

- 위 순서대로 지워주면 된다. 이를 stack 으로 구현하면 어떨까?
  - 52768을 고려하자.
  - 5 
  - 52
  - 527 -> pop(2) -> pop(5) -> 7
  - 76
  - 768 -> pop(6) -> 78

