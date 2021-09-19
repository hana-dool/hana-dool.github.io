---
title:  "1-2 Class Magic Method"
excerpt: "파이썬 클래스의 매직 메서드"
categories:
  - Py_Advanced
last_modified_at: 2021-09-19

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"

use_math : true
---

 아마 비전공자라면, 파이썬의 Class 까지 심도있게 다룬 사람은 별로 없을것입니다. 하지만 파이썬에서 Class 는 매우 중요한 위치를 가집니다. 이러한 Class 에 대해서 알아보고 어떻게 활용할 수 있는지 알아봅시다.
{: .notice--warning}

# [Magic Methods](#link){: .btn .btn--primary}{: .align-center}

- 메서드라는 것은 우리가 클래스를 만들면서 그 안에 만들어 넣은 함수를 말합니다.
- 만들어진 메서드를 사용하려면 객체.메서드()와 같은 형식으로 호출을 해주었습니다.
-  이제는 특별한 메서드들에 대해서 말해보겠습니다.

> ## 은밀하게 수행되던 매직 메서드

- 'ab' + 'cd' = 'abcd' , 왜 옆처럼 각 문자열을 더하면 이어질까요? 
- 그것은 바로 덧셈 연산자를 입력할때, '특정한 동작' 을 수행하도록 매직 메서드로 정의했기 때문입니다. 
- 더 나아가, 파이썬에서 함수의 호출은 custom(x,y) ... 처럼 () 을 붙이는 행동에서 호출이 됩니다. 
  - 하지만 이 또한 () 를 입력하는것은 \_\_call\_\_ 을 호출하는 것이었습니다. 
  - 그 결과로 함수가 호출되는것입니다. 
- 객체에서 . 을 찍어서 해당 객체에 접근 할 수 있었던것도 기억하시나요?
  - 이 역시, \_\_getattribute\_\_ 라는 메직 메서드를 호출하는 것이였습니다. 
- 즉 위와 같이 우리가 무의식에 사용하던 많은 파이썬의 코딩 방법들은 모두 '매직 메서드' 기반으로 구현된 것이였습니다.

> ## \_\_init\_\_ (생성자)

> 객체 생성시 초기화 / 초기 Attribute 를 생성하기 위해 존재하는 메서드 

```python
# bookstore.py

class Book:
    def setData(self, title, price, author):
        self.title = title
        self.price = price
        self.author = author
        
    def printData(self):
        print '제목 : ', self.title
        print '가격 : ', self.price
        print '저자 : ', self.author
        
    def __init__(self):
        print ('책 객체를 새로 만들었어요~')
```

- _\_init\_\_ 메서드는, 인스턴스(객체) 가 생성될때 자동으로 만들어지는 메서드입니다.
- 위처럼 \_\_init\_\_ 함수에, print 를 정의한다면, Book 메서드를 호출할때에 바로 위와 같은 명령어를 호출할 것입니다.

```python
>>> import bookstore
>>> b = bookstore.Book()  
책 객체를 새로 만들었어요~
```

- 위처럼 Book 객체를 만들자 마자, \_\_init\_\_ 이 실행되면서 초기화 메서드가 사용된것을 볼 수 있습니다.

```python
class Calculator:
    def __init__(self):
        self.result = 0
    def add(self, num):
        self.result += num
        return self.result
```

- 주로 위처럼 self 메서드를 사용하여 Attribute 를 정의하는데에 사용됩니다.

> ## \_\_del\_\_ (소멸자) (del)

> 리소스 해제 등의 종료 작업을 알리기 위해 사용

\_\_init\_\_ 과는 반대로 객체가 없어질때에 호출되는 메서드입니다. 

```python
>>> class IceCream:
	def __init__(self, name, price):
		self.name = name
		self.price = price
		print(self.name + "의 가격은 " + str(price) + "원 입니다.")
	def __del__(self):
		print(self.name + " 객체가 소멸합니다.")
	
>>> objectIc = IceCream("월드콘", 1000)
월드콘의 가격은 1000원 입니다.
>>> del objectIc
월드콘 객체가 소멸합니다.
```

- 위와 같이, del 을 통해서 소멸되는 경우, 문구가 출력되는것을 볼 수 있습니다.

> ## \_\_repr\_\_ (프린팅) (print)

> 프린트

- 위에서 printData 의 메서드를 호출하는 대신에, print 문을 사용하여 책 제목을 찍어보려 합니다.
- 이러한 일을 가능하게 해 주는것은, 바로 \_\_repr\_\_ 메서드입니다.

```python
class Book:
    def __init__(self, title, price, author):
        self.title = title
        self.price = price
        self.author = author

    def printData(self):
        print('제목 : ', self.title)
        print('가격 : ', self.price)
        print('저자 : ', self.author)
    def __repr__(self):
        return self.title
    # print 를 사용할때에 출력할것
```

- 이제 클래스를 만들고, 한번 메서드를 써볼까요?

```
>>> b = Book('어린왕자','3000','외국인')
>>> print(b)
어린왕자
```

```python
>>> b = Book('어린왕자','3000','외국인')
>>> print(b)
<__main__.Book object at 0x0000021CBE47A088>
```

- 원래는 위처럼 Book object 라고 출력하는것이 정상입니다.

> Note : \_\_repr\_\_ 은 문자열을 return 해야 합니다.

```python
class Solution() :
    def __init__(self,first,second):
        self.first = first
        self.second = second
    def __repr__(self):
        return self.first + self.second
```

- 위와 같이 하게되면, 에러가 나게됩니다.
- 왜냐하면 repr 의 return 이 숫자형태이기떄문입니다.
  - 이를 고치기 위해서는 str 의 형태로 감싸주어야합니다.

> ## \_\_add\_\_ (덧셈) (\+)

> \+ 기호에 매핑되는 메서드

```python
class Shape:
    def __init__(self,area):
        self.area = area
    def __add__(self, other):
        return self.area + other.area
```

- 위와 같이 객체를 정의했다고 합시다. 

```python
>> a = Shape(10)
>> b = Shape(20)
>> a + b
30
```

- 위와 같이  \_\_add\_\_  메서드를 이용하여 + 를 구현할 수 있습니다. 

> ## \_\_dict\_\_ (내부속성)

> 인스턴스 내부에 어떠한 Attribute 가 있는지 확인하는 메서드

```python
class Person : 
    def __init__(self,name):
        self.name = name
    def getName(self) : 
        return self.name
```

- 위와 같이 Person class 를 정의해봅시다. 

```python
temp = Person('홍길동')
```

- 위와 같이, temp 에 Class 를 정의하여 , name 이라는 Attribute 에 '홍길동' 이라는 속성을 정의합니다.
- 이러한 name 과 홍길동 이라는 관계는 어디에 저장될까요?

```python
temp.__dict__
{'name': '홍길동'}
```

- 위와 같이 , 그 mapping 의 관계를 볼 수 있게 됩니다.

> ## \_\_getattribute\_\_ (Attribute 접근) (.)

- 파이썬에서 객체에 점을 찍으면 , 해당 객체에 접근할 수 있었습니다. 
  - 이렇게 점을 찍는 메서드에 대응되는 메서드입니다! 
- `__getattribute__`는 인스턴스에 해당 attribute가 있든지 없든지 호출되는데, 제일 **“선순위”**로 호출되는 녀석이다.
- 즉, 인스턴스에 그 attribute가 있어도, `__getattribute__`를 먼저 호출하면서 인풋인자로 해당 attribute를 넘겨주게 된다.

> ## \_\_getattr\_\_ (Attribute 없을때)

> 객체의 인스턴스 딕셔너리에 없는 Attribute 에 접근할때 뭔가 처리해야할 때에 사용

```python
# Example 1
class LazyRecord:
    def __init__(self):
        self.exists = 5

    def __getattr__(self, name):
        print(f'* Called __getattr__({name!r}), populating instance dictionary')
        value = f'Value for {name}'
        setattr(self, name, value)
        print(f'* Returning {value!r}')
        return value


# Example 2
data = LazyRecord()
print('Before:', data.__dict__)  # Before: {'exists': 5}
print('First foo:   ', data.foo)
print('After: ', data.__dict__)  # After:  {'exists': 5, 'foo': 'Value for foo'}
print('Second foo:   ', data.foo)
print('Has peach: ', hasattr(data, 'peach'))  # Has peach:  True
```



```python
class A:
    def __getattr__(self, name):
        return ('hahaha-'+name)
a = A()
a.ace = 'ace value'
print(a.ace) # ace value
print(a.ace2) # hahaha-ace2
print(a.__dict__) # {‘ace’: ‘ace value’}
```

- ace 는 처음에 a.ace = 'ace value' 로 할당하였으므로 존재한다.
  - 그러므로 그 값 그대로 출력하게 된다. 
- ace2 라는 녀석은 존재하지 않는다.
  - 그러므로 \_\_getattr\_\_ 가 호출된다. 
- \_\_dict\_\_ 를 보면 ace 라는 Attribute 와 그 값을 볼 수 있습니다.
- 이때에 Class A 에 \_\_aetattribute\_\_ 를 추가하면 어떨까요? 

```python
class A:
    def __getattr__(self, name):
        return (‘hahaha-’+name)
    def __getattribute__(self,name):
        return (‘jajaja-’+name)

a = A()
a.ace = ‘ace value’
print(a.ace)
print(a.ace2)
print(a.__dict__)
```



```python
jajaja-ace
jajaja-ace2
jajaja-__dict__
```

- ace에는 ‘ace value’라는 값을 할당해줬음에도 불구하고 `__getattribute__`가 호출되어 “먼저 가로챈다”는 것을 알 수 있다.
- ace2는 존재하지 않는 녀석인데, 이때도 `__getattr__`가 아닌 `__getattribute__`가 호출된다.
- `a.__dict__`의 출력결과를 보면, `__getattribute__`가 그야말로 가장 “선순위”로 호출됩니다.

- Summary 하면 다음과 같습니다.
  - `__getattribute__`는 (해당 attribute가 있든 없든) 가장 **“선순위”**로 호출된다.
  - `__getattr__`는 (해당 attribute를 찾을 수 없을경우) 가장 **“후순위”**로 호출된다.

---

**reference**

- <https://wikidocs.net/85>
- <https://blog.hexabrain.net/285>
- [https://starriet.medium.com](https://starriet.medium.com/%ED%8C%8C%EC%9D%B4%EC%8D%AC-getattr-%EC%99%80-getattribute-%EC%9D%98-%EC%B0%A8%EC%9D%B4-46ef0174e8e0)

