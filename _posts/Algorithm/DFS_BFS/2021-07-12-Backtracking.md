---
title:  "[DFS] 백트래킹"
excerpt: "N-Queen"
categories:
  - AL_DFS_BFS
tags:
  - 1
last_modified_at: 2021-07-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 문제

- N-Queen 문제는 크기가 N × N인 체스판 위에 퀸 N개를 서로 공격할 수 없게 놓는 문제이다.
- N이 주어졌을 때, 퀸을 놓는 방법의 수를 구하는 프로그램을 작성하시오.
- <https://www.acmicpc.net/problem/9663>

```python
n = int(input())
cnt = 0
def dfs(lst):
    global cnt
    
    if len(lst) == n :# 중단부
        cnt += 1 # 출력부 
        return
    
    ### 가지치기부 ** 백트래킹의 핵심
    candidate = list(range(n))
    for i in range(len(lst)):
        if lst[i] in candidate :
            candidate.remove(lst[i])
        if lst[i] + len(lst) - i  in candidate :
            candidate.remove(lst[i] + len(lst) - i)
        if lst[i] - len(lst) + i in candidate :
            candidate.remove(lst[i] - len(lst) + i)
            
            
    if candidate: # 재귀부 
        for x in candidate :
            lst.append(x)
            dfs(lst)
            lst.pop()

for i in range(n):
    dfs([i])
print(cnt)
```

<br>

- 위와 같이, 체스판 N 개 위에 무턱대고 DFS 를 하기에는 너무 경우의 수가 많다.
- 즉 DFS 를 적용하기 전에, 후보군에 대해 가지치기를 하는것이 백트래킹이라 한다.



# Generate Parentheses

- Given `n` pairs of parentheses, write a function to *generate all combinations of well-formed parentheses*.

**Example 1:**

```
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```

- 늘 (  가 ) 보다 많아야 하고, 마지막에 ( 와 ) 의 합은 같아야 함을 알 수 있습니다.

```python
# 약한 뺵트래킹
class Solution(object):
    def generateParenthesis(self, n):
        ans = []
        def dfs(depth,S) : 
            if depth == 2*n :
                if S.count('(') == S.count(')') :
                    ans.append(S)
                return 
            cnt_1 = S.count('(')
            cnt_2 = S.count(')')
            if cnt_1 > cnt_2 :
                dfs(depth+1,S + '(')
                dfs(depth+1,S + ')')
            else : 
                dfs(depth+1,S + '(')
        dfs(0,'')
        return ans
```

- 위와 같이,  ( 와 ) 를 Count 한 뒤에, (  가 많은 경우만 ) 를 추가하는 형식으로 한 뒤 마지막에 ( 의 수 = ) 의 수가 되게 할 수 있습니다. 
- 하지만 위의 경우도 Count 가 있기때문에 효율성면에서 좋지 않습니다. 

```python
# 강한 백트래킹
class Solution(object):
    def generateParenthesis(self, n):
        ans = []
        def dfs(depth,S,left,right) :
            if depth == 2*n : # 중단부
                if S.count('(') == S.count(')') :
                    ans.append(S) # 출력부
                return
            if left > n : # 뺵트래킹부
                return
            if left > right : # 조건부
                dfs(depth+1,S + '(',left+1,right ) # 재귀부
                dfs(depth+1,S + ')',left  ,right+1)
            else :
                dfs(depth+1,S + '(',left+1,right)
        dfs(0,'',0,0)
        return ans
```

- 위와 같이 ( 의 수를 Left 로, ) 의 수를 Right 로 정의한 다음 DFS 를 해주었습니다.
- 그러면, 위와 같이 뺵트래킹부 (가지치기부) 가 생겨나서, 중간중간, 조건에 맞지 않으면 중단하는 부분을 추가해 너무 늘어나지 않게 조절하였습니다.
- 위와 같이 가지치키를 하면 성능이 2배 증가합니다.
- 즉! 가지치기가 들어갈 부분을 변수로 놓아서, 가지치기가 가능하게 해줍시다!!! 

