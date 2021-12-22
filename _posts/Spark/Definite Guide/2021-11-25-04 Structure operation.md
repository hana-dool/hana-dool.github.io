---
title:  "Structure API Operation"
excerpt: "아파치 스파크의 연산"
categories:
  - Spark_Definite_Guide
last_modified_at: 2021-11-25

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

스파크의 기본만 한번 알아봅시다.
{: .notice--warning}

# [Spark Structure API](#link){: .btn .btn--primary}{: .align-center}

> ## 스파크의 기본 연산

- 여기에서는 Dataframe 과 Dataframe 의 데이터를 다루는 기능을 소개하려 합니다.
- 특히 Datagrame 의 기본 기능을 중심적으로 다루려 합니다.
- DaraFrame 은 Row 타입의 레코드 (테이블의 로우와 같음) 와 각 레코드에 수행할 연산 표현식을 나타내는 여러 칼럼 (스프레드 시트의 컬럼과 같습니다.) 으로 구성됩니다.
- 스키마는 각 컬럼명과 데이터 타입을 정의합니다.
- 파티셔닝은 Dataframe 이나 Dataset 이 클러스터에서 물리적으로 배치되는 형태를 정의합니다.

- 파티셔닝 스키마는 파티션을 배치하는 방법을 정의합니다.

> 데이터 프레임 생성하기

```python
df = spark.read.format('json').load('data/flight-data/json/2015-summary.json')
```

- 위와 같은 코드를 실행하여, 데이터프레임을 생성할 수 있습니다.

```python
df
#DataFrame[DEST_COUNTRY_NAME: string, ORIGIN_COUNTRY_NAME: string, count: bigint]
```

- 위처럼 Dataframe 객체가 생성된것을 볼 수 있습니다!
- Dataframe 은 컬럼을 가지며, 스키마로 컬럼을 정의한다고 하였죠? 앞 예제에서 만든 DataFrame 의 스키마를 살펴보도록 합시다.

> 스키마 살펴보기

```python
df.printSchema()
# root
# |-- DEST_COUNTRY_NAME: string (nullable = true)
# |-- ORIGIN_COUNTRY_NAME: string (nullable = true)
# |-- count: long (nullable = true)
```

- 위처럼 스키마들을 print 하여 살펴볼 수 있습니다. 

> ## 스키마

- 스키마는 Dataframe 의 컬럼명과 데이터 타입을 정의하게 됩니다.
  - 데이터 소스에서 스키마를 얻거나, 직접 정의할 수 있습니다.

데이터를 읽기 전에 스키마를 정의해야하는지 여부는 상황에 달라집니다. 일반적으로 직접 정의하지 않아도 자동적으로 (스키마 온 리드) 잘 작동합니다만, Long 데이터 타입을 interger 로 읽는다던지 등등의 인식 문제가 있을 수 있어서 ETL 작업에 스파크를 쓴다면 직접 스키마를 정의하는게 훨씬정확할 것입니다. 

- 이번 예제에서는 미국 교통통제국이 제공하는 항공운항 데이터를 사용해보도록 하겠습니다. 

```python
spark.read.format('json').load('data/flight-data/json/2015-summary.json').schema
# StructType(List(StructField(DEST_COUNTRY_NAME,StringType,true),StructField(ORIGIN_COUNTRY_NAME,StringType,true),StructField(count,LongType,true)))
```

- 스키나는 여러개의 StructField 타입 필드로 구성된 StrucTrype 객체입니다.

StrucField 란? : 이름, 데이터타입, null 인지아닌지의 불리언 값으로 구성됩니다. 

- 스키마는 복합 데이터타입인 StrucType 을 가질 수 있습니다.
  - 스파크는 런타임에 데이터 타입이 스키마의 데이터 타입과 일치하지 않으면 오류를 발생시키게 됩니다.

> 스키마

- 아래 코드는 DataFrame 에 스키마를 만들고 적용하는 예제입니다.
  - 스파크는 자체적인 데이터 타입 정보를 사용하므로, 프로그래밍 언어의 타입을 스파크의 데이터 타입으로 설정할 수 없음을 주목합시다!

````
from pyspark.sql.types import StructField, StructType, StringType, LongType

myManualSchema = StructType([
  StructField("DEST_COUNTRY_NAME", StringType(), True),
  StructField("ORIGIN_COUNTRY_NAME", StringType(), True),
  StructField("count", LongType(), False, metadata={"hello":"world"})
])
df = spark.read.format("json").schema(myManualSchema)\
  .load("data/flight-data/json/2015-summary.json")
````

> ## 칼럼과 표현식

- 스파크의 컬럼은 스프레드시트, Pandas 의 데이터프레임과 유사합니다.
  - 사용자는 '표현식' 으로 Dataframe 의 컬럼을 선택, 조작, 제거할 수 있습니다.
- 스파크의 컬럼은 표현식을 사용하여 레코드 단위로 계산한 값을 단순하게 나타나는 논리적 구조입니다.
  - 즉 Column 의 실제값을 얻으려면 Row 가 필요합니다. 
  - Row 를 얻으려면 Dataframe 이 필요합니다.
- 이때 칼럼 내용을 수정하려면 반드시 Dataframe 의 스파크 Transformation 을 사용해야 합니다.

> 컬럼

- 컬럼을 생성하고 참조할 수 있는 여러 방법중에서, col 함수나 column 함수를 사용하는것이 제일 간단합니다.
  - 이들 함수는 칼럼명을 인수로 받습니다.

```python
from pyspark.sql.functions import col
col("someColumnName")
```

- 위처럼 col 함수를 사용하여 column 을 생성할 수 있습니다.

> 명시적 컬럼 참조

- Dataframe 의 컬럼은 col 메서드를 이용합니다.
  - col 메서드는 조인시에 유용합니다.
- 예츨 들어서 Dataframe 의 어떤 column 을 다른 column 의 쪼인 대상 column 에서 참조하기 위하여 col 메서드를 사용할 수 있습니다. 
  - col 메서드를 사용하여 명시적으로 column 을 정의하면 스파크는 분석기 실행 단계에서 컬럼 확인 절차를 생략합니다.

> 표현식

- 앞서서 Dataframe 을 정의할때 컬럼은 표현식이라 했습니다.
- 이때 표현식은 Dataframe record 여러 값에 대한 트랜스포메이션 집합을 의미합니다.
- 표현식은 expr 함수로 간단히 사용 가능 
- 이 함수를 이용해 Dataframe 의 컬럼을참조할 수 있음
  - expr('someCole') 과 col('someCol') 구문은 동일하게 동작합니다.

> ## 표현식으로 컬럼 표현

- 컬럼은 표현식의 기능을 제공 아래는 모두 같은 트랜스포메이션 과정을 거침
  - exp('someCol-5') 
  - col('someCol')-5
  - expr('someCol')-5
- 컬럼은 단지 표현식일 뿐이라는것입니다!

```
(((col("someCol") + 5) * 200) - 6) < col("otherCol")
```

![png](/assets/images/Program/18_5.png)

- 위와 똑같은 코드를 다음과 같이 만들 수 있습니다.

```python
from pyspark.sql.functions import expr
expr("(((someCol + 5) * 200) - 6) < otherCol")
```

> ## Dataframe column 에 접근

- PrintSchema 메서드로 Dataframe 의 모든 컬럼 정보 확인 가능
  - 하지만 프로그래밍 방식으로 컬럼 접근시는 Dataframe 의 columns 매서드 사용

```python
spark.read.format("json").load("data/flight-data/json/2015-summary.json").columns
# ['DEST_COUNTRY_NAME', 'ORIGIN_COUNTRY_NAME', 'count']
```

> ## 레코드와 로우

- 스파크에서 Dataframe 의 각 row 는 하나의 레코드
  - 스파크는 레코드를 Row 객체로 표현
- Row 객체는 내부에 바이트 배열을 가지고, 이러한 바이트 배열 인터페이스는 오직 컬럼 표현식으로만 다룰 수 있음
  - Dataframe 을 이용하여 드라이버에게 개별로우를 반환하는 명령어는 하나이상의 ROW 타입을 반환

```
df.first()
```

- 로우를 확인하는 코드

> ## Dataframe 의 트랜스포메이션

- 지금까지 Dataframe 의 핵심 영역을 간단히 살펴 보았습니다.
- 이어서 Dataframe 을 다루는 방법에 대해서 알아봅시다.
  - 로우나 컬럼 추가
  - 로우나 컬럼 제거
  - 로우를 컬럼으로 변환하거나 그 반대로 변환
  - 컬럼값을 기준으로 로우 순서 변경
- 이러한 모든 유형의 작업은 트랜스포메이션으로 변환할 수 있습니다. 

>  Dataframe 생성하기

- 원시 데이터소스에서 Dataframe 을 생성할수 있습니다.

```python
df = spark.read.format("json").load("data/flight-data/json/2015-summary.json")
df.createOrReplaceTempView("dfTable")
```

- 우선 위와 같이 SQL 의 기본 트랜스포메이션을 확인하기 위해서 위처럼 dfTable 이라는 임시 뷰를 등록해 보도록 하겠습니다.

```sql
from pyspark.sql import Row
from pyspark.sql.types import StructField, StructType, StringType, LongType
myManualSchema = StructType([
  StructField("some", StringType(), True),
  StructField("col", StringType(), True),
  StructField("names", LongType(), False)
])
myRow = Row("Hello", None, 1)
myDf = spark.createDataFrame([myRow], myManualSchema)
myDf.show()
```

```
+-----+----+-----+
| some| col|names|
+-----+----+-----+
|Hello|null|    1|
+-----+----+-----+
```

- 위처럼 데이터 프레임을 만들어낼 수 있습니다. (어떻게 만드는지는 Spark 함수를 살펴보도록 합시다.)



**Reference**

- 스파크 완벽 가이드

