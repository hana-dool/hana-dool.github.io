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

# [Primary key Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## 효율적인 테이블 구조

- 외래키를 활용하는 방법에 대해서 알아보기 전에, 왜 외래키가 필요한지에 대해서 알아보도록 합시다. 
- 우리가 온라인 식료품 마트를 운영하고 있다고 가정해봅시다. 온라인 식료품 마트는 사용자로부터 주문을 받아서 배송해주는 시스템을 운영하고 있습니다. 
- 우리는 데이터베이스를 다룰 줄 알기 때문에, 사용자의 주문 내역을 스프레드시트가 아닌 데이터베이스에 테이블을 만들어서 저장, 관리, 분석할 것 입니다.
- 먼저, **사용자에 대한 정보**를 저장하기 위해 테이블에 기본적으로 아래와 같은 열이 필요할 것입니다.

```
아이디 (user_id), 비밀번호 (user_pwd), 이름 (name), 성별 (gender), 배송 주소 (address)
```

- 온라인 마켓이다보니 위의 정보만으로는 주문 정보를 저장할 수 없으므로, 아래와 같은 **주문과 관련된 정보**들이 추가로 필요합니다.

```
주문 일자 (order_date), 제품 ID (product_id), 제품명 (product_title), 수량 (qty)
```

- 위의 모든 열을 합쳐서 테이블을 만든다면 아래와 같은 테이블이 만들어 집니다. 
- 2개의 예시 데이터를 넣어두었습니다. 
  - 예를 들어, marco117 아이디를 사용하는 사용자는 10월 1일 coke를 5개 주문했고, 
  - blondy121 아이디를 사용하는 사용자는 같은 날인 10월 1일에 sprite를 10개 주문했습니다.

![png](/assets/images/Program/78_1.jpg)

- 위의 테이블 구조는 당장에는 큰 문제가 없어보입니다. 
- 하지만, **사실 아주 큰 비효율을 발생시키는 테이블 구조입니다**. 왜냐하면, 주문을 추가할때마다 데이터가 계속 중복해서 쌓이기 때문입니다. 
- 예를 들어, Marco가 몇일 동안 여러개의 제품을 주문했다고 가정합시다. 주문 테이블은 아래와 같이 계속해서 빨간색으로 표시한 중복 데이터가 발생할 것입니다.

![png](/assets/images/Program/78_2.jpg)

- Marco는 이틀에 걸쳐 네번의 주문을 넣었습니다. 이 네번의 주문은 주문입장에서는 모두 달라져서 우측에 파란색으로 표시된 데이터는 새롭게 추가되는 것이 당연합니다. 
- 하지만, 사용자 Marco 와 관련된 정보들 즉, 아이디, 비밀번호, 이름, 성별, 주소는 주문시 변경되는 데이터가 아닙니다. 이렇게 주문에 따라 매번 새롭게 발생하는 주문 정보와 주문을 해도 변경되지 않는 사용자 정보가 하나의 테이블에 들어있으면, 엄청난 양의 데이터 중복이 발생하는 문제가 생깁니다.
- 중복 데이터가 많다는 것은 하나의 데이터를 찾는데 더 많은 시간이 들며 데이터를 저장하기 위한 공간도 훨씬 많이 필요하다는 의미입니다. 
- 어떻게 이 문제를 해결할 수 있을까요? **바로 아래와 같이 주문과 사용자 정보를 나누어서 다른 테이블로 관리하면 됩니다.** 

> **사용자 테이블**

- 사용자 테이블은 사용자에 해당하는 정보만 가지고 있으면 됩니다. 위에서 4개의 행으로 존재했던 데이터들은 모두 중복되기 때문에 아래와 같이 하나의 행으로 데이터를 저장하면 됩니다.

![png](/assets/images/Program/78_3.jpg)

> 주문 테이블 

- 주문 테이블은 주문을 관리하는 테이블로 주문과 관련된 정보만 가지고 있으면 됩니다. 
- 위에서 파란색에 해당하는 정보들만 가지고 있으면 됩니다. 하지만, 이렇게만 테이블을 만들면 큰 문제가 발생합니다. 주문 정보는 추가되는데, 누가 주문을 했는지 알 수 있는 방법이 없다는 것입니다.

![png](/assets/images/Program/78_4.jpg)

- 이 문제를 해결하기 위해서 **orders 테이블에 주문한 사용자를 사용자 테이블에서 찾을 수 있는 정보를 추가하면 됩니다.**
- 이때 사용하는 정보가 바로 사용자 테이블의 기본 키 (Primary Key) 입니다. 기본키는 해당 테이블에서 고유한 값을 가지는 열의 조합입니다. 다시 말해, 사용자 테이블의 기본키 정보만 주문 테이블이 가지고 있으면 사용자 테이블에서 한명의 사용자를 찾을 수 있다는 것 입니다. 
- 위의 사용자 테이블은 사용자 아이디가 기본키 입니다. **그러므로, 아래와 같이 주문 테이블 마지막에 사용자 테이블의 기본키를 추가하면, 중복된 데이터가 없으면서도 문제 없이 데이터를 저장, 관리할 수 있게 됩니다.**

![png](/assets/images/Program/78_5.jpg)

- 주문 테이블에서 사용자 아이디 정보를 활용해 사용자 테이블의 정보를 찾을 수 있게 되었습니다. 
- 바로, 주문 테이블에 존재하는 **사용자 아이디 정보 (기본키) 를 우리는 외래키 (Foriegn Key)라고 부릅니다.**

> ## 왜래키의 역할

- 앞서 살펴본바와 같이, 외래키는 두개의 테이블을 연결해주는 연결 다리 역할을 합니다. 기본키가 중복된 데이터가 하나의 테이블에 삽입되는 것을 방지하는 역할을 했던 것을 기억하실 것 입니다. 외래키 역시 비슷하게 문제를 방지하는 역할을 수행합니다. 외래키는 새롭게 추가되는 행에서 외래키에 해당하는 값이 외래키가 참조하는 테이블에 존재하는지를 체크합니다.
- 예를 들어, 위의 주문 테이블에 새로운 데이터를 넣고자 할때 외래키에 해당하는 사용자 아이디가 아직 가입하지 않은 사용자 아이디 정보면 DBMS 는 에러를 발생시켜서 해당 데이터 삽입을 막습니다. 이 기능은 테이블 내에 저장되어있는 데이터가 항상 참조하는 값이 있다는 것을 보장해주는 역할을 합니다.

![png](/assets/images/Program/78_6.jpg)

# [Primary key in mysql](#link){: .btn .btn--primary}{: .align-center}

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

> ## 1. Create Table 과 같이 사용 

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

> ## 2. Alter 이용 

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

