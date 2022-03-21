---
title:  "Model Construction"
excerpt: ""
categories:
  - SQL_Tunning
last_modified_at: 2022-03-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 MYSQL 과 MariaDB
{: .notice--warning}

# [데이터 모델설계](#link){: .btn .btn--primary}{: .align-center}

> ## 모든 테이블에 기본키가 있는지 확인해라

- 관계형 모델을 따르려면 데이터베이스 시스템이 특정 row 와 , 나머지 row 를 구별할 수 있어야 합니다.
  - 즉 이는 모든 테이블에는 키본 키 (Primary key) 컬럼이 한개 이상 있어야 한다는것을 의미합니다. 

- 키본키는 Row 마다 고유하고, Null 값을 가질 수 없습니다.
- 기본키가 없으면, 일치하는 row 가 없거나, 딱 한개인 조건을 보장할 수 없습니다.
  - 물론 기본키가 없이 데이터베이스를 만들 수 있습니다.


> 기본 키가 없으면? 

```
Orders Name         |
--------------------+
        john.A smith|
       Smith, John A|
          John.Smith|
        John A Smith|
         Smith, John|
```

- 위와 같은 주문 테이블을 생각해봅시다.
- 위 데이터의 경우 모두 이름이 같은 사람입니다. (표기법만 다른것)
- 하지만 이름이 다르므로, 기본 키의 후보 자격은 아래와 같습니다.
  - 유일한 값을 가져야한다.
  - Null 값을 가질 수 없다.
  - 안정적인 값이여야한다. (즉 값을 갱신할 필요가 없음)
  - 가능한 한 간단한 형태. (즉 부동소수점보다는 정수형이 낫고, 여러 컬럼보다는 단일 컬럼이 낫다.)
- 이런 목표를 달성하기 위해서는 일반적으로 숫자 데이터로 자동 생성되는 컬럼을 기본 키로 만듭니다. 
  - mysql 에서는 auto_increment 라고 함. 

> 참조 무결성

- 관게형 데이터베이스에서 참조 무결성은 매우 중요합니다. 
  - 참조 무결성 : 외래키가 설정된 자식 테이블의 각 레코드와 일치하는 레코드가 부모 테이블에 존재한다는것.
- 잘 설계된 테이블이라면 고객정보 컬럼에 외래키를 설정하여, Customer 의 기본키와 연결되어 있을 것입니다. 
  - 따라서 Jon Smith 라는 고객이 여러명이라도, 각 row 는 유일한 key 를 가지므로 각 주문에 대응하는 하나의 고객을 쉽게 식별할 수 있습니다.
