---
title:  "DataFrame"
excerpt: "데이터프레임"
tags:
  - Spark_Function
last_modified_at: 2021-11-27

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 데이터프레임
{: .notice--warning}

# [스파크 데이터 타입으로 변환](#link){: .btn .btn--primary}{: .align-center}

> ## 타입 변환하기

- 프로그래밍 언어의 고유적인 데이터타입을 스파크 데이터타입으로 변환해볼 수 있습니다.
- 이때 데이터 타입 변환은 lit 함수를 사용하게 됩니다. 
  - lit 함수는 다른 언어의 데이터 타입을 스파크 데이터 타입에 맞게 변환하게 됩니다. 

```python
from pyspark.sql.functions import lit
df.select(lit(5), lit("five"), lit(5.0))
```

- 위에서 `lit` 함수를 이용하면 스파크 데이터타입으로 변환하게 됩니다.

**Reference**

- 스파크 완벽 가이드
- https://spark.apache.org/docs/latest/sql-getting-started.html
- https://stackoverflow.com/questions/64054282/what-do-the-sparksession-appname-and-getorcreate-functions-mean
- https://wikidocs.net/16565

