---
title:  "large sum : Knapsack algorithm"
excerpt: "합이 최대가 되게 하는 알고리즘"
categories:
  - AL_Dynamic_Programming
tags:
  - 1
last_modified_at: 2021-08-20

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 가방에 최대값이 되게 넣기

- https://velog.io/@jiffydev/algo-78

```python
if __name__=="__main__":
    n, m=map(int, input().split())
    # 0~무게제한만큼의 리스트를 0으로 초기화
    dy=[0]*(m+1);
    # 보석의 종류만큼 반복문
    for i in range(n):
        # 보석의 무게와 가치를 각각 w,v에 할당
        w, v=map(int, input().split())
        # 보석의 무게부터 시작해서 무게제한까지 반복문
        for j in range(w, m+1):
            # 무게 w의 보석을 넣고 남는 공간이 있고, 그 공간을 채울 보석이 있다면 더해서 기존 dy[j]와 비교해서 큰 것을 넣는다
            dy[j]=max(dy[j], dy[j-w]+v)
    print(dy[m])
```
