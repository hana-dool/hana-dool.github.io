---
title: "[Introduction]"
excerpt: "기본적으로 알아둬야 하는것"
categories:
  - SQL_Basic_Grammer
tags:
  - 1
last_modified_at: 2021-08-22

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

# [Indtroduction](#link){: .btn .btn--primary}{: .align-center}

> ## 기초 Tip

- SQL 문은 대문자와 소문자를 구분하지 않는다. 
- SQL 은 한줄 또는 여러줄로 작성할 수 있다.
  - 이때에 가독성을 위해서, 내용이 달라지면 줄을 달리하자.
  - 명령어는 여러줄로 나누어질 수 없다. 즉 SEL ECT 는 불가능하다. 
- 명령어를 대문자로 작성하고, 나머지는 소문자로 작성하자.
- ctrl + 스페이스바를 누르면 추천해주는 명령어를 출력해준다. 
- ctrl + F7 을 누르면 코드를 가독성 좋게 정렬해준다.
- FROM 절에 기술되는 테이블의 순서를 가장 중심이 되는 테이블부터 기술하자.
- 논리가 복잡해지면, 서브쿼리만 따로 떼어내서 실행해보자. 
- 로직이 잘 맞지 않는다면 주석을 사용해서 점검해보자.
- 워크시트장을 여러개 띄워서 사용하자.

> ## 데이터의 구문순서

FWGHSO

1. **FROM** : SQL은 구문이 들어오면 **테이블을 가장 먼저 확인**합니다. 
2. **WHERE** : 테이블명을 확인했으니, **테이블에서 주어진 조건에 맞는 데이터들을 추출**해줍니다.
3. **GROUP BY** : 조건에 맞는 데이터가 추출되었으니, **공통적인 데이터들끼리 묶어 그룹**을 만들어줍니다.
4. **HAVING** : 공통적인 데이터들이 묶여진 그룹 중, **주어진 주건에 맞는 그룹들을 추출**해줍니다.
5. **SELECT** : 최종적으로 **추출된 데이터들을 조회**합니다.
6. **ORDER BY** : 추출된 데이터들을 **정렬**해줍니다.

위의 순서를 From where / Group by , Having / Select Order by 순으로 외우면 좋습니다. 

- From Where : raw 데이터를 가져오는 단계
- Groupby Having : 우리가 쓸 수 있게 agg 하는 단계
- Select orderby : 표시해주는 단계 

```sql
SELECT col1 as 별칭
FROM df
WHERE 별칭 >= 100
```

- 위와 같게 지정하면 에러가 납니다.  WHERE 에서 이후에 지정되는 별칭을 미리 사용했기 때문입니다.

> ## 상세 구문 순서 

- https://www.eversql.com/sql-order-of-operations-sql-query-order-of-execution/

1. FROM, including JOINs
2. WHERE
3. GROUP BY
4. HAVING
5. WINDOW functions
6. SELECT
7. DISTINCT
8. UNION
9. ORDER BY
10. LIMIT and OFFSET

> ## 문법 작성 순서

- ① SELECT 컬럼명
- ② FROM 테이블명
- ③ WHERE 조건식
- ④ GROUP BY 컬럼명
- ⑤ HAVING 조건식
- ⑥ ORDER BY 칼럼명

> ## 가독성을 높히기

- 가독성을 높히기 위해 SQL 문은 대문자로 / Col 과 Table 명은 소문자로 작성합니다.

```sql
SELECT col1,col2
FROM df
```

- 하지만 현업에서는 그냥 다 소문자로 작성합니다.. 디비버 같은 tool 을 사용하게 되면 소문자로 쓰게된다 하여도 다 변환을 해줍니다. 
