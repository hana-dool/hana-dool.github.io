---
title:  "Table and Manipulation"
excerpt: "테이블 다루기"
categories:
  - SQL_Query_Book
last_modified_at: 2021-10-14

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 테이블을 새로 만들고 적용하기
{: .notice--warning}

# [Table Manipulation](#link){: .btn .btn--primary}{: .align-center}

> ## Table 복사하기

```sql
create table 새로만들테이블명 As(
    select * 
    from 원본테이블
    [where]
     )
```

- 위와 같이 create table 을 통하여 새로운 테이블을 만들 수 있습니다. 
- where 절은 선택입니다. (select 절을 통하여 만들어진 모든 데이터가 create 로 들어가게 됩니다.)

> ## Table 구조만 복사

```sql
create table 새로만들테이블명 as(
    select * 
    from 원본테이블
    where 1 = 2
    )
```

- 위와 같이 where 에 참이 아닌 조건을 넣게되면, 데이터가 하나도 들어있지 않은 구조만 복사되게 됩니다.

> ## Table 이 생성되어있고, 데이터만 복사

```sql
Insert into 복사될테이블명 
(select * 
from 원본테이블)
```

- 위와 같이 진행하게 된다면, 원본 테이블의 데이터가 , 복사될 테이블명에 저장되게 됩니다.

> ## Table 이름 변경

```sql
ALTER TABLE 이전테이블이름
RENAME TO 바꾸고싶은 테이블 이름; 
```

