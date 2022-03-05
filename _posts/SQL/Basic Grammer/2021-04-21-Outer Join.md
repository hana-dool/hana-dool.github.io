---
title:  "Outer Join"
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

# [Outer Join](#link){: .btn .btn--primary}{: .align-center}

> ## Outer join 

- Outer join 은 두 테이블을 합치되, 아무것도 버리지 않는것입니다.

![jpg](/assets/images/Program/60_1.jpg)

- 위처럼 Outer join 을 하기 위한 테이블이 존재한다고 합시다. 위에서 도다시피 requied output 부분이 아무것도 버리지  않는 outer join 이 되겟습니다.

> ## Code

- mysql 의 경우에는 구현되어있지 않아서, Union 을 사용해야 합니다.

```sql
SELECT * FROM t1
LEFT JOIN t2 ON t1.id = t2.id
UNION
SELECT * FROM t1
RIGHT JOIN t2 ON t1.id = t2.id
```

- 위처럼 UNION 을 사용하도록 합시다.

> ## Reference

- https://stackoverflow.com/questions/4796872/how-can-i-do-a-full-outer-join-in-mysql



