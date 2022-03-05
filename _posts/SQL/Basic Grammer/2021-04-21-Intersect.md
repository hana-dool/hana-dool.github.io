---
title: "Intersect"
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

NOTE : MYSQL 에서는 INTERSECT 를 지원하지 않습니다. 여기에서는 intersect 를 어떻게 구현할 수 있을지 예시들을 알아보도록 하겠습니다.
{: .notice--warning}

# [Intersect](#link){: .btn .btn--primary}{: .align-center}

> ## 기본 구조

- intersect 는 두개의 results set 에 대해서 결과를 합치는 쿼리입니다.
- 이때 "겹치는" 결과에 대해서만 그 결과를 합치게 됩니다.

```sql
(SELECT column_list 
FROM table_1)
INTERSECT
(SELECT column_list
FROM table_2);
```

![jpg](/assets/images/Program/68_1.jpg)

> 사용법

- intersect operator 를 사용하려면 다응과 같은 규칙을 지켜야합니다.
  - order and the number of columns 이 일치해야합니다.
  - 각각 columns 의 데이터타입은 compatible 해야 합니다.

> ## Dataset 만들기

```sql
CREATE TABLE t1 (
    id INT PRIMARY KEY
);
CREATE TABLE t2 LIKE t1;
INSERT INTO t1(id) VALUES(1),(2),(3);
INSERT INTO t2(id) VALUES(2),(3),(4);
```

> ## Distinct , Inner join 사용하기

- The following statement uses [`DISTINCT`](https://www.mysqltutorial.org/mysql-distinct.aspx) operator and `INNER JOIN` clause to return the distinct rows in both tables:

```sql
SELECT DISTINCT 
   id 
FROM t1
   INNER JOIN t2 USING(id);
```

> ##  `IN` , subquery 사용하기

````sql
SELECT DISTINCT id
FROM t1
WHERE id IN (SELECT id FROM t2);
````

