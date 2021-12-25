---
title: "insert into select"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2021-05-02

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [INSERT INTO SELECT](#link){: .btn .btn--primary}{: .align-center}

> ## INSERT INTO SELECT

- 우리는 테이블에 하나 이상의 행을 삽입하는 방법을 배웠습니다 

```
INSERT INTO table_name(c1,c2,...)
VALUES(v1,v2,..);
```

- 이때 VALUES 절에서 구구절절 데이터를 삽입할 수 있지만, Select 의 출력을 이용하여 바로 테이블을 생성할수도 있습니다.

```sql
INSERT INTO table_name(column_list)
SELECT 
   select_list 
FROM 
   another_table
WHERE
   condition;
```

- 이 `INSERT INTO SELECT`명령문은 다른 테이블의 데이터를 테이블로 복사하거나 여러 테이블의 데이터를 테이블로 요약할 때 매우 유용합니다.

> ## Example : row 로 연결하기

```sql
CREATE TABLE suppliers (
    supplierNumber INT AUTO_INCREMENT,
    supplierName VARCHAR(50) NOT NULL,
    phone VARCHAR(50),
    addressLine1 VARCHAR(50),
    addressLine2 VARCHAR(50),
    city VARCHAR(50),
    state VARCHAR(50),
    postalCode VARCHAR(50),
    country VARCHAR(50),
    customerNumber INT,
    PRIMARY KEY (supplierNumber)
);
```

- 위처럼 `suppliers` 라고 불리는 새로운 테이블을 만들어 보았습니다.
- 그 이후에, 기존에 존재하는 Customers 테이블에 대해서, 위와 같은 column 스킴을 가지는 테이블을 SELECT 해보겠습니다.

```sql
SELECT 
    customerNumber,
    customerName,
    phone,
    addressLine1,
    addressLine2,
    city,
    state,
    postalCode,
    country
FROM
    customers
WHERE
    country = 'USA' AND 
    state = 'CA';

```

```
customerNumber|customerName                |phone     |addressLine1             |addressLine2|city         |state|postalCode|country|
--------------+----------------------------+----------+-------------------------+------------+-------------+-----+----------+-------+
           124|Mini Gifts Distributors Ltd.|4155551450|5677 Strong St.          |            |San Rafael   |CA   |97562     |USA    |
           129|Mini Wheels Co.             |6505555787|5557 North Pendale Street|            |San Francisco|CA   |94217     |USA    |
           161|Technics Stores Inc.        |6505556809|9408 Furth Circle        |            |Burlingame   |CA   |94217     |USA    |
           205|Toys4GrownUps.com           |6265557265|78934 Hillside Dr.       |            |Pasadena     |CA   |90003     |USA    |
           219|Boards & Toys Co.           |3105552373|4097 Douglas Av.         |            |Glendale     |CA   |92561     |USA    |
           239|Collectable Mini Designs Co.|7605558146|361 Furth Circle         |            |San Diego    |CA   |91217     |USA    |
           321|Corporate Gift Ideas Co.    |6505551386|7734 Strong St.          |            |San Francisco|CA   |94217     |USA    |
           347|Men 'R' US Retailers, Ltd.  |2155554369|6047 Douglas Av.         |            |Los Angeles  |CA   |91003     |USA    |
           450|The Sharp Gifts Warehouse   |4085553659|3086 Ingle Ln.           |            |San Jose     |CA   |94217     |USA    |
           475|West Coast Collectables Co. |3105553722|3675 Furth Circle        |            |Burbank      |CA   |94019     |USA    |
           487|Signal Collectibles Ltd.    |4155554312|2793 Furth Circle        |            |Brisbane     |CA   |94217     |USA    |
```

- 위의 출력값을 삽입하기 위해서는 아래와 같이 INSERT INTO 를 수행하면 됩니다.

```sql
INSERT INTO suppliers (
    supplierName, 
    phone, 
    addressLine1,
    addressLine2,
    city,
    state,
    postalCode,
    country,
    customerNumber
)
SELECT 
    customerName,
    phone,
    addressLine1,
    addressLine2,
    city,
    state ,
    postalCode,
    country,
    customerNumber
FROM 
    customers
WHERE 
    country = 'USA' AND 
    state = 'CA';
```

- 11개의 행이 성공적으로 삽입되었음을 나타내는 다음 메시지를 반환했습니다.

```
11 row(s) affected Records: 11  Duplicates: 0  Warnings: 0
```

```
supplierNumber|supplierName                |phone     |addressLine1             |addressLine2|city         |state|postalCode|country|customerNumber|
--------------+----------------------------+----------+-------------------------+------------+-------------+-----+----------+-------+--------------+
             1|Mini Gifts Distributors Ltd.|4155551450|5677 Strong St.          |            |San Rafael   |CA   |97562     |USA    |           124|
             2|Mini Wheels Co.             |6505555787|5557 North Pendale Street|            |San Francisco|CA   |94217     |USA    |           129|
             3|Technics Stores Inc.        |6505556809|9408 Furth Circle        |            |Burlingame   |CA   |94217     |USA    |           161|
             4|Toys4GrownUps.com           |6265557265|78934 Hillside Dr.       |            |Pasadena     |CA   |90003     |USA    |           205|
             5|Boards & Toys Co.           |3105552373|4097 Douglas Av.         |            |Glendale     |CA   |92561     |USA    |           219|
             6|Collectable Mini Designs Co.|7605558146|361 Furth Circle         |            |San Diego    |CA   |91217     |USA    |           239|
             7|Corporate Gift Ideas Co.    |6505551386|7734 Strong St.          |            |San Francisco|CA   |94217     |USA    |           321|
             8|Men 'R' US Retailers, Ltd.  |2155554369|6047 Douglas Av.         |            |Los Angeles  |CA   |91003     |USA    |           347|
             9|The Sharp Gifts Warehouse   |4085553659|3086 Ingle Ln.           |            |San Jose     |CA   |94217     |USA    |           450|
            10|West Coast Collectables Co. |3105553722|3675 Furth Circle        |            |Burbank      |CA   |94019     |USA    |           475|
            11|Signal Collectibles Ltd.    |4155554312|2793 Furth Circle        |            |Brisbane     |CA   |94217     |USA    |           487|
```

- 위처럼 데이터가 잘 들어갔음을 알 수 있습니다.

> ## Select 를 이용해서 Column 에 삽입

```sql
CREATE TABLE stats (
    totalProduct INT,
    totalCustomer INT,
    totalOrder INT
);
```

- 위와 같이 새로운 Table 인 Stats 을 만들어봅시다. 

```sql
INSERT INTO stats(totalProduct, totalCustomer, totalOrder)
VALUES(
	(SELECT COUNT(*) FROM products),
	(SELECT COUNT(*) FROM customers),
	(SELECT COUNT(*) FROM orders)
);
```

- 위처럼 새로운 columns 에 대해서 각각 집계함수(count) 를 사용한 값을 넣어보았습니다.

```sql
SELECT * FROM stats;
```

```
totalProduct|totalCustomer|totalOrder|
------------+-------------+----------+
         110|          122|       326|
```



