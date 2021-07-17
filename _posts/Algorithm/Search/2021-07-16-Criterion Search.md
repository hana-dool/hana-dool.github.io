---
title:  "Pointer 기준 다르게보기"
excerpt: "발상의 전환"
categories:
  - AL_Search
tags:
  - 1
last_modified_at: 2021-07-16

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

#  Longest Palindromic Substring

- Given a string `s`, return *the longest palindromic substring* in `s`.

```
Input: s = "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

- 무식하게 생각하면, 시작점 i 와 끝점 j 를 생각하게 된다. 
- 하지만 아래와 같이, '길이' 와 '시작점' 을 기준으로 삼는다면 좀 더 문제가 쉬워진다.

```python
class Solution(object):
    def longestPalindrome(self, s):
        l = len(s)
        mx = 0
        for j in range(l,0,-1): # j 는 길이가 된다.
            for i in range(l):
                if i+j <= l :
                    strng = s[i:i+j]
                    if strng == strng[::-1]:
                        print(strng)
                        rst = strng
                        return(rst)
```

<br>

# Container With Most Water

![png](/assets/images/Python/13_1.png)

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```

- 위 문제를 처음 시작점과 마지막 지점으로 완전탐색을 하면 시간초과가 난다.

- Height 를 기준으로 잡고 탐색해도 마찬가지
- 시간을 줄이기 위해서는, 처음과 마지막 지점으로 완전탐색을 하되, 양 끝에서 조여오는 형식으로 서치를 해야한다. 
- 대단..

<br>

# 3 Sum Closest

- Given an array `nums` of *n* integers and an integer `target`, find three integers in `nums` such that the sum is closest to `target`. Return the sum of the three integers. You may assume that each input would have exactly one solution.

```
Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

```python
class Solution(object):
    def threeSumClosest(self, nums, target):
        nums.sort()
        l = len(nums) 
        ans = []
        mn = 99999999
        temp = 0 
        for mid in range(1,l-1):
            start = mid - 1 
            end = mid + 1 
            while end <= l-1 and start >= 0:
                if nums[start] + nums[mid] + nums[end] > target :
                    if mn > abs(nums[start] + nums[mid] + nums[end] - target) :
                        mn = abs(nums[start] + nums[mid] + nums[end] - target)
                        temp = nums[start] + nums[mid] + nums[end]
                    start =start -1
                elif nums[start] + nums[mid] + nums[end] < target :
                    if mn > abs(nums[start] + nums[mid] + nums[end] - target) :
                        mn = abs(nums[start] + nums[mid] + nums[end] - target)
                        temp = nums[start] + nums[mid] + nums[end]
                    end =end + 1 
                else : 
                    return target
        return(temp)
```

- 위처럼, mid 를 고정한 상태에서 start 와 end 가 조금씩 움직이는 형태를 택하였다.
- 그러기 위해서, sort 를 먼저 한 이후에,min를 고정한 상태에서 target 보다 작으면 end가 1씩 상승/ target 보다 크면 start 가 1씩 줄어드는 형태를 택하였다. 
- P

