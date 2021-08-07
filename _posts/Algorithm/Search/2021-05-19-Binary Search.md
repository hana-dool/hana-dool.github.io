---
title:  "이분탐색"
excerpt: "Binary Search"
categories:
  - AL_Search
tags:
  - 1
last_modified_at: 2021-05-19

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# <center><font size="15"> 이진탐색 </font></center>

- 이진탐색은 '정렬된' 리스트의 중간부터 비교해나가는 방법이다.

- 이진검색시에는 다음과 같은 경우의 수가 있다.

  - Key가 리스트의 중간값보다 작으면, 중간 이전까지만 찾으면 된다.

  - Key가 리스트의 중간값과 일치한다면, 검색이 끝난다. 
  - Key 가 리스트의 중간값보다 크다면 중간 이후만 검색하면 된다.

```python
start = 0 
end = len(lst) - 1 

while start <= end :
    mid = (start + end)//2
    if lst[mid] == xx : # 같은게 딱! 나오면
        print(mid) # 출력하고
        break # 멈추기
    elif lst[mid] < xx :
        start = mid + 1 # -1 +1 이런거 없으면 start = mid , mid = end 같은 경우에 참사난다. 
    elif lst[mid] > xx :
        end = mid - 1 # +1 안넣으면 001 경우 대참사
```

- 위와 같이 구현될 수 있다. 

<BR>

<br>

# <center><font size="15"> 값이 없는경우 탐색 </font></center>

```python
start = 0 
end = len(lst) - 1 

ch = 0
while start <= end :
    mid = (start + end)//2
    if lst[mid] == xx : # 같은게 딱! 나오면
        print(mid) 
        ch = 1
        break # 멈추기
    elif lst[mid] < xx :
        start = mid +1 
    elif lst[mid] > xx :
        end = mid - 1 
    print(start, mid, end)
if ch == 0 :
    print('값이없오')
```



<br>

<br>

# <center><font size="15"> 처음 값 탐색 </font></center>

```python
start = 0 
end = len(lst) - 1

while start <= end: # end 가 선 넘을떄 정지
    mid = (start + end) // 2
    if lst[mid] == xx:
        end = mid - 1  # 같더라도 내려가는게 핵심
    elif lst[mid] < xx:
        start = mid + 1 # 같은것 찾아!
    elif lst[mid] > xx :
        end = mid - 1 # 같은것 찾아!
print(start) # end 가 선 넘었다는건? start 가 맞다는거.
```

```python
lst = [1,2,3,3,3,3,4,4,5,6,7] ,xx = 3
print(start) # 2
print(end) # 1
```

- 중복된 값을 찾게 될 때에, start 는 처음 만나게 되는 인덱스를 출력합니다.
  - 그 이유는, end 가 같은 경우에도 계속 작아지면서 선을 넘고있기 때문입니다. 

```python
lst = [1,2,3,3,3,3,4,4,5,6,7] ,xx = 3.5
print(start) # 6 
print(end) # 5
```

- 없는 값을 찾게 될 때에, start 그 값보다 큰, 처음 만나게 되는 인덱스를 출력합니다.
  - 기본적으로, 모든 이분탐색은 아래와 같이, 3.5 를 찾는 상황이라 합시다.

| 3     | 4    | 5    |
| ----- | ---- | ---- |
| start | mid  | end  |

| 3         | 4    | 5    |
| --------- | ---- | ---- |
| start,end | mid  |      |

| 3             | 4    | 5    |
| ------------- | ---- | ---- |
| start,end,mid |      |      |

| 3       | 4     | 5    |
| ------- | ----- | ---- |
| mid,end | start |      |

- 모든 상황을 설명하기는 힘들겠지만, 기본적으로 , 이분탐색시, mid 는 (start + end) // 2여서 기본적으로 왼쪽 (START쪽) 으로 치우칩니다.
  - 즉 그렇다면, 값이 작을 확률이 높아져 기본적으로 start 가 왔다갔다 하고 위처럼 start 가 선을 넘게 되는것입니다. 

<br>

<Br>

# <center><font size="15">마지막 값 탐색 </font></center>

- 값이 나타나는 값 중에서 제일 처음값을 출력한다.
- lst = [1,3,3,3,5] 인 경우 3을 찾는다면 idx 3 을 출력한다.

```python
start = 0 
end = len(lst) - 1 

while start <= end: # start 가 선 넘을떄 정지 
    mid = (start + end) // 2
    if lst[mid] == xx: # 이 경우 같다 하더라도 올라가는게 핵심
        start = mid + 1
    elif lst[mid] < xx: 
        start = mid + 1  # 같은것 찾아! 
    elif lst[mid] > xx:
        end = mid - 1 # 같은것 찾아!
# end 가 멈춰서서, start 가 맞춰주는 느낌이네요. 그러므로 end를 출력하는게 맞죠 (start 가 변하다가 end를 넘어버릴떄 중지하니까요)
print(end)
```

- '마지막 값' 을 얻고싶다면 위와 같이 같을때에 start 값이 올라가게 해주면 됩니다. 
  - 그리고 end 를 출력하면 됩니다. 

```python
lst = [1,2,3,3,3,3,4,4,5,6,7] ,xx = 3
print(start) # 6
print(end) # 5
```

- end 를 해줘야 '마지막' 을 출력 가능합니다.
  - 왜냐하면 위를 보면 같을떄 start 가 선넘으면서 증가하기 떄문

```python
lst = [1,2,3,3,3,3,4,4,5,6,7] ,xx = 3.5
print(start) # 6 
print(end) # 5
```

- 없는 값을 찾게 될 때에, start 그 값보다 큰, 처음 만나게 되는 인덱스를 출력합니다. 
  - 위와 같은 이유는, 어짜피 == 일떄는 고려하지 않기 떄문
- 즉 정리하자면 위의 로직은 다음과 같은 값을 뱉는다.

> 1.값이 하나 존재하면 Exact  한 그 위치 
>
> 2.값이 여러개 존재하면 마지막 위치 
>
> 3.값이 없으면 그 값보다 작은 마지막 위치 

<br>

# Lower bound 이진탐색

![png](/assets/images/Python/22_1.png)

![png](/assets/images/Python/22_2.png)

- 위와 같이 Lower bound 와 Upper bound 는 차이가 난다. 

```python
lst = [1,2,3,3,3,3,4,4,5,6,7]
xx = 3
start = 0
end = len(lst)-1
while start < end :
    mid = (start + end) // 2
    if lst[mid] >= xx :
        end = mid # 같은경우에도 작아지는게 핵심 
    elif lst[mid] < xx : 
        start = mid + 1 # 작은경우는 커져야함
print(start) 
```

```
lst = [1,2,3,3,3,3,4,4,5,6,7] 에 대해서 
xx = 3 : 2 
xx = 3.5 : 6
```

- 우리가 원하는 output 임을 알 수 있습니다. 

# Upper bound 이진탐색

```python
lst = [1,2,3,3,3,3,4,4,5,6,7]
xx = 3
start = 0
end = len(lst)-1
while start < end :
    print(start,end,xx)
    mid = (start + end) // 2
    if lst[mid] <= xx :
        start = mid+1   # 같더라도, 커지는게 핵심
    elif lst[mid] > xx : 
        end = mid 
print(start) # 위의 경우 start 가 막 변하면서 맞춰지는거니까 end
```

```python
lst = [1,2,3,3,3,3,4,4,5,6,7] 에 대해서 
xx = 3 : 6
xx = 3.5 : 6
```

- 우리가 원하는 결과를 얻을 수 있다.

<br>

# 함수와 결합

- 사실 그냥 이진탐색이 이용되는 경우는 드물다.
  - 왜냐하면 이진탐색은 그저 '값에 맞는 인덱스' 를 찾아주는 역할을 하기 때문이다.
- 실제 문제에서는 이와 같지 않다는것을 알아두자.
- <https://www.acmicpc.net/problem/2805>

```python
import sys
read = sys.stdin.readline

N,M = map(int,read().split())
lst = list(map(int,read().split()))


def cal(x):
    val = 0
    for i in lst:
        if i-x > 0:
            val += (i-x)
    return(val)

# M 이 우리의 기준이 된다.

start = 1
end = max(lst)

while start <= end : 
    mid = (start + end)//2
    val = cal(mid)
    if M == val :
        start = mid + 1 
    elif M < val : 
        start = mid + 1
    elif M > val : 
        end = mid - 1
print(end)
```

- 위와 같이 '함수' 를 정의한뒤 이분탐색에 이용하였다. 

