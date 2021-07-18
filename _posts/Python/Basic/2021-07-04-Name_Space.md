---
title:  "Name Space"
excerpt: "네임 스페이스"
categories:
  - Py_Basic
tags:
  - 4
last_modified_at: 2021-07-04

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math : true
---

# Name Space ?

> C 에서는, 함수가 생성될때에 하나의 스택 공간을 할당받아 그 곳에서 변수를 만드는 방식으로, 함수 안의 변수를 관리합니다. 하지만 파이썬은 네임 스페이스 방식을 사용합니다.

- 이때에, 위와 같은 '네임 스페이스 방식' 이란 뭘까요?
- 네임스페이스 방식은 다음과 같은 질문에서 시작되었습니다. 

> 함수 내부에서 사용하는 변수 이름과, 외부에서 사용하는 변수의 이름을 항상 중복되지 않게 관리해야할까? 너무 불편한데, 함수 내부랑 외부의 세상을 분리할 수 없을까?

- 파이썬에서는 위를 위해서, 파이썬의 경우, 식별자(변수명) 을 가지는 모든 객체 (함수, 클래스 등) 는 서로 구분되는 공간에 각각 속하게 설계되어 있습니다.
- 이러한 공간을 네임스페이스라 합니다. 

![png](/assets/images/Python/7_1.png)

- 위와 같이, Name space 는 여러 단계로 나누어져 있습니다. 

## Built in Namespace

- 파이썬에서는 빌트인 네임스페이스라는 최상위 네임스페이스가 있습니다.
- 파이썬의 기본 내장함수 등이 저장되어있는 공간으로서, 가장 최상위에 있는 스페이스입니다. 

```python
print(dir(__builtins__))
['bool','abs','all','bin','formar','dir','sum'........]
```

- 어떠한 코드를 실행하던, '파이썬을' 실행한다면 위  Namespace 가 최상위에 위치기 때문에, 항상 all 등의 함수를 쓸 수 있는것입니다. 
- 이때에 Built in namespace 에 있는 함수와 같은 변수를 지정하면 어떻게 될까요?

```python
max = 'gg'
max([1,3]) # error
```

- 위와 같이 max 라는 함수는 더이상 함수가 아니라 'gg' 라는 string 으로 존재하게 됩니다.

## Module Namespace

- 그 아래에는 파이썬 모듈마다 전역 네임스페이스 가 존재하게 됩니다.
- 그중 하나가 바로, 우리가 파이썬 실행 후, 명령을 내릴때 자동으로 위치하는곳이 __ main __ 입니다. 
- 일반적으로, 프로그램을 실행했을때에 변수를 정의하게 되면, 이 변수는 전역변수에 속하게 됩니다. 



##Local Namespace 

- 함수 및 메서드 별로 존재합니다. 

  - 식별자를 가지는 함수, 메서드 별로 각각의 네임 스페이스가 존재하게 됩니다. 

  

# Name Space 참조

- Namespace 의 경우 '상위' Namespace 는 참조할 수 있습니다. 

![png](/assets/images/Python/7_2.png)

```python
x = [10]
def add():
    x.append(20)
    print(x)
add() # [10,20]
print(x) # [10,20]
```

- 위처럼, 함수 안에서, 전역 변수에 있는 x 를 변형할 수 있습니다. 

```python
x = 3
def add():
    x += 3
    print(x)
add() # error
print(x) # 3
```

- 하지만 위처럼 x+= 연산을 하는 경우 에러가 발생합니다.
- x += 3 은 사실 x = x + 3 인데, 이때에 x 가 local 인지 gloable 인지 헷갈리게 됩니다.
- 그래서 위와 같은 경우는 global x 를 통해 '이 x 는 global 이다!' 라고 알려주어야 합니다. 

```python
max([1,3,4,2])
```

- 기본적으로 위와 같이 파이썬 내에서 빌트인 네임스페이스의 함수인 max 를 아무런 import 없이 참조하는것도, 상위 name space 를 참조하는것이라 할 수 있습니다.

<br>

# Note : For 문의 변수참조

```python
k = 0
for i in range(5):
    k = k + i 
print(i) # 4
```

- 위와 같이 for 문에서 사용하는 변수가, 함수에서처럼 지역변수라고 생각하면 안됩니다.
- for 문에서 쓰이는 변수는, for 문이 끝난 이후에도 해소가 덜 된 상태이기 때문에 주의해야합니다.  
- for 문에서 쓰이게 될 변수는, 그 이후에 사용하지 않는것이 좋습니다. (또는 같은 for 문에서 쓰거나)
