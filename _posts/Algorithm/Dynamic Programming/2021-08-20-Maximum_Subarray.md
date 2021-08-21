---
title:  "Subarray : Kadane Algorithm"
excerpt: "부분수열"
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

# 가장 큰 부분수열

- https://leetcode.com/problems/maximum-subarray/

```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # search every
        l = len(nums)
        dp = [0] * l
        dp[0] = nums[0]
        for i in range(1,l) : 
            dp[i] = max(dp[i-1] +nums[i] , nums[i])
        return max(dp)
```

- `nums`와 같은 값을 가지는 `dp` 배열을 생성한다.

- 이때, `dp[i]`의 의미는  `nums[i]` 로 끝나는 수열중, 최대값을 의미한다. 

- `nums[i]` 원소에 대해 우리는 2가지 행동을 취할 수 있다.

  1. `nums[i-1]` 원소와 `nums[i]` 원소를 더 하는 것
  2. `nums[i]`를 시작으로 새로운 subarray를 시작하는 것

  이걸 그대로 점화식으로 나타낸다면

  ```python
  dp[i] = max(dp[i-1]+nums[i], nums[i])
  ```

- 위 dp 에서 최대값을 Return 하면 됩니다.

# 가장 큰 Product Subarray

```python
class Solution(object):
    def maxProduct(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        min_dp = [0]*len(nums)
        max_dp = [0]*len(nums)
        min_dp[0] = nums[0]
        max_dp[0] = nums[0]
        for i in range(1,len(nums)):
            min_dp[i] = min(nums[i], max_dp[i-1]*nums[i] , min_dp[i-1]*nums[i])
            max_dp[i] = max(nums[i], max_dp[i-1]*nums[i] , min_dp[i-1]*nums[i]) 
        return max(max_dp)
```

- 위 같이 , Subarray 를 dp 처럼 사용한다면 '시작하는 Subarray' 와 , 여태까지의 dp 를 같이 사용하면 됩니다.
