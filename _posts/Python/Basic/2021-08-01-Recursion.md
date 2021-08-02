---
title:  "재귀와 스택"
excerpt: "파이썬의 재귀는 어떻게 이루어질까"
categories:
  - Py_Basic
tags:
  - 1
last_modified_at: 2021-08-01

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 1.재귀가 깊어지는 과정

```python
def recur(x):
    print(x)
    if x == 0 :
        print('끝')
        return
    recur(x - 1)
    print(x)
recur(5)
```

```python
5
4
3
2
1
0
끝
1
2
3
4
5
```

- recursion 함수를 정의하게 되면 위와 같은 호출이 나오게 되는데, 이제 어떻게 되는지 알아보겠습니다.

![png](/assets/images/Python/21_1.png)

- 먼저 함수가 깊어지는 과정에는 위와 같이 점점 스택에 쌓여가는 형태입니다. 
- 이런 스택에 쌓이는것은 총 3가지가 있는데 지역변수,변환주소값,매개변수입니다. 

## 매개변수

```python
def recur(x):
    s = x**2
    print(x)
    if x == 0 :
        print('끝')
        return
    recur(x - 1)
    print(x)
recur(5)
```

- 위와 같은 재귀에서, recursion 첫 단계에서는 다음과 같이 깊어집니다.

```python
# 첫 5에서 어떻게 되는지
def recur(5): # 처음 매개변수는 5
    s = 5**2 # 지역변수 s 는 25를 가진다. 
    print(5) 
    if x == 0 :
        print('끝')
        return
    recur(5-1) # 여기서 깊어짐 (매개변수 4 를 가지며, 이 열을 (7열) 복귀 주소로 기억하게됨)
    print(x)
```

## 변환주소값

- 위에서와 같이, 복귀주소란, 내가 어디서 깊어졌는지를 기억하고 있는것입니다. 
- 즉 위에서는 7열을 기억하고 있습니다. 

## 지역변수

- 함수의 안쪽에서 정의되는것이 바로 지역변수 입니다. 
- 이 경우에는 s 를 나타냅니다.

<br>

# 재귀가 풀리는 과정

- return 을 만나게 되면, 함수가 끝나고, 스택에서 하나씩 없어지는것을 의미합니다. 

![png](/assets/images/Python/21_2.png)

- 이 경우에 맨 위의 최상층부터 사라지게 됩니다.

```python
def recur(x):
    s = x**2
    print(x)
    if x == 0 :
        print('끝')
        return
    recur(x - 1)
    print(x)
recur(5)
```

```python
5 #A={매개변수 = 5 , 복귀주소 없음, 지역변수 25} , Stack [A]
4 #B={매개변수 = 4 , 복귀주소 = 7, 지역변수 16} , Stack [A,B]
3 #C={매개변수 = 3 , 복귀주소 = 7, 지역변수 9 } , Stack [A,B,C]
2 #D={매개변수 = 2 , 복귀주소 = 7, 지역변수 4 } , Stack [A,B,C,D]
1 #E={매개변수 = 1 , 복귀주소 = 7, 지역변수 1 } , Stack [A,B,C,D,E]
0 #F={매개변수 = 0 , 복귀주소 = 7, 지역변수 0 } , Stack [A,B,C,D,E,F]
끝 # -> return 만남  -> E가 풀림 -> Stack [A,B,C,D,E]
1 #Stack 에서 E 가 마지막 열(print(x))까지 실행되고 풀림 -> Stack [A,B,C,D]
2 #Stack 에서 D 가 마지막 열(print(x))까지 실행되고 풀림 -> Stack [A,B,C]
3 #Stack 에서 C 가 마지막 열(print(x))까지 실행되고 풀림 -> Stack [A,B]
4 #Stack 에서 B 가 마지막 열(print(x))까지 실행되고 풀림 -> Stack [A]
5 #Stack 에서 A 가 마지막 열(print(x))까지 실행되고 풀림 -> Stack []
```





