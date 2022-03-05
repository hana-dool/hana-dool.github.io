---
title:  "Create Table"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2021-12-06

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

# [Create Table](#link){: .btn .btn--primary}{: .align-center}

> ## Create Table

```sql
CREATE TABLE table_name(
     column_name_1 data_type default value column_constraint,
     column_name_2 data_type default value column_constraint,
     ...,
     table_constraint
);
```

- 기본적으로 SQL 은 위와 같은 문법을 따릅니다. 

> 테이블 생성 규칙

- 새 테이블을 생성하기 위한 최소한의 필수 정보는 테이블 이름과 열 이름입니다.
- `table_name` 은 데이터베이스 내에서 고유한 이름을 가져야 합니다.
  - 이미 존재하는 것과 동일한 이름의 테이블을 생성하면 데이터베이스 시스템에서 오류가 발생합니다.
- `CREATE TABLE` 은 열 정의시에 쉼표로 구분됩니다.
  - 각 열 정의는 열 이름, 열의 [데이터 유형](https://www.sqltutorial.org/sql-data-types/) , 기본값 및 하나 이상의 열 제약 조건으로 이루어집니다.
- 열 제약 조건
  - 열에 지정할 수 있는 값의 종류를 조절합니다.  예를 들어, `NOT NULL`제약 조건은 열에 NULL 값이 포함되지 않도록 합니다.

```sql
CREATE TABLE courses (
    course_id INT AUTO_INCREMENT PRIMARY KEY,
    course_name VARCHAR(50) NOT NULL
);
```

- 위와 같이 Table 을 형성할 수 있습니다.

```sql
SELECT *
FROM courses ; 
```

```
course_id|course_name|
---------+-----------+
```

- 위와 같이 courses 의 테이블이 만들어진것을 볼 수 있습니다.
- `courses`표는 두 개의 열이 있습니다 `course_id`와 `course_name`.
-  `course_id`  에 대한 제약조건
  - 이 컬럼은 SQL Primary Key 컬럼입니다. 
  - 각 테이블에는 테이블의 각 행을 고유하게 식별하는 하나의 기본 키만 있습니다. 모든 테이블에 대해 기본 키를 정의하는 것이 좋습니다.
- Course_name 열에 대한 제약조건
  - `VARCHAR`최대 길이가 50인 문자열(입니다
  - `NOT NULL`제약 조건은 `course_name`열에 NULL 값이 저장되지 않도록 합니다 .

> ## Example 

```sql
CREATE TABLE testTable(                               (1)
  id INT(11) NOT NULL AUTO_INCREMENT,                 (2)
  name VARCHAR(20) NOT NULL,                          (3)
  ouccupation VARCHAR(20) NULL,                       (4)
  height SMALLINT,                                    (5)
  profile TEXT NULL,                                  (6)
  date  DATETIME,                                     (7)
  CONSTRAINT testTable_PK PRIMARY KEY(id)             (8)
);
```

- (1) 테이블을 생성하는 명령어입니다.
- (2) id라는 컬럼을 추가하는 데, INT 타입으로 지정합니다. NOT NULL은 값을 비워둘 수 없음을 의미합니다. AUTO_INCREMENT는 자동으로 값이 1씩 증가하도록 설정하는 옵션입니다.
- (3) name이라는 컬럼을 추가하는데, 가변길이로 20글자까지 허용합니다. (20글자가 넘어가면 20글자에서 자릅니다.)
- (4) 위와 동일하지만, 값을 비워두는 것을 허용합니다.
- (5) SMALLINT는 INT보다 가질 수 있는 값의 범위가 작습니다. 메모리 측면에서 이득입니다.
- (6) TEXT는 아주 긴 문자열을 취급할 때 사용합니다.
- (7) DATETIME은 날짜와 시간에 관한 타입입니다.
- (8) CONSTRAINT는 제약조건이라는 의미입니다. testTable의 PRIMARY KEY를 id 컬럼으로 지정하겠다는 의미이며, 이 제약조건의 이름을 testTable_PK로 지정한 것입니다.

