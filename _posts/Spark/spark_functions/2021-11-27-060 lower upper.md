---
title:  "lower, upper"
excerpt: "문자열을 소문자/대문자로 변경하기"
categories:
  - Spark_Function
last_modified_at: 2021-11-30

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

알아봅시다
{: .notice--warning}

# [upper / lower](#link){: .btn .btn--primary}{: .align-center}

> ## 공식문서

> pyspark.sql.functions.upper(col)

- Converts a string expression to upper case.
  - New in version 1.5.

> ## 설명

- lower / upper 는 대분자 , 소문자로 바꾸는 방법입니다.

```python
from pyspark.sql.functions import lower, upper
df.select(col("Description"),
    lower(col("Description")),
    upper(lower(col("Description")))).show(2)

#+--------------------+--------------------+-------------------------+
#|         Description|  lower(Description)|upper(lower(Description))|
#+--------------------+--------------------+-------------------------+
#|WHITE HANGING HEA...|white hanging hea...|     WHITE HANGING HEA...|
#| WHITE METAL LANTERN| white metal lantern|      WHITE METAL LANTERN|
#+--------------------+--------------------+-------------------------+
```

---

**Reference**

- 스파크 완벽 가이드
- 스파크 공식 Docs

