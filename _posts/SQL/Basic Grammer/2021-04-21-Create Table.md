---
title:  "Create Table"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2022-03-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

# [Create Table](#link){: .btn .btn--primary}{: .align-center}

> ## 기본 구조

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

- 필수 정보는 테이블 이름과 열 이름입니다
- `table_name` 은 데이터베이스 내에서 고유한 이름을 가져야 합니다.
  - 이미 존재하는 것과 동일한 이름의 테이블을 생성하면 데이터베이스 시스템에서 오류가 발생합니다.
- `CREATE TABLE` 은 열 정의시에 쉼표로 구분됩니다.
  - 각 열 정의는 열 이름, 열의 [데이터 유형](https://www.sqltutorial.org/sql-data-types/) , 기본값 및 하나 이상의 열 제약 조건으로 이루어집니다.
- 열 제약 조건
  - 열에 지정할 수 있는 값의 종류를 조절합니다.  예를 들어, `NOT NULL`제약 조건은 열에 NULL 값이 포함되지 않도록 합니다.

> ## Example 

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

# [Create Table AS : 다른 테이블 이용하기](#link){: .btn .btn--primary}{: .align-center}

> ## 기본 구조 

- MySQL CREATE TABLE AS 문은 기존 테이블의 열을 복사하여 기존 테이블에서 테이블을 생성하는 데 사용됩니다.
- 이러한 방식으로 테이블을 생성할 때 새 테이블은 Slect 문을 기반으로 하는 기존 테이블의 레코드로 채워집니다 .

> 기본구조

```sql
CREATE TABLE [ IF NOT EXISTS ] new_table [ AS ] 
  SELECT expressions
  FROM existing_tables
  [WHERE conditions];
```

> Parameter 

- IF NOT EXISTS (Optional)
  - 지정된 경우 테이블이 이미 존재하는 경우에는 에러를 발생하게 됩니다. 
  - 위와 같이 IF NOT EXIST (new_table 이 존재하지 않을떄에만)  생성하도록 코드를 짤 수 있습니다.

```
-- 에러가 존재하는 경우
SQL Error [1050] [42S01]: Table 'temp_table' already exists
```

- AS (Optional)
  - AS 는 optional 입니다. (AS 를 쓰는것, 안쓰는것은 출력에 대해서 크게 상관이 없음)
  - 하지만 AS 를 쓰는것을 권장..
- Where condition
  - Where 은 select 절에 들어가는 where 입니다. 필터링의 역할을 함..

> ## Example

```sql
CREATE TABLE temp_table AS
SELECT *
FROM emp 
WHERE sal >- 2000 ;  
```

- 위와 같이 실행하게 되면, 우리가 원하는 테이블을 Select 문법을 이용해 만들게 됩니다.
  - 이제 우리는 temp_table 이라는 테이블이 데이터베이스에 적재되게 됩니다.

```sql
SELECT *
FROM temp_table ; 
```

```
empno|ename|job      |mgr |hiredate  |sal    |comm|deptno|
-----+-----+---------+----+----------+-------+----+------+
 7566|JONES|MANAGER  |7839|1981-04-02|2975.00|    |    20|
 7698|BLAKE|MANAGER  |7839|1981-05-01|2850.00|    |    30|
 7782|CLARK|MANAGER  |7839|1981-06-09|2450.00|    |    10|
 7788|SCOTT|ANALYST  |7566|1987-04-19|3000.00|    |    20|
 7839|KING |PRESIDENT|    |1981-11-17|5000.00|    |    10|
 7902|FORD |ANALYST  |7566|1981-12-03|3000.00|    |    20|
```

- 위처럼 temp table 의 값이 잘 생성된것을 볼 수 있습니다!

# [기능별 Example](#link){: .btn .btn--primary}{: .align-center}

> ## 테이블 구조 복사

**Create Table new_table like old_table**

 특징 : 기존 테이블의 설정 그대로 복사 된다.

  참고 ==> 큐브리드의 경우 복사하고자 하는 기존 테이블에 'Primary Key' 또는 'auto_increment' 가 설정 되어 있으면 복사 할 수 없음.

  응용 ==> Create Table IF NOT EXISTS new_table like old_table (new_table 이 없으면 복사)

> ## 구조와 데이터 복사 

\* 구조와 데이터 복사

**Create Table new_table ( select \* from old_table )**

 ﻿특징 : 테이블의 구조와 함께 데이터도 함께 복사가 된다.

   주의 ==> 큐브리드의 경우와 같이 기존 테이블에 'Primary Key' 또는 'auto_increment' 가 설정 되어 있으면

​    해당 설정은 적용 되지 않고 값만 복사 됨.

> ## 데이터 복사

\* 데이터 복사

**Insert Into destination_table ( select \* form source_table)**

 참고 ==> 대상 테이블의 컬럼 중에 자동 증가 값 설정 이 된 컬럼이 있을 경우 해당 컬럼에 데이터 입력시 중복된 데이터가 있으면 오류 발생.

 응용 ==> Insert Into destination_table (column_a, column_b) (select a, b from source_table) 원하는 필드의 데이터만 복사가 가능하다.



---

Reference

- https://m.blog.naver.com/kilsu1024/110162891049
