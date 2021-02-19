---
title:  "카드 역배치"
excerpt: "Algorithm"
categories:
  - Py_Algorithm
tags:
  - 3
last_modified_at: 2021-02-19


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

![png](/assets/images/{Algorithm}/1_1.jpg)

**입력설명**

- 총 10개의 줄에 걸쳐 하나씩 10개의 구간이 주어진다. i 번째 줄에는 i 번째 구간의 시작 위치 a_i 와 끝 위치 b_i 가 차례대로 주어진다. 이때 두 값의 범위는 $ 1 <= a_i <= bi <= 20 $ 이다.

**출력 설명**

- 1부터 20까지 오름차순으로 놓인 카드들에 대해 입력으로 주어진 10개의 구간대로 뒤집는 작업을 했을 때 마지막 카드들의 배치를 한 줄에 출력한다.

**입력 예제**

5 10

9 13

.... (10개의 2개 숫자쌍)

**출력예제**

1 2 3 4 10 9 8 7 13 12 11 5 6 14 15 16 17 18 19 20



# 내 해답

```python
import sys
sys.stdin=open("in1.txt", "r")

lis = list(range(1,21))
for repeat in range(10):
    start,end = map(int,input().split())
    # start-1 부터 end-1 까지의 값을 end-1 ~ start-1 로 읽은 값으로 대체
    reverse_list = lis[start-1:end]
    reverse_list.reverse()
    lis[start-1:end] = reverse_list
print(lis)
```

- 이 때에 주의해야할 점은  lis[start-1:end] =  lis[start-1:end].reserse() 처럼 assign을 직접 하려고 한다던가  lis[start-1:end].reverse() 로 부분만 inplace 하게 바꾸려고 하는 등의 행위는 먹히지 않는다는것이다!



# 답지

```python
import sys
sys.stdin=open("input.txt", "r")
a=list(range(21))
for _ in range(10):
    s, e=map(int, input().split())
    for i in range((e-s+1)//2):
        a[s+i], a[e-i]=a[e-i], a[s+i]
a.pop(0)
for x in a:
    print(x, end=' ')
```

- 나처럼 list methods 를 쓰지 않고, 위와 같이 change 하는 방식으로 없앴다
- 또 이때 좋은 trick 이 하나가 있는데, list indexing 시에 헷갈림을 방지하기 위해 range(21) 을 이용함으로서 [0,1....20] 으로 index 가 1 이면 첫번째 값을 나타나게 된다! 
- 이를 통해서 start , end 의 indexing 을 바로 이용하여 값들을 바꾸어줌
- 그 이후 pop 을 통해 0 제거