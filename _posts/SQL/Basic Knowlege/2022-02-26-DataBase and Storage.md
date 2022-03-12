---
title:  "DataBase and Storage"
excerpt: ""
categories:
  - SQL_Basic_Knowledge
last_modified_at: 2022-02-26

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

# [Error](#link){: .btn .btn--primary}{: .align-center}

> ## Data

- DB : 데이터베이스 프로그램 
- Storage : 데이터 저장 공간 

> ## Storage

- 스토리지는 파일이 담깁니다.
- DB는 엑셀에서 쓰는 내용과 같은 2차원 데이터 형태인 칼럼(Column)과 로우(Row)로 구성되는 테이블형 데이터가 담깁니다.
- 컴퓨터에 데이터를 저장하는 저장소의 역할을 수행하는 부품으로, 하드디스크와 동일한 역할을 수행하는 부품이다.(비휘발성 기억장치)
- 즉, 스토리지는 파일 형태가 되면 무엇이든 담을수 있다.

> ## Database

- 데이터베이스라고 하면 데이터 자체뿐만 아니라 데이터 환경의 구조와 디자인을 모두 의미합니다. 
- 일반적으로 데이터베이스는 데이터베이스 관리 시스템(DBMS)에 의해 구성됩니다. DBMS는 데이터베이스를 생성, 유지 관리 및 액세스하는 데 사용되는 소프트웨어 응용 프로그램입니다. 

> ## 차이점 

- 데이터베이스는 스토리지 입니다. 하지만 스토리지는 데이터베이스일 필요는 없습니다.
  - 데이터베이스는 orgaized storage 라고 할 수 있죠.
- 스토리지는 데이터, 문서, 비디오 등이 컴퓨터 또는 컴퓨터 시스템(로컬 네트워크 서버, 클라우드 호스팅 시스템 등)에 저장되는 장소입니다.
- 데이터베이스는 사용자가 새로운 레코드를 생성하고, 데이터 테이블의 해당 관련 레코드와 함께 기존 레코드를 검색 및 찾고, 레코드를 업데이트하고, 마지막으로 기존 및 발견된 데이터 레코드를 삭제할 수 있도록 데이터를 구성하는 데 사용되는 시스템입니다.
- 데이터베이스는 사용자가 데이터를 쉽게 입력하고, 데이터를 보고하고, 재무 및 마케팅 분석을 수행하여 모성 경쟁 기업을 이끄는 데 도움이 되는 구조화되고 엄격한 규칙 기반 프로세스 및 절차의 사용에 대해 전문가가 프로그래밍하고 설계했습니다. 잘 알려진 시스템은 Microsoft Simple Query Language(SQL Database)이지만 IBM, Digital Research, Oracle, FileMaker(Apple), Dbase 등과 같이 잘 알려진 회사에서 만든 다른 많은 시스템이 있습니다.

> 저장 데이터 종류 

- Storage는 텍스트파일, 이미지, 영상 등 다양한 종류의 데이터가 저장될 수 있다.
- Database는 Id, record, 거래정보와 같은 구조적 또는 반구조적 데이터가 저장될 수 있다.

**reference**

- https://www.quora.com/What-is-the-difference-between-storage-and-database

