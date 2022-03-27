---
title:  "Constraint Primary Key"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2021-05-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true 
typora-root-url: ../../../../hana-dool.github.io
---

- 제약 조건(constraint)이란 데이터의 무결성을 지키기 위해, 데이터를 입력받을 때 실행되는 검사 규칙을 의미합니다.
- 이러한 제약 조건은 CREATE 문으로 테이블을 생성할 때나 ALTER 문으로 필드를 추가할 때도 설정할 수도 있습니다.
- MySQL에서 사용할 수 있는 제약 조건은 다음과 같습니다
  - PRIMARY KEY
  - NOT NULL
  - UNIQUE
  - DEFAULT
  - FOREIGN KEY

# [Primary Key](#link){: .btn .btn--primary}{: .align-center}

> ## 기본 구조

> 기본 키의 주요 성질

- 기본 키는 고유한 값이여야 합니다. 
  - 만일 기본 키가 여러 열로 구성된 경우 이러한 열의 값 조합은 고유해야 합니다.
- 기본 키 열은 `Null` 값을 가질 수 없습니다.
  - primary key 열에 null 을 삽입하려 하면 에러를 발생시키게 됩니다.
- 테이블은 오로지 하나의 primary key 를 가질 수 있습니다. 

> 기본 키 Tip

- mysql 은 integers 에서 좀 더 빠르게 작동하므로 primary key 의 interger type 은 기본적으로 integer 가 되어야 합니다.
  - 이때 주의해야될것은, 많은 row 수를 표현할 수 있을만큼 integer type 이 커야한다는 것입니다.
- key column 은 주로 `Auto_Increment` 의 데이터타입을 가지곤 합니다. 
  - 이는 row 를 insert 할때마다 자동으로 1 씩 증가하게 됩니다.

> 언제 Primary key 설정을 할 수 있는가? 

- primary column 은 table 을 만들때(create), 또는 고칠때 (alter) 사용할 수 잇습니다.

> ## Create Table 과 같이 사용 

> 기본 구조 : 하나의 column 을 Primart Key 로 지정하기 

```sql
CREATE TABLE table_name(
    primary_key_column datatype PRIMARY KEY,
    ...
);
```

- 윛럼 column 에 대해서 datatype 을 PIMARY KEY 라고 지정할 수 있습니다.
- 만일 primary keey 가 여러개라면 table costraints 에 Primary Key 를 추가하셔야 합니다.

> 여러개의 column 을 primary key 로 지정하기 

```sql
CREATE TABLE table_name(
    primary_key_column1 datatype,
    primary_key_column2 datatype,
    ...,
    PRIMARY KEY(column_list)
);
```

- 위와 같은 syntax 에서 column list 는 컴마(,) 로 구분되여야 합니다.

> Auto_Increment  이용하기 

```sql
CREATE TABLE users(
   user_id INT AUTO_INCREMENT PRIMARY KEY,
   username VARCHAR(40),
   password VARCHAR(255),
   email VARCHAR(255)
);
```

> Table Constrant 이용하기 

```sql
CREATE TABLE roles(
   role_id INT AUTO_INCREMENT,
   role_name VARCHAR(50),
   PRIMARY KEY(role_id)
);
```

> ## Alter 이용 

```sql
CREATE TABLE pkdemos(
   id INT,
   title VARCHAR(255) NOT NULL
);
```

- 위와 같이 `pkdemos` 라는 테이블을 만들어보겠습니다.

```sql
ALTER TABLE pkdemos
ADD PRIMARY KEY(id);
```

- 위처럼 `id` 라는 column 을 Primary key 로 지정할 수 있습니다.

# [Unique](#link){: .btn .btn--primary}{: .align-center}

> ## 기본 구조

- 데이터 컬럼중에는 **중복된 데이터가 있으면 안되는** 컬럼이 있을 수 있습니다.
- 이럴때에는 Unique 라는 Constraint 를 쓰면, 데이터 무결성을 보장할 수 있습니다.

```sql
CREATE TABLE table_name(
    ...,
    column_name data_type UNIQUE,
    ...
);
```

- 위처럼 CREATE TABLE 를 만들때에, `UNIQUE` Constraint 를 넣으면 됩니다.

> 둘 이상의 unique 열?

- 둘 이상의 unique 열을 만들기 위해서는 아래처럼 설정합니다.

```sql
CREATE TABLE table_name(
   ...
   column_name1 column_definition,
   column_name2 column_definition,
   ...,
   UNIQUE(column_name1,column_name2)
);
```

> Example 

```sql
CREATE TABLE suppliers (
    supplier_id INT AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    phone VARCHAR(15) NOT NULL UNIQUE,
    address VARCHAR(255) NOT NULL,
    PRIMARY KEY (supplier_id),
    CONSTRAINT uc_name_address UNIQUE (name , address)
);
```

- 이때 위 구조는 아래와 같이 출력됩니다.

```
Field      |Type        |Null|Key|Default|Extra         |
-----------+------------+----+---+-------+--------------+
supplier_id|int         |NO  |PRI|       |auto_increment|
name       |varchar(255)|NO  |MUL|       |              |
phone      |varchar(15) |NO  |UNI|       |              |
address    |varchar(255)|NO  |   |       |              |
```

```sql
INSERT INTO suppliers(name, phone, address) 
VALUES( 'ABC Inc', '(408)-908-2476','4000 North 1st Street'), 
      ('XYZ Corporation','(408)-908-2476','3000 North 1st Street');
```

```
Error Code: 1062. Duplicate entry '(408)-908-2476' for key 'phone'
```

- 위와 같이 insert 를 하게되면 `phone` 에 같은 data 가 들어가기 때문에, insert 가 되지 않습니다. 

# [Not Null](#link){: .btn .btn--primary}{: .align-center}

> ## 기본 구조

- 데이터의 특정 컬럼에 Null 값의 입력을 허용하지 않으려면 Not Null 을 쓰면 됩니다.

# [Check](#link){: .btn .btn--primary}{: .align-center}

> ## 기본 구조

- Check 제약은 특정 컬럼에 특정 조건의 데이터만 입력되거나 수정되도록 제한을 거는 제약입니다.

```sql
CREATE TABLE parts (
    part_no VARCHAR(18) PRIMARY KEY,
    description VARCHAR(40),
    cost DECIMAL(10,2 ) NOT NULL CHECK (cost >= 0),
    price DECIMAL(10,2) NOT NULL CHECK (price >= 0)
);
```

- 위처럼 두 개의 열 `CHECK`제약 조건을 통해 cost 와 price 에 대해서 제한조건을 걸 수 있습니다.

```sql
INSERT INTO parts(part_no, description,cost,price) 
VALUES('A-001','Cooler',0,-100); 
```

- 위처럼 parts 에 값을 insert 하고 있습니다.

```
SQL Error [3819] [HY000]: Check constraint 'parts_chk_2' is violated.
```

- 하지만 price > = 0 조건을 침해하므로 insert 되지 않는것을 볼 수 있습니다! ㅜㅜ

# [Foreign key](#link){: .btn .btn--primary}{: .align-center}
