---
title:  "양방향으로 바라보기"
excerpt: "Start and End"
categories:
  - AL_Others
tags:
  - 1
last_modified_at: 2021-08-12

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 증가하는 연속 수열

![png](/assets/images/Algorithm/6.png)

- 위와 같이 단조증가/ 단조감소하는 수열중에서 최대 길이를 출력하는 문제이다. 

```python
N = int(input())
lst = list(map(int,input().split()))
l = len(lst)

# 점점 증가하는 수열을 탐색
mn = 0
length = 0
ans = []
for i in range(l) :
    if mn <= lst[i] :
        mn = lst[i]
        length += 1
    else :
        mn = lst[i]
        ans.append(length)
        length = 1
ans.append(length)

# 점점 감소하는 수열을 탐색
mx = 0
length = 0
for i in range(l) :
    if mx >= lst[i] :
        mx = lst[i]
        length += 1
    else :
        mx = lst[i]
        ans.append(length)
        length = 1
ans.append(length)
print(max(ans))
```

- 위와 같이 점점 증가 / 같소하는 수열을 한번에 구하려고 하지 말고 나누어서 for 문을 돌리면 매우 쉽게 구할 수 있습니다. 
- 문제를 볼때에 중요한것은 굳이 한번에 구하려 하지 말고 나눌 수 있는것은 나누는게 좋다는것입니다.

