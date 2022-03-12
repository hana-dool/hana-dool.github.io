---
title: "Show Tables"
excerpt: ""
categories:
  - SQL_Basic_Grammer
tags:
  - 1
last_modified_at: 2021-05-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true 
typora-root-url: ../../../../hana-dool.github.io
---

# [Show Tables](#link){: .btn .btn--primary}{: .align-center}

> ## 기본 구조

- 데이터베이스에 어떤 쿼리들이 있는지 검색하는 쿼리입니다.

```sql
show tables ; 
```

```
Tables_in_users|
---------------+
dept           |
emp            |
sales          |
t              |
temp           |
temp_table     |
view_table     |
```

> ## Show Full Tables

- 위와 같은 show tables 만 이용하게 된다면, 테이블이 뷰인지 아닌지 잘 알수가 없습니다. 
- 결과에 테이블 유형까지 포함하기 위해서라면 다음처럼 `Show Tables`  명령문을 사용합니다.

```sql
SHOW FULL TABLES;
```

```
Tables_in_users|Table_type|
---------------+----------+
dept           |BASE TABLE|
emp            |BASE TABLE|
sales          |BASE TABLE|
t              |BASE TABLE|
temp           |BASE TABLE|
temp_table     |BASE TABLE|
view_table     |VIEW      |
```

# [Example : 기능별 예제](#link){: .btn .btn--primary}{: .align-center}

> ## 테이블 이름 조건으로 검색 (LIKE)

- 테이블이 많을떄에는 아래처럼 조건을 이용해서 검색할수도 있습니다.

```sql
SHOW tables LIKE 'temp%' ;
```

```
Tables_in_users (temp%)|
-----------------------+
temp                   |
temp_table             |
```

> ## 뷰 테이블만 찾기 (WHERE)

```sql
SHOW FULL TABLES WHERE table_type = 'VIEW' ;
```

```
Tables_in_users|Table_type|
---------------+----------+
view_table     |VIEW      |
```

