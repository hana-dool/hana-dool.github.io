---
title:  "SparkSession"
excerpt: "스파크 시작하기"
categories:
  - Spark_other_method
last_modified_at: 2021-11-25

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

스파크의 기본만 한번 알아봅시다.
{: .notice--warning}

# [SparkSession](#link){: .btn .btn--primary}{: .align-center}

> ## SparkSession 이란?

> pyspark.sql.SparkSession(sparkContext, jsparkSession=None)

- The entry point to programming Spark with the Dataset and DataFrame API.
- A SparkSession can be used create [`DataFrame`](https://spark.apache.org/docs/latest/api/python/reference/api/pyspark.sql.DataFrame.html#pyspark.sql.DataFrame), register [`DataFrame`](https://spark.apache.org/docs/latest/api/python/reference/api/pyspark.sql.DataFrame.html#pyspark.sql.DataFrame) as tables, execute SQL over tables, cache tables, and read parquet files. To create a [`SparkSession`](https://spark.apache.org/docs/latest/api/python/reference/api/pyspark.sql.SparkSession.html?highlight=sparksession#pyspark.sql.SparkSession), use the following builder pattern:

> Note

- SparkSession 이란 스파크 응용 프로그램의 통합 짐입점입니다.
  - 스파크의 구조와 기능들이 상호방식하는 방식을 제공합니다.
- 스파크의 모든 기능은 SparkSession 클래스에서 시작합니다. SparkSession.builder를 사용해서 가장 기본적인 설정의 SparkSession을 생성합니다:

```python
from pyspark.sql import SparkSession

spark = SparkSession \
    .builder \
    .appName("Python Spark SQL basic example") \
    .config("spark.some.config.option", "some-value") \
    .getOrCreate()
```

- 일반적으로 우리는 처음 스파크를 시작하게 되면 위와 같이 스파크 세션을 먼저 정의하곤 하는데요, 여기에서, 각각이 의미하는것들을 한번 살펴보겠습니다.

> ## 왜 pyspark.sql 에서 import 했는가?

- 왜 하필이면 pyspark.sql 에서 Import 를 하는것일까요? 
- 스파크에는 여러 모듈을 제공합니다. 
  - [Spark SQL](https://spark.apache.org/sql/): Spark Wrapper 함수에 SQL 쿼리를 넣어 추출/전처리/분석이 쉽게 가능하도록 지원
  - [MLlib](https://spark.apache.org/mllib/): 머신러닝 알고리즘 제공
  - [Spark Streaming](https://spark.apache.org/streaming/): 실시간 데이터 처리
  - [GraphX](https://spark.apache.org/graphx/): 그래프 분석 라이브러리
- 이때에 우리는 Spark SQL 을 통하여 데이터 전처리를 하고자 하므로, 위에서처럼 `pyspark.sql`  에서 SparkSession을 Import 한 것입니다.

> ## \ 는 어떤 의미?

```python
string = 'A'\
    +'B'
print(string)
# 'AB'
```

- 위에서처럼 `\`  를 사용한다면 줄바꿈을 하더라도 , 하나의 줄에서 쓴 것처럼 적용됩니다.

```
spark = SparkSession \
    .builder \
    .appName("Python Spark SQL basic example") \
    .config("spark.some.config.option", "some-value") \
    .getOrCreate()
```

- 즉 위와 같은 구문은,  사실 `SparkSession.builder.appName(.........` 와 같이 길게 늘어진 함수를 가독성이 좋게 한것이라고 알 수 있습니다.

> ## Builder 는?

- spark 공식 문서에서 Sparksession 이 어떻게정의되었는지 살펴보겠습니다.
  - https://spark.apache.org/docs/2.4.0/api/python/_modules/pyspark/sql/session.html#SparkSession.Builder

```python
class SparkSession(object) : 
  ........
  ........
  class Builder(object): 
    ......
    ......
    def config()
    ....
    def appName()
    .....
    def getOrCreate()
    ....
  builder = Builder()
  .....
  .....
```

- 위와 같은 구조로 정의됩니다.
  - 즉 builder 를 먼저 호출해서 , Builder 클래스를 만든 후 , 그 뒤의 메서드들을 차례로 사용하기 위하여 아래와 같은 구조가 되었다고 생각하시면 됩니다.

```python
spark = SparkSession \
    .builder \
    .appName("Python Spark SQL basic example") \
    .config("spark.some.config.option", "some-value") \
    .getOrCreate()
```

> ## appName 

- Application 의 이름을 결정합니다.
- 여기서 지정한 이름은 나중에 Spark UI 에 앱 이름으로 표출되게 됩니다. 
- 만일 이때 이름을 지정하지 않으면 랜덤으로 이름이 지정됩니다.

> ## config

- config 옵션을 정의합니다.
- 이는 굳이 없어도 잘 설정되어있다면 잘 돌아갑니다.

> ## getOrCreate

- SparkSession 이 이미 존재하면 존재하는 SparkSession 을 가져옵니다.
- 만일 SparkSession 이 없다면 , builder 에 넣은 설정대로 SparkSession 을 실행합니다.

**Reference**

- 스파크 완벽 가이드
- https://spark.apache.org/docs/latest/sql-getting-started.html
- https://stackoverflow.com/questions/64054282/what-do-the-sparksession-appname-and-getorcreate-functions-mean
- https://wikidocs.net/16565

