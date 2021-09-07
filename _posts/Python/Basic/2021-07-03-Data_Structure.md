---
title:  "자료구조"
excerpt: "기본적인 자료구조"
categories:
  - Py_Basic
tags:
  - 4
last_modified_at: 2021-09-07

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math : true
---

# 1. Array List

- 크기가 가변적으로 변하는 선형 리스트 (배열을 사용하는 선형 자료구조)
  - 인덱스로 접근이  가능합니다.

![png](/assets/images/Python/28_1.png)

![png](/assets/images/Python/28_2.png)

- 위 그림과 같이, 중간에 데이터를 넣었다가 / 뺐다가 를 하면 모든 데이터가 이동해야한다. 
- 즉 빈번한 삭제 / 삽입 이 이루어질때에는 매우 비효율적입니다.

<br>

# 2. Linked List 

- 서로 멀리 떨어져있는 메모리 공간을 포인터를 사용해 연결해놓은 자료 구조 

![png](/assets/images/Python/28_3.png)

- 빈번한 삭제 / 삽입을 시행할떄에 매우 효율적입니다.
- 연결 리스트의 가장 기본적인 구조는 이와 같다. 
- 리스트의 요소 하나를 노드(Node)라고 부르는데, 구조체로 만들어 진다. 
- 여기에는 데이터를 저장하는 부분과 다음 노드를 가리키는 포인터가 들어있다.

## Simple Linked List (단순 연결 리스트)

- 이전 노드 안에 있는 포인터가 다음 노드를 가르키는 구조 
- 마지막 노드의 Link 는 NULL 을 가르킵니다.
- 이때에 뒤로 돌아갈 수 없습니다.

 ![png](/assets/images/Python/28_4.png)

## Circular Linked List (원형 연결 리스트)

![png](/assets/images/Python/28_5.png)

## Doubly Linked List

![png](/assets/images/Python/28_7.png)

- 좋은점은 양방향으로 연결되어있기 떄문에, 노드를 탐색하는 방향이 양쪽으로 가능하다는 것입니다.

**단점**

- 이전 노드를 지정하기 위한 변수를 하나 더 사용해야 합니다. 메모리를 더 많이 사용한다는 의미입니다. 
- 구현이 어려워집니다. 

**장점**

- 양방향으로 탐색이 가능하기때문에 , 탐색 속도가 매우 효율적이 됩니다.

<br>

# 3. Stack

![png](/assets/images/Python/28_8.png)

- 데이터의 삽입과 삭제가 저장소의 맨 윗부분에서만 일어나는 자료구조이다.
- LIFO (Last in , First out) 으로서, 데이터가 순서대로 저장되고 스택의 마지막에 넣은 요소가 처음으로 꺼내진다. 
- 후입 선출방식으로 이루어집니다.

**4가지 기능**

- **pop()** : 맨 마지막의 데이터를 가져오며 지우기
  - .pop()
- **push()** : 새로운 데이터를 맨 위에 하나 쌓기
  - .append()
- **peek()** : 맨 마지막 데이터를 보는것
  - x[-1]
- **isempty()** : 스텍에 데이터가 있는지 없는지 확인
  - not [] 으로, 비어있으면 True 출력

# 4. Queue

![png](/assets/images/Python/28_9.png)

- 큐(queue)는 선입선출, FIFO(First In First Out) 의 자료구조이다.
- 즉 먼저 들어온 데이터가 먼저 나간다.
  - 이 구현은 collections 의 deque 에서 해결할 수 있다.
  - 사실 list 에서 list.pop(0) 으롬도 선입선출을 구현할 수 있다.

## 우선순위 큐(HEAP)

- 들어간 순서에 상관 없이, 우선순위가 높은 데이터가 먼저 나옵니다.
- 우선순위 큐는 heap 으로 구현이 가능 

# 5. Heap

- 완전 이진트리의 일종으로 우선순위 큐를 위해서 만들어진 자료 구조
- 여러개의 값들 중에서 최댓값 / 최소값을 빠르게 찾아내도록 만들어진 자료구조이다. 
- 힙은 일종의 반 정렬 상태를 유지한다. 
  - 큰 값이 상위 / 작은값이 하위 레벨에 있는 상태만 유지. (Max Heap의 경우)
  - List 가 굳이 뺵뺵하게 정렬되어 있지 않다는 뜻입니다.

![png](/assets/images/Python/28_11.png)

- 힙에 삽입 / 삭제하고 나면 트리의 높이만큼 연산이 일어나므로 $log(N)$ 의 복잡도를 가짐

## 삽입시 

![png](/assets/images/Python/28_12.png)

# 6. Hash

![png](/assets/images/Python/28_13.png)

- 키와 그에 해당하는 Value 값을 가지는 자료구조.
- 파이썬에서는 Dictionary 를 쓰면 된다.

# 7. Deque

![png](/assets/images/Python/28_14.png)

- 양쪽에서 삽입 / 인출이 가능한 특성을 가지고 있습니다. 
- 두개의 포인터를 가지고있어서 양쪽에서 접근이 가능합니다.

# Refer

- https://gdtbgl93.tistory.com/35?category=773199
- https://chanhuiseok.github.io/posts/ds-4/
- https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html
