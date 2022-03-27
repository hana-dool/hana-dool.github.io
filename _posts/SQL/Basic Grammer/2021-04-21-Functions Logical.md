---
title:  "Functions &#58; Logical"
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

논리연산자는 어떤게 있는지만 짧게 알아봅시다. (각각의 operator 에 대해서 자세한것은 개별 문서 참조)
{: .notice--warning}

# [SQL Logical Operators](#link){: .btn .btn--primary}{: .align-center}

> ## 논리 연산자

- 우리는 이전에 `Where `에 대해서 배울때에, SQL 의 Logical Operation 을 통하여 where 절을 좀 더 다채롭게 구성할 수 있다는것을 배웠습니다. 
- SQL은 모든 논리 연산자는 `TRUE` , `FALSE` 또는 `NULL` ( `UNKNOWN` )에 평가됩니다. MySQL 그럼, 이들은 1 ( `TRUE` ), 0 ( `FALSE` ) 및 `NULL` 로 구현됩니다. 이 대부분은 다양한 SQL 데이터베이스 서버에 공통입니다. 그러나 일부 서버는 `TRUE` 0이 아닌 임의의 값을 돌려주는 경우가 있습니다.
- 논리연산자를 사용하면게 조건에 대하여 True , False , Unkown(Null) 값을 반환하게 됩니다.

| **Operator** | **Meaning**                                                  |
| :----------- | :----------------------------------------------------------- |
| ALL          | Return true if all comparisons are true                      |
| AND          | Return true if both expressions are true                     |
| ANY          | Return true if any one of the comparisons is true.           |
| BETWEEN      | Return true if the operand is within a range                 |
| EXISTS       | Return true if a subquery contains any rows                  |
| IN           | Return true if the operand is equal to one of the value in a list |
| LIKE         | Return true if the operand matches a pattern                 |
| NOT          | Reverse the result of any other Boolean operator.            |
| OR           | Return true if either expression is true                     |
| SOME         | Return true if some of the expressions are true              |

> ## And

```
expression1 AND expression2
```

- And 는 연결되어있는 두개의 expression 이 둘다 True 일때에 True 를 반환하게 됩니다. 

```sql
SELECT 
    first_name, last_name, salary
FROM
    employees
WHERE
    salary > 5000 AND salary < 7000
ORDER BY salary;
-- salary 가 5000 초과, 7000 미만인 사람 출력
```

```first_name|last_name|salary |
----------+---------+-------+
Bruce     |Ernst    |6000.00|
Pat       |Fay      |6000.00|
Charles   |Johnson  |6200.00|
Shanta    |Vollman  |6500.00|
Susan     |Mavris   |6500.00|
Luis      |Popp     |6900.00|
```

> ## OR

```
expression1 OR expression2
```

- Or 은 두개의 expression 중 하나만 true 여도 true 를 반환하게 됩니다. 

```sql
SELECT 
    first_name, last_name, salary
FROM
    employees
WHERE
    salary = 7000 OR salary = 8000
ORDER BY salary;
-- salary 가 7000 또는 8000인 사람 출력 
```

```
first_name|last_name|salary |
----------+---------+-------+
Kimberely |Grant    |7000.00|
Matthew   |Weiss    |8000.00|
```

> ## Is Null 

- `Is Null` 은 value 가 null 일때에 True 를 반환하게 됩니다. 
  - value 가 Null 이 아니면 false 를 반환하게 됩니다. 

```sql
SELECT 
    first_name, last_name, phone_number
FROM
    employees
WHERE
    phone_number IS NULL
ORDER BY first_name , last_name;
-- phone number 가 null(누락) 된 사람을 출력
```

```
first_name|last_name |phone_number|
----------+----------+------------+
Charles   |Johnson   |            |
Jack      |Livingston|            |
John      |Russell   |            |
Jonathon  |Taylor    |            |
Karen     |Partners  |            |
```

> ## Between

- Between 은 minimum ~ maximum 사이의 값을 출력하게 됩니다.
  - 이때 `between 10 and 30` 이 되면, 10과 30인 값도 포함하게 된다는것을 기억합니다.

```sql
SELECT 
    first_name, last_name, salary
FROM
    employees
WHERE
    salary BETWEEN 9000 AND 12000
ORDER BY salary;    
```

```
first_name|last_name|salary  |
----------+---------+--------+
Alexander |Hunold   | 9000.00|
Daniel    |Faviet   | 9000.00|
Hermann   |Baer     |10000.00|
Den       |Raphaely |11000.00|
Nancy     |Greenberg|12000.00|
Shelley   |Higgins  |12000.00|
```

- 위에서 9000 ~ 12000 의 값이 있는것을 잘 기억하세요!

> ## Exist

- Exist 는 하위 쿼리의 행이 1개 이상이면 true 를 리턴합니다.
- Exist 의 특징으로는, 행을 1개라도 찾게되면 바로 process 를 종료하게 되므로 효율적입니다.

```sql
SELECT 
    select_list
FROM
    a_table
WHERE
    [NOT] EXISTS(subquery);
```

- Exist 는 주로 위와 같이 쓰입니다.

> ## in

- in 연산자는 값을 리스트 안에 값이 있는지와 비교하게 됩니다.
  - 비교하는 값이 목록에서 하나 이상의 값과 일치하면 in 연산자는 true 를 반환하게 됩니다. 

```sql
SELECT 
    first_name, last_name, department_id
FROM
    employees
WHERE
    department_id IN (8, 9)
ORDER BY department_id;
```

```
first_name|last_name |department_id|
----------+----------+-------------+
John      |Russell   |            8|
Karen     |Partners  |            8|
Jonathon  |Taylor    |            8|
Jack      |Livingston|            8|
Kimberely |Grant     |            8|
Charles   |Johnson   |            8|
Steven    |King      |            9|
Neena     |Kochhar   |            9|
Lex       |De Haan   |            9|
```

> ## Like

- Like 는 우리가 검색하려는 값을 좀 더 다채롭게 검색할 수 있게 해줍니다.
  - The percent sign ( `%`) represents zero, one, or multiple characters.
  - The underscore sign ( `_`) represents a single character.

> % operator

```sql
SELECT 
    employee_id, first_name, last_name
FROM
    employees
WHERE
    first_name LIKE 'jo%' -- jo 로 시작되는 이름 (뒤에 붙는 str 에는 제한없음)
ORDER BY first_name;
```

```
employee_id|first_name |last_name|
-----------+-----------+---------+
        110|John       |Chen     |
        145|John       |Russell  |
        176|Jonathon   |Taylor   |
        112|Jose Manuel|Urman    |
```

> _ operator

```sql
SELECT 
    employee_id, first_name, last_name
FROM
    employees
WHERE
    first_name LIKE '_h%'
ORDER BY first_name;
```

```
employee_id|first_name|last_name|
-----------+----------+---------+
        179|Charles   |Johnson  |
        123|Shanta    |Vollman  |
        205|Shelley   |Higgins  |
        116|Shelli    |Baida    |
```

- h 앞에 하나의 문자가 들어가고, 뒤에 붙는 문자에는 제한이 없을때

