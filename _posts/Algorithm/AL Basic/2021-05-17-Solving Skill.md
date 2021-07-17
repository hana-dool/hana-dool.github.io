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

# sort 를 이용하여 같은경우 제외시키기

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

<br>

# Mapping 을 뺄셈으로 구현하기

```
Symbol        Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

- 위 규칙에 맞게, 수를 받을때 로마자를 출력하는 프로그램을 짜야합니다.

```python
Input: num = 1994
Output: "MCMXCIV"
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

```python
class Solution(object):
    def intToRoman(self, num):
        transform ={1000:'M',900:'CM',500:'D',400:'CD',100:'C',
                    90:'XC',50:'L',40:'XL',10:'X',
                    9:'IX',5:'V',4:'IV',1:'I'}
        ans = ''
        for v,s in transform.items() :
            while num - v >= 0 :
                num = num - v
                ans += s
            if num == 0 :
                break
        return(ans)
```

- 여기서 걸리는 문제점이, '각 자릿수에 맞는 HASH' 테이블을 통해서 매핑하는것까지는 좋지만

  - 각 자릿수에 대해서 매핑하고, 3자리일떄랑 2자리일떄랑 구분하고.. 이런 작업이 귀찮습니다.
  - 하지만 위처럼 "한번에 모든 매핑을 구현" 한 뒤에 큰 값부터 Greedy 하게 매핑하며 값을 줄여나가는 방식으로 한다면 구현이 잘 됩니다. 

  
