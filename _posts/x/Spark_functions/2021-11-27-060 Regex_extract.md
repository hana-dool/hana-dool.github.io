---
title:  "regexp_extract"
excerpt: "정규식을 만족할경우 바꾸기"
tags:
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

# [Regex](#link){: .btn .btn--primary}{: .align-center}

> ## 공식문서

> pyspark.sql.functions.regexp_extract(str, pattern, idx)

- Extract a specific group matched by a Java regex, from the specified string column. If the regex did not match, or the specified group did not match, an empty string is returned.
  - New in version 1.5.0.
  

> parameter

- str : 바꾸고자 하는 열의 이름(str) 또는 열(col)
- pattern : regex 조건
- Idx : 몇번째 group 을 출력할지

> Examples

```python
df = spark.createDataFrame([('100-200',)], ['str'])
df.select(regexp_extract('str', r'(\d+)-(\d+)', 1).alias('d')).collect()
#[Row(d='100')]
df = spark.createDataFrame([('foo',)], ['str'])
df.select(regexp_extract('str', r'(\d+)', 1).alias('d')).collect()
#[Row(d='')]
df = spark.createDataFrame([('aaaac',)], ['str'])
df.select(regexp_extract('str', '(a+)(b)?(c)', 2).alias('d')).collect()
#[Row(d='')]
```

> ## 설명

- extract 는 조건에 맞는 group 중 하나에서 출력하는 메서드입니다.

```python
from pyspark.sql.functions import regexp_extract
extract_str = "(BLACK|WHITE|RED|GREEN|BLUE)"
df.select(
     regexp_extract(col("Description"), extract_str, 1).alias("color_clean"),
     col("Description")).show(5)

#+-----------+--------------------+
#|color_clean|         Description|
#+-----------+--------------------+
#|      WHITE|WHITE HANGING HEA...|
#|      WHITE| WHITE METAL LANTERN|
#|           |CREAM CUPID HEART...|
#|           |KNITTED UNION FLA...|
#|        RED|RED WOOLLY HOTTIE...|
#+-----------+--------------------+
```

- 위와 같이 조건에 맞는것들중 처음 나타나는것을 출력합니다. (없으면 출력하지 않음)



---

**Reference**

- 스파크 완벽 가이드
- 스파크 공식 Docs

