---
title:  "ct.parallelize"
excerpt: "RDD 생성하기"
tags:
  - Spark_Function
last_modified_at: 2021-11-26

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

데이터타입 바꾸기
{: .notice--warning}

# [df.union](#link){: .btn .btn--primary}{: .align-center}

> ## 공식문서

> pyspark.SparkContext.parallelize(c, numSlices=None)

- Distribute a local Python collection to form an RDD. Using range is recommended if the input represents a range for performance.

> Example

```python
from datetime import datetime, date
import pandas as pd
from pyspark.sql import Row

# 먼저 rdd 객체를 만들기
rdd = spark.sparkContext.parallelize([
    (1, 2., 'string1', date(2000, 1, 1), datetime(2000, 1, 1, 12, 0)),
    (2, 3., 'string2', date(2000, 2, 1), datetime(2000, 1, 2, 12, 0)),
    (3, 4., 'string3', date(2000, 3, 1), datetime(2000, 1, 3, 12, 0))
])
rdd
# ParallelCollectionRDD[381] at readRDDFromFile at PythonRDD.scala:274
```

- 위와 같이 RDD 를 Array 에서 만들어낼 수 있습니다!

```python
df = spark.createDataFrame(rdd, schema=['a', 'b', 'c', 'd', 'e'])
df
# DataFrame[a: bigint, b: double, c: string, d: date, e: timestamp]
```

- 추가적으로 rbb 로부터 위와 같이 Dataframe 을 만들어낼 수 있습니다! 

> ## 설명

- 스파크에서 RDD는 가장 주요한 개념이입니다. 
  - RDD는 병렬로 수행될 수 있는 엘리먼트의 컬렉션이며, fault-tolerant하다. 
- RDD를 생성하는 방법은 두가지입니다.
  - 첫번째는 내부의 컬렉션으로 부터 생성하는 방식
  - 두번째는 외부의 리소스로부터 생성하는 방식
- 이때에 내부의 개체를 RDD 로 만들려면 Sparkcontext 의 palallelize 메서드를 이용해야 합니다.


---

**Reference**

- 스파크 완벽 가이드
- 스파크 공식 가이드북



