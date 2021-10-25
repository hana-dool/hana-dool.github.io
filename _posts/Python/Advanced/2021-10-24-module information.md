---
title:  "watermark module"
excerpt: "주피터 노트북에서 환경정보 뽑아내기"
categories:
  - Py_Advanced
last_modified_at: 2021-10-24

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"

use_math : true
---

 jupyter notebook 으로만 분석 내용을 소통하고자 하는 경우에, 어떠한 환경에서 수행되었는지 궁금한 경우가 있을텐데요, 그럴떄에 매우 요긴하게 이용할 수 있는 모듈입니다.
{: .notice--warning}

# [watermark module](#link){: .btn .btn--primary}{: .align-center}

> ## Usage

- 우선 내장 모듈이 아니기 떄문에 모듈을 설치하셔야 합니다.

```python
pip install watermark
```

```
%load_ext watermark
```

- 위와 같이 `%load_ext watermark` 를 입력한다면 사용할 수 있습니다. 
- 설명을 보자면 아래와 같습니다. 

```python
%watermark?
```

![png](/assets/images/Python/39_1.png)

> ## Default 

```python
%watermark
```

```
Last updated: 2021-10-24T17:40:02.663821+09:00

Python implementation: CPython
Python version       : 3.7.9
IPython version      : 7.20.0

Compiler    : MSC v.1916 64 bit (AMD64)
OS          : Windows
Release     : 10
Machine     : AMD64
Processor   : Intel64 Family 6 Model 142 Stepping 12, GenuineIntel
CPU cores   : 8
Architecture: 64bit
```

- 위와 같이 `%watermark` 를 사용한다면 자세한 환경 및 언제 수행하였는지도 자세히 나옵니다.
  - 하지만 우리가 제일 관심있는 모듈의 버젼 등이 나오지는 않으므로, 아래와 같이 설정해주는것이 좋습니다.

> ## 모듈의 버젼 한번에 확인

```python
%watermark --iversions
```

```
numpy     : 1.18.5
matplotlib: 3.3.0
sklearn   : 0.0
pandas    : 1.1.0
```

- 위처럼 제가 import 한 모듈을 모두 알려줍니다.

> ## Tip

```python
%watermark -a 'Hans' -n -u -v -m -iv
```

- 저는 일반적으로 위와 같은 세팅을 사용합니다. 
  - `-a` 닉네임을 의미합니다. 뒤의 'Hans' 는 제 닉네임을 넣었습니다. 
  - `-n ` 마지막으로 업데이트한 시간을 알려줍니다. 
  - `-u` 'Last Updated' 라는 String 을 넣어줍니다. 
  - `-v` Python / Ipython 의 버전을 print 합니다. 
  - `-m ` 시스템 정보를 print 합니다. 
  - `-iv` import 한 모듈을 모두 print 합니다. 

```
Author: Hans

Last updated: Sun Oct 24 2021

Python implementation: CPython
Python version       : 3.7.9
IPython version      : 7.20.0

Compiler    : MSC v.1916 64 bit (AMD64)
OS          : Windows
Release     : 10
Machine     : AMD64
Processor   : Intel64 Family 6 Model 142 Stepping 12, GenuineIntel
CPU cores   : 8
Architecture: 64bit

numpy     : 1.18.5
matplotlib: 3.3.0
sklearn   : 0.0
pandas    : 1.1.0
```

**reference**

- <https://pinkwink.kr/1235>

