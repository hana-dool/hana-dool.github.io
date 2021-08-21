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

# Find First and Last Position of Element in Sorted Array

Given an array of integers `nums` sorted in ascending order, find the starting and ending position of a given `target` value.

If `target` is not found in the array, return `[-1, -1]`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

**Example 2:**

```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

**Example 3:**

```
Input: nums = [], target = 0
Output: [-1,-1]
```

- 위에 대한 해답은 아래와 같다
- 물론 , 이렇게 짜게되면 결국 나중에 질문을 받을수도... (라이브러리만 쓰면 안되죠...)

```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        if not nums:
            return [-1, -1]

        left, right = bisect.bisect_left(nums, target), bisect.bisect_right(nums, target)
        return [left, right - 1] if left < right else [-1, -1]

```

- bisect 의 경우, 값이 없다면 left 와 right 의 값이 같다. "기억!"
