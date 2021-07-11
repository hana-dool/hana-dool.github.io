---
title:  "7.Solving Stratige"
excerpt: "팁팁"
categories:
  - AL_Basic
tags:
  - 1
last_modified_at: 2021-07-04

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# String

- 주어진 String 에 대해서, 같은 element 로 구성된 Substring 의 갯수와 종류를 모두 구해보자.

- abba -> {a,a} ,{b,b} ,{ab,ba}, {abb,bba} -> 2,2,2,2 처럼 구해지길 원한다. 

```python
def find_str(s):
    total = 0
    dic = {}
    for i in range(0, len(s)): # 시작점
        for j in range(1,len(s)-i+1): # 끝점
            strng = ''.join(sorted(s[i:i+j]))
            dic[strng] = dic.get(strng,0)  + 1
    return dic
```

- 위처럼 Substring 을 순회하는 for 문을 작성하자.
- 그 이후에 sorted 를 이용하여, ab=ba 처럼 같은 경우를 표현하였다. 
- Hackerrank 의 Sherlock and Anagrams 참조

