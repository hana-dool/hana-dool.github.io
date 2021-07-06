---
title:  "Queue, deque"
excerpt: "큐와 덱"
categories:
  - Py_Basic
tags:
  - 4
last_modified_at: 2021-07-07

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# Queue

- Queue : 줄을 서서 기다리다. 
- 큐는 한쪽 끝에서는 삽입 연산만 이루어지고, 한쪽 끝에서는 삭제 연산만 일어나는 리스트이다. 

![png](/assets/images/Python/2_1.png)

- 먼저 집어넣은 데이터가 먼저 나오는 FIFO (Firtst in , First Out) 의 구조로 되어있다. 
- 데이터가 입력된 시간 순서대로 처리해야할 때에, 이용된다. 
- 큐의 종류는 다음과 같다. 
  - 선형(큐)
    - 크기 제한
    - 빈 공간을 사용하려면 모든 자료를 꺼내거나 자료를 한 칸씩 옮김
  - 원형(큐)
    - 선형 큐의 문제점을 보완
    - front가 큐의 끝에 닿으면 큐의 맨 앞으로 자료를 보내어 원형으로 연결하는 방식

## 파이썬에서는?

- 파이썬에서는 딱히 큐를 지원하지 않는다. 리스트가 큐의 모든 연산을 지원한다. 

# deque

- 보통 큐는 선입 선출 방식으로 일어난다. 
- 반면에 , 양방향 큐가 있는데, 이를 바로 데크 (deque) 라고 한다. 
- 즉 앞, 뒤 양쪽 방향에서 Element 를 추가하는것에 최적화된 연산속도를 자랑합니다. 

- 양 끝 Element 에 접근하여 삽입 / 제거하는데에 O(1) 의 시간밖에 소요되지 않습니다.



## 파이썬에서는?

```python
from collections import deque
```

- 위와 같이 deque 를 지원합니다.
