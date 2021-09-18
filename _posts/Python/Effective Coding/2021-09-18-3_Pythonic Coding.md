---
title:  "Pythonic Coding"
excerpt: "파이썬답게 코딩하기(~ing)"
categories:
  - Py_Effective
date : 2021-09-18 13:00:00 +0900
last_modified_at: 2021-09-12

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 파이썬을 파이썬 답게 코딩하는 방법에 대해서 알아봅시다.
{: .notice--warning}

# [파이썬의 버전 알기](#link){: .btn .btn--primary} 

- 프로그램은 개발자들에 의해 서서히 유지 / 보수됩니다. 
- 같은 프로그램(파이썬) 을 사용하더라도 버전에 따라서 그 문법 / 결과물이 달라지기도 합니다. 

![png](/assets/images/Python/29_1.png)

- 위의 경우 2.x -> 3.x 로 진행될때에 변한 대표적인 파이썬 문법들입니다.
- 즉, 일관성을 지키기 위하여 다른 개발자와 협업할때에 다른 프로그램의 버전을 쓰는것은 일반적으로 용납되지 않습니다. 
- 그러므로 개발자들은 같은 프로그램의 버전을 사용하고, `requirements.txt` 등으로 같은 버전의 패키지를 쓰려고 ㅎㅂ니다.

> ## Version 체크하기

```python
import sys
print(sys.version)

>>> 3.8.1 (default, Jul 10 2020, 17:43:13)
```

- 위와 같이 , 파이썬의 버전을 sys 모듈에서 체크할 수 있습니다.

# [Pep 참고하기](#link){: .btn .btn--primary} 

- Pep 이란 PEP(Python Enhancement Proposal), 즉 파이썬 개선 제안서는 파이썬 코드를 어떻게 구성할지 알려주는 스타일 가이드 입니다. 
- 이러한 Pep 을 참고하여 많은 사람들이 코드 스타일을 일관되게 유지하려고 합니다. 
- Pep 에 대해서는 그 내용이 매우 방대하므로 여기에서는 매우 짧게 설명만하고 자세히는 다른 문서에서 따로 알아보도록 하겠습니다.

## [Bytes, str,unicode 차이알기](#link){: .btn .btn--primary} 

- 인코딩은 매우 중요합니다. 통계학을 공부하는 사람이라면, R 의 Default 언어가 CP949 인지 UTF-8 인지에 따라서 문자가 에러가 나기도 합니다.
- 만일, 나는 CP949 로만 처리가 가능한데, 클라이언트가 UTF-8 로 입력이 오면 어떡할까요? 
  - 상대방의 utf 를 binary stream 으로 변환하고, 그것을 다시 cp949 로 변환해야 할 것입니다.

> ## Bytes 인스턴스란? 

- bytes 인스턴스에 대해 간단히 소개한다.
  - str 문자열을 생성하는 방법은 " ㅁㄴㅇㄻㄴㅇㄹ"와 같이 따옴표 안에 문자나 숫자를 적는 것이다. 
  - 반대로 bytes는 b'\x41'과 같이 문자열 앞에 b를 붙여야 한다.
- 아까 bytes는 8비츠로 이루어진다고 했다. 유의미한 바이츠 인스턴스는 ascii 상수로만 이루어진다. 
  - 저 위의 b'\x41'가 보이는가? 41은 16진수의 수이고 10진수로 65다. 그리고 '\x'가 저 숫자가 16진수임을 보증한다. 
  - 저걸 디코드하면 'A'가 나올 것이다. 왜냐하면 'A'의 ASCII 코드가 65이기 때문이다.

```python
>>> b'\x41'
b'A'
```

> ## 파이썬에서 문자 Sequent 다루는법

- 파이썬에서 문자 Sequence 를 나타내는 방법은 유니코드 문자열 방식과, bytes 방식 2가지입니다. 
  - 문자는 str, 바이츠는 bytes 클래스로 표현합니다.
- 'str -> bytes'는 str의 encode 메소드를 통해야 한다.
- *bytes -> str'은 bytes의 decode 메소드를 통해야 한다.

```python
# example
'a'.encode(encoding='CP949') # 1.
b'\x45'.decode('CP949') # 2.
```

> ## 운영체제마다 다른 인코딩

- Ubuntu를 기준으로 인코딩, 디코딩 모두 기본 인코딩은 'utf-8'을 사용하며, 'CP949' 등 다른 인코딩을 사용하려면 메소드에 인자를 주면 됩니다. 기본 인코딩은 운영체제 환경에 따라 다를 수 있습니다.
- 윈도우를 사용하며 인코딩을 공부하기 위해 바탕화면에 txt 파일을 놓고 쓰고 지우고를 많이 반복했다고 합시다.

```python
fp = open('example.txt', 'r', encoding='utf-8').read()
```

- 위 코드의 결과가 무엇이 나왔을까요? *UnicodeDecodeError* 가 발생합니다.
-  윈도우는 기본적으로 CP949 인코딩을 사용한다. 그런데 그것을 utf-8 인코딩을 사용해 열었으니 안 열리는 것이다. 
- 각 인코딩 방법마다 글자를 표현하는 방법이 다르다. 위와 같은 일을 막기 위해서는 인코딩을 알아야 합니다..

# [Sequence Slice 하는법](#link){: .btn .btn--primary} 

- 파이썬은 다른 프로그래밍 언어와 마찬가지로 리스트 등의 시퀀스를 슬라이스해서 조각으로 만드는 문법을 제공한다.
- 이를 통해 시퀀스의 부분집합을 쉽게 구할 수 있다.

- 파이썬은 기본 슬라이싱뿐만 아니라 *somelist[start : end : stride]* 처럼 슬라이싱의 간격(stride)를 지정하는 특별한 문법도 있다.
- 이 문법을 사용하면 **시퀀스(Sequence)를 슬라이스할 때 매 n번째 아이템을 가져올 수 있다.** 예를 들어 stride를 쓰면 리스트에서 홀수와 짝수 인덱스를 손쉽게 그룹으로 묶을 수 있다.

```
a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
evens = a[::2]
odds = a[1::2]

# 값이 아니라 인덱스다!
print("Evens are ", evens)  # Even indices are  [1, 3, 5, 7, 9]
print("Odds are", odds) # Odd indeices are [2, 4, 6, 8, 10]
```

- 문제는 stride 문법이 종종 예상치 못한 동작을 해서 버그를 만들어내기도 한다는 것이다.
- 예를 들어 파이썬에서 바이트 문자열을 역순으로 만드는 일반적인 방법은 스트라이트 -1로 문자열을 슬라이스하는 것이다.

```python
x = b'mongoose'
y = x[::-1]
print(y)  # b'esoognom'
```

- 위의 코드는 바이트 문자열이나 아스키 문자에는 잘 동작하지만, UTF-8 바이트 문자열로 인코드된 유니코드 문자에는 원하는 대로 동작하지 않는다.

```
w = '김철수'
x = w.encode('utf-8')
y = x[::-1]

z = y.decode('utf-8')
UnicodeDecodeError: 'utf-8' codec can't decode byte 0x98 in position 0: invalid start byte.
```

- 이 이슈는 주요 인코딩 방식인 UTF-8에 종속되는 문제로, 인코딩에 대한 이해가 부족하면 쉽게 이해할 수 없는 문제이기도 하다.

> ## Stride 의 사용법

```
a = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h']
print(a[::2])   # ['a', 'c', 'e', 'g']
print(a[::-2])  # ['h', 'f', 'd', 'b']
```

- `::2`는 처음부터 시작해서 매 두 번째 아이템을 선택하라는 의미이다.
- `::-2`는 끝부터 시작해서 반대 반향으로 매 두 번째 아이템을 선택하라는 의미이다.
- 이건 뭘까?

```python
print(a[2::2])     # ['c', 'e', 'g']
print(a[-2::-2])   # ['g', 'e', 'c', 'a']
print(a[-2:2:-2])  # ['g', 'e']
print(a[2:2:-2])   # []
```

- 물론 고민하면 이해할 수는 있다. 문제는 슬라이싱의 stride 문법이 매우 혼란스러울 수 있다는 것이다. 대괄호 안에 숫자가 세 개나 있으면 빽빽해서 읽기 힘들다.
- 그래서 start, end 인덱스가 stride와 연계되어 어떤 작용을 하는지 분명하지 않다. 특히 stride가 음수이면 더더욱 그렇다.
- 이런 문제를 방지하려면 가급적 **start, end, stride를 함께 사용하지 말아야 한다.**
- Sequence를 slicing할 때, stride를 쓰고 싶다면 다음을 기억하도록 하자.
- stride를 사용해야 하면 양수 값을 사용하고, start, end를 생략하자.
- stride를 start나 end와 함께 꼭 사용해야 한다면

1. **stride를 적용한 결과를 변수에 할당하고**
2. **이 변수를 슬라이스한 결과를 다른 변수에 할당해서 사용하자.**

```
b = a[::2]   # ['a', 'c', 'e', 'g']
c = b[1:-1]  # ['c', 'e']
```

- 슬라이싱부터 하고 스트라이딩을 하면 데이터의 얕은 복사본(shallow copy)가 추가로 생긴다. 첫 번째 연산은 결과로 나오는 슬라이스의 크기를 최대한 줄여야 한다.
- 프로그램에서 두 과정에 필요한 시간과 메모리가 충분하지 않다면 내장 모듈 *itertools* 의 *islice* 메서드를 사용해보자.

> ## Summary

- 한 슬라이스에 start, end, stride를 같이 지정하면 매우 혼란스러울 수 있다.
- 슬라이스에 start와 end 인덱스 없이 양수 stride 값을 사용하자. 음수 stride 값은 가능하면 피하자.
- 한 슬라이스에 start, end, stride를 함께 사용하는 상황은 피하자. 꼭 필요하면 두 번 할당하거나, 내장 모듈 *itertools* 의 *islice* 를 사용하자.

<br>

 이제 하나하나 어떤식으로 파이썬을 파이썬답게 사용할 수 있는지 알아보겠습니다.
{: .notice--success}

