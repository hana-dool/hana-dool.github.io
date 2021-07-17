---
title:  "args, kwargs"
excerpt: "argument 와 keyword arguments"
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

# 가변인자(Variadic Parameter)

## *args (arguments)

>  함수를 정의할때에 여러개의 인자를 받고자 할 떄에 쓰입니다. 

```python
def custom(*names):
    for i in names :
        print(i)
custom('나','너','우리') # 나,너,우리 3개 모드 출력
```

- 위처럼, 여러 변수를 넣게되어도 출력을 할 수 있게 해줍니다.
- 그런데 어떻게 위처럼 할 수 있게 되었을까요? 

```python
def custom(*names):
    print(type(names),names)
custom('나','너','우리')
# <class 'tuple'> ('나', '너', '우리')
```

- 즉 위와 같이 차례로 받은 변수를 tuple 로 저장하는것을 볼 수 있습니다. 
- 즉 args 를 함수에 쓸 경우,  tuple 로 복수개의 인자를 담게됩니다.

<br>

## **kwargs(keyward argument)

> 여러개의 키워드 인자를 받을떄에 쓰입니다.

```python
def custom(**kwargs):
    for k,v in kwargs.items():
        print(k,v)
custom(money = 500,weight = 100) 
# money 500 
# weight 100 출력
```

- 위와 같이, 키워드 인자를 받아서 사용하게 됩니다. 

```python
def custom(**kwargs):
    print(type(kwargs),kwargs)
custom(money = 500,weight = 100) 
# <class 'dict'> {'money': 500, 'weight': 100}
```

- 위와 같이 "키워드 인자를 받아서 Dict 로 저장합니다."

<br>

## 사용시 주의점

```python
def custom(name, *args, age):
    ....... 
custom('나나나','67kg','175cm','29')
# Error : missing 1 required keyword-only argument: 'age'

```

- 위와 같이 에러가 난 이유는 , 파이썬 입장에서는 args 가 앞에 있어서, args 에 얼마나 많은 데이터를 넣어야할지 헷갈리는것이다. 
- 위의 경우 args = ('67kg','175cm','29') 로 다 넣게되어 age 가 받을게 없어진것이다. 
- 그러므로 가변인자를 정의시에는 무조건 맨 마지막에 가야한다.

```python
def mixed_params(age, name="아이유", *args, address, **kwargs):
    print("age=",end=""), print(age)
    print("name=",end=""), print(name)
    print("args=",end=""), print(args)
    print("address=",end=""), print(address)
    print("kwargs=",end=""), print(kwargs)

mixed_params(20, "정우성", "01012341234", "male", address="seoul", mobile="01012341234")
```

- 함수 정의의 순서는 일반적으로 위 순서를 따른다. 

> 1. 일반 positional 인자
> 2. 디폴트 인자 (이미 값을 지정한 인자)
> 3. 가변 인자 (`*args`)
> 4. 디폴트가 아닌 Keyword-Only 인자
> 5. 디폴트 Keyword-Only 인자
> 6. 가변 키워드 인자 (`**kwargs`)

<br>

# Unpacking

아래와 같이, Unpacking 시에 이용할 수 있다.

```python
numbers = [1, 2, 3, 4, 5, 6]

# unpacking의 좌변은 리스트 또는 튜플의 형태를 가져야하므로 단일 unpacking의 경우 *a가 아닌 *a,를 사용
*a, = numbers
# a = [1, 2, 3, 4, 5, 6]

*a, b = numbers
# a = [1, 2, 3, 4, 5]
# b = 6

a, *b, = numbers
# a = 1
# b = [2, 3, 4, 5, 6]

a, *b, c = numbers
# a = 1
# b = [2, 3, 4, 5]
# c = 6
```

- 또한 어떠한 함수가 가변인자를 받는경우에 사용할 수 있다. 

<br>

# Function

> print(*list)

- 리스트의 element 를 빈칸을 두고 출력해준다.

```python
lst = [1,2,3]
print(%lst) # 1 2 3
```

