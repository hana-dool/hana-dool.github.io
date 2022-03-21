---
title:  "Table Information"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2022-02-13

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true 
typora-root-url: ../../../../hana-dool.github.io
---

# [Truncate table](#link){: .btn .btn--primary}{: .align-center}

> ## 테이블 정보 출력 

```sql
SELECT *
FROM INFORMATION_SCHEMA.COLUMNS
WHERE table_name = 'YourTable'
```

- 위와 같은 쿼리를 수행하면 테이블에 대한 다양한 정보를 담은 쿼리를 출력합니다 .

> Example 

```sql
SELECT * 
FROM INFORMATION_SCHEMA.COLUMNS
WHERE table_name = 'emp' ; 
```

```
TABLE_CATALOG|TABLE_SCHEMA|TABLE_NAME|COLUMN_NAME|ORDINAL_POSITION|........
-------------+------------+----------+-----------+----------------+........
def          |users       |emp       |comm       |               7|........
def          |users       |emp       |deptno     |               8|........
def          |users       |emp       |empno      |               1|........
def          |users       |emp       |ename      |               2|........
def          |users       |emp       |hiredate   |               5|........
```

> Example 

```sql
SELECT COLUMN_NAME , DATA_TYPE 
FROM INFORMATION_SCHEMA.COLUMNS
WHERE table_name = 'emp' ; 
```

```
COLUMN_NAME|DATA_TYPE|
-----------+---------+
comm       |decimal  |
deptno     |int      |
empno      |int      |
ename      |varchar  |
hiredate   |date     |
job        |varchar  |
mgr        |smallint |
sal        |decimal  |
```

- https://www.mysqltutorial.org/mysql-math-functions/mysql-truncate/



