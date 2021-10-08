---
title:  "Time packages"
excerpt: "시간을 다루는 파이썬 기본 모듈"
categories:
  - Py_Advanced
last_modified_at: 2021-09-27

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"

use_math : true
---

 시간을 다루는 파이썬의 time 패키지에 대해서 알아봅시다.
{: .notice--warning}

# [time 모듈](#link){: .btn .btn--primary}{: .align-center}

- Time 모듈은 아래와 같이 별도의 package 설치 없이도 사용할 수 있는 내장 모듈입니다.

```
import time
```

> 현재 시간 구하기

```python
>>> time.time()
1526694734.1275969
```

- 위와 같이 time 함수를 표출하게 되면 1970 년 1월 1일 0 시 0분 0초 이후 경과한 시간을 초 단위로 반환하게 됩니다. 

> ## 날짜와 시간 형태 반환

```python
>>> time.localtime(time.time())
time.struct_time(tm_year=2018, 
                 tm_mon=5, 
                 tm_mday=19, 
                 tm_hour=10, 
                 tm_min=54, 
                 tm_sec=25, tm_wday=5, tm_yday=139, tm_isdst=0)
```

- 위와 같이, time 모듈에서 loctime 을 활용할 수 있습니다. 
  - loctime 이라는 말 그대로 현재 시간의 시간대를 그대로 출력해줍니다.
  - 즉 우리나라의경ㅇ , UTC 에 9시간을 더한 숫자를 출력해줍니다. 
- tm_wday 의 경우는 요일 , (월~일 , 0~6) , tm_yday 는 1월1일부터 경과한 일수, tm_isdst 는 서머타임 여부입니다.

> ## 날짜 / 시간 포멧에 맞추어 출력 

- time.localtime으로 만든 객체는 time.strftime 함수를 사용하여 원하는 날짜/시간 포맷으로 출력할 수 있습니다.
  - **time.strftime('포맷', 시간객체)**

```python
>>> time.strftime('%Y-%m-%d', time.localtime(time.time()))
'2018-05-19'
>>> time.strftime('%c', time.localtime(time.time()))
'Sat May 19 11:14:27 2018'
```

- %Y는 연, %m은 월, %d는 일인데, '%Y-%m-%d'는 '연-월-일' 포맷이라는 뜻입니다. 
  - 그리고 %c는 날짜와 시간을 함께 출력합니다.
- 아래는 날자와 시간의 포맷 코드입니다.

| 코드 | 설명                                      | 예                                |
| ---- | ----------------------------------------- | --------------------------------- |
| %a   | 요일 줄임말                               | Sun, Mon, ... Sat                 |
| %A   | 요일                                      | Sunday, Monday, ..., Saturday     |
| %w   | 요일을 숫자로 표시, 월요일~일요일, 0~6    | 0, 1, ..., 6                      |
| %d   | 일                                        | 01, 02, ..., 31                   |
| %b   | 월 줄임말                                 | Jan, Feb, ..., Dec                |
| %B   | 월                                        | January, February, …, December    |
| %m   | 숫자 월                                   | 01, 02, ..., 12                   |
| %y   | 두 자릿수 연도                            | 01, 02, ..., 99                   |
| %Y   | 네 자릿수 연도                            | 0001, 0002, ..., 2017, 2018, 9999 |
| %H   | 시간(24시간)                              | 00, 01, ..., 23                   |
| %I   | 시간(12시간)                              | 01, 02, ..., 12                   |
| %p   | AM, PM                                    | AM, PM                            |
| %M   | 분                                        | 00, 01, ..., 59                   |
| %S   | 초                                        | 00, 01, ..., 59                   |
| %Z   | 시간대                                    | 대한민국 표준시                   |
| %j   | 1월 1일부터 경과한 일수                   | 001, 002, ..., 366                |
| %U   | 1년중 주차, 월요일이 한 주의 시작으로     | 00, 01, ..., 53                   |
| %W   | 1년중 주차, 월요일이 한 주의 시작으로     | 00, 01, ..., 53                   |
| %c   | 날짜, 요일, 시간을 출력, 현재 시간대 기준 | Sat May 19 11:14:27 2018          |
| %x   | 날짜를 출력, 현재 시간대 기준             | 05/19/18                          |
| %X   | 시간을 출력, 현재 시간대 기준             | '11:44:22'                        |

> ## datetime 모듈로 현재날짜와 시간 구하기

- 이번에는 datetime 모듈의 datetime 클래스를 사용해보겠습니다. datetime.datetime으로 현재 날짜와 시간을 구할 때는 today 메서드를 사용합니다(현재 시간대 기준, KST).
  - **datetime.datetime.today()**

```python
>>> import datetime
>>> datetime.datetime.today()
datetime.datetime(2018, 5, 19, 13, 15, 15, 881617)
```

> ## 특정 날짜와 시간으로 객체 만들기

- datetime.datetime에 연, 월, 일, 시, 분, 초, 마이크로초를 넣어서 객체를 만들 수도 있습니다.
  - **datetime.datetime(year, month, day, hour=0, minute=0, second=0, microsecond=0)**

```python
>>> d = datetime.datetime(2018, 5, 19)
>>> d
datetime.datetime(2018, 5, 19, 0, 0)
```

> ## 문자열로 날짜 / 시간 객체 만들기 

- strptime 메서드를 사용하면 문자열 형태의 날짜를 datetime.datetime 객체로 만들 수 있습니다. 이때는 날짜/시간 포맷을 지정해줘야 합니다.
  - **datetime.datetime.strptime('****날짜문자열', '포맷')**

```python
>>> d = datetime.datetime.strptime('2018-05-19', '%Y-%m-%d')
>>> d
datetime.datetime(2018, 5, 19, 0, 0)
```

> ## 날짜/시간 객체를 문자열로 만들기

- 반대로 datetime 객체를 문자열로 만들 수도 있습니다. 이때는 strftime 메서드를 사용합니다.
  - **datetime****객체.strftime('포맷')**

```python
>>> d.strftime('%Y-%m-%d')
'2018-05-19'
>>> d.strftime('%c')
'Sat May 19 00:00:00 2018'
```

> ## 날짜와 시간 속성에 접근하기

- datetime.datetime 객체는 연( year), 월(month), 일(day), 시(hour), 분(minute), 초(second), 마이크로초(microsecond) 속성을 따로 가져올 수 있습니다.

```python
>>> today = datetime.today()
>>> today.year, today.month, today.day, today.hour, today.minute, today.second, today.microsecond
(2018, 5, 19, 9, 54, 15, 868556)
```

> ## 날짜와 시간 차이 계산하기

- datetime 모듈에서 유용한 기능이 바로 datetime.timedelta입니다. datetime.timedelta는 두 날짜와 시간 사이의 차이를 계산할 때 사용합니다.
  - **datetime.timedelta(days=0, seconds=0, microseconds=0, milliseconds=0,
              minutes=0, hours=0, weeks=0)**
- 다음은 2018년 5월 13일에서 20일전 날짜를 구합니다.

```python
>>> d = datetime(2018, 5, 13)
>>> from datetime import timedelta
>>> d - timedelta(days=20)
datetime.datetime(2018, 4, 23, 0, 0)
```

- 즉, datetime.datetime 객체에서 datetime.timedelta를 빼면 이전 날짜와 시간을 구하고, 더하면 이후 날짜와 시간을 구합니다.
- 특히 datetime.datetime 객체에서 datetime.datetime 객체를 빼면 datetime.timedelta 객체가 나옵니다.

```python
>>> datetime(2018, 5, 13) - datetime(2018, 4, 1)
datetime.timedelta(42)
```

---

**reference**

- [https://datascienceschool.net](https://datascienceschool.net/01%20python/02.15%20%ED%8C%8C%EC%9D%B4%EC%8D%AC%EC%97%90%EC%84%9C%20%EB%82%A0%EC%A7%9C%EC%99%80%20%EC%8B%9C%EA%B0%84%20%EB%8B%A4%EB%A3%A8%EA%B8%B0.html)
- <https://dojang.io/mod/page/view.php?id=2463>

