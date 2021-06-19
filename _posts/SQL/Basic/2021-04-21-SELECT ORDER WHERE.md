---
title:  "SELECT, OEDER, WHERE"
excerpt: "SQL 의 첫 기초"
categories:
  - SQL_Basic
tags:
  - 1
last_modified_at: 2021-05-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true 
---

# <center><font size="15">Select</font></center>

SQL 문법에서 SELECT 는 데이터 조회의 기본이 됩니다. SELECT 문을 이용하면 데이터베이스에 있는 데이터를 조회할 수 있습니다. 테이블에서 행을 선택하고, 열을 선택하는 등, 많은 행동을 할 수 있습니다. 

<br>

**데이터 모두 불러오기**

```sql
SELECT * 
FROM df ; 
```

- 이는 df 라는 테이블에서, 모든 columns 를 가져오라는 구문입니다. 

<br>

**특정 column 만 선택해서 출력**

```sql
SELECT col1, col2 
FROM df ;
```

- 위와 같은 구문은, df 라는 데이터에서, column col1, col2 를 가져오라는 구문입니다. 

<br>

**특정 column 을 추가로 더 출력**

```sql
SELECT df.* , col1 
FROM df;
```

| col1 | col2 | .... | col1 |
| ---- | ---- | ---- | ---- |
| 1    | 가   |      | 1    |
| 2    | 나   |      | 2    |
| 3    | 다   |      | 3    |

- 위와 같이 모든열을 다 출력한 이후 맨 뒤에 col1 을 다시 출력하였습니다.

<br>

**별칭 사용**

```sql
-- SELECT 열이름 AS 별칭(별칭은 변경하려는 이름)
SELECT col1 as 나이, COL2 as 연봉 
FROM df ;
```

| 나이 | 연봉 |
| ---- | ---- |
| 28   | 3000 |
| 29   | 3200 |
| 30   | 3100 |

- 별칭은 열 이름을 임시로 변경하는데에 사용된다. 원래의 열 이름이 영구적으로 변경되는것은 아닙니다.
- 이떄에 AS 는 생략될 수 있습니다. 
- 별칭에 공백, 특수문자, 대소문자 등을 사용하려면 "A B" 처럼 큰따움표로 묶어야합니다.

수식에 컬럼을 사용하면 ORDER BY 절을 사용할때에 매우 유용합니다.

```sql
SELECT salary / 1200 as 달러월급
FROM df 
ORDER BY 달러월급 
```

- 위와 같이 SELECT 에서 정의한 명칭을 그대로 사용할 수 있기 떄문입니다. 

<BR>

**중복된 출력 값 제거하기**

```sql
SELECT DISTINCT col1
FROM df ;
```

- 위 의미는 df 에서 col1 열을 출력하되, 중복값을 제거하여 종류별로 하나만 출력하는 명령어입니다. 
- DISTINCT 대신에 UNIQUE 를 사용할 수 있습니다.

<br>

**데이터 값 연결하기**

```sql
SELECT col1 , col2 || col3
FROM df ; 
```

- 위 의미는 아래 표처럼 col2 와 col3 을 붙여서 출력한다는것입니다. 

| col1 | col2\|\|col3 |
| ---- | ------------ |
| 100  | 돌쇠29세     |
| 102  | 말숙33세     |
| 103  | 인범24세     |

- 이를 문자열과 연결해서 출력하면, 의미를 크게할 수 있습니다.

```sql
SELECT name || '의 직업은' || job as 직업정보
FROM df
```



| 직업정보                      |
| ----------------------------- |
| 돌쇠의 직업은 백수            |
| 장쇠의 직업은 데이터 엔지니어 |
| 말숙이의 직업은 광부          |

<br>

**산술 처리**

```sql
-- 산수 연산자에는 + = / * () 등을 사용 가능하다.
SELECT col1, col1+300, 
FROM df ;
```

- FROM 절을 제외한 보든 절에서 산술 연산자를 사용할 수 있다.
- 수학의 일반적인 계산순서와 마찬가지로, 우선순위는 (), *,/,+,- 순이다.

<br>

<BR>

# <center><font size="15">Order By</font></center>

**정렬하기**

```sql
SELECT col1, col2 
FROM df 
ORDER BY col1 DESC ; --- ACS 는 오름차순
```

- 위 의미는 df 를 정렬하되, col1 을 기준으로 내림차순으로 정렬하라는 의미입니다. 

- ORDER BY 는 맨 마지막에 작성됩니다. 실행 순서에도 맨 뒤입니다.

<BR>

**별칭 사용 정렬**

```sql
SELECT sal/1200 달러월급
WHERE df
ORDER BY 달러월급 ASC ;	
```

- 실행순서가 맨 뒤이므로, SELECT에서 지정한 별칭을 ORDER BY 로 사용할 수 있습니다.

<BR>

**여러개 정렬**

```sql
SELECT col1, col2
FROM df
ORDER BY col1 ASC, col2 ASC ;
```

- 위 의미는 먼저 col1 을 기준으로 정렬한 이후 col2 를 기준으로 정렬한것입니다.

| col1 | col2 |
| ---- | ---- |
| 1    | 5    |
| 3    | 1    |
| 3    | 2    |
| 3    | 3    |
| 5    | 8    |

- 위와 같이 col1 을 먼저 정렬 후, 같은 col1 의 값 안에서 col2 가 정렬됩니다.

<br>

**컬럼명 대신 숫자지정**

```sql
SELECT col1,col2
FROM df
ORDER 1 asc 2 desc ; 
```

- 위와 같이 대신 숫자를 적어서 지정할 수 있습니다.
- 1 은 col1 / 2는 col2 를 지정하고 있습니다. 

<BR>

<BR>

# <center><font size="15">Where</font></center>

**WHERE을 이용한 검색**

```sql
SELECT 열 이름
FROM 테이블 이름
WHERE 조건식 ; 
```

- 위와 같이 진행됩니다. 참조하려는 테이블로부터(FROM) 해당 조건식으로 (WHERE) 열을 선택(SELECT) 하여 조회합니다.
- WHERE 절에는 연산자를 같이 쓸 수 있습니다. 
- 연산자의 종류는 아래와 같습니다. 

| 연산자 종류 | 의미             | 예시           |
| ----------- | ---------------- | -------------- |
| 비교 연산자 | 조건을 비교      | =, < , >       |
| SQL 연산자  | 조건 비교를 확장 | BETWEEN, IN 등 |
| 논리 연산자 | 조건 논리 연결   | AND, OR        |

- 연산자의 우선순위는 괄호 > 부정 > 비교 > SQL 연산 수능로 처리됩니다.

<bR>

## 비교 연산자

```sql
-- 비교 연산자는 > , >= , < , <= , = , != 이 있다.
SELECT *
FROM df
WHERE id = 40 
-- df 라는 테이블에서, id 가 40 인 데이터를 뽑아내라.
```

- 위와 같이 WHERE 뒤에 비교연산자를 넣어서, 조건을 추가할 수 있습니다.

<BR>

## SQL 연산자

SQL 연산자는 비교 연산자보다 조금 더 확장된 연산자입니다. 

| 연산자          | 의미                               |
| --------------- | ---------------------------------- |
| BETWEEN a AND b | a 와 b 사이에 값이 있음 (a,b 포함) |
| IN (list)       | list 중 어느 값이라도 일치         |
| LIKE '비교문자' | 비교 문자와 현태가 일치            |
| IS NULL         | null 값을 갖음                     |

**1.BETWEEN**

- BETWEEN 은 두 값의 범위에 해당하는 값을 출력할떄에 사용한다.

```sql
SELECT * 
FROM df 
WHERE col1 BETWEEN 10 AND 100
-- df 테이블에서 col1 의 값이 10~100 사이인 데이터 출력
```

<BR>

**2.IN** 

- 조회하고자 하는 데이터값이 여러개일때 사용한다. 
- = 연산자와 비슷하지만 , IN 은 데이터값을 여러개 목록으로 지정할 수 있다. 즉 여러개의 값 목록중에서 하나의 값이라도 만족하면, 해당하는 결과를 출력한다.

```sql
SELECT *
FROM df
WHERE col1 IN (10,20,30)
-- df 테이블에서 col1 의 값이 10,20,30 중 하나인 데이터 출력
```

<BR>

**3.LIKE**

- LIKE 연산자는 조회 조건값이 명확하지 않을때에 사용한다. 
- LIKE 연산자는 %(모든 문자) , _(한 글자) 같은 기호연산자와 함께 사용한다. 

```sql
SELECT *
FROM df 
WHERE 이름 LIKE '김%'
-- df 테이블에서, 이름이 김으로 시작하는 데이터 출력
```

```sql
SELECT *
FROM df 
WHERE 이름 LIKE '_김_'
-- df 테이블에서, 3글자 이름을 가지는데, 가운데 글자가 김인 사람
```

- %인% (이름 중간에 인 있으면 출력), %현(이름이 현으로 끝나면 력) 등으로 확장할 수 있습니다. 

<BR>

**4.IS NULL**

- ISNULL 연산자는 데이터값이 NULL 인 경우를 조회하고자 할 때에 사용합니다. 

```sql
SELECT *
FROM df 
WHERE ID IS NULL ;
-- DF 테이블에서, ID 가 비어있는 테이터를 추출
```

<br>

## 논리 연산자

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

# <center><font size="15">Order BY</font></center>

- Order by 는 정렬을 하는 하게 해줍니다.

```sql
SELECT col1, col2 
FROM df 
ORDER BY col1 DESC ; --- ACS 는 오름차순
```

- 다중열에게 적용할수도 있습니다.

```sql
SELECT *
FROM df 
ORDER BY col1 DESC, col2 ACS 
```

