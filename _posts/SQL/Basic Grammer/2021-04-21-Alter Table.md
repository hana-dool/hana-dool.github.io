---
title:  "Alter Table"
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

# [Alter Table](#link){: .btn .btn--primary}{: .align-center}

> ## 기본 구조

- mysql 에서 alter table 은 다음과 같은 연산을 수행할 수 있습니다.
  - column 더하기 
  - column 이름 다시 지정하기
  - column 삭제하기
  - table 이름 다시 지정하기

> Date - set

```sql
CREATE TABLE vehicles (
    vehicleId INT,
    year INT NOT NULL,
    make VARCHAR(100) NOT NULL,
    PRIMARY KEY(vehicleId)
);
```

- 위와 같은 데이터를 먼저 만들어봅시다.

> ## ADD : 컬럼 추가하기

- 새로운 column 을 생성하기 위해서는 `ALTER TABLE ADD COLUMN` 와 같은 명령를 사용합니다.

```sql
ALTER TABLE table_name
ADD 
    new_column_name column_definition
    [FIRST | AFTER column_name]
```

- column 이 추가될 테이블의 이름을 (`table_name`) 부분에 넣습니다. 
- 그리고 column 의 이름을 `new_column_name` 에 추가하고, 뒤에는 제약조건 (`column_definition`) 을 추가합니다.
- `FIRST | AFTER column_name` 는 새로운 column 이 추가되는 위치를 지정합니다.
  - (`ATER column_name`) 을 사용하여 existing column 인 column_name 오른쪽에 삽입 가능
  - first column (`FIRST`) 에 사용 가능 
  - 만일 생략하면 맨 오른쪽에 삽입되게 됩니다.

```sql
ALTER TABLE vehicles
ADD model VARCHAR(100) NOT NULL;
```

- 위와 같이 vehicles 테이블에 새로운 column 을 추가할 수 있습니다.

```
Field    |Type        |Null|Key|Default|Extra|
---------+------------+----+---+-------+-----+
vehicleId|int         |NO  |PRI|       |     |
year     |int         |NO  |   |       |     |
make     |varchar(100)|NO  |   |       |     |
model    |varchar(100)|NO  |   |       |     |
```

> ## ADD : 여러 컬럼 한번에 추가하기 

````sql
ALTER TABLE table_name
    ADD new_column_name column_definition
    [FIRST | AFTER column_name],
    ADD new_column_name column_definition
    [FIRST | AFTER column_name],
    ...;
````

- 위처럼 한번에 여러개의 column 을 추가할 수 있습니다. 

```sql
ALTER TABLE vehicles
ADD color VARCHAR(50),
ADD note VARCHAR(255);
```


```
Field    |Type        |Null|Key|Default|Extra|
---------+------------+----+---+-------+-----+
vehicleId|int         |NO  |PRI|       |     |
year     |int         |NO  |   |       |     |
make     |varchar(100)|NO  |   |       |     |
model    |varchar(100)|NO  |   |       |     |
color    |varchar(50) |YES |   |       |     |
note     |varchar(255)|YES |   |       |     |
```

- 위와 같이 여러개의 Column 을 한번에 만들 수 있습니다.

> ## MODIFY : 컬럼 타입 수정하기 

```sql
ALTER TABLE table_name
MODIFY column_name column_definition
[ FIRST | AFTER column_name];    
```

- 위처럼 modify 를 이용하여서 column 의 타입을 수정할 수 있습니다.

```sql
DESCRIBE vehicles;
```

```
Field    |Type        |Null|Key|Default|Extra|
---------+------------+----+---+-------+-----+
vehicleId|int         |NO  |PRI|       |     |
year     |int         |NO  |   |       |     |
make     |varchar(100)|NO  |   |       |     |
model    |varchar(100)|NO  |   |       |     |
color    |varchar(50) |YES |   |       |     |
note     |varchar(255)|YES |   |       |     |
```

- 원래는 위와 같았습니다. `note` 컬럼의 type 을 varchar(100) 으로 바꾸고 싶다고 합시다.

```sql
ALTER TABLE vehicles 
MODIFY note VARCHAR(100) NOT NULL;
```

```
Field    |Type        |Null|Key|Default|Extra|
---------+------------+----+---+-------+-----+
vehicleId|int         |NO  |PRI|       |     |
year     |int         |NO  |   |       |     |
make     |varchar(100)|NO  |   |       |     |
model    |varchar(100)|NO  |   |       |     |
color    |varchar(50) |YES |   |       |     |
note     |varchar(100)|YES |   |       |     |
```

- 위처럼 잘 바뀐것을 볼 수 있습니다.

> ## MODIFY : 여러컬럼 타입 수정하기 

```sql
ALTER TABLE table_name
    MODIFY column_name column_definition
    [ FIRST | AFTER column_name],
    MODIFY column_name column_definition
    [ FIRST | AFTER column_name],
    ...;
```

- 이렇게 여러개 Column 의 타입 변경도 가능합니다.

```sql
ALTER TABLE vehicles 
MODIFY year SMALLINT NOT NULL,
MODIFY color VARCHAR(20) NULL AFTER make;
```

```
Field    |Type        |Null|Key|Default|Extra|
---------+------------+----+---+-------+-----+
vehicleId|int         |NO  |PRI|       |     |
year     |smallint    |NO  |   |       |     |
make     |varchar(100)|NO  |   |       |     |
color    |varchar(20) |YES |   |       |     |
model    |varchar(100)|NO  |   |       |     |
note     |varchar(100)|YES |   |       |     |
```

> ## CHANGE COLUMN : 테이블 이름 바꾸기

```sql
ALTER TABLE table_name
    CHANGE COLUMN original_name new_name column_definition
    [FIRST | AFTER column_name];
```

- 위처럼 CHANGE COLUMN 이라는 명령어를 쓰면 이름을 바꿀 수 있습니다.

```sql
ALTER TABLE vehicles 
CHANGE COLUMN note vehicleCondition VARCHAR(100) NOT NULL;
```

```
DESCRIBE vehicles;
```

```
Field           |Type        |Null|Key|Default|Extra|
----------------+------------+----+---+-------+-----+
vehicleId       |int         |NO  |PRI|       |     |
year            |smallint    |NO  |   |       |     |
make            |varchar(100)|NO  |   |       |     |
color           |varchar(20) |YES |   |       |     |
model           |varchar(100)|NO  |   |       |     |
vehicleCondition|varchar(100)|NO  |   |       |     |
```

> ## DROP : 컬럼 쳐내기

> 기본 구조

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

> 예시

```sql
ALTER TABLE vehicles
DROP COLUMN vehicleCondition;
```

```
Field    |Type        |Null|Key|Default|Extra|
---------+------------+----+---+-------+-----+
vehicleId|int         |NO  |PRI|       |     |
year     |smallint    |NO  |   |       |     |
make     |varchar(100)|NO  |   |       |     |
color    |varchar(20) |YES |   |       |     |
model    |varchar(100)|NO  |   |       |     |
```

> ## RENAME TABLE : 테이블 이름 바꾸기 

> 기본구조

```sql
ALTER TABLE table_name
RENAME TO new_table_name;
```

> 예시 

```
ALTER TABLE vehicles 
RENAME TO cars; 
```

