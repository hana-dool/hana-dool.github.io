---
title:  "Linked List"
excerpt: "외국 사이트에서 나오는 문제"
categories:
  - AL_Others
tags:
  - 1
last_modified_at: 2021-08-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

- Linked List 문제는 주로 한국에서는 나오지 않는 문제입니다. 
  - 파이썬에 기본적으로 구현되어있지 않기 때문입니다.
- 하지만 해커랭크 / leetcode 에 가끔 나오는 문제로 풀어보는것이 중요하다고 생각합니다.

# Linked List 에서 insert 구현하기

- https://www.hackerrank.com/challenges/30-linked-list/problem?h_r=internal-search

```python
class Node:
    def __init__(self,data):
        self.data = data
        self.next = None # None 인 이유는 우리가 지정하라는거 

class Solution: 
    def display(self,head):
        current = head
        while current: # tail 을 마주칠떄까지 계속 탐색
            print(current.data,end=' ')
            current = current.next # next 로 깊어짐

    def insert(self,head,data): 
        node = Node(data) # 노드 생성 (마지막에 붙여야됨)
        if not head: # None 이면 그냥 node를 return 하라는것
            head = node
        else:
            current = head # 어짜피 current 를 update 해주는건데 같은 객체니까.. 상관없음
            # current.next 가 None(끝) 일떄(즉 tail 일때까지)
            while(current.next):  
                current = current.next
            current.next = node # current.next = None -> node 로 업데이트
        return head # 그 후에 head 

mylist= Solution()
T=int(input())
head=None # None 을 준다는건 , 처음에는 그냥 Insert 한다는거
for i in range(T):
    data=int(input())
    head=mylist.insert(head,data)    
mylist.display(head); 	  
```

<br>

# Print the Elements of a Linked List

- https://www.hackerrank.com/challenges/print-the-elements-of-a-linked-list/problem?h_r=internal-search

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

# Merge Two Sorted Lists

- https://leetcode.com/problems/merge-two-sorted-lists/

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
    head=ListNode(-1)
    cursor=head

    while l1!=None and l2!=None:
        if l1.val <= l2.val:
            cursor.next=l1 # Update next node
            l1=l1.next # Update l1
        else:
            cursor.next=l2 #Update next node
            l2=l2.next # Updata l2
            cursor=cursor.next #Move cursor
        # Last node
        if l1!=None:
    		cursor.next=l1
        else : 
            cursor.next =l2
        return head.nex
```



