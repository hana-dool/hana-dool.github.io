---
title: "1.Data Infra Structure"
excerpt: "데이터의 인프라 Structure"
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



## Intro

https://www.youtube.com/watch?v=g_c742vW8dQ 의 데이터인프라 소개글을 보고 정리한 내용입니다

<br>

## 데이터 인프라의 목적

- 데이터 기반의 의사 결정을 할 수 있도록 도와주기 위해서, 
- 서비스, 제품을 데이터의 도움을 받아 향상시키기 위함이다.

<br>

## 데이터 인프라의 기초

- Production 시스템이 데이터가 생겨나는 곳이다. 
- SQL , ORACLE 등의 프로덕션 시스템등이 해당
- 각각의 데이터들은, 분석하고 싶다고 할때에, 각각의 플랫폼별로 분석도구가 다르다.
- 그래서 통합된 보고서 작성을 위해서 다양한 소스로부터 데이터를 저장하는 Data Warehouse 가 필요하게 되었다.

![png](/assets/images/Data/2_1.png)

<BR>

## 데이터 웨어하우스

- Production system 과 Data Warehouse 에는 차이가 있다.

![png](/assets/images/Data/2_2.png)

- Production system 
  - Normalized Schema 라고 하는 작은 테이블로 다 쪼샌다.
  - 사용자 / 주문번호 / 매출 .... 다 쪼개서 저장.
- Data Warehouse
  - Dimensional Schema 라고 하는 테이블을 쓴다.
  - 가운데에 Fact 테이블이 있고, 그를 중심으로 붙어있는 형식
  - 원하는 데이터만을 딱 뽑을 수 있게 만들어졌다. (분석을 위함이므로)

- 이제 두 System 을 쓰려면 어떻게 해야할까? 
- 데이터를 Production system 에서 data ware house 로 옮겨야 한다는 것이다.
- 이렇게 옮기는 과정을 ETL 이라고 한다.  

<br>

## ETL / ELT

![png](/assets/images/Data/2_3.png)

- 데이터를 Production system 에서 뽑아낸다.(추출)
- 그것을 작고 작게 쪼개진 normalized schema 를 dimensional schema 로 변환한다.
- 그러고 나서 이를 데이터 Ware house 로 적제한다.
- 하지만 추출과 변환이 자동화되기가 너무 힘들고, 회사마다 다르다.
- 그래서 수정할게 많다.

![png](/assets/images/Data/2_4.png)

- 추출해서 적재하는것은 우선 다 해놓는다. (자동화 가능 )
- 그 이후에 ware house 에서 변환하는것이다. 이를 ELT 라 한다.

<br>

# Overall Structure

![png](/assets/images/Data/2_5.png)

- Source
  - 회사내의 모든 데이터가 만들어지는곳
- Ingestion and Transformation
  - 데이터를 가져와 변환
- Storage
  - 데이터의 저장소 (warehouse, lake)

- Historical
  - 옛날의 데이터들을 분석하는것
- Predictive
  - 미래의 데이터를 예측하는것
- Output
  - 분석된 결과를 보여주는것