---
title:  "Start Transaction"
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

# [Start Transaction](#link){: .btn .btn--primary}{: .align-center}

> ## 트렌젝션 제어문 

- 트랜잭션을 시작하려면 `START TRANSACTION` 명령문을 사용합니다. 
  - `BEGIN` 또는  `BEGIN WORK` 을 사용하는 경우도 있습니다만, 모두 같은 함수 ( `START TRANSACTION`) 에 대한 별칭입니다.
- 현재 트랜잭션을 커밋하고 변경 사항을 영구적으로 만들려면 `COMMIT`명령문을 사용합니다.
- 현재 트랜잭션을 롤백하고 변경 사항을 취소하려면 `ROLLBACK`명령문을 사용합니다.
- 현재 트랜잭션에 대한 자동 커밋 모드를 비활성화하거나 활성화하려면 `SET autocommit` 명령문을 사용합니다.

> ## MySQL 의 Default Setting

- MYSQL 의 기본 설정은, 변경 사항을 데이터베이스에 영구적으로 자동 커밋하는 것입니다.
- mySQL 이 변경사항을 자동으로 커밋하지 않도록 조절하려면

```sql
SET autocommit = 0
```

또는

```sql
SET autocommit = OFF
```

- 자동 커밋 모드를 명시적으로 활성화하려면 다음 문을 사용합니다.

```sql
SET autocommit = 1 ;
```

또는

```sql
SET autocommit = ON;
```

> ## Rooback 이 통하지 않는 구문 (mysql)

- Rollback 이 신처럼 시간을 되돌리는것은 아닙니다. 몇게 구문에 대해서는 이러한 적용이 불가한 경우가 있습니다.
  - CREATE / ALTER / DROP DATABASE
  - CREATE /ALTER / DROP / RENAME / TRUNCATE TABLE
  - CREATE / DROP INDEX
  - CREATE / DROP EVENT
  - CREATE / DROP FUNCTION
  - CREATE / DROP PROCEDURE

> ## 활용 

- 데이터베이스에 우리가 연습삼아 데이터를 Delete 하고, 수정하는 작업이 있을때에 `START TRANSACTION` 명령어를 실행한 뒤에, 데이터를 수정하고, 나중에 ROLLBACK 을 하면 됩니다!

> ## Note 

```sql
START TRANSACTION ; 
//// 쿼리
COMMIT ; 
-- Commit 또는 Rollback 을 한번 하고나면 그 이후의 연산들은 추적하지 않음 
-- 즉 transaction 을 다시 써주어야 합니다.
```

# [Example : 기능별](#link){: .btn .btn--primary}{: .align-center}

> ## 단순 예시 

```sql
START TRANSACTION ; 

INSERT INTO emp(empno,ename,sal,deptno)
VALUES (1122,'XXXXXXX',3000,20) ;

SELECT *
FROM emp ;
```

```
empno|ename  |job      |mgr |hiredate  |sal    |comm   |deptno|
-----+-------+---------+----+----------+-------+-------+------+
 7369|SMITH  |CLERK    |7902|1980-12-17| 800.00|       |    20|
 7499|ALLEN  |SALESMAN |7698|1981-02-20|1600.00| 300.00|    30|
 7521|WARD   |SALESMAN |7698|1981-02-22|1250.00| 500.00|    30|
 7566|JONES  |MANAGER  |7839|1981-04-02|2975.00|       |    20|
 7654|MARTIN |SALESMAN |7698|1981-09-28|1250.00|1400.00|    30|
 7698|BLAKE  |MANAGER  |7839|1981-05-01|2850.00|       |    30|
 7782|CLARK  |MANAGER  |7839|1981-06-09|2450.00|       |    10|
 7788|SCOTT  |ANALYST  |7566|1987-04-19|3000.00|       |    20|
 7839|KING   |PRESIDENT|    |1981-11-17|5000.00|       |    10|
 7844|TURNER |SALESMAN |7698|1981-09-08|1500.00|   0.00|    30|
 7876|ADAMS  |CLERK    |7788|1987-05-23|1100.00|       |    20|
 7900|JAMES  |CLERK    |7698|1981-12-03| 950.00|       |    30|
 7902|FORD   |ANALYST  |7566|1981-12-03|3000.00|       |    20|
 7934|MILLER |CLERK    |7782|1982-01-23|1300.00|       |    10|
 1122|XXXXXXX|         |    |          |3000.00|       |    20|
```

- 위처럼  emp 테이블에 데이터를 넣어봤습니다. 

```sql
ROLLBACK ; 
```

```sql
SELECT *
FROM emp ;
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

- 위처럼 Rollback 으로 되돌릴 수 있습니다! 

# [Real Example](#link){: .btn .btn--primary}{: .align-center}

- https://www.mysqltutorial.org/mysql-transaction.aspx
  - 나중에 좀 더...

> ## 신규 판매 주문 생성

- 트랜잭션을 신규 판매 주문을 생성하는것으로 정의했다고 합시다.
  - 먼저 명령문 `START TRANSACTION` 을 사용하여 트랜잭션을 시작합니다 .
  - `orders` table 에서 제일 최신의 주문번호(sales number) 를 선택하고, 다음 판매 주문 번호를 새 판매 주문 번호로 사용합니다.
  - 그런 다음 테이블에 새 판매 주문을 삽입 `orders`합니다.
  - `orderdetails`그런 다음 판매 주문 항목을 테이블 에 삽입 하십시오.
  - `COMMIT`마지막으로 명령문 을 사용하여 트랜잭션을 커밋합니다 .
