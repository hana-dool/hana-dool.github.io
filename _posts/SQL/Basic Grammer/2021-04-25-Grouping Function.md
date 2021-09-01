---
title:  "Grouping Function"
excerpt: "그룹함수로 데이터 요약"
categories:
  - SQL_Basic_Grammer
tags:
  - 1
last_modified_at: 2021-05-02

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 그룹 함수란

- 그룹함수는 함수가 적용되어 하나의 Aggregated 된 결과값을 내보냅니다. 

```
SELECT 그룹함수(열이름)
FROM 테이블 이름
[WHERE 조건식]
[ORDER BY 열이름]
```

- 주요 그룹 함수는 다음과 같습니다. 

| 함수     | 설명           | 예                | NULL 처리 |
| -------- | -------------- | ----------------- | --------- |
| COUNT    | 행 갯수를 센다 | COUNT(열 이름)    |           |
| SUM      | 합계           | SUM(열 이름)      | NULL 제외 |
| AVG      | 평균           | AVG(열 이름)      | NULL 제외 |
| MAX      | 최댓값         | MAX(열 이름)      | NULL 제외 |
| MIN      | 회소값         | MIN(열 이름)      | NULL 제외 |
| STDDEV   | 표준편차       | STDDEV(열 이름)   | NULL 제외 |
| VARIANCE | 분산           | VARIANCE(열 이름) | NULL 제외 |

- 이때 특징은 WHERE 절이 거짓이여도 결과를 항상 출력한다는 점입니다.

```sql
SELECT *
FROM df 
WHERE 1 = 2 
```

- 위의 결과는 NULL 으로 출력됩니다.

<br>

# COUNT

```
COUNT(열 이름)
```

```sql
-- employees 테이블에서, salary 의 행 수가 몇개인지 세어서 출력
SELECT COUNT(salary) 행 수 
FROM employees ; 
```

![png](/assets/images/SQL_Basic/4_1.png)

<br>

# SUM / AVG

```
SUM(열이름) , AVG(열이름)
```

```sql
-- employees 테이블에서 salary의 합계와 평균을 구해보자.
SELECT AVG(salary) 평균,
       SUM(salary) 합계
FROM employees ;
```

```sql
 -- Null 값을 포함해서 평균을 계산
 SELECT AVG(NVL(salary,0))
 FROM employees ;
```

<br>

# MIN / MAX

최대, 최소값을 출력하는 함수이다. 모든 데이터 타입에 대해서, MAX, MIN 을 사용할 수 있다. 

- 문자의 경우 ordering 은 (a < b < c .....) 가 된다. 
- 날짜의 경우 ordering 은 (01 < 02 < ....) 가 된다. 

```sql
 -- employees 테이블에서 salary 의 최대값 / 최소값을 출력
 SELECT MIN(salary)
 FROM employees ; 
```


