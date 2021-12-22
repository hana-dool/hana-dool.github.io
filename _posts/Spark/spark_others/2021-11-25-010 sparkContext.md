---
title:  "SparkContext"
excerpt: "스파크 컨텍스트로 저수준 다루기"
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

# [SparkContext](#link){: .btn .btn--primary}{: .align-center}

> ## SparkContext 이란?

- Spark2.0이후 부터는 아래와 같은 계층 구조를 가진다.
  - SparkSession > SparkContext > HiveContext > SQLContext
- SparkSession은 spark2.X 이후부터 지원한다.
- 일반적으로 SparkContext 에서 구현되는 것들은 모두 SparkSession 에서 사용할 수 있습니다.
- SparkContext 는 저수준 를 
- 저수준 API 는 두가지 종류가 있습니다.
  - 하나는 분산 데이터처리를 위한 RDD
  - 두번째는 분산형 공유 변수를 배포하고 다루기 위한 API
- SparkContext 는 저수준 API 기능을 사용하기 위한 짐입 지점입니다.
  - 스파크클러스터에서 연산을 수행하는데에 필요한 SparkSession 을 이용해서 SparkContext 에 접근할 수 있습니다.

> note : 자세한거는 나중에...

**Reference**

- 스파크 완벽 가이드
- <https://deviscreen.tistory.com/104>

