---
title:  "GROUP FUNCTION"
excerpt: "그룹함수로 데이터 요약"
categories:
  - SQL_Basic
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

# <center><font size="15">그룹 함수란</font></center>

그룹함수는 함수가 적용되어 하나의 Aggregated 된 결과값을 내보냅니다. 

```
SELECT 그룹함수(열이름)
FROM 테이블 이름
[WHERE 조건식]
[ORDER BY 열이름]
```

주요 그룹 함수는 다음과 같습니다. 

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

## COUNT

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

## SUM / AVG

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

## MIN / MAX

최대, 최소값을 출력하는 함수이다. 모든 데이터 타입에 대해서, MAX, MIN 을 사용할 수 있다. 

- 문자의 경우 ordering 은 (a < b < c .....) 가 된다. 
- 날짜의 경우 ordering 은 (01 < 02 < ....) 가 된다. 

```sql
 -- employees 테이블에서 salary 의 최대값 / 최소값을 출력
 SELECT MIN(salary)
 FROM employees ; 
```





# Group by

지금까지의 그룹 함수들은 하나의 열을 그룹화 하여 적용하였습니다. 하지만 특정 그룹끼리 다른 연산을 적용하고 싶다면 어떻게 해야할까요? (예를 들어서 데이터 직무끼리만 평균 계산 등..) 이런 경우에 그룹함수를 적용할 수 있습니다. 

```
SELECT 기준열 , 그룹 함수(열이름) #4
FROM 테이블 이름 #1
[WHERE 조건식] #2 
GROUP BY 열 이름 #3 
[ORDER BY 열 이름] #5
```

1. 테이블에 접근 
2. WHERE 조건식에 맞는 데이터 값만 골라내기
3. 기술된 기준 열을 기준으로 같은 데이터 값끼리 그룹화
4. 결과 출력
5. 오름차순(ASC) / 내림차순(DESC) 으로 정렬

<BR>

<BR>

GROUP BY 절의 특징은 다음과 같습니다. 

- SEELCT 절에 기준 열과, 그룹 함수가 같이 지정되면, GROUP BY 절에 열 이름이 반드시 쓰여져야 한다.
- WHERE 절을 사용하게 되면, 행을 묶기 전에 조건식이 먼저 적용된다.
- SELECT 절에 그룹 함수를 사용하지 않아도, GROUP BY 절 만으로도 사용 가능

<br>

```sql
-- employees 테이블에서, employee_id 가 10 이상인 직원에 대해 job_id 별로 그룹화 하여서 
-- job_id 별 총 급여와, job_id 별 평균 급여를 구하고
-- job_id 별 총 급여를 기준으로 내림차순 정렬
SELECT job_id 직무 , SUM(salary) 봉급합 , AVG(salary) 봉급평균
FROM employees
WHERE employee_id >= 10 
GROUP BY job_id
ORDER BY 봉급합 desc;
```

<br>

```sql
-- employees 테이블에서, job_id 로 먼저 grouping 후에 manager_id 로 grouping 
-- 그 이후에 봉급의 평균 출력 
SELECT job_id,
        manager_id,
        AVG(salary)
FROM employees
GROUP BY job_id, manager_id ;
```



# HAVING

HAVING 절은 그룹화된 값에 조건식을 적용할 떄에 사용합니다. WHERE 절에서는 오로지 데이터를 읽어들일때에 Filtering  하는 효과를 가지므로, HAVING 절을 이용해서, AGG 된 값에 대해 조건식을 적용하는것입니다. 

HAVING은 일반적으로 GROUPBY 절 뒤에 적습니다. 

```
SELECT 열 이름, 그룹함수(열 이름) #5
FROM 테이블이름 #1
[WHERE 조건식] #2
GROUP BY 열이름 #3
[HAVING 조건식] #4 
[ORDER BY 열이름] #6
```

1. 테이블에 접근
2. WHERE 조건식에 맞는 데이터 값만 골라내기
3. 기술된 기준 열을 기준으로 같은 데이터 값끼리 그룹화
4. 그룹화된 값에 대해 조건식 적용
5. 결과 출력
6. 결과에 대한 Ordering

<br>

```sql
-- employees 테이블에서, employee_id 가 10 이상인 직원에 대해서, job_id 별로 그룹화 하여 총 급여 계산
-- 이 떄에 총 급여가 30000 보다 큰 값만 출력하자. 
-- 결과는 내림차순
SELECT  job_id 직업코드,
        SUM(salary) 봉급합
FROM employees
WHERE employee_id >= 10
GROUP BY job_id
HAVING SUM(salary) >= 30000
ORDER BY 봉급합 DESC; 
```