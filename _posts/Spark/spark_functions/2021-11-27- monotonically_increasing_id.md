---
title:  "monotonically_increasing_id"
excerpt: "모든 row 에 대해 고유 id 추가하기"
categories:
  - Spark_Function
last_modified_at: 2021-12-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

알아봅시다
{: .notice--warning}

# [Coalesce](#link){: .btn .btn--primary}{: .align-center}

> ## 공식 문서

> pyspark.sql.functions.monotonically_increasing_id()

- *New in version 1.6.0.*
- A column that generates monotonically increasing 64-bit integers.
- The generated ID is guaranteed to be monotonically increasing and unique, but not consecutive. The current implementation puts the partition ID in the upper 31 bits, and the record number within each partition in the lower 33 bits. The assumption is that the data frame has less than 1 billion partitions, and each partition has less than 8 billion records.

> Example

```python
from pyspark.sql.functions import monotonically_increasing_id
df.select(monotonically_increasing_id()).show(10)
```

```
+-----------------------------+
|monotonically_increasing_id()|
+-----------------------------+
|                            0|
|                            1|
|                            2|
|                            3|
|                            4|
|                            5|
|                            6|
|                            7|
|                            8|
|                            9|
+-----------------------------+
```

- 위와 같이 monotonically_increasing_id 함수는 모든 로우에 대해서 ID 값을 추가하게 됩니다.


---

**Reference**

- 스파크 완벽 가이드
- 스파크 공식 Docs

