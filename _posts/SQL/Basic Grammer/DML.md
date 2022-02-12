---
title:  "DML"
excerpt: "Data Manipulation LANGUAGE(INSERT/UPDATE/DELETE)"
categories:
  - SQL_Basic_Grammer
tags:
  - 1
last_modified_at: 2021-05-09

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# DML

- DML 은 데이터를 조작하는 명령어이다. 
- SELECT 도 DML 에 속하지만, 단시 조회 및 출력에만 국한되었다.
- 데이터를 직접 삽입, 갱신, 삭제하는 명령어를 더 배울것이다.
- 데이이터를 조작하고 저장하는 과정을 트렌젝션(Transaction) 이라 한다.
- dml 은 트랜잭션을 다루는 명령어이다. 

| 명령어 | 역할                                |
| ------ | ----------------------------------- |
| INSERT | 테이블에 새로운 행을 삽입한다.      |
| UPDATE | 테이블에 있는 행의 내용을 갱신한다. |
| DELETE | 테이블의 행을 삭제한다.             |

<BR>

# INSERT

- INSERT 는 테이블에 새로운 행을 추가할 때에 사용한다.

```sql
INSERT INTO df (col1, col2 ...)]
VALUES (val1, val2 .... )
```

<br>

# DELETE

- DELETE 는 테이블의 값을 삭제할때에 사용된다.

```sql
DELETE [FROM] 테이블 이름
[WHERE 조건식]
```

![png](/assets/images/SQL_Basic/9_1.png)

<br>

# UPDATE

- UPDATE 는 기존의 데이터값을 다른 데이터로 변경할때에 사용한다.

```sql
UPDATE df -- 변경하려는 데이터
SET col1 = val1 .....
[WEHER 조건식] ; 
```

![png](/assets/images/SQL_Basic/9_2.png)

- UPDATE 명령어도, 서브쿼리를 이용하여 대량의 데이터를 갱신할 수 있다.

```sql
UPDATE df -- 변경하려는 데이터
SET col1, .... = (SELECT col1...
                  FROM df2
                  WHERE ..
                 )
WHERE ..
```

위 식을 다음과 같이 할 수 있다.

```sql
-- department 테이블에서 department_id 가 40인 manager_id 와 location_id 의 데이터값을 찾아내고
-- department_name 이 'GG' 인 행의 manager_id 와 location_id 를 찾아낸 데이터값으로 변경
UPDATE departments
SET (manager_id,location_id) = (
        SELECT manager_id, location_id
        FROM departments
        WHERE department_id = 40) 
WHERE department_name = 'GG' ; 
```

<br>

<br>