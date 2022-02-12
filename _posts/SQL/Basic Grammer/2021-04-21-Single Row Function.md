---
title:  "Single-Row Function"
excerpt: "단일행 함수"
categories:
  - SQL_Basic_Grammer
tags:
  - 1
last_modified_at: 2021-05-02

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 단일행  함수란?

한번에 하나의 데이터를 처리한 함수. 즉 그룹핑처럼 aggregate 하는게 아니라 각각의 값에 대해서 연산을 해준다고 생각하면 된다. 

- 각 행에 대해서 연산
- 데이터 타입에 맞는 함수를 사용해야한다.
- 행별로 하나의 결과를 반환
- SELECT , WHERE , ORDER BY 에서 사용할 수 있다.
- 함수속의 함수처럼 중첩해서 사용 가능. 
- 중첩해서 사용할 경우 가장 안쪽 단계에서 바깥쪽 단계의 순서가 된다.

<br>

# 데이터 타입

테이블의 열은 한가지 데이터 타입으로 지정되어 있다. 지정된 데이터 타잊과 일치하는 타입만 저장할 수 있다.

| 저장 데이터 | 데이터 타입 | 설명                                            |
| ----------- | ----------- | ----------------------------------------------- |
| 문자        | CHAR(n)     | n 길이만큼 고정 길이의 문자 타입 저장           |
| 문자        | VARCHAR2(n) | n 길이만큼 가변 길이의 문자타입 저장            |
| 숫자        | NUMBER(p,s) | 숫자 타입 저장(p: 정수 자릿수, n : 소수 자릿수) |
| 날짜        | DATE        | 날자 타입 저장                                  |

note) 이외에도 타입이 많으나, 나중에 더 알아보도록 하자.

단일행 함수에는 다음과 같이 많은 종류가 있다.

| 종류      | 설명                                                |
| --------- | --------------------------------------------------- |
| 문자 타입 | 문자를 입력받아 문자와 숫자를 반환                  |
| 숫자 타입 | 숫자를 입력받아 숫자를 반환                         |
| 날짜 타입 | 날짜에 대해 연산                                    |
| 변환 타입 | 임의의 데이터 타입의 값을 다른 데이터 타입으로 변환 |
| 일반      | NVL, CASE, WHEN, 순위함수 등                        |

<Br>

# 문자 타입 함수

| 함수    | 설명                               | 형식                                                         | 예                    | 결과 |
| ------- | ---------------------------------- | ------------------------------------------------------------ | --------------------- | ---- |
| LOWER   | 값을 소문자로 변환                 | LOWER('문자열' / 열이름)                                     | LOWER('AB')           | ab   |
| UPPER   | 값을 대문자로 뱐환                 | UPPER('문자열' / 열이름)                                     | UPPER('ab')           | AB   |
| INITCAP | 첫번째 글자만 대문자로 변환        | INITCAP('문자열' / 열이름)                                   | INITCAP('ab')         | Ab   |
| SUBSTR  | 문자열 중 일부출력                 | SUBSTR('문자열' / 열이름, 시작 위치, 길이)                   | SUBSTR('ABC',1,2)     | AB   |
| REPLACE | 특정 문자열을 찾아 바꿈            | REPLACE('문자열' / 열이름 , '바꾸려는 문자열' , '바뀔 문자열') | REPLACE('AB','A','C') | CB   |
| CONCAT  | 두 문자열 연결(\|\|)               | CONCAT('문자열'/열이름 , '문자열' / 열이름)                  | CONCAT('A','B')       | AB   |
| LENGTH  | 문자열의 길이를 구함               | LENGTH('문자열' / 열이름)                                    | LENGTH('AB')          | 2    |
| INSTR   | 문자의 위치를 구함                 | INSTR('문자열' / 열이름 , 문자)                              | INSTR('ABC','B')      | 2    |
| LPAD    | 왼쪽부터 특정 문자로 자리 채움     | LPAD('문자열' / 열이름 , 만들어질 자리수, 채워질 문자)       | LPAD('AB',4,'%')      | %%AB |
| RPAD    | 오른쪽부터 특정 문자로 자리 채움   | RPAD('문자열' / 열이름 , 만들어질 자리수, 채워질 문자)       | RPAD('AB',4,'%')      | AB%% |
| LTRIM   | 주어진 문자열의 왼쪽 문자 지우기   | LTRIM('문자열' / 열이름 , '삭제할 문자')                     | LTRIM('ABCD','AB')    | CD   |
| RTRIM   | 주어진 문자열의 오른쪽 문자 지우기 | RTRIM('문자열' / 열이름 , '삭제할 문자')                     | RTRIM('ABCD','CD')    | AB   |

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



<br>

# 숫자 타입 함수

| 함수  | 설명                          | 형식            | 예   |
| ----- | ----------------------------- | --------------- | ---- |
| ROUND | 숫자를 반올림한다.            | ROUND(13.44, 0) | 13   |
| TRUNC | 숫자를 절삭한다.              | ROUND(13.44,1)  | 13.4 |
| MOD   | 나누기 후 나머지를 구한다.    | MOD(13,4)       | 1    |
| CEIL  | 숫자를 정수로 올림            | CEIL(13.44)     | 14   |
| FLOOR | 숫자를 정수로 내림            | FLOOR(13.44)    | 13   |
| SIGN  | 양수(1), 음수(-1), 영(0) 구별 | SIGN(0.001)     | 1    |
| POWER | 거듭제곱                      | POWER(2,4)      | 16   |
| SQRT  | 제곱근                        | SQRT(4)         | 2    |



```sql
-- employees 테이블에서 salary 를 30으로 나눈 값의 소숫점 둘쨰자리에서 반올림한값
SELECT ROUND(salary/30,1)
FROM employees ; 
```

```sql
-- employees 테이블에서 salary 를 30으로 나눈 값의 소숫점을 2개만 표현(즉 3자리에서 절삭)
SELECT TRUNC(salary/30,2)
FROM employees ; 
```

<Br>

# 날짜 타입 함수

날짜 타입의 경우, 타입이 특이하기 떄문에 계산 법칙이 달라집니다. 그러므로 아래와 같이 먼저 날짜타입의 연산이 어떻게 이루어지는지 확인해봅시다.

- 날짜에 숫자를 더하거나 뺴면 날짜 결과를 출력
- 날짜에서 날짜를 빼면 두 날짜 사이의 일수를 출력
- 날짜에 시간을 더하거나 뺴려면 시간을 24로 나누어서 더하거나 뺸다.

| 날짜 연산            | 설명                        | 반환값 |
| -------------------- | --------------------------- | ------ |
| Date +/- Number      | 날짜에서 일수 더하거나 뺴기 | Date   |
| Data - DATE          | 날짜에서 날짜 빼기          | 일수   |
| Date +/- Number / 24 | 날짜에서 시간을 더하기      | Date   |

이제 날짜 함수의 종류를 알아보겠습니다.

| 날짜 함수     | 설명                                                         | 형식                          | 예시                            | 결과     |
| ------------- | ------------------------------------------------------------ | ----------------------------- | ------------------------------- | -------- |
| MONTH_BETWEEN | 두 날짜 사이의 월 수 계산                                    | MONTH_BETWEEN()               |                                 |          |
| ADD_MONTHS    | 월을 날짜에 더함                                             | ADD_MONTH(날짜, 숫자)         | ADD_MONTH(2021-04-24,5)         | 21-09-24 |
| NEXT_DAY      | 명시된 날짜로부터 돌아오는 요일에 대한 날짜 출력(1:Sunday , 2: Monday) | NEXT_DAY(날짜, 요일 / 숫자 )  | NEXT_DAY(2021-04,26 ,'금요일' ) | 21/04/30 |
| LAST_DAY      | 월의 마지막 날 계산                                          | LAST_DAY(날짜)                | LAST_DAY(21-04-03)              | 21/04/30 |
| ROUND         | 날짜를 가장 가까운 연도,월로 반올림(YEAR / MONTH)            | ROUND(날짜, 'MONTH' / 'YEAR') | ROUND('21-05-23','MONTH')       | 21/06/01 |
| TRUNC         | 날짜를 가장 가까운 연도 또는 월로 절삭(즉 내려버림)(YEAR / MONTH) | TRUNC(날짜,'MONTH')           | TRUNC('21-05-23','MONTH')       | 21/05/01 |

```sql
-- employees 테이블에서 employees_id 가 100과 106 사이인 직원의 
-- hire_date 에 3개월을 더한값을 출력
SELECT ADD_MONTHS(hire_date,3)
FROM employees
WHERE (100 <= employee_id) AND (employee_id <= 106) ; 
```

<br>

# 변환 함수

오라클 시스템은 각 열에 대해 데이터 타입을 규정하고 있다. 그러므로, sql 을 실행하기 위해서 데이터의 형식을 바꾸어야할 경우가 있다. 
<Br>

**자동 데이터 타입 변환**

SQL 문 조작시에, 데이터 타입을 자동으로 변환한다. 예를 들면 VARCHAR2 타입으로 입력되어있는 100 은, NUMBER 타입으로 변환되어 계산될 수 있다.

| FROM            | TO             |
| --------------- | -------------- |
| VARCHAR2 / CHAR | NUMBER(숫자)   |
| VARCHAR2 / CHAR | DATE(날짜)     |
| NUMBER          | VARCHAR2(문자) |
| DATE            | VARCHAR2(문자) |

```sql
SELECT 1 + '2'
FROM DUAL ; 
```

위의 출력 결과는 3이 나오게 된다.  즉 문자를 연산하였는데 Number 가 올바르게 나온것이다. 

<br>

**수동 데이터 타입 변환**

SQL 은 사용자가, 데이터 타입을 자유롭게 변환할 수 있도록 지원한다.

| 함수      | 설명                                                     |
| --------- | -------------------------------------------------------- |
| TO_CHAR   | 숫자, 문자, 날짜 값을 지정 형식의 VARCHAR2 타입으로 변환 |
| TO_NUMBER | 문자를 숫자타입으로                                      |
| TO_DATE   | 날짜를 나타내는 문자열을 날짜타입으로 변환               |



## TO_CHAR(날짜,'지정형식')

날짜 지정 형식

| 지정 형식           | 실행      | 예                       | 결과   |
| ------------------- | --------- | ------------------------ | ------ |
| CC                  | 세기      | TO_CHAR(19/02/04,'CC')   | 21     |
| YYYY / YYY / YY / Y | 년도      | TO_CHAR(21/02/04,'YYYY') | 2021   |
| Q                   | 분기      | TO_CHAR(21/02/04,'Q')    | 1      |
| MM                  | 두자리월  | TO_CHAR(21/02/04,'MM')   | 02     |
| DAY                 | 요일 이름 | TO_CHAR(21/02/04,'DAY')  | 토요일 |
|                     |           |                          |        |

<BR>

시간 지정 형식을 지정할 수도 있습니다. 

| 지정 형식        | 설명               |
| ---------------- | ------------------ |
| AM / PM          | 오전 / 오후        |
| HH / HH12 / HH24 | 시간 / 1~12 / 0~23 |
| MI               | 분 (0~59)          |
| SS               | 초 (0~59)          |

```sql
SELECT TO_CHAR(SYSDATE,'YYYY/MM/DD HH:MI:SS'),
       SYSDATE
FROM DUAL ; 
-- 2021/04/27 12:23:29 의 값이 나오게 됩니다.
```

"문자" 나 / . - 를 활용하여, 날짜와 시간 데이터를 꾸밀 수 있습니다. (문자의 경우 쌍따움표여야 합니다.)

```sql
SELECT TO_CHAR(SYSDATE,'"날짜" YYYY/MM/DD "시간" HH:MI:SS'),
       SYSDATE
FROM DUAL ; 
-- 2021/04/27 12:23:29 의 값이 나오게 됩니다.
```



## TO_CHAR(숫자,'지정형식')

숫자값을 지정한 형식의 문자열로 바꾸어준다. 

| 지정 형식 | 설명                 | 예                         | 결과               |
| --------- | -------------------- | -------------------------- | ------------------ |
| 9         | 9로 출력 자릿수 지정 | TO_CHAR(salary,'99999')    | 230 #앞에 두칸빈칸 |
| 0         | 자릿수만큼 0 출력    | TO_CHAR(salary,'09999')    | 00230              |
| $         | 달러기호             | TO_CHAR(salary,'$99999')   | $230               |
| L         | 지역 화폐 기호(원)   | TO_CHAR(salary,'L99999')   | ₩230               |
| .         | 명시한 위치에 소숫점 | TO_CHAR(salary,'99999.99') | 230.00             |
| ,         | 명시한 위치에 쉼표   | TO_CHAR(salary,'9,9999')   | 1,0000             |



## TO_NUMBER(숫자)

숫자 타입의 문자열을 숫자 데이터 타입으로 변환한다. 출력 결과는 바뀌지 않고, 데이터 타입만 바뀐다. 

```sql
TO_NUMBER('11')
-- 이 출력은 11 이 나오게 된다.
```



## TO_DATE(문자열,'지정 형식')

날짜를 나타내는 문자열을 명시된 날짜로 변환한다.

```sql
SELECT TO_DATE('20140301', 'YYMMDD')
FROM DUAL ;
-- 14/03/01 의 값이 나오게 된다. 
```

<br>

# 일반 함수

## NVL

null 값을 처리하는 함수이다. null 값은 다음과 같은 특성이 있다

- 할당되지 않았거나, 알려져 있지 않아 적용이 불가능한 값 (0,공백과는 다르다)
- null 값을 포함하는 산술 연산의 결과는 null

아래와 같이, Null 을 포함하는 연산의 경우 Null 이 나오는것을 볼 수 있다. 

![png](/assets/images/SQL_Basic/3_1.png)

NVL(열 이름 , 치환 값) 을 하게되면, null 값을 일괄적으로 변환하게 된다.

```sql
-- salary 와 work_month 를 곱하되, work_month 의 null 값에 대해서는 1로 치환하여 곱하기
SELECT salary * NVL(work_month,1) -- NVL(열 이름 , 치환 값) 
FROM employees ;
```



## DECODE

IF THEN ELSE END 의 조건 논리를 가능하게 해주는 함수이다.

```
DECODE(열 이름, 조건 값, 치환 값, 기본 값)
# 치환값 : 조건에 해당할 경우 출력할 값
# 기본값 : 조건에 해당하지 않을경우 출력할 값

DECODE(열 이름, 조건값1, 치환값1, 조건값2, 치환값2 .., 기본값)
# 위와 같이 if elif elif .. else 처럼 구현할 수도 있다. 
```

```sql
-- employees 테이블에서 원래 봉급(salary) 를 출력하고, 
-- department_id 가 60 인 경우에는 10% 인상을 출력 나머지 경우에는 아니 나는? 을 출력
SELECT salary 원_봉급,
       DECODE(department_id, 60, '10%인상' ,'아니 나는?') 조정된_봉급
FROM employees ;
```

DECODE(열 이름, 조건 )



## CASE

복잡한 조건식을 여러개 적용해야 할 때에는, DECODE 함수보다 CASE 표현식을 이용하는것이 유용하다. 

```
CASE
	WHEN 조건1 THEN 출력1
	WHEN 조건2 THEN 출력2
	...
	ELSE 출력3
END
```

```sql
-- employees 테이블에서 job_id 가 IT_PROG 라면 employee_id, first_name, last_name, salary 출력하되
-- salary 가 9000 이상이면 '상위급여' , 6000~8999 사이면 '중위급여' 그 외는 '하위급여' 라고 출력
SELECT employee_id, first_name , last_name , salary,
        CASE 
            WHEN salary >= 9000 THEN '상위급여'
            WHEN salary between 6000 and 8999 then '중위급여'
            ELSE '하위급여'
        END AS 급여등급
FROM employees 
WHERE job_id = 'IT_PROG' ;
```

![png](/assets/images/SQL_Basic/3_2.png)

## RANK, DENSE_RANK, ROW_NUMBER

RANK, DENSE_RANK, ROW_NUMBER 는 데이터 값에 순위를 매기는 함수이다. 순위를 매기는것은 동일하지만 사용법이 조금씩 다르다. 

| 함수       | 설명                                      | 순위 예       |
| ---------- | ----------------------------------------- | ------------- |
| RANK       | 공통 순위를 출력한다. 그 이후는 건너띈다. | 1 2 2 4 5 ... |
| DENSE_RANK | 공통 순위를 출력한다. 그 이후는 이어진다. | 1 2 2 3 4 ... |
| ROW_NUMBER | 공통 순위 없이 출력한다.                  | 1 2 3 4 5 ... |

```
RANK () OVER ([PARTITION BY 열이름] ORDER BY 열이름)
# [PARTITION BY 열이름] : 그룹으로 묶어서 순위를 매겨야할때에 
# ORDER BY 열이름 : 순위를 매길 열
```

```sql
-- RANK, DENSE_RANK , ROW_NUMBER 함수를 각각 이용하여, employees 테이블의 Salary 값이 높은 순서대로 순위를 매겨 출력
SELECT salary,
       RANK() OVER (ORDER BY salary) RANK,
       DENSE_RANK() OVER (ORDER BY salary) DENSE_RANK ,
       ROW_NUMBER() OVER (ORDER BY salary) ROW_NUMBER
FROM employees ;
```

![png](/assets/images/SQL_Basic/3_4.png)

## EXTRACT()

- 입력된 날짜에서 추출하고자 하는 연,월,시간 등을 반환한다.

```sql
SELECT EXTRACT(YEAR FROM SYSDATE) AS YEAR
           ,EXTRACT(MONTH FROM SYSDATE) AS MONTH
           ,EXTRACT(DAY FROM SYSDATE) AS DAY
           FROM df
```

