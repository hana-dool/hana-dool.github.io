---
title:  "Union_Find Algorithm"
excerpt: "유니온 파인드 알고리즘"
categories:
  - AL_Graph_Tree
tags:
  - 1
last_modified_at: 2021-08-01

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 서로소 집합

![png](/assets/images/Python/19_1.png)

- 서로소 집합은 위와 같이, 서로 겹치는 원소가 없는 집합을 의미합니다. 

![png](/assets/images/Python/19_2.png)

- 위와 같이 서로소 집합 자료구조는, 두 종류의 연산을 지원합니다.

![png](/assets/images/Python/19_3.png)

![png](/assets/images/Python/19_4.png)

- 초기 단계에서는, 각자의 집합은 자기 자신을 노드로 가집니다.

![png](/assets/images/Python/19_5.png)

- 작은것을 루트로 가지도록 사용합니다. (물론 큰것을 루트로 할 수도 있습니다.)

![png](/assets/images/Python/19_6.png)

![png](/assets/images/Python/19_7.png)

- '부모가 다르다는것은' 다른 집합임을 알 수 있습니다. 

![png](/assets/images/Python/19_8.png)

![png](/assets/images/Python/19_9.png)

- 위처럼 연결을 다 끝내고 나면, 연결성을 통해 총 몇개의 그룹이 존재하는지를 알 수 있습니다.

```python
# 특정 원소가 속한 집합 찾기 (경로압축)
def find_parent(parent,x) :
    # parent 에 '연결된 루트' 가 아니라 '제일 깊은 부모' 를 출력함으로서 시간단축
    # 연결된 루트만 표시하면 지렁이 줄줄이로 시간이 엄청 걸릴수도 있다.
    if parent[x] != x : 
        parent[x] = find_parent(parent,parent[x])
    return x 

# 두 원소가 속한 집합 합치기
def union_parent(parent,a,b):
    a = find_parent(parent,a)
    b = find_parent(parent,b)
    if a<b :
        parent[b] = a
    else :
        parent[a] = b 

# 노드의 갯수와 간선(union 연산) 의 갯수 입력
v,e = map(int,input().split())

# 부모 테이블 (자기 자신이 부모)
parent = list(range(v+1))

for i in range(e) : 
    a,b = map(int,input().split())
    union_parent(parent,a,b) 
    
# 각 원소가 속한 집합 출력 
for i in range(1,v+1) :
    print(find_parent(parent,i),end=' ') 
    
# 부모 테이블 내용 출력
# 단순히 부모테이블 내용일 뿐이지, 집합을 표현하는게 아니란것을 명심! 
# 즉 parent 는 의미 없어요... 
print(parent)
```

<br>

# 집합의 표현

- <https://www.acmicpc.net/problem/1717>

```python
import sys
sys.setrecursionlimit(10**9)
input = sys.stdin.readline



n,m = map(int,input().split())
parent = list(range(n+1))

def find_parent(parent,x):
    if parent[x] != x :
        parent[x] = find_parent(parent,parent[x])
    return parent[x]

def union_parent(parent,a,b) :
    if find_parent(parent,a) != find_parent(parent,b) :
        a_p = find_parent(parent,a)
        b_p = find_parent(parent,b)
        if a_p < b_p :
            parent[b_p] = a_p
        else :
            parent[a_p] = b_p

for _ in range(m):
    oper,a,b = map(int,input().split())
    if oper == 0 :
        union_parent(parent,a,b)
    elif oper == 1 :
        if find_parent(parent,a) == find_parent(parent,b) : # 중요!
            print('YES')
        else :
            print('NO')
```

