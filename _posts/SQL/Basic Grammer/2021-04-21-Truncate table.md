---
title:  "Truncate Table"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2022-02-13

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true 
---

# [Truncate table](#link){: .btn .btn--primary}{: .align-center}

> ## Definition 

- The MySQL `TRUNCATE TABLE` statement 는 테이블의 데이터를 모두 삭제해줍니다.
- 논리적으로는 ,  `TRUNCATE TABLE` 쿼리는 table 의 모든 row 를 `DETETE` 하는것과 같습니다.
- 하지만 `TRUNCATE TABLE` 의 경우에는 모든 row 를 다 삭제해버리고 다시 원본 테이블을 생성한다는 점에서 `DETETE` 보다 훨씬 효율적입니다.

```sql
TRUNCATE [TABLE] table_name;
```

- 일반적으로 위와 같은 형태를 따르게 됩니다.
  - 위 쿼리의 의미는 "table_name" 이라는 이름을 가지는 테이블을 모두 삭제하고 다시 생성한다는 의미입니다. 
  - `TABLE` 은 붙여도 되고, 안붙여도 됩니다, 즉 위 문법에서 `[TABLE]` keyword 는 옵션입니다. 
    - 하지만 TRUNCATE 함수와 구분짓기 위해서 쓰는것을 권장합니다.
- If there is any `FOREIGN KEY` constraints from other tables which reference the table that you truncate, the `TRUNCATE TABLE` statement will fail.
- Because a truncate operation causes an implicit commit, therefore, it cannot be rolled back.
- The `TRUNCATE TABLE` statement [resets value in the AUTO_INCREMENT column ](https://www.mysqltutorial.org/mysql-reset-auto-increment)to its start value if the table has an `AUTO_INCREMENT` column.
- The `TRUNCATE TABLE` statement does not fire `DELETE` triggers associated with the table that is being truncated.
- Unlike a `DELETE` statement, the number of rows affected by the `TRUNCATE TABLE` statement is 0, which should be interpreted as no information.

> ## Example 

```sql
TRUNCATE TABLE TEST; 
```

> ## Reference

- https://www.mysqltutorial.org/mysql-math-functions/mysql-truncate/



