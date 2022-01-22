---
title:  "countDistinct"
excerpt: "고유한 갯수 세기"
categories:
  - Spark_Function
last_modified_at: 2021-12-25

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

알아봅시다
{: .notice--warning}

# [countDistinct](#link){: .btn .btn--primary}{: .align-center}

> ## 공식 문서

> pyspark.sql.functions.countDistinct(col, *cols)

- Returns a new Column for distinct count of col or cols.
- An alias of count_distinct(), and it is encouraged to use count_distinct() directly.
- New in version 1.3.0.

> ## 설명

- Data set 에 대해서 Discinct 한 값의 갯수를 출력합니다.

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

- 위처럼 StockCode 의 DIstinct 한 row 들을 출력합니다.


---

**Reference**

- 스파크 완벽 가이드
- 스파크 공식 Docs

