---
title:  "Functions &#58; String"
excerpt: ""
categories:
  - SQL_Basic_Grammer
last_modified_at: 2021-05-02

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

# [String Functions](#link){: .btn .btn--primary}{: .align-center}

> ## 문자 타입 함수

| 함수    | 설명                               | 형식 (T : String)                              | 예                    | 결과 |
| ------- | ---------------------------------- | ---------------------------------------------- | --------------------- | ---- |
| LOWER   | 값을 소문자로 변환                 | LOWER( T )                                     | LOWER('AB')           | ab   |
| UPPER   | 값을 대문자로 뱐환                 | UPPER( T )                                     | UPPER('ab')           | AB   |
| SUBSTR  | 문자열 중 일부출력                 | SUBSTR( T , 시작 위치, 길이)                   | SUBSTR('ABC',1,2)     | AB   |
| REPLACE | 특정 문자열을 찾아 바꿈            | REPLACE( T  , '바꾸려는 문자' , '바뀔 문자열') | REPLACE('AB','A','C') | CB   |
| RIGHT   | 문자열 왼쪽 n 개 출력              | RIGHT( T , n )                                 | RIGHT('ABCDE',2)      | DE   |
| LEFT    | 문자열 왼쪽 n 개 출력              | LEFT( T, n )                                   | LEFT('ABCDE',2)       | AB   |
| CONCAT  | 두 문자열 연결(\|\|)               | CONCAT( T1 ,  T2 )                             | CONCAT('A','B')       | AB   |
| LENGTH  | 문자열의 길이를 구함               | LENGTH( T )                                    | LENGTH('AB')          | 2    |
| INSTR   | 문자의 위치를 구함                 | INSTR( T  , 문자)                              | INSTR('ABC','B')      | 2    |
| SUBSTR  | 문자열 T의 x번째에서 y개의 문자열  | SUBSTR(T,x,y)                                  | SUBSTR('ABCDE',3,2)   | CD   |
| LPAD    | 왼쪽부터 특정 문자로 자리 채움     | LPAD( T  , 만들어질 자리수, 채워질 문자)       | LPAD('AB',4,'%')      | %%AB |
| RPAD    | 오른쪽부터 특정 문자로 자리 채움   | RPAD( T  , 만들어질 자리수, 채워질 문자)       | RPAD('AB',4,'%')      | AB%% |
| LTRIM   | 주어진 문자열의 왼쪽 문자 지우기   | LTRIM( T  , '삭제할 문자')                     | LTRIM('ABCD','AB')    | CD   |
| RTRIM   | 주어진 문자열의 오른쪽 문자 지우기 | RTRIM( T  , '삭제할 문자')                     | RTRIM('ABCD','CD')    | AB   |

- '삭제할 문자' 를 주지않으면 공백을 제거한다.

```sql
-- email 열은 첫 글자만 대문자, id 는 모두 소문자로 출력 
SELECT INITCAP(email),
	   LOWER(id)
FROM df ; 
```

```sql
-- df 테이블에서 job_id의 데이터 값에 대해 
-- 왼쪽 방향부터 F 문자를 만나면 삭제
-- 그리고 오른쪽 방향부터 T 문자를 만나면 삭제한 job_id 출력
SELECT RTRIM(LTRIM(job_id,'F'),'T')
FROM df ; 
```

```sql
-- df 테이블에서 테이블의 값에 대해서 앞 3자리 출력
SELECT SUBSTR(col1,1,3)
FROM df ; 
```

```sql
-- df 테이블에서 이름의 철자 갯수 출력
SELECT LENGTH(col1)
FROM df; 
```

```sql
-- 문자에서 특정 철자의 위치 출력
SELECT INSTR('S')
FROM df ; 
```

```sql
-- 날짜에서 / 을 지우는 쿼리
SELECT REPLACE( date,'/' , '')
FROM emp ; 
```

```sql
-- 아래와 같이 REGEXP 를 이용할수도 있다. 
-- 고용 
SELECT REGEXP_REPLACE(hiredate,'[0-3]' , '_')
FROM emp ; 
```

```sql
-- 봉급을 1000단위로 나눈 뒤 , s 를 출력하는 쿼리 
SELECT LPAD('s',ROUND(SAL/1000),'s') 
FROM emp ; 
```
