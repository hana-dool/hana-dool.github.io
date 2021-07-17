---
title:  "길이가 정해지지 않은 상태"
excerpt: "DFS 및 재귀"
categories:
  - AL_Others
tags:
  - 1
last_modified_at: 2021-07-17

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

#  Letter Combinations of a Phone Number

![png](/assets/images/Python/14_1.png)

- 위와 같이 얼마나 숫자패드를 누를지 알 수 없어서, for 문을 얼마나 돌릴지 알 수가 없습니다.
- 이러한 경우 구현하는 방법은 DFS 가 대표적이고, 재귀로도 구현할 수 있습니다.

```python
class Solution(object):
    def letterCombinations(self, digits):
        if not digits:
            return []
        results = ['']
        map = {'2': 'abc', '3': 'def', '4': 'ghi', '5': 'jkl', '6': 'mno', '7': 'pqrs', '8': 'tuv', '9': 'wxyz'}
        for nums in digits:
            s = []
            for d in map[nums]:
                for r in results: 
                    s.append(r+d)
            results = s # results 가 계~속 업데이트!
        return results
```

```python
class Solution(object):
    def letterCombinations(self, digits):
        mapping = {'2':'abc','3':'def','4':'ghi', '5':'jkl','6':'mno','7':'pqrs','8':'tuv','9':'wxyz'}
        l = len(digits)
        if l == 0 :
            return []
        ans = []
        def dfs(depth,strng) : 
            if depth == l :
                ans.append(strng)
            else : 
                for i in mapping[digits[depth]] :
                    dfs(depth+1 , strng + i )    # 이건 너무 유명한 DFS라.. 설명생략
        dfs(0,'')
        return ans
```

