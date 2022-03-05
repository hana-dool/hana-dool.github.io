---
title:  "Coalesce(ifnull)"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2021-07-13

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

# [Coalesce](#link){: .btn .btn--primary}{: .align-center}

> ## 기본 구조

```
COALESCE(value1,value2,...);
```

- **`COALESCE`**는 **지정한 표현식들 중에 NULL이 아닌 첫 번째 값을 반환**한다.
  - 모든 DBMS에서 사용가능
- 표현식은 여러 항목 지정이 가능하고, 처음으로 만나는 NULL이 아닌 값을 출력한다.
  - 표현식이 모두 NULL일 경우엔 결과도 NULL 반환
- **`COALESCE`**는 배타적 OR 관계 열에서 활용도가 높다.
  - *엔터티(테이블)에서 두 개 이상의 속성(열) 중 하나의 값만 가지는 데이터 일 경우*

```sql
-- NULL 처리 상황
SELECT COALESCE(Column명1, Column명1이 NULL인 경우 대체할 값)
FROM 테이블명
```

```sql
-- 배타적 OR 관계 열
-- Column1 ~ 4 중 NULL이 아닌 첫 번째 Column을 출력
SELECT COALESCE(Column명1, Column명2, Column명3, Column명4)
FROM 테이블명
```

- Example

```sql
-- NAME Column의 값이 NULL인 경우 다음 표현식으로 넘어간다.
-- 다음 표현식인 "No name"이 Null이 아니므로 "No name"을 출력.
SELECT COALESCE(NAME, "No name")
FROM ANIMAL_INS
```

> ## 기본 성질

```
SELECT COALESCE(NULL, 0);  -- 0
SELECT COALESCE(NULL, NULL); -- NULL;
```



# [MYSQL : IFNULL](#link){: .btn .btn--primary}{: .align-center}

- 해당 **Column의 값이 NULL을 반환할 때, 다른 값으로 출력할 수 있도록 하는 함수**이다.
  - 기본 구조

```sql
SELECT IFNULL(Column명, "Null일 경우 대체 값") FROM 테이블명; 
```

- Example

```sql
-- NAME Column이 NULL인 경우 "No name"을 출력, NULL이 아닌 경우 NAME Column을 출력
SELECT IFNULL(NAME, "No name") as NAME
FROM ANIMAL_INS
```

> ## IF()??

- **Null 처리는 사실 `IF` 함수와 `IS NULL` 조건으로도 가능**합니다..

> Example

```sql
--  NAME Column이 NULL이 True인 경우 "No name"을, False인 경우는 NAME Column을 출력
SELECT IF(IS NULL(NAME), "No name", NAME) as NAME
FROM ANIMAL_INS
```



---

Ref

- <https://royzero.tistory.com/50>
- https://velog.io/@gillog/DB-MySQL-NULL-%EC%B2%98%EB%A6%ACIFNULL-CASE-COALESCE

