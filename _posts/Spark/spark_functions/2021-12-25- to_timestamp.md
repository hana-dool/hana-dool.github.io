---
title:  "to_timestamp"
excerpt: "문자열을 timestamp로 변환하기"
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

# [to_timestamp](#link){: .btn .btn--primary}{: .align-center}

> ## 공식 문서

> pyspark.sql.functions.to_timestamp(col, format=None)

- *New in version 2.2.0.*
- Converts a `Column` into `pyspark.sql.types.TimestampType` using the optionally specified format. Specify formats according to datetime pattern. By default, it follows casting rules to `pyspark.sql.types.TimestampType` if the format is omitted. Equivalent to col.cast("timestamp").

>  Example

```python
df = spark.createDataFrame([('1997-02-28 10:30:00',)], ['t'])
df.select(to_timestamp(df.t).alias('dt')).collect()
# [Row(dt=datetime.datetime(1997, 2, 28, 10, 30))]
```

```python
df = spark.createDataFrame([('1997-02-28 10:30:00',)], ['t'])
df.select(to_date(df.t, 'yyyy-MM-dd HH:mm:ss').alias('date')).collect()
# [Row(date=datetime.date(1997, 2, 28))]
```

> ## 설명

- to_timestamp 데이터는 timestamp 데이터 타입으로 변환시킵니다.


---

**Reference**

- 스파크 완벽 가이드
- 스파크 공식 Docs

