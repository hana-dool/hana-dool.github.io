---
title:  "Dictionary 와 List"
excerpt: "해시로 사용할 수 있는 자료형"
categories:
  - AL_Hash
tags:
  - 1
last_modified_at: 2021-06-07

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

- 우리는 일반적으로 해시를 구현하라고 하면 List 와 dictionary 를 생각합니다. 
  - dictionary 는 key 와 value 를 통하여 구현할 수 있습니다.
    - 이 경우에는 string 을 받더라도 갯수를 셀 수 있다는 장점이 있습니다.
  - list 는 index 와 value 를 통하여 hash 를 구현할 수 있습니다.
    - dict 는 '값을 입력 받는 순서대로' key 가 정렬되는 단점이 있습니다.
    - 그러므로 '값이 증가하는 순서대로' 몇개가 있었는지 출력하라 같은 문제는 풀 수 없습니다. 
    - 이러한 경우 list 를 사용한다면 이미 index 별로 정렬되더있는 상태이기 떄문에 쉽게 풀립니다.
- 해시도 어떤 자료형을 사용할지 잘 정해야 합니다.

# 수 정렬하기 (List 사용)

![png](/assets/images/Algorithm/8.png)

```python
import sys
input = sys.stdin.readline
N = int(input())
lst = [0]*10001

for _ in range(N):
    val = int(input())
    lst[val] += 1
for i in range(1,10001) :
    if lst[i] != 0 :
        for _ in range(lst[i]) :
            print(i)
```

- 그냥 list 로 모든 입력을 받고 sort 로 해결하려다간 메모리 초과에 걸리게 된다. 
- 그러므로 위와 같이 list 를 hash 처럼 이용하여 풀어야 한다.
  - dictionary 를 써도 안된다...! 
  - dict 를 쓰게되면 입력되는 순서대로 정렬이 되기떄문에 모든 input 을 받고나서 다시 한번 key 값대로 정렬을 해주어야 한다.
