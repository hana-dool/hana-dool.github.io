---
title: "3.Ingestion and Transformation"
excerpt: "데이터 소스"
categories:
  - Data_Infra
tags:
  - 3
last_modified_at: 2021-05-09

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---



<bR>

https://www.youtube.com/watch?v=g_c742vW8dQ 의 데이터인프라 소개글을 보고 정리한 내용입니다

<br>

![png](/assets/images/Data_Infra/2_1.png)

# 1.Connectors

- 소스에서 나왔던 데이터를, 데이터 웨어하우스  또는 데이터 레이트로 전달한다.
- Fivetran , Stitch,Matllion 등이 있다.

<br>

## Fivetran

![png](/assets/images/Data_Infra/2_2.png)

- 이벤트 콜렉터, 광고데이터 등 다양한 데이터들에서 발생하는 것들을 수집한다.
- 그리고 Normalization 을 통해서 데이터를 정규화 한다.
- 그리고 SQL Transforma 을 통해서, 분석 가능한 데이터로 바꾸어준다.

<br>

## Stitch

- 데이터 ETL 도구이다.
- 많은 데이터 소스들을 지원한다. 
- 대부분의 비즈니스 서비스의 분석도구들을 지원한다. 

<br>

<br>

# 2.Data Modeling

![png](/assets/images/Data_Infra/2_3.png)

- 소스에서 오지 않는다.
- 데이터가 웨어하우스와 레이크에서 오게 된다.

<br>

## dbt

- dbt 는 데이터 built tool 이다.
- 이는 데이터 분석가를 위한 데이터 엔지니어링이다.
- 일반적으로 엔지니어가 추출한 데이터를 분석가가 받아 쓰는 형태이다.

![png](/assets/images/Data_Infra/2_4.png)

- 하지만 위와 같이 SQL 을 사용하여 데이터를 가져와 그 데이터를 테스트 ,Deploy 등을 할 수 있게 해준다.
- 어떤 데이터를 가져와 변환할지 등을 SQL 로 다 할 수 있다.
- 이는 웨어하우스에 영향을 미치지 않아서 분석가가 한번 변환, 등을 해볼 수 있는것이다.

<br>

## Look ML

- 대시보드나 리포트를 만들기 위해 쓰는 도구
- BI 쪽에서 만든 모델링을 할 수 있는 도구이다.
- 내가 원하는 데이터를 Transform 해볼 수 있음

<br>

<br>

# 3.Workflow Manager

- 데이터 소스에서 데이터를 가져와 데이터 웨어하우스 / Lake 로 옮긴다.
- 하지만 이를 워크플로우 단위로 관리한다. (의존성 관리/ 작동순서 등등을 관리)

<br>

## Apach workflow

- 복잡한 워크플로우를 관리해준다.
- 테스크 스케쥴링 해준다. (언제 어떤일울 수행할것인가)
- 분산 Execution : 여러대에서 분산해서 실행
- 어떤것을 먼저 실행할지에 대해서 Dependency 를 관리

![png](/assets/images/Data_Infra/2_5.png)

- 위와 같이 어떤 행동을 하기 위해, 작동되어야 하는 순서를 처리 / 계획한다.

<br>

## Dagster

- 에어플로우와 비슷하다.
- 데이터를 변환하는 모든것을 어플리케이션처럼 만들었다.

<br>

<br>

# Workflow 와 Spark,python,hive 의 관계

![png](/assets/images/Data_Infra/2_6.png)

- 위를 보면 여러 플랫폼 (Spark / Python) 이 같이 묶여져있는것을 볼 수 있다.
- 이때에 워크플로우와 연결이 되어있는것을 볼 수 있는데 왜 그럴까?
  - 워크플로우 매니저에서는 테스크의 실행 순서를 할당한다.
  - 매우 많은 양의 데이터를 다루다보면, 수천대에서 분할 분석해야한다. 이 때에 순서가 매우 중요하다.
  - 즉 워크플로우가 스파크에 큰 작업순서를 할당하는 형식이다.

# 4.Python 

- 파이썬 라이브러리에는 pandas .. 등이 있다.

### Pandas

- 판다스는 Panel data 로부터 온 이름이다.

![png](/assets/images/Data_Infra/2_7.png)

- 위와 같이 Tabular 데이터를 다룬다.
- 다양한 Json / Csv ... 등의 데이터를 Dataframe 으로 바꿔서 분석한 이후, 이를 다시 다양한 Format 으로 내보낼 수 있게 해준다.
- 데이터의 형태를 바꾸거나 분석 등의 많은 작업을 할 수 있다.

### boto

- 아마존 웹서비스에 접근해줄 수 있게 해주는 라이브러리
- 파이썬에서 아마존 리소스를 사용할 수 있게 해주는 API

### DASK

- 파이썬으로 만들어진것은 대부분 Local 에서 혼자 돌아간다.
- 하지만 이를 병렬처리하게 해주는 라이브러리

![png](/assets/images/Data_Infra/2_8.png)

- 위에서 보면 Numpy , Pandas 등의 데이터를 각각 나누어서 여러 서버에서 분산처리 할 수 있게 해준다. 

### Lay

- Dask 랑 거의 같게 분산처리할 수 있게 해준다.

<br>

# 5.Apache Spark

- 대규모 데이터 처리를 위한 빠르고 범용적인 엔진이다. 
- 오픈소스로 된 분산처리를 해주는 Frame Work 이다.
- 여러대의 서버에 나누어서 처리를 할 수 있게 해준다.

![png](/assets/images/Data_Infra/2_9.png)

- 위처럼 항상 하둡가 비교디어왔다.
- 요즘은 아파치 스파크가 거의 다 장악한 상황이라고 한다.

- 스파크는 하둡 맵 리듀스보다 더 빠르다고 한다.

### 맵 리듀스(하둡)

- 맵 리듀스는 어떤 일이 있을때, 그 일을 쪼개서 여러 서버에 나누어준다.
- 나누어진 일을 처리한것을 다시 서버에 보낸다. 
- 이렇게 일들을 나누고, 다시 합치는것이 하둡 파일 시스템에서만 진행되어서 매우 느렸다.

### 맵 리듀스(Spark)

- 맵 리듀스가 큰 데이터 분석을 쉽게 만들어주긴 하였다.

- 데이터를 하둡 파일 시스템에 넣엇다 뺴었다 하니까 느린것! 
- 이걸 램으로 해버린것이다.

![png](/assets/images/Data_Infra/2_10.png)

- 하지만 램은 빠르지만 꺼지면 날아갈 수 있다.
  - 어떻게 하면 꺠지지 않는 램을 만들 수 있을까? 
  - 즉 램을 Read only 로만 쓰는것. RDD(Resilient Distributed Datasets) 로서 쉽게 복원이 되는 분산 데이터셋으로 만들자.
  - RDD는 데이터가 한번 만들어지고 나면 수정이 되지 않는다. 어떻게 만들어졌는지만 계보만 기록한다.
  - 이것만 가지고도 변한것을 쫒아가면서 복원이 가능하다! 
- RDD 에는 매우 많은 명령어가 있다.
  - 그래서 효율적인 스케쥴링이 가능함 (놀고있는 워커들 (분산처리할당하는 작은 서버들) 에게 일을 시킬수 있음)

### 특징

- 하둡보다 최대 100배 빠르게 가능(램덕분)
- 내부는 Scalar 로 구현되어있지만 Python,R,SQL 등을 이용할 수 있게 지원한다.
-  스파크는 RDD 를 처리하는 로직이다. 이 위에 여러 Component 들을 올릴 수 있다.

![png](/assets/images/Data_Infra/2_11.png)

- 위처럼 스파크 위에 SQL , 그래프도 그릴 수 있고 머신러닝도 할 수 있게 위에다가 얹을 수 있다.
- 즉 위처럼 많은것을 빠르게 처리할 수 있다.

# 6.Hive

- 아파치 스파크 위에 있는 데이터를 쿼리하기 위한 엔진이다.(SQL 사용)

- 하둡통해서 데이터를 쿼리하려면 맵 리듀스 잡을 짜야한다.
- 하지만 HIve 에서 SQL 을 사용하면 SQL 잡이 맵 리듀스 잡으로 자동으로 변환된다.
- 스파크 SQL 을 왜 사용하지 않을까? 왜 하이브가 있지? 
  - 하이브를 실행하는 엔진으로 스파크를 쓰게 되면 많은것을 할 수 있다.
  - 서로 보완하는 요소가 있음 (하이브만의 장점이 있음...)

