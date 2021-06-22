---
title:  "Control Flow"
excerpt: "흐름 제어문의 구현"
categories:
  - SQL_Basic_Grammer
tags:
  - 1
last_modified_at: 2021-05-29

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# <center><font size="15">IF , Else</font></center> 

- SQL 에서는 if 문을 구현하기 위해서 DECODE 를 사용합니다.

```sql
SELECT DECODE(col1,'홍길동',10,
             	   '임꺽정',100,
             		30)
FROM df             		
```

- 위 의미는 col1 의 값이 '홍길동' 이면 10을 출력하고, '임꺽정' 이면 100을 출력하며 , 둘다 아니면 30을 출력하라는것입니다.
- 즉 if , else 를 구현한 것입니다. 

```sql
SELECT DECODE(MOD(col,2),
			 0,'짝수'
			,1,'홀수') 
FROM df
```

- 홀 / 짝을 구분하는 쿼리
- 하지만 이 경우, DECODE 는 (=) 비교만 가능하다는것을 주목합시다.

<br>

# <center><font size="15">Case When</font></center> 

- 위와 같이 = 비교만 가능하다는 단점을 해결하기 위해서 이런 경우 CASE, WHEN 을 사용하게 됩니다.

```sql
SELECT SAL , CASE WHEN sal >= 3000 THEN '부자'
					WHEN sal >= 1000 THEN '중산층'
					ELSE '가난' END AS 계층
FROM emp ; 
```

- count 와 쓰여서, 조건에 맞는 데이터만 세게 할 수 있습니다. 

```sql
SELECT sum(CASE WHEN deptno = 10 THEN 1 ELSE 0 end)
FROM emp ;
```

