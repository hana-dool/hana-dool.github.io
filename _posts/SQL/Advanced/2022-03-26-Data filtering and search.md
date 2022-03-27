---
title: "데이터 필터링과 검색"
excerpt: "기본적으로 지켜야할것"
categories:
  - SQL_Advanced
last_modified_at: 2021-08-22

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [Indtroduction](#link){: .btn .btn--primary}{: .align-center}

> ## 일치하지 않거나 누락된 코드 찾기

- Order_Details 에 팔린 물건이 orderdetails 로 기록되고 있다고 합시다.
- Products 에 제품 목록이 products 으로 관리되고 있다고 합시다. 
- 이떄 , "팔리지 않은 제품" 을 검색하려면 어떻게 해야할까요? 

> Example 1 : Subquery 이용

```sql
SELECT
	productCode
FROM
	products p
WHERE
	(p.productCode NOT IN 
		(
		SELECT
			productCode
		FROM
			orderdetails
		)  
	);
```

- 위처럼 쿼리를 짜면 서브쿼리 전체에 대해서 `NOT IN` 로 계속 Searching 을 진행하므로 매우 비효율적입니다. 

> Example 2 : Exist 구문 활용

- 일반적으로 Exist 가 Not In 보다 더 효율적입니다. 왜냐하면 Exist 는 일치하는것을 찾으면 거기서 중단하는데, Not in 은 계속 데이터를 찾기 때문입니다. 

```sql
SELECT
	productCode
FROM
	products p
WHERE
	(p.productCode NOT IN 
		(
		SELECT
			productCode
		FROM
			orderdetails
		)  
	);
```

