---
title:  "first , last"
excerpt: "처음과 마지막 값을 얻을떄"
categories:
  - Spark_Function
last_modified_at: 2022-01-14

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

알아봅시다
{: .notice--warning}

# [first , last](#link){: .btn .btn--primary}{: .align-center}

> ## 공식 문서

> pyspark.sql.functions.first(col, ignorenulls=False)

- Aggregate function: returns the first value in a group.
- The function by default returns the first values it sees. It will return the first non-null value it sees when ignoreNulls is set to true. If all values are null, then null is returned.
- *New in version 1.3.0.*

> pyspark.sql.functions.last(col, ignorenulls=False)

- Aggregate function: returns the last value in a group.
- The function by default returns the last values it sees. It will return the last non-null value it sees when ignoreNulls is set to true. If all values are null, then null is returned.
- *New in version 1.3.0.*

> ## 설명

- 함수명에서도 알 수 있듯이 first와 last 함수는 DataFrame의 칫 번째 값이나 마지막 값을 얻을 때 사용합니다. 
- 이들 함수는 DataFrame의 값이 아년 로우를 기반으로 동작합니다.

```python
from pyspark.sql.functions import first, last
df.select(first("StockCode"), last("StockCode")).show()
```

```
+----------------+---------------+
|first(StockCode)|last(StockCode)|
+----------------+---------------+
|          85123A|          22138|
+----------------+---------------+
```


---

**Reference**

- 스파크 완벽 가이드
- 스파크 공식 Docs

