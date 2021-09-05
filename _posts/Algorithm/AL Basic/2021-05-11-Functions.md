---
title:  "2.내장 Function"
excerpt: "파이썬의 내장함수"
categories:
  - AL_Basic
tags:
  - 1
last_modified_at: 2021-07-04

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: false

use_math : true
---


# function

## all

- all(iterable) 함수는 인자로 받은 반복 가능한 자료형(iterable)의 모든 요소가 참(True)이면 참(True)을 반환하는 함수
- 즉 리스트, 튜플, 집합, 딕셔너리, 문자열에 대해서 all 을 쓸 수 있다.


```python
a = [1,2,3,4,5]
all([a[x]>a[x-1] for x in range(1,3)])
```


    True



## any

- any(iterable) 함수는 인자로 받은 반복가능한 자료형(iterable)중 단 하나라도 참(True)이 있으면 참(True)를 반환한다.


```python
a = [1,2,3,4,5]
any([a[x] == 3 for x in range(1,3)])
```




    True



## copy / deepcopy

- copy 의 경우, 새로운 id 를 부여하게 되며, 그 요소들을 바꾼다 해도 복사된 변수에는 영향이 없다.


```python
a = [1,2,3]
b = a.copy() # a[:] 도 가능하다.
print(id(a)) ; print(id(b))
a[1] = 'gogo' ; print(b) # a를 바꾸더라도 영향이 없음
```

    1907314651656
    1907314652104
    [1, 2, 3]


- 하지만 리스트 안의 리스트처럼 , mutable 객체 안에 mutable 이 들어있을때에 문제가 된다
- 아래 처럼 id(a[0])과 id(b[0])은 같은 주소를 바라보고 있습니다.


```python
a = [[1,2], [3,4]]
b = a[:]
print(id(a)) ; print(id(b))
print(id(a[0])) ; print(id(b[0])) # 안의 mutable 객체는 아예 같다. 
a[0][0] = 'gogo' ; print(b) # a를 바꾸었는데 b가 바뀌고 말았다. 
```

    1907314604168
    1907318369224
    1907322478280
    1907322478280
    [['gogo', 2], [3, 4]]


- 위와 같이 '내부의 객체들' 에 까지 모두 새롭게 copy 하기 위해서는 deepcopy 메서드를 써야 한다. 


```python
import copy
a = [[1,2],[3,4]]
b = copy.deepcopy(a)
a[1].append(5)
print(a) ; print(b)
```

    [[1, 2], [3, 4, 5]]
    [[1, 2], [3, 4]]


## def + return

- def 는 함수를 정의한다. 이때에 return 을 만나게 된다면 함수를 바로 빠져나와 호출한 쪽으로 되돌아간다.
- 아래와 같이 return 을 만나면 구문이 여러개 있더라도 다시 되돌아간다. 즉 return 은 def 안에서 어떻게 보면 sys.exit 와 같이 종료구문이라 생각해도 무방하다.


```python
def operation(a,b) :
    return a+b
    return a*b
    return a-b

operation(5,2)
# 처음 만난 return a+b의 결과만 반환됨
```




    7



## del

- del 은 '객체를 지우는것' 이 아니라 변수와 객체의 연결을 끊어내는 것이다.
- del 은 시간이 많이 걸리는 작업이라 주의를 요망합니다.


```python
x = [1,2,3]
del(x[1]) # [1,3]
```


## Enumerate

- index 와 value 를 같이 취급할 수 있게 해주는 메서드입니다. 
- 이 경우 idx, val in enumerate(iterable) 이라는 명령어를 통해서 index 와 value 를 출력할 수 있습니다.

```python
for i, name in enumerate(['딸기','사과','포토']):
    print(i, name)
```

    0 딸기
    1 사과
    2 포토

- 그리고 , Enumerate 로 쌓인 객체는 iterable 이기 떄문에, 아래와 같이 list 로 만들어줄 수 도 있습니다.

```python
lst = ['a','b','c']
list(enumerate(lst))[::-1] # [(2, 'c'), (1, 'b'), (0, 'a')] 
```



## Filter

- filter함수는 특정 조건으로 걸러서 걸러진 요소들로 iterator객체를 만들어서 리턴해준다.
- map함수와 사용 방법은 동일하다. 하지만 함수의 결과가 참인지 거짓인지에 따라, 해당 요소를 포함할지를 결정한다.


```python
target = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# 함수를 정의한다.
def is_even(n):
    return True if n % 2 == 0 else False

# filter 를 통해서 map 과 같이 target 에 함수를 적용한다.
# 이 때에 filter 에서 'TRUE'를 뽑아내는 경우에만 target 값에서 뽑아낸다.
result = filter(is_even, target)

# result 는 filter 객체이기 떄문에 list 로 변환시켜주어야 한다.
print(list(result))
```

    [2, 4, 6, 8, 10]

## Format

- format 내장 함수를 이용하면 숫자를 다른 진수의 문자열로 바꿀 수 있습니다. 

```python
format(42,'b') # b는 binary 즉 2진수를 출력
>>> '101010'
```

- 이 경우 위의 연산을 반대로 수행하기 위해서라면 , int 명령어를 쓰면 됩니다. 

```python
int('101010',2)
>>> 42
```

## F-string

- F-string 을 Print 말고도 string 을 사용하는 다양한곳에 이용 가능합니다.

```python
i = 0
s = f'나는 {}번쨰'
print(s) # 나는 0번째 
```

## in / not in 

- x in 리스트	/ x not in 리스트 ($O(n)$)
- x in 튜플	/ x not in 튜플 ($O(n)$)
- x in 문자열 / x not in 문자열 ($O(n)$)
- x in 셋 / x not in 셋 ($O(1)$)

```python
1 in [1, 2, 3] # 1 이 list 안에 있는가?
# True
```

## len

> len(s)

- len(s)은 입력값 s의 길이(요소의 전체 개수)를 돌려주는 함수이다.
- parameter 로 string, list, dict,set 등이 가능합니다. 


```python
len([1,4]) # 2
len({1,4}) # 2
len({1:3,2:4}) # 2
```

- 이때, len(비어있는 객체) 를 할 경우 0 이 나온다.

```python
len('') # 0
```

## Lambda

- Lamda 함수는 (lambda x,y: x + y)(10, 20) 처럼 함수 def 없이 바로 적용하게 해준다.
  - lambda 변수 : return 값 처럼 사용된다.
- map 이나 filter 등에서 사용된다.


```python
list(map(lambda x: x ** 2, range(5)))
# [0, 1, 4, 9, 16]
```


```python
list(filter(lambda x: x % 2, range(10)))
# [1, 3, 5, 7, 9]
```

## max/min

- max 도 마찬가지로 sum 과 같이 작동가능하다.

> max(iterable)

- 아래와 같이 List, Set, String 에서 사용 가능합니다. 


```python
max([1,2,9]) #9 
max({4,3,9}) #9
max('4329')  #9 
max('abfc')  #f
```

- 비어있는 값을 만나면 error 가 납니다.

```python
max([]) # error!
```

> max(iterable, key = lambda x : x[0])

```python
min([(2, 0), (1, 1), (3, 2), (2, 3)],key = lambda x :x[1])
# (2, 0)
```

- Sort 와 마찬가지로, max,min 의 경우에도,정렬의 기준을 정할 수 있습니다. 
- 위 경우는, 두번쨰 원소를 기준으로 min 을 찾는 함수입니다.

## map

- iterable객체를 받아서, 각 요소에 함수를 적용해주는 함수이다.
- map은 원본 리스트를 변경하지 않고 새 리스트를 생성합니다
- 모든 element 들에 대해서 같은 적용을 하고 싶을때에 자주 사용한다.
    - ex) str.map(lambda x : x.zfill(3))

```python
# 리스트의 모든 값을 정수로 변환하고 싶다고 하자.
# MAP 함수를 모른다면 아래와 같이 for 문으로 일일히 int 함수를 적용시켜야 한다.
lis = [1.2, 2.5, 3.7, 4.6]
for i in range(len(lis)):
    lis[i] = int(lis[i])
lis
```


```python
# 하지만 아래와 같이 적용 가능
lis = list(map(int, lis))
```

- map 에 다양한 Custom 함수를 적용 가능합니다. 

```python
lst = [(1,4),(2,10),(3,11)]
list(map(lambda x : x[0] , lst)) 
# [1,2,3]
```

- 위와 같이 lambda 를 적용한다면, 매우 쉽게 모든 element 에 대해 연산을 수행할 수 있습니다.



## print

- 문자열을 출력하는 함수
- 기본적으로 print 함수를 쓸때마다, 줄바꿈으로 문자가 바뀐다. 
    - 이를 수정하기 위해서는 end 를 바꾸어 주면 된다.
- 변수의 '이름' 이 아니라 그 '값' 을 출력하고 싶다면 그 앞에 f 를 쓴 뒤 중괄호로 변수를 싸주면 된다.


```python
a = 10 ; b = 20
print('x') ; print('y') # x,y 가 줄바꿈으로 구분되어 출력되고있다.
print('x',end = ' ') ; print('y') # x,y 가 띄어쓰기를 경계로 구분되고 있다.
print(f'{a} 와 {b}') # f string 을 이용해 변수의 '값' 을 출력하고 있는 모습
```

    x
    y
    x y
    10 와 20


## reversed

- mutable 한 객체를 reverse 하게 만들고 싶을때 쓴다.
  - 근데 별로 안씀... 쓰면 [::-1] 을 더 많이씀
- [1,2,3].reverse() 를 해버리면 원래 list 가 없어지고 inplace 하게 reversed 가 되어서 불편할 떄가 많은데, 그럴 때에 사용하는 함수가 reversed


```python
lis = [1,4,3,2,5]
```


```python
print(list(reversed(lis)))
print(lis)
```

    [5, 2, 3, 4, 1]
    [1, 4, 3, 2, 5]


## range

- range(a,b) : a,a+1.....b-1 의 range 객체를 만든다.
- range(a,b,k) : a,a+k... 으로 간격이 k 가 됨
    - 이때 k 는 음수도 가능합니다.
    - 다만 음수를 넣으려고 한다면 , a>b 가 되어야 합니다.
- range(a,a) : 이 경우 아무것도 출력하지 않습니다.


```python
for i in range(0):
    print(i)
```


```python
for i in range(10,10):
    print(i)
```

- 이때에 역방향으로 적용하고 싶은 경우 아래와 같은 방법이 좀 더 직관적입니다.

```python
for i in range(N)[::-1] : 
    print(i)
```

## sorted

- sorted 를 통해서 iterable 객체를 정렬할 수 있다.
- .sort() 는 list 만 가능하지만 위 sorted 는 iterable 객체에 대해서 모두 성립한다.

- 내림차순 정렬 : sorted({},reverse=True))
- 기준을 선택해 정렬 : sorted(a, key = lambda x : x[0]) # element의 의 첫번째 인자가 기준이 되어 정렬된다.
- 기준을 여러개 선택해 정렬 sorted(a, key = lambda x : (x[0],x[1])) # element 의 첫번쨰, 두번째 인자가 차례로 기준이 되어 정렬됨 


```python
# a 의 element 가 tuple 이여도 정렬할 수 있습니다. 
a = [(1, 2), (0, 1), (5, 1), (5, 2), (3, 0)]
```


```python
# 인자없이 그냥 sorted()만 쓰면, 리스트 아이템의 각 요소 순서대로 정렬을 한다.
b = sorted(a)
# b = [(0, 1), (1, 2), (3, 0), (5, 1), (5, 2)]
# key 인자에 함수를 넘겨주면 해당 함수의 반환값을 비교하여 순서대로 정렬한다.
c = sorted(a, key = lambda x : x[0])
# c = [(0, 1), (1, 2), (3, 0), (5, 1), (5, 2)]
d = sorted(a, key = lambda x : x[1])
# d = [(3, 0), (0, 1), (5, 1), (1, 2), (5, 2)]
e = sorted(a, key = lambda x: (x[0],x[1]))
# e = [(0, 1), (1, 2), (3, 0), (5, 1), (5, 2)]
```

- sorted 가 string 을 인자로 받으면, 그 출력은 항상 list 가 됩니다. 

```python
a = '1432'
sorted(a) # ['1','2','3','4']
```

- key 를 임의로 조절할 수 있습니다.
  - key 로 받은 데이터에 대해 '오름차순 정렬' 한다는것을 명심합시다!

```python
def solution(strings, n):
    answer = sorted(strings, key = lambda x : x[n]+x[:n]+x[n+1:])
    return answer
# 위와 같이, n 번째 알파벳을 우선시하는 사전순 정렬 sorting 을 구현할 수 있습니다.
```

- 또한 key 에 음수 등을 곱함으로서 내림 / 오름차순을 동시에 적용할 수 있습니다.

```python
sorted(lst, key= lambda x : (-1*x[1],x[2],-1*x[3],x[0]))
# 1,3 index 에는 내림차순, 2,0 index에는 오름차순을 적용합니다.
```

- 또는 key 에 직접 정의한 함수를 넣을 수도 있습니다.

```python
def custom(x) : 
    ans = []
    ans.append(len(x)) # 먼저 길이를 기준으로 Ordering 
    for i in x :
        if i.isdigit() :
           cnt += int(i)
    ans.append(cnt) # x 내에서 , 숫자의 합을 기준으로 Ordering
    ans.append(x) # 그 이후에는 사전순 Ordering 
    return ans
sorted(lst, key = custom) # 길이 / 숫자합 / 사전순 순서로 Ordering
```

- 위와 같이 Custom 함수를 이용하여 Ordering 을 할 수 있습니다.

## sum

- List 나 dict 가 자체적으로 연산은 불가능하지만 sum 의 메소드는 작동한다
- 즉 평균이나 합은 쉽게 구할 수 있다.


```python
sum([1,2,3]) #6
sum({1,2,3}) #6
```

- 비어있는 경우에는 0 을 출력합니다. (조심..) 
  - max, min 은 에러인데... 

```
sum([]) # 0
```



## type

- type 은 객체에 대한 자료형이 무엇인지 알려 주는 함수이다.
- 어떤 형태인지 알기 위해서 쓸 수 있다.
    - pandas 에 .dtype 등의 메서드가 있지만 위 type 은 내장함수이기 때문에 범용적으로 사용된다. 


```python
type("abc")
```




    str

## zip

- 파이썬 에서는 zip이라는 내장함수가 있다. zip() 은 동일한 개수로 이루어진 자료형을 묶어 주는 역할을 하는 함수이다.
- dataframe 의 column 을 df.columns 로 리스트 형태로 받은 뒤, 그에 따른 weight 를 지정해 준 후 dict(zip 으로 묶어서 classification 시에 이용할 수 있다.
    - keras/lgbm 등은 weight 를 설정할 때에, 각 분류에 따른 가중치를 dict 형식으로 받는다.
- 또는 같은 길이의 list 를 여러개 묶은 뒤 for문을 한번에 적용할 수 있다.
    - fot i,j in zip(lis1,lis2): 로 쓴다면 i,j 를 한번에 쓸 수 있다.



```python
fruits = ["Apple", "Pear", "Peach", "Banana"]
prices = [0.35, 0.40, 0.40, 0.28]
```


```python
# 아래와같이 같은 길이의 list(혹은 numpy 도 사용할 수 있음)를 이용하면 dict로 변환가능
dic = dict(zip(fruits, prices))
print(dic)
```

    {'Apple': 0.35, 'Pear': 0.4, 'Peach': 0.4, 'Banana': 0.28}



```python
lis = list(zip(fruits,prices))
print(lis)
```

    [('Apple', 0.35), ('Pear', 0.4), ('Peach', 0.4), ('Banana', 0.28)]


## list , tuple , set
- 각 패키지의 메소드마다 입력값으로 받는것이 다르다.
    - list 만 받는다던가, dict 형태로만 받는등....
- 그럴때에 맞는 형태로 바꾸기 위해서 쓰인다.

- **list( )**: 리스트 변환
- **tuple( )**: tuple 변환
- **set( )**: 집합 변환

## input

- input 은 어떠한 값을 입력받을때 사용된다.
- 주로 코딩테스트시에 많이 이용됨
- input 은 입력한 값은 string 으로 불러오기 때문에 따로 수로 지정하고 싶은 경우 int 를 사용자가 직접 지정해 주어야 한다.

**Example** 

- a,b = input().split()
    - 띄어쓰기로 구분된 값을 a,b 로 각각 받는다.
    - 2 4 -> a:2/b:4
- lis = list(input().split()) 
    - 띄어쓰기로 구분된 값을 list 형태로 받는다.
    - 5 6 3 2 1 -> lis:[5,6,3,2,1] 
- num=list(map(int, str(num))) 
    - num 을 각각 구분된 int 로 분해
    - 35243 -> num = [5,6,2,4,3]
- list(string) 
    - string 을 각각 구분된 글자로 분해
    - 'love' -> ['l','o','v','e']

## sys.exit

- 아예 프로그램을 종료해버는 역할을 한다.
- 원하는 답이 나와서 print('답') 만 하고, 나머지는 다 무시해버리고 싶을때에 사용! (재귀문에서 사용됨)





# Flow control

## if

- if 문은 다양한 구문을 조건문으로 가질 수 있다.

> IF list : 

- 위처럼 'list 가 비어있지 않을떄에' 로 사용할 수 있다.

> IF 10 <= a < 14 :

- 위처럼 부등호를 양쪽에 적용할 수 있다.

> IF 10<a and 3<k and ........ 

- 다양한 구문들을 And 로 엮을 수 있다. 

> IF not a == k : 

- not , or 등과 활용할 수 있다.

> IF x == (4 or 6) and x == 7

- 위와 같이 or 과 같이 쓰게되면 괄호로 분명하게 명시해야 합니다.

## if any(..for) / if all(..for)

- any 와 all 은 각각 하나라도 / 모두의 의미를 가지고 있다.
- 아래처럼 all 과 for문을 통해서 '모두 맞을때' 의 의미를 구성할 수 있다.
- all / any 는 iterable 를 입력으로 받아, 안의 모든것들이 True 거나 또는 하나 이상이 True 일 때에 True 를 반환한다.


```python
lis = list(range(5))
if all([lis[1] < 10 for x in lis]):
    print(3)
```

    3


## continue

- 코드를 continue 를 통해서 건너뛸 수 있다.
- continue 아래의 코드는 실행하지 않고 건너뛴 뒤 다음 반복을 시작한다.


```python
for i in range(5):       # 0부터 5까지 증가하면서 반복
    if i % 2 == 0:         # i를 2로 나누었을 때 나머지가 0면 짝수
        continue           # 아래 코드를 실행하지 않고 건너뜀
    print(i)
```

    1
    3



```python
i = 0
while i < 5:        
    i += 1            
    if i % 2 == 0: # 2의 배수이면 
        continue   # 같은 블록안의 싸~악 건너 띄고 '다음 반복'을 시작하세요~
    print(i)
print('이건무시못함') # 같은 줄에 있지를 않아서 이건 무시 못한다.
```

    1
    3
    5
    이건무시못함


## Break

- for와 while 문법에서 제어흐름을 벗어나기 위해 사용한다. 
- break는 제어흐름을 중단하고 빠져 나오지만
- continue는 제어흐름(반복)을 유지한 상태에서 코드의 실행만 건너뛰는 역할을 합니다



```python
i = 0
while True:    # 무한 루프
    print(i)
    i += 1          # i를 1씩 증가시킴
    if i == 5:    # 5일때
        break       # 반복문을 끝냄. while의 제어흐름을 벗어남
```

    0
    1
    2
    3
    4



```python
for i in range(10000):    # 0부터 9999까지 반복b
    print(i)
    if i == 5:    # i가 100일 때
        break       # 반복문을 끝냄. for의 제어흐름을 벗어남
print('이건무시못하지') # for 문 뒤의 값은 무시 못한다.
```

    0
    1
    2
    3
    4
    5
    이건무시못하지


## Pass

- 아무 일도 하지 않지만, if/while/for 등의 문장 구조 형태를 유지하고 싶다면 Pass 를 쓰자.


```python
for i in range(10):    # 10번 반복
    pass               # 아무 일도 하지 않는다
```


```python
if i == 0 :
    pass # 이 역시 마찬가지
```


```python

```

## for else

- for문을 사용하다보면, 루프 중간에 break 문으로 빠져나오는 경우들이 있는데, 이게 break문이 걸려서 빠져나가는지 아닌지를 판단이 필요한 경우가 있습니다.
- for문과 같은 레벨에 else를 둬서 break없이 빠져나온 경우를 처리하는 방법이 있다.




```python
for x in range(4):
    if x == 2:
        print ('loop out')
        break
else:
    print ('loop end')
```

    loop out


-  위 예제의 경우는 x =2 에서 루프를 빠져나오기때문에, else문이 실행이 되지 않고, 'loop out' 이 출력이 된다.


```python
for x in range(4):
    pass
else:
    print ('loop end')
```

    loop end


- 위와 같은 경우는 , for loop가 break없이 빠져나왔으므로 'loop end' 가 출력이 된다.

## for while

- 각각의 작업들을 어떤 조건을 만족할때까지 수행시키고 싶다고 할 때에 사용합니다.


```python
num = [1,2,3,4]
stack = [1,4,3,2]
for x in num: 
    while stack and stack[-1]<x: # 스택이 비거나, 제일 위의 스택이 num 의 값보다 작을때 멈춘다!
        stack.pop() 
print(stack)
```

    [1, 4]


## try exept

- 다음에서 진행되는 flow 들은 에러발생시 어떻게 대처해야하는지의 구문들이다.


```python
Image('./image/try.png')
```




​    
<img src="/assets/images/2.Functions/output_116_0.png">
​    



- try, exept 문
- try 안에는 기본적으로 실행하는 코드를 넣ㅎ고, exept 절에는 에러가 발생했을 경우 시행할 코드를 넣는다.


```python
try:
    print(5/0)
except:
    print('wrong division')
```

    wrong division


## try except else

- try 절과 except 절에 else 를 추가하여 구성할 수 있다.
- else 는 예외가 발생하지 않아 except 절을 실행하지 않았을 때에 실행되는 구문이다


```python
try:
    print(5/1)
except:
    print('error')
else:
    print('no error')
```

    5.0
    no error


## try except finally

- finally 절은 try 절에서 예외의 발생여부에 관계없이 항상 실행되는 절이다.


```python
try:
    print(5/0)
except:
    print('error')
finally:
    print('end')
```

    error
    end


## 이중 for문 탈출

- 단일 for 문이라면 Break 를 통해서 빠져나올 수 있었다. 
- 하지만 이중 for 문이라면 어떨까?


```python
a = 0 
for x in range(5):
    for y in range(5):
        a = y 
        print(a)
        if a == 1 : # a 가 1이 되면 모든 for 문을 중지시키고 싶다!
            break
print(a)
```

    0
    1
    0
    1
    0
    1
    0
    1
    0
    1
    1


- 위처럼 print 를 할 때에 제대로 수행되지 않음을 볼 수 있다.
- 하나의 break 를 하게되면 그 바로 상단의 반복문, 즉 for y 의 부분을 중지시키기 때문이다.


```python
a = 0 
for x in range(5):
    for y in range(5):
        a = y 
        if a == 1 : # a 가 1이 되면 모든 for 문을 중지시키고 싶다!
            break
    a = 2
    break 
print(a)
```

    2


- 위와 같이 두번의 break 을 준다고 해도 결과는 같다. 둘이 '별개로' break 가 작용하기 때문에 둘의 break 는 연동되지 않는다. 
- 그 증거로 위에서 a = 2 를 시행하고 어서, 결과가 2가 나온것을 볼 수 있다.
- break 가 연동된다면 a = 1 이여야 한다.


```python
a = 0 
switch = False
for x in range(5):
    for y in range(5):
        a = y 
        if a == 1 : # a 가 1이 되면 모든 for 문을 중지시키고 싶다!
            switch = True
            break
    if switch :
        break
```

    0
    1

