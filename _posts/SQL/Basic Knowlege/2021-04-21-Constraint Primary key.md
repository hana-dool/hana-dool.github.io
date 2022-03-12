---
title:  "Constraint &#58; Primary Key"
excerpt: ""
categories:
  - SQL_Basic_Knowledge
last_modified_at: 2021-05-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true 
typora-root-url: ../../../../hana-dool.github.io
---

# [Constraints](#link){: .btn .btn--primary}{: .align-center}

> ## Definition 

- 제약 조건(constraint)이란 데이터의 무결성을 지키기 위해, 데이터를 입력받을 때 실행되는 검사 규칙을 의미합니다.
- 이러한 제약 조건은 CREATE 문으로 테이블을 생성할 때나 ALTER 문으로 필드를 추가할 때도 설정할 수도 있습니다.
- MySQL에서 사용할 수 있는 제약 조건은 다음과 같습니다
  - NOT NULL
  - UNIQUE
  - PRIMARY KEY
  - FOREIGN KEY
  - DEFAULT

> ## Primary Key

- Primary key 는  테이블의 각 행을 고유하게 식별하는 열 또는 열 집합입니다. 기본 키는 다음 규칙을 따릅니다.
- 기본 키 열은 `NULL`값을 가질 수 없습니다.
- 테이블에는 Primary Key 가 하나만 있을 수 있습니다.
- MySQL은 정수로 더 빠르게 작동하기 때문에 기본 키 열의 [데이터 유형](https://www.mysqltutorial.org/mysql-data-types.aspx) 은 정수여야 합니다(예: . 그리고 기본 키에 대한 정수 유형의 값 범위가 테이블에 있을 수 있는 모든 가능한 행을 저장하기에 충분한지 확인해야 합니다
- 기본 키 열에 는 테이블 [에 새 행을 삽입할](https://www.mysqltutorial.org/mysql-insert-statement.aspx)`AUTO_INCREMENT` 때마다 자동으로 순차 정수를 생성하는 속성 이 있는 경우가 많습니다.
- 테이블에 대해서 primary key 를 지정하면 mysql 은 자동적으로 인덱스를 생성합니다.

