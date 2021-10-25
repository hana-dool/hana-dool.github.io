---
title:  "Functions &#58; open,closed"
excerpt: "파일을 읽어내고, 저장하는 함수 알아보기"
categories:
  - Py_Advanced
last_modified_at: 2021-09-28

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"

use_math : true
---

 파일을 읽고 저장하는 함수에 대해서 알아봅시다. 분석을 하다 보면 파일의 결과를 관리해야될 순간이 옵니다. 이를 위해서 결과를 저장하는 방법에 대해서 알아봅시다. 
{: .notice--warning}

# [write files](#link){: .btn .btn--primary}{: .align-center}

> ## w : 파일에 내용 쓰기

- 다음 소스 코드를 에디터로 작성해서 저장한 후 실행해 봅시다.
- 프로그램을 실행한 디렉터리에 새로운 파일이 하나 생성된 것을 확인할 수 있을 것입니다.

```python
f = open("새파일.txt", 'w')
f.close()
```

![png](/assets/images/Python/35_1.png)

- 위처럼, 파일이 하나 생성된것을 볼 수 있습니다. 
- 파일을 생성하기 위해 우리는 파이썬 내장 함수 open을 사용했습니다. 
  - open 함수는 다음과 같이 "파일 이름"과 "파일 열기 모드"를 입력값으로 받고 결괏값으로 파일 객체를 돌려주게 됩니다.

> 파일 객체 = open(파일 이름, 파일 열기 모드)

- 파일 열기 모드에는 다음과 같은 모드가 있습니다.

| 파일열기모드 | 설명                                                       |
| :----------- | :--------------------------------------------------------- |
| r            | 읽기모드 - 파일을 읽기만 할 때 사용                        |
| w            | 쓰기모드 - 파일에 내용을 쓸 때 사용                        |
| a            | 추가모드 - 파일의 마지막에 새로운 내용을 추가 시킬 때 사용 |

- 파일을 쓰기 모드로 열면 해당 파일이 이미 존재할 경우 원래 있던 내용이 모두 사라지고, 해당 파일이 존재하지 않으면 새로운 파일이 생성된다.
- 위 예에서는 디렉터리에 파일이 없는 상태에서 새파일.txt를 쓰기 모드인 'w'로 열었기 때문에 새파일.txt라는 이름의 새로운 파일이 현재 디렉터리에 생성되는 것 입니다. 

> 파일을 상대경로를 이용해 저장하기

![png](/assets/images/Python/35_2.png)

- 위와 같이 파일을 w 로 열게되면 새로운 이름의 파일이 경로에 저장되게 됩니다. 

> ## close : 파일 객체 닫기 

- 위 예에서 `f.close()`는 열려 있는 파일 객체를 닫아 주는 역할을 한다. 
- 사실 이 문장은 생략해도 된다. 프로그램을 종료할 때 파이썬 프로그램이 열려 있는 파일의 객체를 자동으로 닫아주기 때문이다. 
- 하지만 `close()`를 사용해서 열려 있는 파일을 직접 닫아 주는 것이 좋다. 쓰기모드로 열었던 파일을 닫지 않고 다시 사용하려고 하면 오류가 발생하기 때문이다.

> ## 출력값 저장하기

- 위 예에서는 파일을 쓰기 모드로 열기만 했지 정작 아무것도 쓰지는 않았다. 
- 이번에는 에디터를 열고 프로그램의 출력값을 파일에 직접 써 보자.

```python
f = open("./history/새파일.txt", 'w')
for i in range(1, 11):
    data = f"{i}번째 줄입니다.\n"
    f.write(data)
f.close()
```

- 위와 같이 데이터를 계속 txt 파일에 저장할 수 있습니다. 

![png](/assets/images/Python/35_3.png)

- 위와 같이 데이터의 내용이 저장되는것을 볼 수 있습니다.

# [Read files](#link){: .btn .btn--primary}{: .align-center}

- 파이썬에서는, 외부 파일을 읽어서 프로그램을 저장할 수 있는 방법이 여러개 있습니다.

> ## readline 함수 이용하여 읽기

```python
f = open("./history/새파일.txt", 'r')
line = f.readline()
print(line)
# >> 1번째 줄입니다.
f.close()
```

- 위와 같이, readline 을 사용하여 제일 첫번쨰 줄을 읽어들입니다. 
- 위를 이용하여, 모든 line 을 읽어들이고 싶가면 , While True 함수와 같이 사용해야합니다.

```python
f = open("./history/새파일.txt", 'r')
while True:
    line = f.readline()
    if not line: break
    print(line)
# >> 1번째 줄입니다.
# >> 2번째 줄입니다.
# ......
# >> 10번째 줄입니다.
f.close()
```

> ## readlines 함수 이용하여 읽기

- 두번째 방법은 readlines 함수를 이용하는것입니다.

```python
f = open("./history/새파일.txt", 'r')
lines = f.readlines()
print(lines)
# ['1번째 줄입니다.\n', '2번째 줄입니다.\n', '3번째 줄입니다.\n', '4번째 줄입니다.\n', '5번째 줄입니다.\n', '6번째 줄입니다.\n', '7번째 줄입니다.\n', '8번째 줄입니다.\n', '9번째 줄입니다.\n', '10번째 줄입니다.\n']
f.close()
```

- readlines 함수는 파일의 '모든 줄을 읽어서' 각각의 줄을 요소로 가지는 list를 돌려줍니다. 
- 이떄에 위에서 보이는 \n 을 지우고 싶다면 

> ## read 함수 사용하여 읽기

```python
f = open("./history/새파일.txt", 'r')
data = f.read()
data
# '1번째 줄입니다.\n2번째 줄입니다.\n3번째 줄입니다.\n4번째 줄입니다.\n5번째 줄입니다.\n6번째 줄입니다.\n7번째 줄입니다.\n8번째 줄입니다.\n9번째 줄입니다.\n10번째 줄입니다.\n'
```

- 위와 같이 read() 를 이용하여 파일을 읽을 수 있습니다.
- 그 경우에는 모든 파일을 string 으로 읽어들입니다.

```python
data.strip().splitlines()
['1번째 줄입니다.',
 '2번째 줄입니다.',
 '3번째 줄입니다.',
 '4번째 줄입니다.',
 '5번째 줄입니다.',
 '6번째 줄입니다.',
 '7번째 줄입니다.',
 '8번째 줄입니다.',
 '9번째 줄입니다.',
 '10번째 줄입니다.']
```

- 위와 같이 splitlines() 를 쓰게 되면 list 가 잘 적용됩니다.

# [Add contents to files](#link){: .btn .btn--primary}{: .align-center}

- 쓰기 모드('w')로 파일을 열 때 이미 존재하는 파일을 열면 그 파일의 내용이 모두 사라지게 된다. 
- 하지만 원래 있던 값을 유지하면서 단지 새로운 값만 추가해야 할 경우도 있다. 
- 이런 경우에는 파일을 추가 모드('a')로 열면 된다. 에디터를 켜고 다음 소스 코드를 작성해 보자.

```python
f = open("./history/새파일.txt", 'a')
for i in range(1, 11):
    data = f"{i}번째 줄입니다.\n"
    f.write(data)
f.close()
```

![png](/assets/images/Python/35_4.png)

- 위와 같이 새 파일에 내용이 더 더해지는것을 볼 수 있습니다.

> ## With 을 이용하여 파일 저장하기 

```python
f = open("foo.txt", 'w')
f.write("Life is too short, you need python")
f.close()
```

- 계속 위와 같이 파일을 열고 닫는 방식으로 파일을 열고 저장했습니다. 
- 하지만 이럴때에 이것을 자동으로 처리할려면 어떻게 해야할까요?
  - with 문을 사용하면 됩니다. 

```python
with open("foo.txt", "w") as f:
    f.write("Life is too short, you need python")
```

- 위와 같이 with문을 사용하면 with 블록을 벗어나는 순간 열린 파일 객체 f가 자동으로 close되어 편리하다.

# [Create Folders](#link){: .btn .btn--primary}{: .align-center}

- 출력값이 사진등 많을 경우에는 Directory folder 를 직접 만들어내서 저장할 수 잇습니다.
  - 폴더가 없는 경우, 해당 Directory 가 없는경우 Directory 를 형성할수도 있습니다. 

> ## 하위 위치에 폴더 형성

```python
import os
os.makedirs('./folder')
```

- 위와 같이 실행하게 된다면, 하위 directory 에 folder 문서를 만들게 됩니다. 

```python
path = './text'
try:
    if not os.path.exists(path):
        os.makedirs(path)
except OSError:
    print("Error: Cannot create the directory {}".format(path))
```

- 위 코드는 path 에 folder 가 있지 않는 경우 folder 를 형성하는 코드입니다.
  - OSE error 는 생성 파일 이름에 잘못된 값 (ex. '/' '\' ':' 등의 문자)이 들어간 경우 OSERROR 발생합니다.
  - 그러므로 OSE  error 가 발생시에는 위와 같은 구문을 print 하게 됩니다.

---



**reference**

- [https://datascienceschool.net](https://datascienceschool.net/01%20python/02.15%20%ED%8C%8C%EC%9D%B4%EC%8D%AC%EC%97%90%EC%84%9C%20%EB%82%A0%EC%A7%9C%EC%99%80%20%EC%8B%9C%EA%B0%84%20%EB%8B%A4%EB%A3%A8%EA%B8%B0.html)
- <https://dojang.io/mod/page/view.php?id=2463>
- <https://data-make.tistory.com/170>
- <https://growingsaja.tistory.com/28>
- <https://wikidocs.net/26>

