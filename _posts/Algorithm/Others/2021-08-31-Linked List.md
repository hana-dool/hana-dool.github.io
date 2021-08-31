---
title:  "Linked List 2 "
excerpt: "링크드 리스트 구현"
categories:
  - AL_Others
tags:
  - 1
last_modified_at: 2021-08-31

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 링크드 리스트 구현

### 노드 구현

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
```

### 링크드 리스트 구현

```python
class LinkedList:
    def __init__(self, data):
        self.head = Node(data)
    
    #헤더부터 탐색해 뒤에 새로운 노드 추가하기
    def append(self, data):
        cur = self.head
        while cur.next is not None:
            cur = cur.next
        cur.next = Node(data)
	
    #모든 노드 값 출력
    def print_all(self):
        cur = self.head
        while cur is not None:
            print(cur.data)
            cur = cur.next
```

### 노드 인덱스 알아내기

```python
    def get_node(self, index):
        cnt = 0
        node = self.head
        while cnt < index:
            cnt += 1
            node = node.next
        return node
```

### 삽입

```python
    def add_node(self, index, value):
        new_node = Node(value)
        if index == 0:
            new_node.next = self.head
            self.head = new_node
            return
        node = self.get_node(index-1)
        next_node = node.next
        node.next = new_node
        new_node.next = next_node
```

> `[5] -> [12] -> [8]`를 `[5] -> [6] -> [12] -> [8]` 만들기 위해서 인덱스 1자리인 12에 들어가기 위해 5 노드 위치를 파악하고, 그 다음 next에 6 노드를 연결한다. [6]의 next는 12가 연결되게끔 해야한다.



### 삭제

```python
    def delete_node(self, index):
        if index == 0:
            self.head = self.head.next
            return
        node = self.get_node(index-1)
        node.next = node.next.next
```

- 삭제하는 것은 더 간단한다. `[5] -> [6] -> [12] -> [8]`에서 삭제하고자 하는 index 번 째 노드의 전 노드를 찾아 바로 다음 노드가 될 것을 연결해주면 된다.

=

# 링크드 리스트 Insert 구현

- https://www.hackerrank.com/challenges/30-linked-list/problem?h_r=internal-search
- 문제는 data 를 인자로 받는 새 노드를 만들고 이를 Linked List 맨 뒤에 넣으라는 것입니다.

![png](/assets/images/Algorithm/12.png)

- Class node 는 data 와 next 메서드를 가집니다.
  - data : 데이터 
  - next : 다른 노드 Pointer

```python
class Node:
    def __init__(self,data):
        self.data = data
        self.next = None 
class Solution: 
    def display(self,head):
        current = head
        while current:
            print(current.data,end=' ')
            current = current.next

    def insert(self,head,data): 
    #Complete this method

mylist= Solution()
T=int(input())
head=None
for i in range(T):
    data=int(input())
    head=mylist.insert(head,data)    
mylist.display(head); 	  
```

## 풀이

```python
def insert(self,head,data): 
    if not head : 
        head = Node(data)
    else : 
        current = head 
        while current.next : 
            current = current.next
        current.next = Node(data)
    return head
```

- 연결형 리스트를 구현해야 합니다.  
- Linked LIst 는, 마치 Next 에 node 들이 재귀함수처럼 (또는 마트로슈카 처럼) 주우욱 이어져 있는 형태를 가르킵니다.

<br>

- https://www.hackerrank.com/challenges/print-the-elements-of-a-linked-list/problem?h_r=internal-search

# 링크드 리스트 print 구현

```python
def printLinkedList(head):
    while head :
        print(head.data)
        head = head.next

if __name__ == '__main__':
    llist_count = int(input())

    llist = SinglyLinkedList()

    for _ in range(llist_count):
        llist_item = int(input())
        llist.insert_node(llist_item)
    printLinkedList(llist.head)
```

<br>

# 링크드 리스트 Merge

```python
def mergeLists(headA, headB):
    if headA is None and headB is None:
        return None
    
    if headA is None:
        return headB

    if headB is None:
        return headA
    
    if headA.data < headB.data:
        smallerNode = headA
        smallerNode.next = mergeLists(headA.next, headB)
    else:
        smallerNode = headB
        smallerNode.next = mergeLists(headA, headB.next)
    
    return smallerNode
```

