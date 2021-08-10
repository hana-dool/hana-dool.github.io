---
title:  "사전순 정렬"
excerpt: "lexicographically Order"
categories:
  - AL_Others
tags:
  - 1
last_modified_at: 2021-08-08

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 다리를 지나는 트럭

- s 는 단어 'abcsef' 가 들어갑니다.
- return 은 그 다음 사전순으로 큰 단어가 들어갑니다.

```
# 5 7 3 6 4 2 1  : 맨 뒤의 값부터 바꿀것을 선택 (start)
#### 3 을 선택했다 하자.  
# 5 7 3 6 4 2 1  : 선택한 값에 의해서, 맨 뒤의 값부터 탐색 (end)
#### 3>1 / 3>2 / 3<4 즉 3과 4 바꾸기
# 5 7 4 6 3 2 1  : 이제 나머지 lst 를 오름차순 정렬해 붙입니다.
# 5 7 4 1 2 3 6 
```

```python
def biggerIsGreater(w):
    l = len(w)
    w = list(w)
    for start in range(l)[::-1]: 
        for end in range(start+1,l)[::-1]: 
            if w[start] < w[end] :
                w[start],w[end] = w[end],w[start]
                ans = w[:start+1] + sorted(w[start+1:])
                return ''.join(ans)
    return 'no answer'
```

- 겁나 유용합니다...
- '바로 그다음' lexitropical 을 뽑아내는..
