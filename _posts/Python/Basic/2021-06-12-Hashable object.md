---
title:  "Hashable Object"
excerpt: "해시"
categories:
  - Py_Basic
tags:
  - 4
last_modified_at: 2021-06-12

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# <center><font size="15"> Hashable OBject </font></center>

- 파이썬에서 hashable object 란 hash 함수에 인자(input)로 들어갈 수 있는 객체를 의미한다.
- 그러면 Hash 는 어떤것일까? 

![png](/assets/images/Py_Basic/3_1.png)

- hash란 object 의 저장된 내용을 기준으로 한개의 정수를 생성해 반환하는 함수다.
  - 이를 Hasher 라고도 한다. 
  - 위 그림을 보면, string 이 무엇이던간에 hash 함수를 거치고 나면 하나의 숫자로 반환되는것을 볼 수 있다. 
- Hashable 은 왜 필요할까?
  - 바로 비교를 위해서 사용이 된다.
  - Hash 를 하고나면 각 객체가 숫자로 나오게 되므로, 다른 객체인지 비교할 수 있다.
  - 이 경우 같은 숫자면 같은 객체로 인식하게 된다. 
  - 컨테이너인 객체들 입장에서도 Hash 를 이용하면 한번에 비교가 가능하다. 
    - 예로, (a,b,c) 와 (b,c,a) 의 객체를 비교시에 각각의 원소가 같은지 여러번 비교하는것이 아니라, Hash 값만 있으면 한번에 비교할 수 있다. 
    - 즉 계산상의 이점을 가지기 위해서 Hash 함수가 사용된다. 

<br>

<br>

# <center><font size="15"> Hashable OBject </font></center>

- 어떤 오브젝트가 Hashable 할까? 
  - 리스트, 셋, DIctionary 와 같이 , 데이터 변경이 가능한 컨테이너는 Hashable 하지 않다.
  - 그 이유는 데이터가 변경 가능한 객체들은 해시를 만들어 놓고도, 중간에 데이터가 변경되면 해시값도 매번 변경되어야 하기 때문이다. 
  - 이러한 경우 Type Errror 가 발생한다.
  - 즉 Nemeric , Immutable Container 이 Hashable 하다.
- 숫자 (int,bool,float)
  - 그 자체로 숫자이기떄문에, 숫자를 바꿀 수 없고 변경불가능 
  - 즉 Hashable
- Immutable Container(Tuple, String)
  - 변경 불가능한 경우에도 , 바꿀 수 있없으므로 Hashable 하다.

