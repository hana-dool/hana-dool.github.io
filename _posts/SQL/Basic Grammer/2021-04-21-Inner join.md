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
typora-root-url: ../../../../hana-dool.github.io
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

- Inner join 동등 조인이란, 양쪽 테이블에서 조인 조건이 일치하는 행만 가져오는 일반적인 join 법입니다. 

```sql
SELECT *
FROM df1 , df2
WHERE df1.col1 , = df2.col2 
-- df1 의 col1 과 df2 의 col2 를 key 로 inner join 한다.
```

```sql
SELECT
    select_list
FROM t1
INNER JOIN t2 ON join_condition1
INNER JOIN t3 ON join_condition2
...;
```

> ## Note : inner join 의 순서가 중요할까? 

```sql
-- A
select *
from   a left join b
           on <blahblah>
       left join c
           on <blahblan>
-- B
select *
from   a left join c
           on <blahblah>
       left join b
           on <blahblan>  
-- C
select *
from   a join b
           on <blahblah>
       join c
           on <blahblan>
-- D
select *
from   a join c
           on <blahblah>
       join b
           on <blahblan>  
```

- 위와 같이 데이터의 inner join 순서가 있다고 합시다. 
  - 위 4개의 경우 모두 같은 결과를 내게 될까요? 
- 결론은 모두 같다는 것입니다! 
  - inner join 은 합집합이라는것을 명심합시다. 즉 $A\cap B \cap C$ = $A\cap C \cap B$ .... 모두 수학적으로 일치하므로 같은 결과를 내게 되는것입니다.

# [Example](#link){: .btn .btn--primary}{: .align-center}

> ## Basic Example

```sql
SELECT 
    productCode, 
    productName
FROM
    products t1
INNER JOIN productlines t2 
    ON t1.productline = t2.productline;
```

```
productCode|productName                                |
-----------+-------------------------------------------+
S10_1949   |1952 Alpine Renault 1300                   |
S10_4757   |1972 Alfa Romeo GTA                        |
S10_4962   |1962 LanciaA Delta 16V                     |
S12_1099   |1968 Ford Mustang                          |
S12_1108   |2001 Ferrari Enzo                          |
S12_3148   |1969 Corvair Monza                         |
S12_3380   |1968 Dodge Charger                         |
.....
```

- Inner join 을 이용하면 productline 를 키로 하여서 합치게 합니다.

> ## Using 을 사용한 join

```sql
SELECT 
    productCode, 
    productName
FROM
    products
INNER JOIN productlines USING (productline);
```

```sql
SELECT 
    productCode, 
    productName
FROM
    products t1
INNER JOIN productlines t2 
    ON t1.productline = t2.productline;
```

- 이떄 `products` 테이블과 `productlines` 테이블이 같은 key 이름 (productline) 을 가지고 있기 떄문에 using 을 사용해서 위처럼 합칠 수 있습니다. ( 위 두 예시는 같은 예시입니다. ) 

> ## 조건과 Inner join

- 추가적으로 조건을 써 넣을 수 있습니다.

```sql
SELECT ename,loc, job, e.deptno 
FROM emp e
INNER JOIN dept d
ON e.deptno = d.deptno AND e.job = 'ANALYST';
```

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

- 위처럼 `ANALYIST` 인 사람에만 제한한다는 조건을 걸어서 추가적인 join 조건을 걸수도 있습니다.

> ## 여러개의  Table join

![jpg](/assets/images/Program/66_1.jpg)

- 위와 같이 3개의 테이블에 대해서 join 을 실시한다고 합시다.
- 이때 `orders` 가 중심이 되어서,`orderdetails` 와 `products` 두개의 테이블을 join 하는 형태입니다.

```sql
SELECT 
    orderNumber,
    orderDate,
    orderLineNumber,
    productName,
    quantityOrdered,
    priceEach
FROM
    orders
INNER JOIN
    orderdetails USING (orderNumber)
INNER JOIN
    products USING (productCode)
ORDER BY 
    orderNumber, 
    orderLineNumber;
```

```
orderNumber|orderDate |orderLineNumber|productName                              |quantityOrdered|priceEach|
-----------+----------+---------------+-----------------------------------------+---------------+---------+
      10100|2003-01-06|              1|1936 Mercedes Benz 500k Roadster         |             49|    35.29|
      10100|2003-01-06|              2|1911 Ford Town Car                       |             50|    55.09|
      10100|2003-01-06|              3|1917 Grand Touring Sedan                 |             30|   136.00|
      10100|2003-01-06|              4|1932 Alfa Romeo 8C2300 Spider Sport      |             22|    75.46|
      10101|2003-01-09|              1|1928 Mercedes-Benz SSK                   |             26|   167.06|
      10101|2003-01-09|              2|1938 Cadillac V-16 Presidential Limousine|             46|    44.35|
      10101|2003-01-09|              3|1939 Chevrolet Deluxe Coupe              |             45|    32.53|
      10101|2003-01-09|              4|1932 Model A Ford J-Coupe                |             25|   108.06|
      10102|2003-01-10|              1|1936 Mercedes-Benz 500K Special Roadster |             41|    43.13|
      10102|2003-01-10|              2|1937 Lincoln Berline                     |             39|    95.55|
      10103|2003-01-29|              1|1962 Volkswagen Microbus                 |             36|   107.34|
      10103|2003-01-29|              2|1926 Ford Fire Engine                    |             22|    58.34|
      10103|2003-01-29|              3|1980’s GM Manhattan Express              |             31|    92.46|
      10103|2003-01-29|              4|1962 LanciaA Delta 16V                   |             42|   119.67|
      10103|2003-01-29|              5|1940s Ford truck                         |             36|    98.07|
```

- 위처럼 3개의 테이블을 합칠 수 있습니다.
