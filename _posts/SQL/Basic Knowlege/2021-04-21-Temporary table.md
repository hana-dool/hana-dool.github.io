---
title:  "Derived tables"
excerpt: ""
categories:
  - SQL_Basic_Knowledge
last_modified_at: 2021-12-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [derived table](#link){: .btn .btn--primary}{: .align-center}

- https://www.mysqltutorial.org/mysql-temporary-table/

> ## 기본 구조

- derived table 이란 select statement 로 생성된 가상 테이블입니다. 
- 이때 derived table 은 temporary table 과 비슷합니다. 
  - 하지만 temporary table 은 임시 테이블 생성을 강제하지만 derived table 은 그렇지 않아서 훨씬 간단합니다.


![jpg](/assets/images/Program/64_1.jpg)

> Subquery 와 Derived Table?

- 이때 subquery 와 derived table 은 위처럼 서로 바꾸어서 쓰일 수 있습니다. 

> derived table and Alias

- Derived Table 은 무조건 Alias 를 가져야합니다.

```sql
SELECT 
    select_list
FROM
    (SELECT 
        select_list
    FROM
        table_1) derived_table_name
WHERE 
    derived_table_name.c1 > 0;
```

