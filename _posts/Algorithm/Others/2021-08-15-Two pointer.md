---
title:  "Two Pointer"
excerpt: "투 포인터"
categories:
  - AL_Others
tags:
  - 1
last_modified_at: 2021-08-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

- 투 포인터는 기본적으로 아래를 따릅니다.

![png](/assets/images/Python/26_1.png)

- 위와 같이 두개의 포인트(start/end) 를 움직이면서 순회합니다.
- 이 방법이 모든 start,end 를 순회하는것보다 훨씬 시간이 적게듭니다.

# EX : 부분합

![png](/assets/images/Python/27_1.png)

```python
N, S = map(int, input().split())
arr = list(map(int, input().split()))

left, right = 0, 0
tmp_sum = 0
min_length = 10**9

while True:
   if tmp_sum >= S:
       min_length = min(min_length, right - left)
       tmp_sum -= arr[left] # 클떄는 작아져야한다.
       left += 1
   elif right == N: # right 가 idx 이상으로 커졌을때 (모두 고려했다는뜻)
       break
   else:
       tmp_sum += arr[right]
       right += 1

if min_length == 10**9:
   print(0)
else:
   print(min_length)
```

<br>

# 두 용액

- https://www.acmicpc.net/problem/2470

```python
import sys
input = sys.stdin.readline
n = int(input())
lst = sorted(list(map(int, input().split())))

start = 0
end = len(lst) - 1
mn = [10**12,0,0]
while start < end :
    val = lst[end] + lst[start]
    mn = min([abs(val),lst[start],lst[end]],mn,key = lambda x : x[0])
    if val == 0  :
        print(lst[start],lst[end])
        break
    if val > 0 : # 너무 크니까 end 가 줄어라
        end -= 1
    if val < 0 :
        start += 1
print(*(mn[1],mn[2]))
```

