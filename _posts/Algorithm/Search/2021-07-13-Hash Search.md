---
title:  "Search"
excerpt: "with Hash"
categories:
  - AL_Search
tags:
  - 1
last_modified_at: 2021-07-13

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 해시를 이용한 서치

| code                    | n = 100000    | n = 1000000   | n = 1000000   | Time Complexity |
| ----------------------- | ------------- | ------------- | ------------- | --------------- |
| x in list               | 0.000494      | 0.019270      | 0.235368      | O(n)            |
| list.index(x)           | 0.000537      | 0.020288      | 0.246275      | O(n)            |
| for a in list: if(a==x) | 0.010289      | 0.107806      | 1.036934      | O(n)            |
| **x in set**            | **0.000002 ** | **0.000002 ** | **0.000006 ** | **O(1)**        |
| list to set             | 0.115826      | 0.066516      | 0.716471      |                 |
| **x in dict**           | **0.000005 ** | **0.000005 ** | **0.000004**  | **O(1)**        |
| list to dict            | 0.147385      | 0.223651      | 2.232983      |                 |

- 위를 보다시피, 해시 (set 또는 dict) 을 이용한 경우 in 연산의 속도가 매우 빠르다.
- 즉 이를 이용하여 Search 를 진행한다면 매우 빠를것이다. 

<br>

# EX1 (2개 값의 합)

- https://leetcode.com/problems/two-sum/

```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].
```

```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

- 해답은 아래와 같다.

```python
class Solution(object):
    def twoSum(self, nums, target):
        dic = dict()
        ans = []
        for i, v in enumerate(nums):
            if target - v in dic:
                ans.extend([dic[target - v], i])
                break
            else:
                dic[v] = i
        return(ans)
```

- 떨어진 후보군들을 'dict' 에 저장한다. 
- 이는 , 중복되는 value 가 없다는것이 확정되어있을때에 쓸 수 있는 방법이다. 문제의 조건에서, 2개의 값을 고르라고 되어있으므로 위와 같이 할 수 있었던 것이다.
