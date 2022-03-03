---
title:  "Dense_Rank"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2022-03-03

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true

---

# [Dense_Rank](#link){: .btn .btn--primary}{: .align-center}

> ## Definition 

- The `RANK()` function 은 각 partition set 내에서 row 마다 랭크를 매겨주는 함수입니다. 

```sql
DENSE_RANK() OVER (
    PARTITION BY <expression>[{,<expression>...}]
    ORDER BY <expression> [ASC|DESC], [{,<expression>...}]
)
```

- 원래 Rank 는 값이 같은 row 가 있다면, 그 둘은 같은 랭킹을 지니고, 그 뒤 row 에 대해서는 rank 를 겹친 row 수만큼 증가시킵니다. 
- 하지만 Dense rank 는 얼마나 값이 겹치든 1씩 Ranking 을 증가시킵니다.

| ENAME |   JOB   | SAL  | RANK | DENSE_RANK |
| :---: | :-----: | :--: | :--: | :--------: |
| FORD  | ANALYST | 3000 |  1   |     1      |
| SCOTT | ANALYST | 3000 |  1   |     1      |
| JONES | MANAGER | 2975 |  3   |     2      |
| BLAKE | MANAGER | 2850 |  4   |     3      |
| CLARK | MANAGER | 2450 |  5   |     4      |

> parameters

- `PARTITION BY` : Results Set 을 어떤 기준으로 partition 할지 결정한다. 
  - Ranking 은 위의 partition by 로 나뉜 그룹 기준으로 매기게 됩니다.
- `ORDER BY` : sorting 되는 기준을 정합니다.

> ## Example 

```sql
SELECT
	ename,
	job,
	sal,
	RANK() over (
		ORDER BY Sal DESC) AS rank_,
	DENSE_RANK() over (
		ORDER BY Sal DESC) AS dense_rank_
FROM
	emp
WHERE
	job in ('ANALYST', 'MANAGER') ; 
```

```
ename|job    |sal    |rank_|dense_rank_|
-----+-------+-------+-----+-----------+
SCOTT|ANALYST|3000.00|    1|          1|
FORD |ANALYST|3000.00|    1|          1|
JONES|MANAGER|2975.00|    3|          2|
BLAKE|MANAGER|2850.00|    4|          3|
CLARK|MANAGER|2450.00|    5|          4|
```

