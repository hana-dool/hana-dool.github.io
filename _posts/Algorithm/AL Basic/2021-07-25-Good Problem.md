---
title:  "좋은문제"
excerpt: "좋다고 생각되는 문제모음"
categories:
  - AL_Basic
tags:
  - 1
last_modified_at: 2021-07-25

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# Programmers

- <https://programmers.co.kr/learn/courses/30/lessons/42885>

- <https://programmers.co.kr/learn/courses/30/lessons/42883>
  - 큰수 만들기.. 유명한 문제 + Stack 활용

```python
def solution(number, k):
    stack = [number[0]]
    for num in number[1:]:
        while len(stack) > 0 and stack[-1] < num and k > 0:
            k -= 1
            stack.pop()
        stack.append(num)
    if k != 0:
        stack = stack[:-k]
    return ''.join(stack)
```

