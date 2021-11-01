---
title: "Introduction" 
excerpt: "Tensor 를 자유자재로 다루어보기"
categories:
  - Py_mlflow

last_modified_at: 2021-11-01
date : 2021-11-01 12:00:00 +0900

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 텐서의 연산에 대해서 알아봅시다.
{: .notice--warning}

# [ML Flow](#link){: .btn .btn--primary}{: .align-center}

> ## what is mlflow? 

- MLflow는 End to End로 머신러닝 라이프 사이클을 관리할 수 있는 오픈소스
  - 데이터브릭스에서 만들었습니다.

- 주요 기능
  - 1) MLflow Tracking
    - 파라미터와 결과를 비교하기 위해 실험 결과를 저장
  - 2) MLflow Projects
    - 머신러닝 코드를 재사용 가능하고 재현 가능한 형태로 포장
    - 포장된 형태를 다른 데이터 사이언티스트가 사용하거나 프러덕션에 반영
  - 3) MLflow Models
    - 다양한 ML 라이브러리에서 모델을 관리하고 배포, Serving, 추론
- REST API, CLI를 통해 모든 기능에 액세스 할 수 있기 때문에 모든 라이브러리, 프로그래밍 언어에서 사용 가능
- API는 Python, R, Java 존재

> ## 설치  및 코드 준비

> Virtual env 설정하기 

- 저는 윈도우에서 실습하는거라, Activate 에서 실행하도록 하겠습니다.

```
conda create -n [가상환경 이름]
```

- 위의 코드를 이용하여 가상경을 만들어냅니다. (저는 temp 로 함)
- 그 이후, 위 가상환경을 Activate 시킵니다. 

```
activate temp
```

- 이제 github 에서 예제를 Clone 해 옵니다.

```python
git clone https://github.com/mlflow/mlflow
```

- 그 이후에 examples 폴더로 이동합니다. 

> ## 실행해보기

- 위에서 본 값들을 실행해봅시다. 

```python
# mlflow_tracking.py
import os
from random import random, randint

from mlflow import log_metric, log_param, log_artifacts

if __name__ == "__main__":
    print("Running mlflow_tracking.py")

    log_param("param1", randint(0, 100))

    log_metric("foo", random())
    log_metric("foo", random() + 1)
    log_metric("foo", random() + 2)

    if not os.path.exists("outputs"):
    	os.makedirs("outputs")
    with open("outputs/test.txt", "w") as f:
    	f.write("hello world!")

    log_artifacts("outputs")
```

- 위 파일을 잘 보면 mlflow 에서 log_metric , log_param , log_artifacts 를 불러와서 사용하고 있음을 알 수 있습니다. 
  - 이러한 log 라는 이름만 보더라도 '아 ! 어떤것을 기록하는 역할을 하겠구나!' 라고 생각할 수 있습니다.
- 예제 코드는 위와 같습니다. 이 파일을 어떻게 하면 실행할 수 있을까요? 
  - 위 파일은 examples 의 quickcode 에 위치하고 있으므로, 여기에 이동한 뒤 실행해 봅시다.

```
(temp) C:\Users\goran\mlflow\examples>cd quickstart
(temp) C:\Users\goran\mlflow\examples\quickstart>python mlflow_tracking.py
```

- 실행하고 나면 , mirus 와 outpus 디렉토리가 생겨 있을것입니다. 

```
(temp) C:\Users\goran\mlflow\examples\quickstart>tree
폴더 PATH의 목록입니다.
볼륨 일련 번호는 C084-979C입니다.
C:.
├─mlruns
│  ├─.trash
│  └─0
│      └─38314f84582c4fed87cf2b8538cd57a2
│          ├─artifacts
│          ├─metrics
│          ├─params
│          └─tags
└─outputs
```

- 위처럼 mirus 와 output 디렉토리가 생겼습니다! 

> ## 디렉토리 구경하기

- 위의 디렉토리를 보면 아래 세개의 디렉토리가 눈에 띕니다.
  - `artifacts`
  - `metrics`
  - `params`
- 위 디렉토리에 우리가 이전에 log_metric , log_param , log_artifacts 으로 떠넘긴 변수들이 위치합니다. 

> ## 웹 대시보드

```
mlflow ui
```

- 위와 같이 명령어를 치면 대시보드용 웹 서버를 이용할 수 있습니다.

```
(temp) C:\Users\goran\mlflow\examples\quickstart>mlflow ui
INFO:waitress:Serving on http://127.0.0.1:5000
```

- <http://127.0.0.1:5000> 로 들어가 봅시다. 그러면 

![png](/assets/images/Python/50_1.png)

- 위와 같이 ml flow 의 화면을 볼 수 있습니다. 

> ## 종료

```
(temp) C:\Users\goran\mlflow\examples\quickstart>mlflow ui
INFO:waitress:Serving on http://127.0.0.1:5000

Aborted!

(temp) C:\Users\goran\mlflow\examples\quickstart>
```

- 실행중이라면 Control + C 를 누르셔서 , 실행되는 서버를 종료할 수 있습니다.

**Reference**

- <https://wikidocs.net/52460>
- <https://zzsza.github.io/mlops/2019/01/16/mlflow-basic/>

ing
{: .notice--success}

