---
title: "Join &#58; Full Outer"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2021-12-06

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

# [Full outer join](#link){: .btn .btn--primary}{: .align-center}

- Note : MYsql 에는 구현되어있지 않기 때문에 LEFT JOIN 과 RIGHT JOIN 등을 적절히 이용하여서 구현되었습니다.

> ## 기본 구조

```sql
SELECT * FROM t1
LEFT JOIN t2 ON t1.id = t2.id
UNION
SELECT * FROM t1
RIGHT JOIN t2 ON t1.id = t2.id
```

- 이때 위 쿼리를 수행하게 되면 Ful outer join 을 수행하게 됩니다. 즉 

![jpg](/assets/images/Program/70_1.jpg)

- 위와 같은 로직입니다. 

> Note

- 하지만 위와 같이 수행하게 되면 한가지 단점이 있습니다.
- 그것은 바로 "겹치는 row" 는 자동으로 drop 한다는 것인데요, 이는 UNION 의 특성 떄문입니다. 

```sql
SELECT * FROM t1
LEFT JOIN t2 ON t1.id = t2.id
UNION ALL
SELECT * FROM t1
RIGHT JOIN t2 ON t1.id = t2.id
WHERE t1.id IS NULL
```

- 이전과 같은 상황이 일어나지 않게 하려면 위처럼 UNION ALL 을 사용하여서 비록 'ROW' 가 겹친다 하더라도, 합쳐버리면 됩니다. 

> ## Example

