---
title:  "width_bucket"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2021-12-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [width_bucket](#link){: .btn .btn--primary}{: .align-center}

> ## width_bucket

```sql
WIDTH_BUCKET
   (expr, min_value, max_value, num_buckets)
```

- expr : 분할할 데이터. 컬럼명이나 수식 등
- min_value : expr 값 중 분할 할 가장 작은 값
- max_value : expr 값 중 분할 할 가장 큰값
- num_buckets : 분할 할 개수
- WIDTH_BUCKET함수는 동일한 넓이를 갖는 히스토그램을 생성합니다. (동일한 높이를 갖는 히스토그램을 생성하는 NTILE함수를 비교)
- 이론적으로 각 버킷은 실수 라인의 closed-open 의 간격을 표시하게 됩니다. 
  - 예를 들어, 10은 포함하고 20은 배제되는것을 나타내기 위해서 버킷은 10.00과 19.99... 사이의 스코어를 할당할수 있다. 이것은 종종 [10,20)으로 나타낸다.

```sql
WITH 
df AS (
SELECT 1 AS age UNION
SELECT 30 UNION
SELECT 35 UNION
SELECT 37 UNION
SELECT 40 UNION
SELECT 52 UNION
SELECT 60 UNION
SELECT 77 UNION
SELECT 80 UNION
SELECT 100) 
SELECT age , WIDTH_BUCKET(age,1,101,4)
FROM df ;
```

$\begin{array}{|c|c|}
\hline \text { age } & \text { width bucket } \\
\hline 1 & 1 \\
\hline 30 & 2 \\
\hline 35 & 2 \\
\hline 37 & 2 \\
\hline 40 & 2 \\
\hline 52 & 3 \\
\hline 60 & 3 \\
\hline 77 & 4 \\
\hline 80 & 4 \\
\hline 100 & 4 \\
\hline
\end{array}$

- 이렇게 값이 나오는 이유는 버킷을 값으로 나눠서 구분하기 때문입니다. 
- 참고로 위 예에서 최대값을 101로 적은 이유는 최대값은 버킷 범위에 포함되지 않기 때문에 100을 버킷범위에 포함시키기 위해서 입니다. 

**WIDTH_BUCKET(AGE, 1, 101, 4)**

- 를하면 범위는 1~100까지가 되고, 이를 4개의 버켓으로 나누면 범위는 아래와 같이 됩니다. 
  - 1번 버킷 범위 : 1~25
  - 2번 버킷 범위 : 26~50
  - 3번 버킷 범위 : 51~75
  - 4번 버킷 범위 : 76~100
- 그래서 AGE 값이 1인것은 1번 버킷에, 30은 2번버킷, 52는 3번버킷, 77은 4번 버킷으로 분류됩니다. 
- 데이터 중에 범위를 벗어난 데이터들은 버킷번호를 가지지 못하고, 최소값보다 작은 데이터는 0을, 최대값보다 같거나 큰 데이터는 num_buckets + 1 의 값이 리턴됩니다.

```sqlite
WITH 
df AS (
SELECT 1 AS age UNION
SELECT 30 UNION
SELECT 35 UNION
SELECT 37 UNION
SELECT 40 UNION
SELECT 52 UNION
SELECT 60 UNION
SELECT 77 UNION
SELECT 80 UNION
SELECT 100) 
SELECT age , WIDTH_BUCKET(age,5,90,4)
FROM df 
order by age ; 
```

$\begin{array}{|c|c|}
\hline \text { age } & \text { width bucket } \\
\hline 1 & 0 \\
\hline 30 & 2 \\
\hline 35 & 2 \\
\hline 37 & 2 \\
\hline 40 & 2 \\
\hline 52 & 3 \\
\hline 60 & 3 \\
\hline 77 & 4 \\
\hline 80 & 4 \\
\hline 100 & 5 \\
\hline
\end{array}$

- 데이터 중에 범위를 벗어난 데이터들은 버킷번호를 가지지 못하고, 최소값보다 작은 데이터는 0을, 최대값보다 같거나 큰 데이터는 num_buckets + 1 의 값이 리턴됩니다.


