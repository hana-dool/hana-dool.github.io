---
title:  "Pycharm Settings"
excerpt: "파이참을 잘 다루어봅시다."
categories:
  - Py_Advanced
last_modified_at: 2021-10-12
toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
use_math : true
---

 파이참을 제대로 다뤄보는 법에 대해서 알아봅시다.
{: .notice--warning}

> ## IDE

- IDE 란 통합 개발 환경 (Integrated Development Environment) 로서 코딩 / 디버그 / 컴파일 / 배포 등 프로그램 개발에 관련된 모든 작업을 하나의 프로그램 안에서 해결하게 해 줍니다.
  - 물론 IDE 없어도 프로그래밍을 하는데에는 아무런 제약이 없습니다. 하지만 IDE 를 이용해 개발하면 매우 편리한 기능이 많습니다.
- 대부분의 IDE 가 가지고 있는 편리한 기능을 소개해 보겠습니다.
  - 코드의 자동 완성 기능
  - 실시간 문법 검사 
  - 유형에 맞는 색깔 
  - 디버거로 오류 점검
- 여기서 우리는 Python 의 대표적인 IDE 인 차이참에 대해서 알아보겠습니다.

> ## professional Edition

- 공짜버전(Community Edition) 과 유료 (Professional) 버젼이 나누어 있습니다.
- Professional 버전은 기본적으로 웹 개발, 데이터베이스 등을 지원합니다. 

> ## .idea 파일

- 이 폴더가 있으면 다른데 가서도 파이참을 이용해 불러올 수 있음
- 환경설정이 되어있는 파일

# [기본적인 환경 세팅](#link){: .btn .btn--primary}{: .align-center}

> ## 처음 설치시 

- Exising Interpreter 를 선택했을떄에 아무것도 뜨지 않을떄가 있습니다.
  - 기존에 설치되어있는 파이썬을 사용할지를 묻는것으로, 만일 파이썬이 우리 컴퓨터에 설치되어있지 않는 경우, 작동되지 않습니다. 
- 파이썬을 설치하게 된다면, Existing interpreter 에 파이썬이 추가가 되며 , 잘 작동하게 됩니다.

![png](/assets/images/Python/36_7.png)

- 저는 위처럼 Base Interpreter 를 Python 3.7 로 설정했기 떄문에 잘 볼 수 있습니다.

> ## 계정이름

![png](/assets/images/Python/36_8.png)

- 위와 같이 프로젝트가 만들어진것을 볼 수 있습니다.
- 이때에 계정 이름은 '영어' 가 되어야 해요! 안그러면 나중에 문제가 생기게 됩니다.

> ## Base interpreter 의 이점 

![png](/assets/images/Python/36_9.png)

- 파이참을 시작하면 위와 같이 첫 화면을 볼 수 있는데요 (이게 안보이는분은  아직 컴퓨터에 파이썬이 없기 떄문 ) 
- 이떄에 interpreter 를 base 로 하게 되면 제가 여태껏 base 에 설치했던 패키지를 그대로 활용할 수 있어 좋습니다.
  - 다만.. 가상환경이 아니기 때문에 여기서 깔리는것은 base 에 패키지가 깔리는거라 조심.

> ## 프로젝트 형성하기

- 우선 프로젝트를 형성합니다. 이때에 가상환경을 통하여 파이썬을 관리하는게 좋습니다.
  - 파이썬은 가져다 쓸 수 있는 패키지가 많은데 프로젝트마다 필요한 모듈 / 패키지가 다를 수 있습니다.
  - 가상환경은 이러한 모듈 , 패키지를 관리할 수 있게 합니다. 
  - 한곳에 모두 설치하게되면 어느순간 문제가 (얽혀서) 발생할 수 있을것입니다.

![png](/assets/images/Python/36_1.png)

- 파이참의 장점중 하나는 Virtual env 를 기본으로 내장하고 있다는 것인데요, 

![png](/assets/images/Python/36_2.png)

- venv 는 '고립된 환경' 입니다. 여기에서 패키지를 설치하고 변경하는것은 '가상 environment' 에만 영향을 끼칠 뿐이고, 설치된 python 에는 영향을 미치지 않습니다. 
- Existingg interpreter 는 현재 PC 에 설치되어있는 python 으로 구동하게 됩니다.
- 위에서 Location 에 dalso_test 라는 이름으로 프로젝트를 만들었습니다. 이게 바로 프로젝트의 이름이 됩니다.

![png](/assets/images/Python/36_3.png)

- 위와 같이 python 을 설치하게 됩니다.

> ## 패키지 설치 

```
pip install 패키지
```

- 위와 같이 패키지를 설치할 수 있습니다.

![png](/assets/images/Python/36_5.png)

- 위와 같이 파이썬 터미널에서 실행시키면 다운을 받을 수 있습니다.
- 또는 Settings -> 

> ## 단축키

| 개요                 | 단축키 (window)           | 설명                                 |
| -------------------- | ------------------------- | ------------------------------------ |
| 세팅                 | Ctrl + Alt + S            |                                      |
| 전체 검색            | Shift * 2  (닫을때는 ESC) |                                      |
| 현재 파일 실행       | Shitf F10                 |                                      |
| 현재 파일 실행(처음) | Ctrl + Shift + F10        | 처음 파일을 불러올떄에 활성하 시켜줌 |
|                      |                           |                                      |
|                      |                           |                                      |
|                      |                           |                                      |
|                      |                           |                                      |
|                      |                           |                                      |
|                      |                           |                                      |
|                      |                           |                                      |
|                      |                           |                                      |
|                      |                           |                                      |
|                      |                           |                                      |

> ## Customizing

- 전체적인 테마 변경
  - file -> Settings -> Appreance 에서 Them 변경이 가능합니다. 

# [코딩](#link){: .btn .btn--primary}{: .align-center}

> ## Alt + Enter

![png](/assets/images/Python/36_10.png)

- Alt + Enter 를 누르면 다양한 선택 가능한 옵션이 뜹니다. 
  - 각각의 옵션을 통해서 우리는 function 작성을 쉽게 할 수 있습니다.

```python
def custom(x: float) -> int:
    """ 실수형 값을 제곱으로 return 한다.
    :param x: 
    :return: 
    """
    k = x**2
    print(k)
    return k

custom(10)
```

> Specify return type using annotation 

```python
def custom2(x,y) -> object:
    return x+y
```

- 위처럼, custom 함수에 대해서 어떤 값이 나오는데 

# [디버깅](#link){: .btn .btn--primary}{: .align-center}

```python
def check(number) :
    if number % 15 == 0 :
        return '15'
    if number % 5 == 0  :
        return '5'
    if number % 3 == 0 :
        return '3'
    return 'Nono'

if __name__ == '__main__' :
    print(check(4))
```

- 위와 같은 함수가 있다고 합시다. 이때에 , 디버깅을 선택할 수 있습니다.

![png](/assets/images/Python/36_6.png)

- 위처럼 '빨간 점' 을 찍어놓으면 그 점에서 프로그램의 흐름이 딱 멈추게 됩니다. 그리고 , 여기에서 Step by Step 으로 체크하면서 프로그램이 맞는지 아닌지를 확인할 수 있습니다.

**reference**

- <https://greeksharifa.github.io/references/2019/02/07/PyCharm-usage/>
- 
