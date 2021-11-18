---
title: "2.Data Source"
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



## Intro

https://www.youtube.com/watch?v=g_c742vW8dQ 의 데이터인프라 소개글을 보고 정리한 내용입니다

<br>

## 데이터 소스

- 데이터가 발생되고, 저장하는 공간.
- 발생하는 원본소스들을 따른데에 보낼수도 있다.

- 데이터 인프라 스트럭쳐에서 아래의 Source 부분을 이해하는데에 목적을 둡니다.

![png](/assets/images/Data_Infra/1_1.png)

<br>

## OLTP

- OLTP 는 보통 은행계좌 예시를 많이 든다.
- 돈을 이체할때에는 A 의 입금과 B 의 수령이 같이 이루어져야 한다.
- 이와 같이, 두가지 Operation 이 Transaction 으로 묶이고, 이 묶여진 데이터가 처리하는 데이터 베이스를 OLTP 라 한다.

![png](/assets/images/Data_Infra/1_2.png)

- 보통 Transaction 이 많고, 빨리 처리해야 되므로 정규화된 데이터를 처리한다. 
- OLAP 는 데이터 분석 / 웨어하우스에서 분석쿼리를 날리는 곳이라고 생각하면 된다.

<Br>

## Application /ERP/ CRM 

- 오라클, Saleforce ... 등이 있다.
- 비즈니스 입장에서 생성되는 데이터 관리
- ERP (전사적 자원관리)
  - 회사에서 일어나는 모든 자원이 ERP 에서 일어난다.
  - 프로젝트 변경, 인사변경 등등 매우 중요한것이 저장된다.
- CRM
  - 고객과 관련된 모든 모든 행동을 처리/ 생성해준다.. 
  - 판매 , 마케팅 등등. ..

<br>

##  Event Collection

- 사용자가 만들어내는 모든 데이터를 모으는 도구

- 예시로 이용자가 어느것을 구매했고, 어떤것을 클릭했는지 등등을 측정할 수 있다. (구글 어날리틱스)

![png](/assets/images/Data_Infra/1_3.png)

- Segment 는 어떤 서비스일까?
  - 커스터머 데이터 플랫폼이다. 
  - 세그먼트는 웹 / 모바일 / 등등에서 오는 데이터가 모두 통합이 된다.
  - 그 이후에 각각의 분석 툴로 보낸다.
  - 즉 Event 를 수집하고, 각각의 툴로 보내주는것이다.
  - 세그먼트의 큰 장점은 수많은 분석툴과 연결되어있다.
  - 개발자가 세그먼트 없이 한다면 코딩을 모두 따로해야된다.

![png](/assets/images/Data_Infra/1_4.png)

- Snowflow 도 Segment 와 비슷하다.

<br>

## Log

- 우리가 운영하는 웹서버 등에 대한 로그 데이터
- 엑세스 로그, 행동 로그 등....

<br>

## 3rd Party API

- 회사에서 운영하지 않는, 외부서비스의 데이터

<Br>

## File and Object Storage

- 직접 어떤 문서를 저장한다거나,
- 어떤 파일을 저장하는 데이터