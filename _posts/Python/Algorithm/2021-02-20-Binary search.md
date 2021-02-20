---
title:  "이분 검색"
excerpt: "Algorithm"
categories:
  - Py_Algorithm
tags:
  - 3
last_modified_at: 2021-02-20

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

- 문제 및 답 출처 : [링크](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/dashboard)

- 해당 링크에 가시면 훨씬 더 전문적인 해설 및 / 강의를 보실 수 있습니다. 

# 문제

**문제**  

임의의 N 개의 숫자가 입력으로 주어진다. N 개의 수를 오름차순으로 정렬한 다음 N개의 수중 한 개의 수인 M 이 주어지면 이분검색으로 M 이 정렬된 상태에서 몇 번째에 있는지 구하는 프로그램을 작성하라.

단 중복값은 존재하지 않는다.

**입력설명**

- 첫 줄에 자연수 N,M 이 주어진다.

**출력 설명**

- 첫 줄에 정렬 후 M 값의 위치 번호를 출력한다.

**입력 예제**

8 32

23 87 65 12 57 32 99 81

**출력예제**

3

# 내 해답

- 위치번호 출력은 list.index(M) 을 쓰면 되지만, 이 때 문제에서 이진검색을 이용하라고 하였으므로 이 생각은 기각.
- 이진검색시에 조건은 SORTING 이 되어있을것이다. 즉 우선 list.sort 를 통해 정렬하고 난 후, 비교를 통해 M 의 위치를 알아보자.
- 아직 이진탐색이 서툴러서 인터넷 검색을 통해서 힌트를 얻고 진행하였다..

```python
import sys
sys.stdin=open("in2.txt", "r")

N,M = map(int,input().split())
lis = list(map(int,input().split()))

# 오름차순 정렬 해보기
lis.sort()
left = 0
right = N-1

while left <= right :
    mid = (left + right)//2 # 이분탐색이므로 중앙 정의
    if lis[mid] < M :
        left = mid+1
    elif lis[mid] > M :
        right = mid-1
    else :
        ans = mid
        break

print(ans+1)
```

- 시간 복잡도를 N -> log(N) 으로 낮출수 있다!

# 다른 답

```python
import sys
sys.stdin=open("input.txt", "r")
n, m=map(int, input().split())
a=list(map(int, input().split()))
a.sort()
lt=0
rt=n-1
while lt<=rt:
    mid=(lt+rt)//2
    if a[mid]==m:
        print(mid+1)
        break
    elif a[mid]>m:
        rt=mid-1
    else:
        lt=mid+1
```

