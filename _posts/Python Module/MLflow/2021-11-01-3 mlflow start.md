---
title: "ML Flow with Titanic Example" 
excerpt: "ML flow 실습하기"
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

MLflow 를 실제 코드와 함께 알아봅시다. from <https://github.com/lsjsj92/python_mlflow_example>
{: .notice--warning}

# [ML Flow](#link){: .btn .btn--primary}{: .align-center}

> ## MLflow start

- mlflow 는 머신러닝 라이프 사이클을 관리하는 오픈소스입니다.
  - mlflow는 앞의 내용을 웹 브라우저에서 GUI 기반으로 관리할 수 있습니다. 또한 rest API, cli도 가능하며 python, r, java 에서 API 사용가능 합니다.
- 주요기능은 다음과같습니다.

> Tracking

- parameter, metric 정보 등 비교

> Projects

- 재사용 가능한 형태로 배포

> Models

- sklearn, tensorflow, pytorch, keras 등 여러 머신러닝 라이브러리에서 만들어지는 모델 관리, 배포, 서빙, 추론

> ## Tracking

- 추적을 의미하는데요, 프로그램이 동작하면서 변수값 또는 프로그램을 실행시키기 위해 전달한 `argument` 등을 관리할 수 있습니다.

```python
import os
from random import random, randint

import mlflow
import mlflow.sklearn
from mlflow import log_metric, log_param, log_artifacts

if __name__ == '__main__':
  ri = randint(0, 100)
  r = random()
  log_param('param1', ri)
  
  print(ri, r)
  log_metric('foo', r)
  log_metric('foo', r + 1)
  log_metric('foo', r + 2)

  path = "outputs"

  if not os.path.exists(path):
    os.makedirs(path)
  
  with open("%s/test.txt"%(path), 'w') as f:
    f.write("hello world")
  
  log_artifacts("%s"%(path))
```

- 해당 코드를 실행하면 outputs/test.txt 파일에 hello world가 적힌 파일을 생성합니다.
- 그리고 해당 디렉터리에 mlruns/ 디렉터리를 생성하는데 mlflow가 라이프사이클을 관리하기 위한 정보가 담긴 디렉터리 입니다. 다음 명령어를 통해 해당 정보를 UI로 볼 수 있습니다.

```
$ mlflow ui
```

![png](/assets/images/Program/22_1.png)

- 앞의 코드를 실행할 때 마다 테이블에 row가 추가됩니다. 여기서 parameters와 metrics는 log_param, log_metric을 호출하면 확인됩니다. 
  - 이 둘은 key-value 형태로 관리하며 하나의 키에서 여러 값을 가질 수 없습니다.
- Start Time은 해당 코드가 실행된 시간입니다. 
- 코드를 자세히 보면 가장 하단에 log_artifacts가 있습니다.
  - 우리가 전달한 디렉터리에 있는 파일들을 볼 수 있습니다.

> ## Package

- 두번째로 나오게 될 개념은 Package 입니다.

**Reference**

- <https://wikidocs.net/52460>
- <https://zzsza.github.io/mlops/2019/01/16/mlflow-basic/>

ing
{: .notice--success}

