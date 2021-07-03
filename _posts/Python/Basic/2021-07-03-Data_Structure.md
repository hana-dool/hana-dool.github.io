---
title:  "자료구조"
excerpt: "기본적인 자료구조"
categories:
  - Py_Basic
tags:
  - 4
last_modified_at: 2021-07-03

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math : true
---

## Stack

- 데이터의 삽입과 삭제가 저장소의 맨 윗부분에서만 일어나는 자료구조이다.
- LIFO (Last in , First out) 으로서, 데이터가 순서대로 저장되고 스택의 마지막에 넣은 요소가 처음으로 꺼내진다. 
- 후입 선출로서, 너무나도 불공평한 방식이다 ㅜㅜ

**4가지 기능**

- **pop()** : 맨 마지막의 데이터를 가져오며 지우기
  - .pop()
- **push()** : 새로운 데이터를 맨 위에 하나 쌓기
  - .append()
- **peek()** : 맨 마지막 데이터를 보는것
  - x[-1]
- **isempty()** : 스텍에 데이터가 있는지 없는지 확인
  - not [] 으로, 비어있으면 True 출력

**기본활용**

- list 자료형에 대해서 for 문을 활용하여 각 element를 Stack 에 쌓는지 마는지를 조건문을 통해 결정한 뒤, Stack 을 완성할 수 있다.

## Queue

- 큐(queue)는 선입선출, FIFO(First In First Out) 의 자료구조이다.
- 즉 먼저 들어온 데이터가 먼저 나간다. 이제야 좀 공평해진거같네!
- 이 구현은 collections 의 deque 에서 해결할 수 있다.
- 사실 list 에서 list.pop(0) 으롬도 선입선출을 구현할 수 있다.

## Hash

- 키와 그에 해당하는 Value 값을 가지는 자료구조.
- 파이썬에서는 Dictionary 를 쓰면 된다.
