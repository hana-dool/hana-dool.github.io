---
title:  "Set Default Root"
excerpt: "BD 의 기본 경로 설정하기"
categories:
  - DBeaver
last_modified_at: 2021-12-04

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [Default Route](#link){: .btn .btn--primary}{: .align-center}

> ## db Default Route 설정하기

```sql
select *
from sys.sys_config sc ; 
```

- 위와 같이 sql 문을 작성하다 보면, 앞에 db 이름을 써야합니다.
- 이때에 DB 이름을 계속 넣어준다면 상당히 귀찮아집니다. 이를 위해서는  아래처럼 Default 위치를 설정하면 계속 붙일 필요가 없어집니다.

![jpg](/assets/images/Program/34_1.jpg)

```sql
select *
from sys_config sc  
```

```
variable                            |value|set_time           |set_by|
------------------------------------+-----+-------------------+------+
diagnostics.allow_i_s_tables        |OFF  |2021-12-04 13:25:51|      |
diagnostics.include_raw             |OFF  |2021-12-04 13:25:51|      |
...
```



---

**reference**

- <https://www.sqltutorial.org/sql-distinct/>



