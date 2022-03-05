---
title:  "Comparison operations"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2021-05-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true 
typora-root-url: ../../../../hana-dool.github.io
---

# [Comparison operations](#link){: .btn .btn--primary}{: .align-center}

> ## 비교연산자

- 비교연산자입니다. 다양한 값들에 대해서 연산을 할 수 있습니다.

| 비교 연산자 | 의미              |
| ----------- | ----------------- |
| =           | 같다.             |
| <> (!=)     | 같지 않다.        |
| >           | 보다 크다.        |
| >=          | 보다 크거나 같다. |
| <           | 보다 작다.        |
| <=          | 보다 작거나 같다. |

> ## Equal (=)

```sql
SELECT 
    employee_id, first_name, last_name
FROM
    employees
WHERE
    last_name = 'Himuro'; 
```

```
employee_id|first_name|last_name|
-----------+----------+---------+
        118|Guy       |Himuro   |
```

- 조건에 맞는 (='humuro') 데이터만을 내보냅니다.

> ## Not Equal (!= , <>)

```sql
SELECT 
    employee_id, first_name, last_name, department_id
FROM
    employees
WHERE
    department_id <> 8  -- department 가 8이 아닌 데이터 출력 
ORDER BY first_name , last_name;
```

```sql
employee_id|first_name |last_name  |department_id|
-----------+-----------+-----------+-------------+
        121|Adam       |Fripp      |            5|
        103|Alexander  |Hunold     |            6|
        115|Alexander  |Khoo       |            3|
        193|Britney    |Everett    |            5|
...
```

> ## Larger than (>)

```sql
-- 비교 연산자는 > , >= , < , <= , = , != 이 있다.
SELECT
	employee_id,
	first_name,
	last_name,
	salary
FROM
	employees
WHERE
	salary > 14000
```

```
employee_id|first_name|last_name|salary  |
-----------+----------+---------+--------+
        100|Steven    |King     |24000.00|
        101|Neena     |Kochhar  |17000.00|
        102|Lex       |De Haan  |17000.00|
```

- 위처럼 Salary 가 14000 이상인 값들을 출력하게 됩니다. 
