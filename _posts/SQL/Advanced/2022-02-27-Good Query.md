---
title: "[Introduction]"
excerpt: "기본적으로 지켜야할것"
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
---

# [Indtroduction](#link){: .btn .btn--primary}{: .align-center}

## 

- 실무에서 데이터 분석가에게 가장 필요한 기술 중 하나는 SQL 쿼리를 작성하는 능력입니다. 
- 이 때, 단순히 원하는 데이터를 추출하는 것에서 더 나아가 가독성 좋은 구문을 작성할 수 있다면 더욱 좋겠죠. 
  - 아래 링크는 좋은 쿼리문을 작성하는데 필요한 내용이 잘 정리되어 있습니다. 위 내용의 좀 더 간략한 버전으로 https://towardsdatascience.com/writing-good-sql-ccb578ff9919 도 같이 보시면 좋을 것 같네요.

> ## 대문자와 소문자 

- SELECT, FROM, WHERE 와 같은 예약어는 대문자로 그 외에 테이블명이나 컬럼명 등은 소문자로 작성 
- 각 예약어는 오른쪽 정렬이 되게 작성한다.

> ## 서브쿼리

- 서브 쿼리 대신 WITH 절과 파이프 연산자를 활용한다.

> ## 복잡한 조건문 

- 조건문이 복잡할 경우 BETWEEN 과 IN 을 적절히 활용한다. (BETWEEN은 다중 AND 조건을, IN은 다중 OR 조건을 각각 대체할 수 있습니다.)

> ## Avoid using Asterik(*)

- 테이블에 컬럼 수가 적으면 괜찮을지 모르지만, 컬럼 수가 많을 때 asterik를 쓰면 실제 쿼리에 필요 없는 컬럼까지 색인하게 되므로 쿼리 성능이 떨어질 수 있다. 
- 또 개인적인 경험으로는 내가 만들지 않은 쿼리를 다룰 때 *로만 표기되어 있으면 어느 컬럼을 추출하려는지 확실하지 않아 코드의 목적을 파악하기가 어려울 때가 있었다. 
  - 그러면 쿼리를 수정해야 하는지, dto를 손봐야 하는지 헷갈리기도 했다.

> ## EXISTS, NOT EXISTS than IN, NOT IN

- EXISTS, IN 모두 서브쿼리를 활용할 때 사용할 수 있는 구문이다. 
  - EXISTS가 훨씬 선호되는데 가장 큰 이유는 EXISTS는 해당 서브쿼리에 해당하는 값이 하나라도 있으면 검색을 멈추지만, IN의 경우는 모든 인덱스를 검색하기 때문에 성능 상의 차이가 난다. 
- 같은 맥락으로 검색하는 경우가 아니고서는 LIKE보다 항등연산자(=)를 사용하는 것이 바람직하다.

> ## Reference 

- https://www.dpriver.com/blog/2011/09/27/a-list-of-sql-best-practices/
- https://codingsight.com/sql-query-optimization-tips/
