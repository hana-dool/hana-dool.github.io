---
title:  "Kit_1"
excerpt: "여러 예제"
categories:
  - SQL_Kit
tags:
  - 1
last_modified_at: 2021-05-17

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# <center><font size="6">Quantile</font></center>

- Quantile 을 표현해주는 함수는 Ntile (Number of Quantile) 입니다. 

```sql
SELECT NTILE(4) OVER (col BY SAL ASC NULLS LAST)
FROM EMP ; 
```

- 위 함수의 경우 Quantile 을 4개로 쪼개서 나타내게 됩니다.
- 이 경우 null 를 높게 취급하느냐 낮게 취급하느냐에 따라 달라질 수 있으므로 주의하셔야 합니다.
  - NULL LAST : NULL 을 마지막으로 몰아 넣음
  - NULL FIRST : NULL 을 처음으로 몰아 넣음

<BR>

<BR>

# <center><font size="6">CUME _DIST</font></center>

- CUME_DIST 함수를 쓰게 되면, 전체 데이터에서 특정 비율을 알 수 있게 됩니다.
- 
