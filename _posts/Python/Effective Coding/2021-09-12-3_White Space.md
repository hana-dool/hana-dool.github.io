---
title:  "White Space, indent Convention"
excerpt: "파이썬에서 공백 제대로 활용하기"
categories:
  - Py_Effective
date : 2021-09-12 12:00:00 +0900
last_modified_at: 2021-09-13 

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 다음의 Convension 은 기본적으로 Pep8 을 따릅니다. 일부 모호한 기준은 Google 의 python style guide 를 따르고 있으며, 다른 Style guide (Numpy , Scipy Style guide) 등을 따르기도 합니다. 제가 조사한것이니 만큼, 저의 주관이 다소 들어가있습니다.
{: .notice--warning}

# [White Space Convension](#link){: .btn .btn--primary}{: .align-center}

> ## 기본적인 연산자 들여쓰기

- 다음의 이진 연산자들은 항상 단일 공백으로 둘러싸자.
  - 할당( = ), 증강 할당( += , -=, 등), 
  - 비교( == , < , > , != , <> , <= , >= , in, not in , is , is not ),
  - 논리( and , or , not).

```python
i = i + 1
submitted += 1
if A and B : 
```

> ## 연산 우선순위와 들여쓰기 

- 다른 우선순위를 갖는 연산자들이 사용되면, 가장 낮은 우선순위를 갖는 연산자를 공백으로 둘러싸는 것을 고려하자. 

```python
x = x*2 - 1
hypot2 = x*x + y*y
c = (a+b) * (a-b)
```

> ## 함수 들여쓰기(indentation)

- 한번의 들여쓰기에 4개의 스페이스를 사용하여야 한다.
- 괄호(대,중,소) 및 괄호안의 괄호와 같이 연결되는 라인에서 줄바꿈이 일어나는 요소들은 수직으로 정렬되어야 한다. 
  - 즉, 변수들을 이쁘게 세로로 한줄 / 또는 요소별로 묶어서 세로로 잘 보이게 해야된다는 것입니다.

> 좋은 예시

```python
# 여는 구분기호로 정렬되는 경우
foo = long_function_name(var_one, var_two,
                         var_three, var_four)

# 아랫줄과 구분을 위해 더 많은 들여쓰기 포함된 경우
def long_function_name(
        var_one, var_two, var_three,
        var_four):

# 매달린 형태의 들여쓰기는 하나의 들여쓰기 레벨을 추가해야 함
foo = long_function_name(
    var_one, var_two,
    var_three, var_four)
```

> 나쁜 예시

```python
# 수직 정렬을 하지않고 첫 줄에 인자들을 쓰면 안된다.(눈에 안들어옵니다.)
foo = long_function_name(var_one, var_two,
    var_three, var_four)

# 이후 구문과 구별이 되도록 더 들여쓰기를 해야한다.
def long_function_name(
    var_one, var_two, var_three,
    var_four):
    print(var_one) # 함수 실행부분이 변수와 같은 indent 를 가져서 구분이 어려움
```

> 애매

```python
# hanging 들여쓰기는 꼭 공백 4개일 필요가 없다.
foo = long_function_name(
  var_one, var_two,
  var_three, var_four)
```

> ## If 구문 들여쓰기

- if 문이 여러줄을 사용해서 길어질경우 if구문의 실행 부분과 혼동을 일으킬 수 있습니다.
- Pep 에서는 특정한 기준을 제시하지는 않으나, 아래와 같이 코딩하기를 권유합니다.

```python
# 추가적인 들여쓰기가 없는 경우
if (this_is_one_thing and
    that_is_another_thing):
    do_something()

# 문법적으로 강조를 하여 if구문과 본문을 구분하기 위한 주석 추가
if (this_is_one_thing and
    that_is_another_thing):
    # 두 조건이 모두 맞을때에 아래를 실행
    do_something()

# 아랫 줄에 추가적인 들여쓰기 (실행 / 조건부분을 구분하게 해줍니다.)
if (this_is_one_thing
        and that_is_another_thing):
    do_something()
```

- 위오 같이 다양한 경우가 있으므로 이를 참고하시면 됩니다.

> ## 여러줄 변수 닫는 위치

```python
# 첫번째 요소 아래 맞추는 경우 
my_list = [
    1, 2, 3,
    4, 5, 6,
    ]

result = some_function_that_takes_arguments(
    'a', 'b', 'c',
    'd', 'e', 'f',
    )

# 라인의 가장 앞에 맞추는 경우 
my_list = [
    1, 2, 3,
    4, 5, 6,
]
```

- 위와 같이 여러줄의 변수가 있을때에, 닫는 위치는 2가지가 가능합니다. 
- 첫번째 요소에 맞추는 경우나(제가 선호합니다. ㅎㅎ) / 마지막처럼 라인의 앞에 맞출 수 있습니다.

> ## Tap 또는 Spaces? 

- 공백이 들여쓰기 방법으로 훨씬 선호됩니다.

![png](/assets/images/Python/29_2.png)

- 탭은 편집기에 따라 인덴트가 달리 보이는 문제로 공백을 넣는것을 추천합니다.
- 그래서 편집기에서 탭을 공백4으로 알아서 변환해주는 기능을 쓰곤 합니다.
  - Pycharm , VSCode 등에서 이러한 기준을 사용합니다.

> ## 이진 연산자의 앞이나 뒤에서 indent

- 수십년간 장려되는것은 이진 연산자의 뒤에서 줄바꿈을 하는것이였습니다.

```python
# No: operators sit far away from their operands
income = (gross_wages +
          taxable_interest +
          (dividends - qualified_dividends) -
          ira_deduction -
          student_loan_interest)
```

- 하지만 위와 같은 방법은 어느 항목이 뺴지고 더해지는지 알려면 줄을 바꾸어 가면서 눈이 왔다 갓다 해야합니다.
- 그래서 수학의 전통을 따라서 아래와 같이 연산자 이후에 변수가 오게 설정합니다.

```python
# Yes: easy to match operators with operands
# 좋은 예: 연산자를 피연산와 매치시키기 쉽다
income = (gross_wages
          + taxable_interest
          + (dividends - qualified_dividends)
          - ira_deduction
          - student_loan_interest)
```

> ## Import 와 indent

- Import 는 행으로 구분되어야 합니다. 

```python
# 좋은 예
import os
import sys
```

```python
# 나쁜 예 : 
import sys, os
```

- 다만 아래와 같이 , 같은 모듈에서 여러개가 import 되는 경우는 사용해도 됩니다.

```python
from subprocess import Popen, PIPE
# 또는 아래와 같이
from subprocess import (Popen,
                        PIPE)
```

> ## 의미없는 공백 피하기

- 아래와 같이 상관 없는 공백은 피하는게 좋습니다.

> 중괄호 , 대괄호, 괄호 안

```python
custom(dic[1],dic2) #good
custom( dic[ 1 ], dic[ 2 ]) # bad
```

> 뒤에 오는 콤마와 오는 괄호 사이 

```python
han = (0,) # good
han = (0, ) # bad
```

> 콤마, 세미콜론 , 콜론 전 

```python
if x == 4: print x, y; x, y = y, x #good
if x == 4 : print x , y ; x , y = y , x # bad
```

- 즉 별 의도 없이 띄어쓰기를 남발하지 말자는 의미입니다.

> ## 키워드 변수와 indent

- 키워드 독립변수(keyword argument) 혹은 기본 파라미터 값을 나타내기 위해 “=” 사인 주변에 스페이스를 사용하지 말도록 한다.

```python
# Good
def complex(real, imag=0.0):
    return magic(r=real, i=imag)
```

```python
# Bad
def complex(real, imag = 0.0):
    return magic(r = real, i = imag)
```

# Reference

- <https://www.python.org/dev/peps/pep-0008/>
- <https://www.javatpoint.com/pep-8-in-python>
- <https://wikidocs.net/7914>
- [https://kongdols-room.tistory.com/18](https://kongdols-room.tistory.com/18)

<br>

 위와 같이 , Pep 에서 설명하는 다양한 그 기준과 제안에 대해서 알아보았습니다. 물론 제안일 뿐이며 지킬 필요는 없지만 위의 기준을 명심하면서 파이썬 코딩을 해야, 개발자끼리 의사소통도 효율적으로 이루어질 것입니다.
{: .notice--success}











