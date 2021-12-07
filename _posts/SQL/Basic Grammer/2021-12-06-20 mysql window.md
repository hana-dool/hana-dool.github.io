---
title:  "Window Functions"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2021-12-06

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [MYSQL](#link){: .btn .btn--primary}{: .align-center}

```mysql
CREATE TABLE sales(
    sales_employee VARCHAR(50) NOT NULL,
    fiscal_year INT NOT NULL,
    sale DECIMAL(14,2) NOT NULL,
    PRIMARY KEY(sales_employee,fiscal_year)
);

INSERT INTO sales(sales_employee,fiscal_year,sale)
VALUES('Bob',2016,100),
      ('Bob',2017,150),
      ('Bob',2018,200),
      ('Alice',2016,150),
      ('Alice',2017,100),
      ('Alice',2018,200),
       ('John',2016,200),
      ('John',2017,150),
      ('John',2018,250);

SELECT * FROM sales;
```

- 우선 위와 같이 테이블을 만들어봅시다.

> Note : Aggregate function 이란?

- Aggregate function 은 데이터를 single results 로 요약하게 됩니다. 

```sql
SELECT 
    SUM(sale)
FROM
    sales;
```

```
SUM(sale)|
---------+
  1500.00|
```

- 위처럼 하나의 결과로 요약할 수 있습니다. 

> ## 기본 구조

- 우선 over 의 생김새는 아래와 같습니다.

```
window_function_name(expression) OVER ( 
   [partition_defintion]
   [order_definition]
   [frame_definition]
)
```

- 위에서 `over` 는 () 가 붙어있어야 합니다!

```
window_function_name(expression) OVER()
```

> ## Partition 함수

- The `partition_clause` 는 row 들을 덩어리 또는 partition 으로 분할하게 됩니다. 

```
PARTITION BY <expression>[{,<expression>...}]
```

- 위와 같은 맥락으로 분할되고는 합니다. 

> ## order by 함수

```
ORDER BY <expression> [ASC|DESC], [{,<expression>...}]
```



- breaks up the rows into chunks or partitions. Two partitions are separated by a partition boundary.
