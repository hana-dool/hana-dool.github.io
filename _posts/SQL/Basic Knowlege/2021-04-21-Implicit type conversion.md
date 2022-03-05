---
title: "Implicit type conversion"
excerpt: ""
categories:
  - SQL_Basic_Knowledge
last_modified_at: 2022-02-27

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [Indtroduction](#link){: .btn .btn--primary}{: .align-center}

> ## 기초 Tip

- 우선 emp 가 아래처럼 생겼음을 기억합시다.

```sql
select *
from emp
```

```
empno|ename |job      |mgr |hiredate  |sal    |comm   |deptno|
-----+------+---------+----+----------+-------+-------+------+
 7369|SMITH |CLERK    |7902|1980-12-17| 800.00|       |    20|
 7499|ALLEN |SALESMAN |7698|1981-02-20|1600.00| 300.00|    30|
 7521|WARD  |SALESMAN |7698|1981-02-22|1250.00| 500.00|    30|
 7566|JONES |MANAGER  |7839|1981-04-02|2975.00|       |    20|
 7654|MARTIN|SALESMAN |7698|1981-09-28|1250.00|1400.00|    30|
 7698|BLAKE |MANAGER  |7839|1981-05-01|2850.00|       |    30|
 7782|CLARK |MANAGER  |7839|1981-06-09|2450.00|       |    10|
 7788|SCOTT |ANALYST  |7566|1987-04-19|3000.00|       |    20|
 7839|KING  |PRESIDENT|    |1981-11-17|5000.00|       |    10|
 7844|TURNER|SALESMAN |7698|1981-09-08|1500.00|   0.00|    30|
 7876|ADAMS |CLERK    |7788|1987-05-23|1100.00|       |    20|
 7900|JAMES |CLERK    |7698|1981-12-03| 950.00|       |    30|
 7902|FORD  |ANALYST  |7566|1981-12-03|3000.00|       |    20|
 7934|MILLER|CLERK    |7782|1982-01-23|1300.00|       |    10|
```

- 이때 sal 안의 데이터 column 타입은 숫자입니다. 

```sql
select ename , sal 
from emp 
where sal = '3000' ; 
```

- 이떄 위처럼 쿼리를 수행하게 되면 type 형태가 맞지 않으므로 출력할 수 없어야 정상일 것입니다. 

```
ename|sal    |
-----+-------+
SCOTT|3000.00|
FORD |3000.00|
```

- 앗? 근데 위처럼 값을 출력하고 있음을 알 수 있습니다.
- sal은 숫자형 데이터 컬럼인데 "3000"을 문자형으로 비교하고 있습니다. 그러면 '숫자형=문자형' 비교하여 데이터 검색이 안 될 것 같은데 결과가 나옵니다. $\mathrm{SAL}=^{\prime} 3000^{\prime}$ 으로 잘못 비교해서 실 행했지만 SQL이 알아서 '숫자형=숫자형'으로 암시적으로 형 변환을 하기 때문에 에러가 발생 하지 않고 검색됩니다. 
- MYSQL은 문자형과 숫자형 두 개를 비교할 때는 문자형을 숫자형으로 변환합니다.

