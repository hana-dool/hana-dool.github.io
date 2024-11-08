---
title:  "Grouping Set"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2021-05-08

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

# [Grouping Set](#link){: .btn .btn--primary}{: .align-center}

> ## 집합 연산자

우리가 계속 해온 join 기법은 , 다음과 같이 이루어졌다. 

```sql
FROM 데이터
WHERE 조건
```

이러한 기법 외에도, 테이블에서 데이터를 조회하는 방법이 더 있다. 바로 Set operator 를 활용하는것이다.

| 종류               | 설명                                                        |
| ------------------ | ----------------------------------------------------------- |
| UNION (합집합)     | SELECT 문의 조회 결과의 합집합. 중복되는 행은 한 번만 출력  |
| UNION ALL (합집합) | SELECT 문의 조회 결과의 합집합. 중복되는 행도 그대로 출력   |
| INTERSET (교집합)  | SELECT 문의 조회 결과의 교집합. 중복되는 행만 출력          |
| MINUS (차집합)     | 첫 번째 SELECT 문의 조회 결과에서 두 번째 조회 결과를 뺀다. |

```sql
SELECT col1 , col2 ....
FROM df
집합 연산자

SELECT 	col1, col2 ...
FROM df
```

- 첫번째 SELECT 에서 기술한 열과, 두번째 SELECT 에서 기술한 열은 왼쪽부터 순서대로 1:1 대응한다.
- 열 개수 , 데이터 타입이 일치해야해야한다.
- 열 순서가 다르면 에러가 난다. 
- SELECT 문에 대한 연산은 위에서 아래로 수행된다. 
- ORDER BY 는 맨 끝에 기술된다.

> ## UNION 

- SQL 문을 이용하여, SELECT 문의 실행 결과를 집합 하나로 묶을 수 잇다.
- 즉 각기 다른 SELECT 문을 이용해 실행한 결과를 하나로 출력할 수 있다.

![png](/assets/images/SQL_Basic/7_1.png)

- 위 출력결과가 의미하는것은 employees 테이블과, department 테이블에서, 유일한 값을 가지는 department_id 데이터가 총 28 건이라는 의미이다.

> ## UNION ALL

- UNION ALL 은 UNION 과 거의 동일하지만, 중복열도 모두 출력한다는것이 다르다. 

![png](/assets/images/SQL_Basic/7_2.png)

위 출력결과가 의미하는것은, employees 07개 데이터와 department 27개 데이터를 합쳐서 134건을 출력한 것이다.

> ## INTERSECT

- INTERSECT 는 양쪽 SELECT 에 겹치는 데이터만 출력한다. 

![png](/assets/images/SQL_Basic/7_3.png)

양쪽 SELECT 문에 모두 존재하는 행이 출력되었다. 이 값들은 employees 데이터와 department 데이터에 같이 겹치는 deparment_id 이다.

> ## MINUS

- MUNUS 연산자는 첫번째 SELECT 결과 - 두번쨰 SELECT 결과 로 이루어져 있습니다. 
- 차집합이라고 생각하시면 됩니다. 

![png](/assets/images/SQL_Basic/7_4.png)

위의 결과는 department 데이터에서 employees 데이터를 뺸것과 같다. 