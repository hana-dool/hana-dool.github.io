---
title:  "lit trim read rtrim trim"
excerpt: "문자열의 공백 다루기"
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

> ## 설명

- 공백을 제거하는 방법론들입니다!

```python
from pyspark.sql.functions import lit, ltrim, rtrim, rpad, lpad, trim
df.select(
    ltrim(lit("    HELLO    ")).alias("ltrim"),
    rtrim(lit("    HELLO    ")).alias("rtrim"),
    trim(lit("    HELLO    ")).alias("trim"),
    lpad(lit("HELLO"), 3, " ").alias("lp"),
    rpad(lit("HELLO"), 10, " ").alias("rp")).show(2)

#+---------+---------+-----+---+----------+
#|    ltrim|    rtrim| trim| lp|        rp|
#----------+---------+-----+---+----------+
#|HELLO    |    HELLO|HELLO|HEL|HELLO     |
#|HELLO    |    HELLO|HELLO|HEL|HELLO     |
#+---------+---------+-----+---+----------+

```

- ltrim : 왼쪽의 공백 없애기
- rtrim : 오른쪽의 공백 없애기
- trim : 양쪽의 공백 없애기
- lpad : 오른쪽에 수만큼 문자삽입 (단 그 문자길이가 수를 초과하면 오히려 없앰)
- rpad : 왼쪽에 문자삽입 (단 그 문자길이가 그 수를 초과하면 오히려 없앰)

---

**Reference**

- 스파크 완벽 가이드
- 스파크 공식 Docs

