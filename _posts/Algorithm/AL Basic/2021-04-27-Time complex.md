---
title:  "0.Time Complexity"
excerpt: "Algorithm"
categories:
  - AL_Basic
tags:
  - 4
last_modified_at: 2021-06-28

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---



# 시간복잡도

시간 복잡도는 문제를 푸는데 걸리는 시간을 나타냅니다. 주로 big - O 표기법을 사용합니다. 

# 시간 복잡도 Summary

# List 

|      | Operation     | Example       | Class       | Notes                                   |
| ---- | ------------- | ------------- | ----------- | --------------------------------------- |
| 1    | Index         | l[i]          | O(1)        | 인덱스로 값 찾기                        |
| 2    | Store         | l[i] = 0      | O(1)        | 인덱스로 데이터 저장                    |
| 3    | Length        | len(l)        | O(1)        | 리스트 길이                             |
| 4    | Append        | l.append(5)   | O(1)        | 리스드 뒤에 데이터 저장                 |
| 5    | Pop           | l.pop()       | O(1)        | 가장 뒤의 데이터 pop                    |
| 6    | Clear         | l.clear()     | O(1)        | l = []                                  |
| 7    | Slice         | l[a:b]        | O(b-a)      | 슬라이싱되는 요소들 수 만큼 비례        |
| 8    | Extend        | l.extend(...) | O(len(...)) | 확장되는 길이만큼                       |
| 9    | Construction  | list(...)     | O(len(...)) | 리스트 길이만큼                         |
| 10   | check ==, !=  | l1 == l2      | O(N)        | 전체 리스트가 동일한지 확인             |
| 11   | Insert        | l[a:b] = ...  | O(N)        | 데이터 삽입                             |
| 12   | Delete        | del l[i]      | O(N)        | 데이터 삭제                             |
| 13   | Containment   | x in/not in l | O(N)        | 포함 여부 확인                          |
| 14   | Copy          | l.copy()      | O(N)        | 복제                                    |
| 15   | Remove        | l.remove(...) | O(N)        | 제거                                    |
| 16   | Pop           | l.pop(i)      | O(N)        | 제거된 값 이후를 전부 한칸씩 당겨줘야함 |
| 17   | Extreme value | min(l)/max(l) | O(N)        | 전체 데이터를 확인해야함                |
| 18   | Reverse       | l.reverse()   | O(N)        | 뒤집기                                  |
| 19   | Iteration     | for v in l:   | O(N)        | 전체 데이터 확인하므로                  |
| 20   | Sort          | l.sort()      | O(N Log N)  | 파이썬 기본 정렬 알고리즘               |
| 21   | Multiply      | k*l           | O(k N)      | 리스트의 곱은 리스트 개수 늘어남        |

<br>

# Set

|      | Operation      | Example       | Class            | Notes                    |
| ---- | -------------- | ------------- | ---------------- | ------------------------ |
| 1    | Add            | s.add(5)      | O(1)             | 집합 요소 추가           |
| 2    | Containment    | x in/not in s | O(1)             | 포함 여부 확인           |
| 3    | Remove         | s.remove(..)  | O(1)             | 요소 제거                |
| 4    | Discard        | s.discard(..) | O(1)             | 특정 요소 제거           |
| 5    | Pop            | s.pop()       | O(1)             | 랜덤하게 하나 pop        |
| 6    | Clear          | s.clear()     | O(1)             | similar to s = set()     |
| 7    | Construction   | set(...)      | O(len(...))      | 길이만큼                 |
| 8    | check ==, !=   | s != t        | O(len(s))        | 전체 요소 동일 여부 확인 |
| 9    | <=/<           | s <= t        | O(len(s))        | 부분집합 여부            |
| 10   | >=/>           | s >= t        | O(len(t))        | 부분집합 여부            |
| 11   | Union          | s, t          | O(len(s)+len(t)) | 합집합                   |
| 12   | Intersection   | s & t         | O(len(s)+len(t)) | 교집합                   |
| 13   | Difference     | s - t         | O(len(s)+len(t)) | 차집합                   |
| 14   | Symmetric Diff | s ^ t         | O(len(s)+len(t)) | 여집합                   |
| 15   | Iteration      | for v in s:   | O(N)             | 전체 요소 순회           |
| 16   | Copy           | s.copy()      | O(N)             | 복제                     |

<Br>

# dict

|      | Operation      | Example     | Class       | Notes                                |
| ---- | -------------- | ----------- | ----------- | ------------------------------------ |
| 1    | Store          | d[k] = v    | O(1)        | 데이터 저장                          |
| 2    | Length         | len(d)      | O(1)        | 길이 출력                            |
| 3    | Delete         | del d[k]    | O(1)        | 요소 제거                            |
| 4    | get/setdefault | d.get(k)    | O(1)        | key에 따른 value 확인                |
| 5    | Pop            | d.pop(k)    | O(1)        | pop                                  |
| 6    | Pop item       | d.popitem() | O(1)        | 랜덤하게 선택해서 pop                |
| 7    | Clear          | d.clear()   | O(1)        | similar to s = {} or = dict()        |
| 8    | View           | d.keys()    | O(1)        | same for d.values() / 키값 전체 확인 |
| 9    | Construction   | dict(...)   | O(len(...)) | (key, value) 튜플 개수만큼           |
| 10   | Iteration      | for k in d: | O(N)        | 전체 딕셔너리 순회                   |

<br>

# String

<br>



# Set 의 구조와 연산속도

- in 연산의 처리의 경우 Set 이 월등히 빠르다.

> Set is implemented by a hash-table data structure. For this reason, checking if a specific value exists in the set, is instant O(1) time, requires no iteration. On the other hand to check if a value is included in a list, all elements must be checked in a loop, so that is O(n) time. But the elements of the set are not ordered, not indexed. So sometimes a list is a better choice, depending what you want to use it for.

- 그 이유는 위와 같이 set 은 기본적으로 해시 테이블 Structure 이기 떄문이다
- 즉 set에서는 값을 찾기 위해서는 그저 O(1) 의 연산만이 필요하다.
- 그에 비해, list 에서는 값을 찾기 위해서는 O(n) 의 연산이 필요하다. 

![png](/assets/images/Python/4_1.png)

- 위와 같이 해시테이블은 array 구조를 이용하여 key 에 value 를 저장하는 자료구조이다. 
- 키와 값은 1:1 로 연관되어있고, key 를 이용해 값을 불러올 수 있다.
  - 이렇게 1:1 로 대응시키기 위하여 해시함수가 이용된다. 
- 해시 테이블은 key(키) , Value(값) , 해시함수, Bucket(저장소) 로 이루어져 있다.
  - 키(key) 는 해시함수를 거쳐서, 해시로 변경된다. 
  - 그리고 그 해시는 값과 매칭되어 저장소에 저장된다. 
- 우리가 사용하는 Set 의 경우 해시값은 존재하지 않는다. 
  - 이떄 핵심은, Set 에 원소 저장시 기존의 리스트, 어레이처럼 앞뒤에 원소를 넣어주는것이 아니다.
  - Set 은 원소를 저장할때 해시함수를 거친 해시로 저장소에 넣어둔다. 
- 그러므로 k 값이 set에 있는지 없는지를 알려면, 해시함수를 이용해 k 를 변환시킨 값이 set 안에 있는지 없는지 검사하면 된다. 
  - 그러므로 탐색에 O(1) 만 필요하다. 
- 또한 해시테이블의 삽입/ 삭제 과정은 O(1) 을 따른다.
  - 해시함수의 결과로 나온 해시와 값을 저장소에 넣기만 하면 되기 떄문
  - 해시함수의 충돌 문제도 있긴 하지만, 파이썬에서는 이를 방지하기 위한 장치가 많아 O(1) d이라고 생각하면 된다고 한다. 
