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

---

**Reference**

- 스파크 완벽 가이드

