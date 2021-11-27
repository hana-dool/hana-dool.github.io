---
title:  "Structure API"
excerpt: "아파치 스파크의 구조적 API"
categories:
  - Spark_Definite_Guide
last_modified_at: 2021-11-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

스파크의 기본만 한번 알아봅시다.
{: .notice--warning}

# [Spark Structure API](#link){: .btn .btn--primary}{: .align-center}

> ## 스파크의 구조적 API

- 구조적 API 는 비정형 로그파일부터 반정형 CSV 등 다ß양한 유형의 데이터를 처리할 수 있습니다.
- 구조적 API 는 다음과 같이 3개의 분산 컬렉션 API 가 존재합니다.
  - Dataset
  - Dataframe
  - SQL 테이블과 뷰
- 구조적 API 는 데이터 흐름을 정의하는 기본적인 추상화 개념입니다.
- 이 장에서는 반드시 이해해야될 세가지 개념을 설명하게 됩니다.
  - 타입형(typed) / 비타입형 (untyped) API 의 개념과 차이점
  - 핵심 용어
  - 스파크가 구조적 API 의 데이터 흐름을 해석하고 클러스터에서 실행하는 방식

> ## Dataframe 과 DataSet

- 스파크는 Dataframe 과 Dataset 이라는 두가지 구조화된 개념을 가지고 있습니다.
  - 이는 잘 정의된 row 와 col 을 다루는 분산 테이블 형태의 컬렉션입니다.
  - 각 칼럼은 다른 컬럼과 동일한 수의 row 를 가져야 합니다. (값 없음은 null 로 표시합니다.)
  - 그리고 컬렉션의 모든 로우는 같은 데이터 타입 정보를 가지고 있어야 합니다. 
- Dataframe 과 Dataset 은 결과를 생성하기 위해 어떤 데이터에 어떤 연산을 적용해야 하는지 정의하는 지연 연산의 실행 계획이며, 불변성을 가집니다.
  - Dataframe 에 액션을 호출하면 스파크는 트랜스포메이션을 실제로 실행하고, 결과를 반환합니다.
  - 이 과정은 사용자가 원하는 결과를 얻기 위해 로우와 컬럼을 처리하는 방법에 대한 계획을 나타냅니다.

> ## 스키마

- 스키마는 분산 컬렉션에 저장할 데이터 타입을 정의하는 방법입니다.
  - 스키마는 Dataframe 의 칼럼, 데이터 타입을 정의합니다. 
- 스키마는 데이터 소스에서 얻거나, 직접 정의할 수 있습니다.
  - 스키마는 여러 데이터 타입으로 구성되므로, 어떤 데이터 타입이 어느 위치에 있는지 정의하는 방법이 중요합니다.

> ## 스파크의 구조적 데이터 타입

- 스파크는 프로s그래밍 언어입니다.
- 스파크는 실행 계획 수립과 처리에 사용하는 자테 데이터 타입 정보를 가지고 있는 카탈리스크 엔진을 사용합니다.
  - 카탈리스트 엔진은 다양한 실행 최적화 기능을 제공합니다.

- 스파크는 자체 데이터 타입을 지원하는 여러 언어 API 와 직접 매핑됩니다. 
  - 이때 각 언어에 대한 매핑 테이블을 가지고 있습니다.
  - 파이썬이나 R 을 이용해 스파크의 구조적 API 를 사용하더라도 대부분은 파이썬, R 의 데이터 타입이 아니라 스파크의 데이터 타입을 사용하게 됩니다. 

- 아래의 예제는 파이썬이 아닌 '스파크' 의 덧셈을 수행합니다.

```python
df = spark.range(500).toDF('number')
df.select(df['number']+10)
```

- 파이썬 $\to$ 카탈리스크 엔진에서 변환 $\to$ 스파크 데이터 타입으로 변환되어 처리됨
  - 위처럼 파이썬은 단지 '변환' 되고 있음을 알 수 있습니다.
- 이러한 연산이 어떻게 가능한지에 대해서 알아보기 위해, 아래에서 처럼 Dataset 을 먼저 알아보도록 하겠습니다.

> ## Dataframe 과 Dataset 비교

- 본질적으로 구조적 API 에는 비타입형인 Dataframe 과 타입형인 Dataset 이 있습니다.
  - 물론 Dataframe 에도 데이터타입이 있습니다. 하지만 스키마에 명시된 데이터 타입의 일치 여부를 '런타임' 이 되서야 확인합니다.
  - 그에 반해서 Dataset 은 스키마에 명시된 데이터 타입의 일치 여부를 '컴파일 타임' 에 확인합니다. 
- Dataset 은 JVM기반인 스칼라와 자바에서만 지원합니다... (ㅜㅜ)
- 이 책에서는 다행히 대부분 Dataframe 을 사용합니다. 
  - 스파크의 Dataframe 은 row 타입으로 구성되어있습니다.
- Row 타입은 스파크가 사용하는 연산에 최적화된 표현 방식입니다.
  - Row 타입을 사용하면 이미 최적화가 되어있어 매우 효율적인 연산이 가능합니다. 

> ## 컬럼

- 컬럼의 표현 가능한 것들
  - 컬럼은 정수형이나 문자열 같은 단순 데이터 타입
  - 배열이나 맵 같은 복합 데이터타입
  - null
- 스파크는 데이터타입의 모든 정보를 추적하고, 다양한 변환을 제공합니다.
- 스파크의 컬럼은 테이블의 컬럼으로 생각하시면 됩니다. 

> ## 로우

- 로우는 데이터 레코드입니다.
  - Dataframe 의 레코드는 Row 타입으로 구성됩니다.
- 로우는 SQL, RDD 등으로 직접 만들 수 있습니다. 
- 아래처럼 range 메서드를 사용하여 dataFrame 을 직접 만들어 보겠습니다. 

```python
spark.range(2).collect()
# [Row(id=0), Row(id=1)]
```

- 위처럼 Row 객체로 이루어진 배열을 만들어내고 있음을 볼 수 있습니다.

> ## 스파크 데이터 타입

- 스파크는 여러개지 내부 데이터타입을 가지고 있습니다. 

| **Data type** | **Value type in Python**                                | **API to access or create a data type**          |
| ------------- | ------------------------------------------------------- | ------------------------------------------------ |
| ByteType      | int or long [1]                                         | ByteType()                                       |
| ShortType     | int or long [2]                                         | ShortType()                                      |
| IntegerType   | int or long [3]                                         | IntegerType()                                    |
| LongType      | long [4]                                                | LongType()                                       |
| FloatType     | float [5]                                               | FloatType()                                      |
| DoubleType    | float                                                   | DoubleType()                                     |
| DecimalType   | decimal.Decimal                                         | DecimalType()                                    |
| StringType    | string                                                  | StringType()                                     |
| BinaryType    | bytearray                                               | BinaryType()                                     |
| BooleanType   | bool                                                    | BooleanType()                                    |
| TimestampType | datetime.datetime                                       | TimestampType()                                  |
| DateType      | datetime.date                                           | DateType()                                       |
| ArrayType     | list, tuple, or array                                   | ArrayType(elementType, [containsNull])           |
| MapType       | dict                                                    | MapType(keyType, valueType, [valueContainsNull]) |
| StructType    | list or tuple                                           | StructType(fields).                              |
| StructField   | The value type in Python of the data type of this field | StructField                                      |

- [1] : Numbers will be converted to 1-byte signed integer numbers at runtime. Ensure that numbers are within the range of –128 to 127.
- [2] :  Numbers will be converted to 2-byte signed  ShortType integer numbers at runtime. Ensure that numbers are within the range of –32768 to 32767.
- [3] : Python has a lenient definition of “integer.” Numbers that are too large will be rejected by Spark SQL if you use the IntegerType(). It’s best practice to use LongType
- [4] : Numbers will be converted to 8-byte signed integer numbers at runtime. Ensure that numbers are within the range of –9223372036854775808 to 9223372036854775807. Otherwise, convert data to decimal.Decimal and use DecimalType.
- [5] : Numbers will be converted to 4-byte single- precision floating-point numbers at runtime.

> 스파크 데이터 타입 사용하기

- 위의 표를 이용하여 특정 데이터의 칼럶을 초기화 하고 정의하는 법을 알아보도록 합시다.

```
from pyspark.sql.types import *
b = ByteType()
```

- 위처럼 파이썬의 객체 지향 성질을 이용하여 b 에다가 spark 의 데이터타입을 저장하고 있는 모습을 볼 수 있습니다. 

> ## 구조적 API 의 실행 과정

- 이 절에서는 스파크 코드가 클러스터에서 실제 처리되는 과정을 살펴보겠습니다. 진행과정은 아래와 같습니다.

1. Dataframe / SQL 을 이용하여 코드를 작성합니다.
2. 정상적인 코드라면 스파크가 논리적 실행 계획으로 변환합니다.
3. 스파크는 논리적 실행 계획을물리적 실행 계획으로 변환하며 그 과정에서 추가적인 최적화를 할 수 있는지 확인합니다.
4. 스파크는 클러스터에서 물리적 실행 계획(RDD 처리) 를 실행합니다.

![png](/assets/images/Program/18_1.png)

- 먼저 위의 순서에 따라서 실행할 코드를 작성해 봅시다.이 작성한 코드는 카탈리스트 옵티마이저로 전달되며, 카탈리스트 옵티마이저는 실제 실행계획을 생성하고 이를 실행한 뒤 결과를 반환하게 됩니다. 

> 1.논리적 실행 계획

- 첫번쨰 실행 단계에서는 사용자의 코드를 논리적 실행 계획으로 변환합니다.

![png](/assets/images/Program/18_2.png)

- 논리적 실행 계획의 단계에서는 추상적인 Transformation 만 표현합니다.
  - 이 단계에서는 드라이버나 익스큐터의 정보를 고려하지 않습니다.
- 사용의 다양한 표현식을 최적화된 버전으로 변환합니다. 
  - 이 과정으로 사용자의 코드는Unresolved logical plan 으로 변환됩니다.
- 아직은 코드의 유효성 + 테이블이타 컬럼의 존재 여부 만을 판단하는 과정입니다. 즉 아직 실행 계획을 검증하지는 않은 상태라는것을명심합니다.
- 스파크 분석기는 컬럼과 테이블을 검증하기 위해 카탈로그, 테이블 저장소 , Dataframe정보를 활용합니다.
  - 필요한 테이블이나 컬럼이 카탈로그에 없으면, 검증 전 논리 실행계획이 만들어지지 않습니다.
- 검증 결과는 카탈리스트 옵티마이저로 전달됩니다. 

> 2.물리적 실행계획

- 이제 물리적 실행계획을 생성하는 과정이 시작됩니다
  - .스파크 실행계획이라고 불리는 물리적 실행 계획은 논리적 실행 계획을 클러스터 환경에서 실행하는 방법을 정의합니다.

![png](/assets/images/Program/18_3.png)

- 위처럼 다양한 물리적 실행 전략을 생성하고 Cost model 을 정의하여 비교한 후에 최적의 전략을 선택합니다.
  - Cost model 을 이용하는 예시 : join 연산 수행에 필요한 비용을 계산한뒤 비교해봄
- 이러한 물리적 실행 계획은 일련의 RDD 와 트랜스포메이션으로 변환됩니다. 
  - 스파크는 Dataframe , Dataset , SQL 로 정의된 쿼리를 RDD 트랜스포메이션으로 컴파일합니다.
- 즉 스파크를 컴파일러라고 하기도 한답니다.

> 3.실행

- 스파크는 물리적 실행 계획을 선정한 다음 RDD 를 대상으로 모든 코드를 실행합니다.
  - 스파크는 자체적으로 최적화를 수행한 뒤, 처리 결과를 사용자에게 반환합니다.



**Reference**

- 스파크 완벽 가이드

