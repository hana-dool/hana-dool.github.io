---
title: "Create Table As"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2021-05-02

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

# [Create Table as](#link){: .btn .btn--primary}{: .align-center}

> ## INSERT INTO SELECT

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
  - 지정된 경우 테이블이 이미 존재하는 경우 CREATE TABLE AS 문은 오류를 발생시키지 않습니다.
- AS (Optional)
  - AS 를 쓰는것, 안쓰는것은 출력에 대해서 크게 상관이 없음

> ## Example

```sql
CREATE TABLE temp_table AS
SELECT *
FROM customers 
WHERE customerNumber <= 130 ;
```

- 위와 같이 실행하게 되면, 우리가 원하는 테이블을 Select 문법을 이용해 만들게 됩니다.
  - 이제 우리는 temp_table 이라는 테이블이 데이터베이스에 적재되게 됩니다.

```sql
SELECT *
FROM temp_table ; 
```

```
customerNumber|customerName                |contactLastName|contactFirstName|phone            |addressLine1                |addressLine2|city         |state   |postalCode|country  |salesRepEmployeeNumber|creditLimit|
--------------+----------------------------+---------------+----------------+-----------------+----------------------------+------------+-------------+--------+----------+---------+----------------------+-----------+
           103|Atelier graphique           |Schmitt        |Carine          |40.32.2555       |54, rue Royale              |            |Nantes       |        |44000     |France   |                  1370|   21000.00|
           112|Signal Gift Stores          |King           |Jean            |7025551838       |8489 Strong St.             |            |Las Vegas    |NV      |83030     |USA      |                  1166|   71800.00|
           114|Australian Collectors, Co.  |Ferguson       |Peter           |03 9520 4555     |636 St Kilda Road           |Level 3     |Melbourne    |Victoria|3004      |Australia|                  1611|  117300.00|
           119|La Rochelle Gifts           |Labrune        |Janine          |40.67.8555       |67, rue des Cinquante Otages|            |Nantes       |        |44000     |France   |                  1370|  118200.00|
           121|Baane Mini Imports          |Bergulfsen     |Jonas           |07-98 9555       |Erling Skakkes gate 78      |            |Stavern      |        |4110      |Norway   |                  1504|   81700.00|
           124|Mini Gifts Distributors Ltd.|Nelson         |Susan           |4155551450       |5677 Strong St.             |            |San Rafael   |CA      |97562     |USA      |                  1165|  210500.00|
           125|Havel & Zbyszek Co          |Piestrzeniewicz|Zbyszek         |(26) 642-7555    |ul. Filtrowa 68             |            |Warszawa     |        |01-012    |Poland   |                      |       0.00|
           128|Blauer See Auto, Co.        |Keitel         |Roland          |+49 69 66 90 2555|Lyonerstr. 34               |            |Frankfurt    |        |60528     |Germany  |                  1504|   59700.00|
           129|Mini Wheels Co.             |Murphy         |Julie           |6505555787       |5557 North Pendale Street   |            |San Francisco|CA      |94217     |USA      |                  1165|   64600.00|
```

