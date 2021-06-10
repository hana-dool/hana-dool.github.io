---
title:  "Recursion"
excerpt: "재귀함수"
categories:
  - Py_Algorithm
tags:
  - 1
last_modified_at: 2021-06-07

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# <center><font size="15"> Theory </font></center>

- 아래의 경우 출력하게 되면 어떻게 될까요? 

```python
def DFS(x):
    if x >= 0 :
        print(x)
        DFS(x-1)
    else :
        return
```

```python
DFS(5)
5
4
3
2
1
...
```

- 위와 같이 값이 계속 감소하게 됩니다. 

<br>

- 아래의 경우는 어떨까요?

```python
def DFS(x):
    if x >= 0 :
        DFS(x-1)
        print(x)
    else :
        return
```

```
DFS(5)
1
2
3
4
5

```

- 위와 같이 계속 증가하게 됩니다. 
- 재귀함수는 깊어질대로 깊어졌다가, 종료문을 만나고나면, 그 위부터 호출되는 형식입니다. 
  - 즉 함수가 스택에 쌓인다고 생각하시면 됩니다. 

![png](/assets/images/Py_Algorithm/3_1.png)

- '쌓이고 나서' 출력문을 만나는것과 '쌓이기 전에' 출력문을 만나는것은 그 순서차이가 있습니다. 
- 재귀문이후에 만나는것들은 

# <center><font size="15"> Level 1 </font></center>

- 십진수를 입력받으면 2진수를 출력하는 프로그램을 출력하라.

```python
# 입력예제1
11
# 출력예제1
1011
```

- 

```python
def DFS(x):
    if x == 0 :
        return
    else :
        DFS(x//2)
        print(x%2, end = '')
```

