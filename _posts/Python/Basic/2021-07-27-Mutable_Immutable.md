---
title:  "Immutable,Mutable"
excerpt: "Mutable 과 Immutable"
categories:
  - Py_Basic
tags:
  - 1
last_modified_at: 2021-07-17

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 1. Mutable 과 Immutable

| class |                  설명                   |   구분    |
| :---: | :-------------------------------------: | :-------: |
| list  |    mutable 한 순서가 있는 객체 집합     |  mutable  |
|  set  | mutable 한 순서가 없는 고유한 객체 집합 |  mutable  |
| dict  |  key와 value가 맵핑된 객체, 순서 없음   |  mutable  |
| bool  |                 참,거짓                 | immutable |
|  int  |                  정수                   | immutable |
| float |                  실수                   | immutable |
| tuple |   immutable 한 순서가 있는 객체 집합    | immutable |
|  str  |                 문자열                  | immutable |

- t 로 끝나면 , mutable 이라고 기억하면 쉽습니다. (int, floar , bool 은 당연히 immutable 이니까요)

# 2. Mutable

- 객체가 가진 값들을 변경할 수 있는 객체입니다. 

```python
lst = [1, 1, 3, 4] # id(lst) = 465223
lst[1] = 2 # id(lst) = 465223
```

- 위와 같이 객체가 가진 값을 바꾼다 하더라도, 그 id (주소값) 이 일치합니다. 
  - id 는 객체별로 가지는 유일한 숫자(주소값)

```python
sorted_list_data = list_data.sort()
print(sorted_list_data) # None
```

- 우와 같이 값을 변경시키는 메소드를 실행시키면, 새로운 객체를 내뱉는게 아니라, 기존의 객체를 변형시킵니다.
- 그러므로 return 값이 없어 None 을 출력하게 됩니다. 
- '기존의 객체를 변경' 할 수 있기때문에 Inplace 연산이 많습니다. 

<br>

# 3. Immutable

- 객체가 가진 값(정보) 를 변경 불가능한 객체입니다. 

```python
lst = (1, 1, 3, 4) # id(lst) = 465223
lst[1] = 2 # id(lst) = 469992
```

- 위와 같이, Tuple 을 변화시키면 id 가 변합니다. 
- 즉 객체가 변한게 아니라 lst 라는 변수가 담고 있는 '객체' 가 변한것입니다.

```python
s = 'string'
v = s.replace('s','l')
print(v) # s = 'ㅔㅛltring'
```

- 위와 같이 inplace 연산이 없습니다. (immutable 이기 때문)
- 즉 메서드들은 모두 객체를 내뱉으며 위와 같이 None 을 출력하지 않는것을 볼 수 있습니다.

# 4. 왜 Mutable / Immutable 나눔?

- 왜 mutable/immutable 이 있을까?
  - 이는 바로 성능적인 이점떄문입니다.

- Mutable
  - 경우 많은 메소드 적용 가능(append)
  - mutable 에 계속 for문 돌리면서 변경하면 메모리 부족하게 됨 (계속 변하는 )
    - 이는 객체를 변화시키더라도, 기존의 값이 찌꺼기처럼 메모리에 남기 떄문입니다.

- immutable 
  - 은 많은 메소드를 적용하지 못하나, 메모리상의 이점이 있음
  - 또는 mutable 의 객체를 계속 형성하고 삭제하지 않으면 메모리를 잡아먹는다.
    - 그래서 연산시 메모리를 절약하기 위해서 mutable 을 immutable 로 바꾼다음에 연산을 한 다음 mutable 로 다시 바꾸는 경우도 있다.

<br>

