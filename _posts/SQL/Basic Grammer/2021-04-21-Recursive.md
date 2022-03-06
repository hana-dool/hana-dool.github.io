---
title:  "Recursive"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2022-03-03

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

# [Recursive](#link){: .btn .btn--primary}{: .align-center}

> ## 기본 구조 

- 스스로를 참조하는 쿼리입니다.

```sql
WITH RECURSIVE cte_name AS (
    initial_query  -- anchor member
    UNION ALL
    recursive_query -- recursive member that references to the CTE name
)
SELECT * FROM cte_name;
```

- Recursive CTE는 세 가지 주요 부분으로 구성됩니다.
  - CTE 구조의 기본 결과 집합을 형성 하는 초기 쿼리 (앵커라고도 함)
  - 재귀 쿼리 부분은 CTE 이름을 참조하는 쿼리이므로 재귀 멤버라고 합니다. 재귀 멤버는 `UNION ALL`또는 `UNION DISTINCT` 연산자로 앵커 멤버와 결합됩니다.
  - 재귀 멤버가 행을 반환하지 않을 때 재귀가 중지되도록 하는 Termination Condition
- Recursive CTE의 실행 순서는 다음과 같습니다.
  1. 먼저 멤버를 앵커 멤버와 재귀 멤버로 분리합니다.
  2. 다음으로 앵커 멤버를 실행하여 기본 결과 집합( `R0`)을 형성하고 이 기본 결과 집합을 다음 반복에 사용합니다.
  3. 그런 다음 `Ri` 결과 집합을 입력으로 사용 하여 재귀 멤버를 실행하고 `Ri+1` 을 출력합니다. 
  4. 그런 다음 재귀 멤버가 빈 결과 집합을 반환할 때까지, 즉 종료 조건이 충족될 때까지 3 단계를 반복합니다.
  5. `UNION ALL`마지막으로 연산자 를 사용하여 R0에서 Rn까지 결과 집합을 결합합니다 .

> ## Example

- 다음의 간단한 재귀 CTE 의 예시를 참조해봅시다.

```sql
WITH RECURSIVE cte_count (n) 
AS (
      SELECT 1
      UNION ALL
      SELECT n + 1 
      FROM cte_count 
      WHERE n < 3
    )
SELECT n 
FROM cte_count;
```

- 이떄 아래 쿼리를 봅시다. 

```sql
SELECT 1
```

- 이 쿼리는 앵커 멤버로서, Base Result set 으로서 1 을 return 합니다.
- 그 다음 쿼리

```sql
SELECT n + 1
FROM cte_count 
WHERE n < 3
```

- 이 쿼리는 recursive member 입니다. 왜냐하면 CTE 의 이름인 `cte_count` 를 참조하고 있기 떄문입니다.
- expression`n < 3` 은 termination condition 입니다.
  - 만약 n = 3  이 된다면 위 조건을 지키지 못하게 되므로, recursive member 는 empty set 을 return 하고 이는 recursion 을 정지하게 만듭니다.

> 작동 순서

![jpg](/assets/images/Program/71_9.jpg){: .align-center}

- 종합하면 위와 같이 작동하게 됩니다.

```sql
WITH RECURSIVE cte_count (n) 
AS (
      SELECT 1
      UNION ALL
      SELECT n + 1 
      FROM cte_count 
      WHERE n < 3
    )
SELECT n 
FROM cte_count;
```

```
n|
-+
1|
2|
3|
```

- 즉 이를 실행하면 위와 같은 결과가 나오게 됩니다.

> 실행 절차

- The execution steps of the recursive CTE is as follows:
  1. First, separate the anchor and recursive members.
  2. Next, the anchor member forms the initial row ( `SELECT 1`) therefore the first iteration produces 1 + 1 = 2 with n = 1.
  3. Then, the second iteration operates on the output of the first iteration (2) and produces 2 + 1 = 3 with n = 2.
  4. After that, before the third operation ( n = 3), the termination condition ( `n < 3`) is met therefore the query stops.
  5. Finally, combine all result sets 1, 2 and 3 using the `UNION ALL` operator

> ## Example

- `ANIMAL_OUTS` 테이블은 동물 보호소에서 입양 보낸 동물의 정보를 담은 테이블입니다. `ANIMAL_OUTS` 테이블 구조는 다음과 같으며, `ANIMAL_ID`, `ANIMAL_TYPE`, `DATETIME`, `NAME`, `SEX_UPON_OUTCOME`는 각각 동물의 아이디, 생물 종, 입양일, 이름, 성별 및 중성화 여부를 나타냅니다.

| NAME             | TYPE       | NULLABLE |
| ---------------- | ---------- | -------- |
| ANIMAL_ID        | VARCHAR(N) | FALSE    |
| ANIMAL_TYPE      | VARCHAR(N) | FALSE    |
| DATETIME         | DATETIME   | FALSE    |
| NAME             | VARCHAR(N) | TRUE     |
| SEX_UPON_OUTCOME | VARCHAR(N) | FALSE    |

- 보호소에서는 몇 시에 입양이 가장 활발하게 일어나는지 알아보려 합니다. 0시부터 23시까지, 각 시간대별로 입양이 몇 건이나 발생했는지 조회하는 SQL문을 작성해주세요. 이때 결과는 시간대 순으로 정렬해야 합니다.
- SQL문을 실행하면 다음과 같이 나와야 합니다.

| HOUR | COUNT |
| ---- | ----- |
| 0    | 0     |
| 1    | 0     |
| 2    | 0     |
| 3    | 0     |
| 4    | 0     |
| 5    | 0     |
| 6    | 0     |
| 7    | 3     |
| 8    | 1     |
| 9    | 1     |
| 10   | 2     |
| 11   | 13    |
| 12   | 10    |
| 13   | 14    |
| 14   | 9     |
| 15   | 7     |
| 16   | 10    |
| 17   | 12    |
| 18   | 16    |
| 19   | 2     |
| 20   | 0     |
| 21   | 0     |
| 22   | 0     |
| 23   | 0     |

> Answer

```sql
WITH RECURSIVE TEMP AS (
    SELECT 0 AS HOUR
    UNION ALL
    SELECT HOUR+1 FROM TEMP
    WHERE HOUR<23
)
SELECT HOUR, COUNT(ANIMAL_OUTS.DATETIME) AS COUNT 
FROM TEMP 
LEFT JOIN ANIMAL_OUTS
ON TEMP.HOUR = HOUR(ANIMAL_OUTS.DATETIME)
GROUP BY HOUR;
```

