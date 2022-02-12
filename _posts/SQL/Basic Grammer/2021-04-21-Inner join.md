---
title:  "Inner Join"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2021-12-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [Inner Join](#link){: .btn .btn--primary}{: .align-center}

> ## Join

- 관계형 데이터베이스라는 말은 테이블이 '관계' 를 맺고 조작된다는 원리에서 유래하였습니다. 
- 테이블은 각 유형에 맞는 데이터가 연결되어있고, 테이블은 일정한 규칙에 따라 서로 연결이 되어있습니다. 
- 데이터가 이리저리 테이블에 흩어져서 존재하므로, 이를 다루기 위해서는 join 등의 기법을 이용해 데이터들을 연결해야 합니다.

| 조인 기법  | 설명                                                     |
| ---------- | -------------------------------------------------------- |
| inner join | 조인 조건이 정확히 일치하는 경우에 결과를 출력한다.      |
| outer join | 조인 조건이 정확히 일치하지 않아도 모든 결과를 출력한다. |
| self join  | 자체 테이블에서 조인할때에 사용                          |

![png](/assets/images/SQL_Basic/6_4.png)

> ## 기본 구조

- SQL 은 Column 이나 Table 에 대해서 별칭을 지을 수 있습니다.

![jpg](/assets/images/Program/49_1.jpg)

- Inner join 동등 조인이란, 양쪽 테이블에서 조인 조건이 일치하는 행만 가져오는 일반적인 join 법이다. 

```sql
SELECT *
FROM df1 , df2
WHERE df1.col1 , = df2.col2 
-- df1 의 col1 과 df2 의 col2 를 key 로 inner join 한다.
```

```sql
SELECT *
FROM df1 
INNER JOIN df2 on df1.sal = df2.sal  ; 
```

![png](/assets/images/SQL_Basic/6_1.png)

- 위와 같이 같을 열 (department_id) 을 기준으로 join 을 하였다. 그러자 이름 뒤에 1 이 붙여져서 구분이 되고 있음을 알 수 있다.

![png](/assets/images/SQL_Basic/6_2.png)

- 위는 AND 연산자를 활용하여, join 조건을 추가한 것이다. 이 실행은 어떻게 이루어지는 것일까? 아래처럼 먼저 A 와 B 를 join 한 이후에 B 와 C 를 join 하게 된다.

![png](/assets/images/SQL_Basic/6_3.png)

- 위와 같이 하지 않고, 아래와 같이 명령어를 짤 수도 있습니다. 

![png](/assets/images/SQL/9_1.png)

> ## Example

```sql
SELECT ename,loc 
FROM emp, dept 
WHERE emp.deptno = dept.deptno ;
```

```
ename |loc     |
------+--------+
CLARK |NEW YORK|
KING  |NEW YORK|
MILLER|NEW YORK|
SMITH |DALLAS  |
JONES |DALLAS  |
SCOTT |DALLAS  |
ADAMS |DALLAS  |
.....
```

- 위와 같이 Inner join 을 쓰면 department_id 와 department_id 를 이용해서 조인하게 됩니다

> ## 조건과 Inner join

- inner join 을 쓸때마다 테이블의 이름을 쓰기가 귀찮습니다.
- 이떄에는 별칭을 이용하여 아래와 같이 join 을 합니다.

```sql
SELECT ename,loc, job, e.deptno 
FROM emp e , dept d 
WHERE e.deptno = d.deptno AND e.job = 'ANALYST';
```

```
ename|loc   |job    |deptno|
-----+------+-------+------+
SCOTT|DALLAS|ANALYST|    20|
FORD |DALLAS|ANALYST|    20|
```

- 위처럼 `ANALYIST` 의 조건을 걸 

> ## 여러개의  Table join

> Employees

```
employee_id|first_name |last_name  |email                            |phone_number|hire_date |job_id|salary  |manager_id|department_id|
-----------+-----------+-----------+---------------------------------+------------+----------+------+--------+----------+-------------+
        100|Steven     |King       |steven.king@sqltutorial.org      |515.123.4567|1987-06-17|     4|24000.00|          |            9|
        101|Neena      |Kochhar    |neena.kochhar@sqltutorial.org    |515.123.4568|1989-09-21|     5|17000.00|       100|            9|
        102|Lex        |De Haan    |lex.de haan@sqltutorial.org      |515.123.4569|1993-01-13|     5|17000.00|       100|            9|
        103|Alexander  |Hunold     |alexander.hunold@sqltutorial.org |590.423.4567|1990-01-03|     9| 9000.00|       102|            6|
        104|Bruce      |Ernst      |bruce.ernst@sqltutorial.org      |590.423.4568|1991-05-21|     9| 6000.00|       103|            6|
        105|David      |Austin     |david.austin@sqltutorial.org     |590.423.4569|1997-06-25|     9| 4800.00|       103|            6|
.........
```

> departments

```
department_id|department_name |location_id|
-------------+----------------+-----------+
            1|Administration  |       1700|
            2|Marketing       |       1800|
            3|Purchasing      |       1700|
            4|Human Resources |       2400|
            5|Shipping        |       1500|
            6|IT              |       1400|
....
```

> Jobs

```
job_id|job_title                      |min_salary|max_salary|
------+-------------------------------+----------+----------+
     1|Public Accountant              |   4200.00|   9000.00|
     2|Accounting Manager             |   8200.00|  16000.00|
     3|Administration Assistant       |   3000.00|   6000.00|
     4|President                      |  20000.00|  40000.00|
     5|Administration Vice President  |  15000.00|  30000.00|
.....
```

> Three Join

```sql
SELECT
	e.department_id,
	e.job_id,
	first_name,
	last_name,
	job_title,
	department_name
FROM
	employees e
INNER JOIN departments d ON
	e.department_id = d.department_id
INNER JOIN jobs j ON
	e.job_id = j.job_id
WHERE
	e.department_id IN (1, 2, 3) ;
```

```
department_id|job_id|first_name|last_name |job_title               |department_name|
-------------+------+----------+----------+------------------------+---------------+
            1|     3|Jennifer  |Whalen    |Administration Assistant|Administration |
            2|    10|Michael   |Hartstein |Marketing Manager       |Marketing      |
            2|    11|Pat       |Fay       |Marketing Representative|Marketing      |
            3|    14|Den       |Raphaely  |Purchasing Manager      |Purchasing     |
            3|    13|Alexander |Khoo      |Purchasing Clerk        |Purchasing     |
            3|    13|Shelli    |Baida     |Purchasing Clerk        |Purchasing     |
            3|    13|Sigal     |Tobias    |Purchasing Clerk        |Purchasing     |
            3|    13|Guy       |Himuro    |Purchasing Clerk        |Purchasing     |
            3|    13|Karen     |Colmenares|Purchasing Clerk        |Purchasing     |
```

- 위와 같이 여러 조건을 이용해서 inner join 을 이용할 수 있습니다.

```sql
SELECT
	first_name,
	last_name,
	job_title,
	department_name
FROM
	employees e,
	departments d,
	jobs j
WHERE
	e.department_id = d.department_id
	AND e.job_id = j.job_id
	AND e.department_id  IN (1,2,3) ; 
```

- 위도 같은 조건입니다.
