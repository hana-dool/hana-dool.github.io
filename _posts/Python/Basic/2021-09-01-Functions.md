---
title:  "Function in python"
excerpt: "파이썬의 함수 정의에 대해 알아보자."
categories:
  - Py_Basic
last_modified_at: 2021-09-19

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 파이썬은 def 를 통해서 함수를 정의합니다. 아마도 파이썬을 쓰시다 보면 제일 많이 사용하는것 중 하나일 것입니다. 이러한 함수를 파이썬에서 어떻게 다루고, 어떻게 작동하는지에 대해서 알아봅시다.
{: .notice--warning}

# [Python Function Object](#link){: .btn .btn--primary}{: .align-center}

> ## 함수는 코드에 대한 이름표

- 변수가 값에 대한 이름표라면 함수 이름은 코드에 대한 이름표입니다.
- 다음과 같은 코드를 우리는 함수를 정의했다고 표현하면 실제로 아무일도 일어나지 않는다고 배웠습니다.

```python
def hello():
    print("hello")    
```

-  하지만 파이썬 인터프리터가 아래의 코드를 실행하면 메모리에 함수 객체를 할당하고 이를 hello라는 함수 이름이 바인딩하게 됩니다.

```python
>>> id(hello)
4399217408
```

![png](/assets/images/Python/33_1.png)

- 파이썬에서 변수는 자주 사용되는 값을 기억히가 위해 값 객체를 바인딩 하는것입니다.
  - 즉, 자주 사용되는 값을 메모리에 주소 위에 올려두고, 그 주소를 변수 이름과 매칭하는 것이죠
  - Note : a = 3 이란 동작을 파이썬에서는 a 에 실제로 3을 부여하는게 아니라, 메모리 위에 3 이라는 객체를 생성하고, 이 메모리 주소와 a 를 binding 하는것입니다.
- 함수도 똑같습니다. 사용되는 코드(함수) 를 메모리 위에 올려두고 그 함수 객체를 바인딩 하는것입니다.

```python
def hello():
    print("hello")

f = hello
f()
```

![png](/assets/images/Python/33_2.png)

- 위와 같이, 함수도 결국 객체라는것이죠. '파이썬은 모든것이 객체다!' 라는것을 기억합시다.

> ## What is () ? 

- 결국 함수 이름을 정하는것은, 함수 타입의 객체와 binding 할 변수 이름을 정하는것이라고 배웠습니다.

```python
def custom(var1,var2) :
    return var1 + var2 
# custom 이라는 이름의 변수에 , 함수 객체 (var1 + var2를 호출하는 코드 블럭 객체) 를 binding
```

- 이때에 ()를 통해서, 함수 안의 var1, var2 의 Local 변수를 만들어내는데요, () 는 대체 어떤 메서드일까요?

- 이는 바로, \_\_call\_\_ 클래스로 구현된 것입니다. 
- 함수 클래스를 정의할때에, 이러한 \_\_call\_\_ 매직 메서드를 정의하면 , 객체를 생성한 후 () 를 붙이면 마치 \_\_init\_\_ 처럼 자동으로 실행됩니다.

# [Variable Arguments](#link){: .btn .btn--primary}{: .align-center}

> ## *args (arguments)

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

> ## **kwargs(keyward argument)

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

> ## 사용시 주의점

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

1. 일반 positional 인자
2. 디폴트 인자 (이미 값을 지정한 인자)
3. 가변 인자 (`*args`)
4. 디폴트가 아닌 Keyword-Only 인자
5. 디폴트 Keyword-Only 인자
6. 가변 키워드 인자 (`**kwargs`)

> ## Unpacking

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

> ## Example

> print(*list)

- 리스트의 element 를 빈칸을 두고 출력해준다.

```python
lst = [1,2,3]
print(%lst) # 1 2 3
```

# [Lambda Function](#link){: .btn .btn--primary}{: .align-center}

- 파이썬에서 lambda 는 간단한 함수를 정의할때에 사용합니다 

- Lamda 함수는 (lambda x,y: x + y)(10, 20) 처럼 함수 def 없이 바로 적용하게 해준다.
  - lambda 변수 : return 값 처럼 사용된다.
- map 이나 filter 등에서 자주 사용됩니다.


```python
list(map(lambda x: x ** 2, range(5)))
# [0, 1, 4, 9, 16]
```


```python
list(filter(lambda x: x % 2, range(10)))
# [1, 3, 5, 7, 9]
```

# [함수와 변수 범위](#link){: .btn .btn--primary}{: .align-center}

> ## LEGB 규칙

- 파이썬에서 변수에 값을 바인딩하거나 변수의 값을 참조하는 경우 LEGB 규칙을 따릅니다. 
- LEGB는 각각 다음과 같은 의미를 가집니다.

| 변수 | 의미                                                         |
| :--- | :----------------------------------------------------------- |
| L    | Local의 약자로 함수 안을 의미합니다.                         |
| E    | Enclosed function locals의 약자로 내부함수에서 자신의 외부 함수의 범위를 의미합니다. |
| G    | Global의 약자로 함수 바깥 즉, 모듈 범위입니다.               |
| B    | Built-in의 약자로 open, range와 같은 파이썬 내장 함수들을 의미합니다. |

> ## 변수를 참조할때

> Local 변수와 Global 변수가 같은 이름으로 정의된 경우

```python
a = 10
def test():
    a = 20
    print(a)
test() # 20
```

- 위와 같이 함수 안에서 정의되는 Local 변수와, global 변수인 a 가 상충되는 상황입니다.
- 이럴 경우에 위의 출력은 20을 출력하게 됩니다.

> Local 변수 없이 Global 변수만 참조될 경우

```python
a = 10
def test():
    print(a)
test() # 10
```

- 위의 경우, Local 변수가 없으므로 Global 변수인 a 를 먼저 출력하게 됩니다.

# [Mutable 과 Immutable](#link){: .btn .btn--primary}{: .align-center}

- immutable : '객체를 변혈할 수 없음'
  - bool
  - int
  - float
  - str
  - tuple
- mutable : append 등의 조작으로 '객체를 변형 가능'
  - list
  - dict
  - set

> ## def

- 함수를 정의할때에, 바깥 Namespace 에 있는 값은 안쪽 name space 에서 사용이 가능합니다.
- 즉 특별히 global 을 쓰지 않아도 '참조' 자체는 가능합니다만 문제는 이를 변형하거나 대체하려할 떄에 일어납니다.
- 함수 내에서는 , Mutable 의 변형(주소는 그대로 바꾸는)은 global 없이 가능합니다. 
- 하지만 immutable 객체의 변형 / 또는 mutable 객체의 재할당 등에 대해서는 수정이 불가합니다.
  - 이럴떄에는 global 을 써서 '재할당' 을 가능하게 해줌으로서 해결하려 합니다.

> ## List 와 변형

- 아래와 같은 경우는 id 를 그대로 보존(mutable 이라서) 하므로 가능합니다. 

```python
lst = [1]
def custom():
    lst.append(3)
custom()
print(lst)
# [1,3]
```

```python
lst = [1]
def custom():
    lst[0] = 3
custom()
print(lst)
# [3]
```

- 아래와 같은 경우는 아예 lst 에 다른 객체를 재할당하므로 변하지 않습니다.

```python
lst = [1]
def custom():
    lst = [3,4]
custom()
print(lst) # [1]
```

```python
lst = [1]
def custom():
    lst += [3]
custom() # Error 
print(lst)
```

- 그러므로 아래와 같이 수정해야합니다.

```python
lst = [1]
def custom():
    global lst
    lst = [3,4]
custom()
print(lst) # [3,4]
```

> ## Immutable

- Immutable 한 값의 경우는 간단합니다. 변형하려면 global 을 쓰고 그렇지 않으면 안써도 됩니다.

```python
cnt = 0
def custom():
    print(cnt)
custom()
```

# [작성규칙](#link){: .btn .btn--primary}{: .align-center}

- 파이썬의 함수를 정의할때에는 docstring 을 써주면 좋습니다.
- 또한 variable 에 대한 자료형과 , 그 출력을 적어줘도 좋습니다.

```python
def kk(k : int ) -> int :
    print(k)
kk(3)
```

