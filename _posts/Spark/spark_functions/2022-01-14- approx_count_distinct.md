---
title:  "approx_count_distinct"
excerpt: "고유한 갯수 세기(근사치)"
categories:
  - Spark_Function
last_modified_at: 2021-01-14

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

알아봅시다
{: .notice--warning}

# [approx_count_distinct](#link){: .btn .btn--primary}{: .align-center}

> ## 공식 문서

> pyspark.sql.functions.approx_count_distinct(col, rsd=None)

- Aggregate function: returns a new [`Column`](https://spark.apache.org/docs/3.1.1/api/python/reference/api/pyspark.sql.Column.html#pyspark.sql.Column) for approximate distinct count of column col.
- New in version 2.1.0

> parameters

- col : [`Column`](https://spark.apache.org/docs/3.1.1/api/python/reference/api/pyspark.sql.Column.html#pyspark.sql.Column) **or str**
- rsd : float, optional
  - maximum relative standard deviation allowed (default = 0.05). For rsd < 0.01, it is more efficient to use countDistinct()

> ## 설명

- 대규모 데이터셋을 다루다 보면 정확한 고유 개수가 무의미할 때도 있습니다. 
- 어느 정도 수준의 정화도를 가지는 근사치만으로도 유의미하다면 approx_count_distinct 함수를 사용해 근사치를 계산할 수 있습니다.

```python
from pyspark.sql.functions import countDistinct
df.select(countDistinct("StockCode")).show() # 4070
```

```
+-------------------------+
|count(DISTINCT StockCode)|
+-------------------------+
|                     4070|
+-------------------------+
```

- 우선 위처럼 countDistinct 의 값은 4070 임을 기억합시다. 

```python
from pyspark.sql.functions import approx_count_distinct
df.select(approx_count_distinct("StockCode", 0.1)).show() # 3364
```

```
+--------------------------------+
|approx_count_distinct(StockCode)|
+--------------------------------+
|                            3364|
+--------------------------------+
```

- 위처럼 출력값이 약간의 오차가 있지만, 어느정도 잘 추정하고 있는것을 볼 수 있습니다.

```python
from pyspark.sql.functions import approx_count_distinct
df.select(approx_count_distinct("StockCode", 0.05)).show() # 3804
```

```
+--------------------------------+
|approx_count_distinct(StockCode)|
+--------------------------------+
|                            3804|
+--------------------------------+
```

- 위와 같이 정확도를 올리니, 좀 더 추정이 정확해지는것을 볼 수 있어요!


---

**Reference**

- 스파크 완벽 가이드
- 스파크 공식 Docs

