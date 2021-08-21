---
title:  "Operation"
excerpt: "+,-,%,= ..."
categories:
  - SQL_Basic_Grammer
tags:
  - 1
last_modified_at: 2021-07-13

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true 
---

# + - * / 

- 기본 연산자입니다.
- Select , WHERE 절 등에서 이용 가능합니다.

```sql
SELECT price * num 
from df ;
```

```sql
select *
from df 
where price / num <= 300 ; 
```

<br>

# %(mod) round

- % 는 나머지를 출력하는 역할을 합니다.
- oracle 에서는 이 연산자가 mod 로 대체됩니다. (오라클은 진짜 왜이러냐..)

```sql
select id % 3 -- mod(id,3)
from df 
```

<bR>

# > < = != 

- 비교 연산자는 주로, Where 절 , CAse when 등 조건이 들어가는 곳에서 사용됩니다.
- 그 이유는 '비교 연산자' 는 True / False 를 나타내가 떄문입니다.

```sql
-- 비교 연산자는 > , >= , < , <= , = , != 이 있다.
SELECT *
FROM df
WHERE id = 40 
-- df 라는 테이블에서, id 가 40 인 데이터를 뽑아내라.
```

- 위와 같이 WHERE 뒤에 비교연산자를 넣어서, 조건을 추가할 수 있습니다.

<BR>

## and or not

- 논리 연산자는 여러 조건을 논리적으로 연결할떄에 사용합니다.

  | 연산자 | 의미               |
  | ------ | ------------------ |
  | AND    | T and T 일때만 T   |
  | OR     | 하나만 True 이면 T |
  | NOT    | 반대결과           |

```sql
SELECT * 
FROM df
WHERE salary > 3000 
AND job = '목수'
-- 봉급이 3000 이상인 목수 데이터를 출력하라는 의미
```



```sql
SELECT *
FROM df
WHERE salary > 3000
AND (job = '목수' OR job = '농부') ; 
-- 봉급이 3000 이상인 목수 또는 농부
```

<br>

**진리 연산표**

| [[AND]]   | TRUE  | FASLE | NULL  |
| --------- | ----- | ----- | ----- |
| **TRUE**  | TRUE  | FALSE | NULL  |
| **FALSE** | FALSE | FASLE | FALSE |
| **NULL**  | NULL  | FASLE | NULL  |

<br>

| [[OR]]    | TRUE | FASLE | NULL |
| --------- | ---- | ----- | ---- |
| **TRUE**  | TRUE | TRUE  | TRUE |
| **FALSE** | TRUE | FASLE | NULL |
| **NULL**  | TRUE | NULL  | NULL |

<br>

| NOT      | TRUE  | TRUE | NULL |
| -------- | ----- | ---- | ---- |
| **TRUE** | FALSE | TRUE | NULL |



## NOT

| 연산자              | 의미                       |
| ------------------- | -------------------------- |
| NOT 열이름 =        | ~ 가 아니다.               |
| NOT 열이름 >        | ~보다 크지않다.            |
| NOT BETWEEN a AND b | a,b 사이에 값이 없다.      |
| NOT IN (list)       | list 값과 일치하지 않는다. |
| IS NOT NULL         | NULL 값을 가지지 않는다.   |

```sql
SELECT *
FROM df
WHERE salary IS NOT NULL
-- 봉급이 NULL 값이 아닌 데이터 출력
```

```sql
SELECT *
FROM df
WHERE salary NOT BETWEEN 10 AND 100 ; 
-- 봉급이 10~100 이 아닌 데이터출력
```



```sql
SELECT *
FROM df
WHERE date BETWEEN '1981/01/01' AND '1999/09/09'
```



```sql
SELECT *
FROM df
WHERE job not in ('목수','광부','데이터엔지니어')
-- 위의 세 값이 아닌 직업을 뽑아낸다. 
```

<br>
