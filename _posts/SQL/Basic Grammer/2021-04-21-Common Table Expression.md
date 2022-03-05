---
title:  "common table expression(CTL)"
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

평균에 대해서 알아보자.
{: .notice--warning}

# [CTL](#link){: .btn .btn--primary}{: .align-center}

> ## 기본 구조

- common table expression(CTE)는 named temporary result set 을 미리 저장해서 사용하는것을 의미합니다.
- CTE와 비교대상으로는 VIEW가 있다. VIEW는 만들기 위해 권한이 필요하고 사전에 정의를 해야한다. 반면, CTE는 권한이 필요 없고 하나의 쿼리문이 끝날때까지만 지속되는 일회성 테이블이다.
- CTE는 주로 복잡한 쿼리문에서 코드의 **가독성**과 **재사용성**을 위해 파생테이블 대신 사용하기에 유용하다.

```
WITH 테이블명 AS (SELECT ...)
```

- 위를 좀 더 풀어쓰면 아래와 같습니다.

```sql
WITH cte_name (column_list) AS (
    query
) 
SELECT * FROM cte_name;
```

> 2개 이상의 가상 테이블

```sql
## 2개 이상의 가상 테이블 ##
WITH 
가상1 AS ( 서브쿼리문 ), 
가상2 AS ( 서브쿼리문 )

## 실제 사용 ##
SELECT 컬럼, [컬럼, ...] FROM 가상1, 가상2
```

- 위처럼 2개 이상의 테이블을 사용할수도 있습니다.

> Seuquery

- 이때 굳이 가상테이블을 with 문으로 만들 강제성은 없습니다.
  - 아래처럼 서브쿼리로 사용해도 충분합니다.

```sql
Select [컬럼],....
FROM (서브쿼리문...)
WHERE 조건...
```

- With문을 활용하였을 때 해당 SQL 환경에서 임시로 재사용이 가능하다는 장점을 가지고 있어서 사용자에게 편리합니다.

> ## 주의점

- MySQL 8과 PostgreSQL에서는 CTE를 **Materializing**한다. 테이블이 cache처럼 임시로 저장된다는 의미이다.
- 이로 인해 CTE를 무분별하게 사용할 경우, Query performance가 오히려 더 떨어질 수 있다. Subquery 형태로 사용하는 것이 나을 수도 있다.

> ## Example : 단일 CTE

```sql
WITH customers_in_usa AS (
	SELECT
		customerName,
		state
	FROM
		customers
	WHERE
		country = 'USA'
) 
SELECT
	customerName
FROM
	customers_in_usa
WHERE
	state = 'CA'
ORDER BY
	customerName;
```

- 위처럼 쿼리를 짠다면 country = USA 인 데이터중에서, state = 'CA' 인 데이터를 뽑아내는 뭐리가 됩니다.

> ## Example : Advanced

```sql
WITH salesrep AS (
    SELECT 
        employeeNumber,
        CONCAT(firstName, ' ', lastName) AS salesrepName
    FROM
        employees
    WHERE
        jobTitle = 'Sales Rep'
),
customer_salesrep AS (
    SELECT 
        customerName, salesrepName
    FROM
        customers
            INNER JOIN
        salesrep ON employeeNumber = salesrepEmployeeNumber
)
SELECT 
    *
FROM
    customer_salesrep
ORDER BY customerName;
```

- 위 예시에서는 두개의 CTE 를 한번에 사용했습니다. 
- 특정 고객에게 어떤 점원이 물건을 팔았는지 알고 싶다고 합시다. 

![jpg](/assets/images/Program/64_2.jpg)

- 이떄 , CTE 를 여러번 사용하여서, 원하는 작업을 수행할 수 있습니다.

# [Advanced](#link){: .btn .btn--primary}{: .align-center}

> ## WITH절에 정의된 쿼리는 여러번 사용할수록 효율이 증가한다.

```sql
WITH EX AS 
(
   SELECT *
    FROM PRODUCTS 
   WHERE STANDARD_COST > 1000
)
 
SELECT * FROM EX WHERE EX.CATEGORY_ID = '1'
UNION ALL
SELECT * FROM EX WHERE EX.CATEGORY_ID = '2'
UNION ALL
SELECT * FROM EX WHERE EX.CATEGORY_ID = '3'
```

- WITH절에 정의된 내용을 한번만 사용한다면 서브 쿼리를 사용하는 것과 크게 성능 차이가 나지 않는다. 
- WITH문의 가장 큰 장점은 한 번 WITH절의 내용을 한 번에 올려놓고 계속 재사용한다는 것에 큰 의미가 있기에 WITH절에 구문을 여러 번 참조하는 쿼리를 만들수록 그 효과가 배로 증가한다.
