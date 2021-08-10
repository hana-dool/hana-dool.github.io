---
title:  "이분탐색 2"
excerpt: "Binary Search"
categories:
  - AL_Search
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

# 이분탐색 

- <https://www.hackerrank.com/challenges/climbing-the-leaderboard/problem?isFullScreen=true>

```python
import bisect

n = int(input())
scores = sorted(set(map(int,input().split())))

m = int(input())
alice = list(map(int,input().split()))

# your code goes here
for i in alice:
    print(len(scores)+1-bisect.bisect_right(scores,i))
```

