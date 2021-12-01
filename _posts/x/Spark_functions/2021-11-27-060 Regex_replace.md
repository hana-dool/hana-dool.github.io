---
title:  "regexp_replace"
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

> pyspark.sql.functions.regexp_replace(str, pattern, replacement)

- Replace all substrings of the specified string value that match regexp with rep.
  - New in version 1.5.

> parameter

- str : 바꾸고자 하는 열의 이름(str) 또는 열(col)
- pattern : regex 조건
- replacement : 조건에 맞을때 바뀌어질 문자

> Examples

```python
df = spark.createDataFrame([('100-200',)], ['str'])
df.select(regexp_replace('str', r'(\d+)', '--').alias('d')).collect()
#[Row(d='-----')]
```

> ## 설명

- 문자열을 복잡하게 계산하기 위해서는 정규식을 사용하는게 좋습니다. 
- 스파크는 자바 정규표현식 문법을 활용합니다. (그러므로 다시 한번 검토하는것이 중요합니다.)

```python
from pyspark.sql.functions import regexp_replace
regex_string = "BLACK|WHITE|RED|GREEN|BLUE"
df.select(
  regexp_replace(col("Description"), regex_string, "COLOR").alias("color_clean"),
  col("Description")).show(2)

#+--------------------+--------------------+
#|         color_clean|         Description|
#+--------------------+--------------------+
#|COLOR HANGING HEA...|WHITE HANGING HEA...|
#| COLOR METAL LANTERN| WHITE METAL LANTERN|
#+--------------------+--------------------+
```

- 위처럼 `BLACK|WHITE|RED|GREEN|BLUE` 에 해당하는 단어가 나온다면, 그때 이름을 `COLOR` 라고 고칩니다!



---

**Reference**

- 스파크 완벽 가이드
- 스파크 공식 Docs

