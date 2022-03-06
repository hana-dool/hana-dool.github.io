---
title:  "Join &#58; Cross"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2021-05-06

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

# [Cross Join](#link){: .btn .btn--primary}{: .align-center}

> ## Cross Join

- **CROSS JOIN**은 **상호 조인**이라고도 불리며, **한 쪽 테이블의 모든 행들과 다른 테이블의 모든 행을 조인**시키는 기능을 한다. 
  - 그래서, CROSS JOIN의 결과 개수는 두 테이블의 행의 개수를 곱한 개수가 됩니다.

> 기본 구조 

```
SELECT column_list
FROM A
CROSS JOIN B;
```

- 다음 그림은 테이블 A와 테이블 B 간의 교차 조인 결과를 보여줍니다. 
- 아래의 경우 테이블 A에는 세 개의 행 1, 2, 3이 있고 테이블 B에도 세 개의 행 x, y, z가 있습니다. 
  - 결과적으로 데카르트 곱에 의하여 9개의 행이 출력되게 됩니다.

![jpg](/assets/images/Program/54_1.jpg)

- 이떄 위의 Cross join 을 수행하는것은 아래의 쿼리를 수행하는것과 같습니다.

```sql
SELECT 
    column_list
FROM
    A,
    B;
```

> 예제로 활용할 cities 테이블

|  id  | city | latitude | longitude |
| :--: | :--: | :------: | :-------: |
|  1   | 서울 | 37.5407  |  126.957  |
|  2   | 광주 |  35.126  |  126.831  |
|  3   | 대구 | 35.7988  |  128.583  |

- 모든 경우의 수, 즉 `A 테이블 row 개수 X B 테이블 row 개수` 만큼의 row를 가진 테이블이 출력된다.
- 이 방식은 **Cartesian Product, 곱집합**이라는 용어로 정의되어 있다.
- cities 테이블과 간단하게 만든 transport 테이블과의 CROSS JOIN을 시도해 보았습니다.

|  id  | category |
| :--: | :------: |
|  1   |   bus    |
|  2   |  subway  |
|  3   |   taxi   |

- CROSS JOIN은 여러가지로 표현할 수 있는데, 아래 3가지 모두 같은 결과를 출력한다.

```sql
SELECT * FROM cities CROSS JOIN transport;
```

- 3 X 3 = 9개의 row를 가진 테이블이 출력된다.

|  id  | city | latitude | longitude |  id  | category |
| :--: | :--: | :------: | :-------: | :--: | :------: |
|  1   | 서울 | 37.5407  |  126.957  |  1   |   bus    |
|  2   | 광주 |  35.126  |  126.831  |  1   |   bus    |
|  3   | 대구 | 35.7988  |  128.583  |  1   |   bus    |
|  1   | 서울 | 37.5407  |  126.957  |  2   |  subway  |
|  2   | 광주 |  35.126  |  126.831  |  2   |  subway  |
|  3   | 대구 | 35.7988  |  128.583  |  2   |  subway  |
|  1   | 서울 | 37.5407  |  126.957  |  3   |   taxi   |
|  2   | 광주 |  35.126  |  126.831  |  3   |   taxi   |
|  3   | 대구 | 35.7988  |  128.583  |  3   |   taxi   |

> ## Example

```sql
CREATE TABLE sales_organization (
	sales_org_id INT PRIMARY KEY,
	sales_org VARCHAR (255)
);

INSERT INTO sales_organization (sales_org_id, sales_org)
VALUES
	(1, 'Domestic'),
	(2, 'Export');

CREATE TABLE sales_channel (
	channel_id INT PRIMARY KEY,
	channel VARCHAR (255)
);

INSERT INTO sales_channel (channel_id, channel)
VALUES
	(1, 'Wholesale'),
	(2, 'Retail'),
	(3, 'eCommerce'),
	(4, 'TV Shopping');
```

- 위와 같은 쿼리를 이용하여 Example 을 형성해봅시다. 

> sales_organization 테이블

```
sales_org_id|sales_org|
------------+---------+
           1|Domestic |
           2|Export   |
```

> sales_channel 테이블

```
channel_id|channel    |
----------+-----------+
         1|Wholesale  |
         2|Retail     |
         3|eCommerce  |
         4|TV Shopping|
```

> Cross Join 

```sql
SELECT
	sales_org,
	channel
FROM
	sales_organization
CROSS JOIN sales_channel; 
```

```
sales_org|channel    |
---------+-----------+
Export   |Wholesale  |
Domestic |Wholesale  |
Export   |Retail     |
Domestic |Retail     |
Export   |eCommerce  |
Domestic |eCommerce  |
Export   |TV Shopping|
Domestic |TV Shopping|
```

> ## Note : 위치 바뀌어도 동일

```sql
SELECT
	sales_org,
	channel
FROM
	sales_channel
CROSS JOIN sales_organization; 
```

```
sales_org|channel    |
---------+-----------+
Export   |Wholesale  |
Domestic |Wholesale  |
Export   |Retail     |
Domestic |Retail     |
Export   |eCommerce  |
Domestic |eCommerce  |
Export   |TV Shopping|
Domestic |TV Shopping|
```

- 위와 같이 `sales_channel` 와 `sales_organization` 의 위치가 바뀌었음에도 그 결과는 같습니다. 왜냐하면 inner join 과 같이 순서가 상관 없기 때문입니다.

> ## 동일한 쿼리문

```sql
SELECT
	sales_org,
	channel
FROM
	sales_channel
CROSS JOIN sales_organization; 
```

- 위와 동일한 의미는 아래와 같습니다. 

```sql
SELECT
	sales_org,
	channel
FROM
	sales_organization,
	sales_channel;
```
