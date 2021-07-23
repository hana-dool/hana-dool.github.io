---
title:  "Distribution"
excerpt: "분포 확인하기"
categories:
  - SQL_Query_Book
tags:
  - 1
last_modified_at: 2021-07-23

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

- SQL 에서 바로 분포를 확인하기 위한 쿼리를 작성해 보았습니다.

# [Conti] Round 를 이용한 확인

```sql
SELECT bucket,
	   count(*) AS cnt,
	   RPAD(' ', LN(COUNT(*)), '*') AS bar
FROM (
	SELECT ROUND(cases, -2)    AS bucket
	FROM covid 
	 )
GROUP BY bucket 
ORDER BY bucket;
```

![png](/assets/images/SQL/11_1.png)

- 위와 같이 Round 를 활용하여, Continuous 한 값을 Binning 을 통해 Discrete 한 값으로 바꾼 후에, 히스토그램을 그릴 수 있습니다. 

<br>

# [conti] Equal width bining 

```sql
WITH bins AS(
   SELECT min(cases) AS min_value
        , ((max(cases)-min(cases)) / 1000) + 0.0000001 AS bin_width
   FROM covid
)
SELECT bin,
	   count(*) AS cnt    
FROM (
	SELECT covid.cases,
	   floor((cases-bins.min_value) / bins.bin_width ) AS bin
	FROM covid, bins
 	 )
GROUP BY bin 
ORDER BY bin ; 
```

![png](/assets/images/SQL/11_2.png)

- 위와 같이, 히스토그램을 이용하여 Binnning 을 시도할 수 있습니다. 
- width 는 max-mid /1000 이고 , bin 은 총 1000개가 형성됩니다. 

