---
title:  "Functions"
excerpt: "테블로 함수들에 대해 알아보자"
categories:
  - Tableau
tags:
  - 1
last_modified_at: 2021-02-09

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# Intro

- 테블로를 파이썬에서 어느정도 처리(정규화....) 한 뒤에 받는다 하더라도 계속 Python 과 같이 쓸 수는 없다.
- 최댓값, 스케일링, 제외, 필터링 등의 어느정도 간단한 연산은 알고 있어야, 즉석에서 변수를 변화시키면서 다양한 visualization 이 가능하다.
- 즉 이를 위해서는 테블로의 함수식에 대해서 잘 알아두어야 한다!
- 테블로 공식 사이트에서, 많은 함수식을 확인할 수 있으나 '너무 많다.' 여기에서는 어느정도 사용이 되는 함수들을 정리하자.



# 숫자함수

- ABS() : 절댓값 반환
- DIV(a,b) : a 를 b 로 나누는 연산의 몫만 출력
  - DIV(11,2) = 5
- MAX(a,b) : a,b 중 큰 값 반환
- MIN(a,b) : a,b 중 작은값 반환
- ROUND(num,[decimals]) : 숫자를 지정한 자릿수로 반올림
  - ROUND(3.5,1) = 4
- ZN(expression) : Null 이 아니면 식을 반환, Null 이면 0을 반환



# 문자열

- CONTAINS(string,substring) : 주어진 문자열에 지정한 부분 문자열이 포함되어 있으면 true를 반환.
  
  - ex)CONTAINS(“Calculation”, “alcu”) = true
- ENDSWITH(string, substring) : 주어진 문자열이 지정한 부분 문자열로 끝나면 true를 반환합니다. 후행 공백은 무시됩니다
  
- ex)ENDSWITH(“Tableau”, “leau”) = true
  
- LEN(string) : 문자열의 길이를 반환합니다.
  
- LEN("Matador") = 7
  
- RIGHT(string, number)  : string에서 가장 오른쪽에 있는 문자 수를 반환합니다.
  
- RIGHT("Calculation", 4) = "tion"
  
- SPLIT(string, delimiter, token number)  : 구분 기호 문자를 사용하여 문자열을 토큰 시퀀스로 분할하는 방식으로 문자열에서 부분 문자열을 반환합니다.
  
  - SPLIT (‘a-b-c-d’, ‘-‘, 2) = ‘b’
  
- $$
    SPLIT (‘a|b|c|d’, ‘|‘, -2) = ‘c’
    $$
  
- DATEDIFF(date_part, date1, date2, [start_of_week])  date_part 단위로 표시된 date1과 date2의 차이를 반환합니다.
  
- 주의 첫 번째 일로 고려할 요일을 지정할 때 사용할 수 있는 start_of_week 매개 변수는 선택 사항입니다. 가능한 값은 'monday', 'tuesday' 등입니다. 생략되면 주 시작은 데이터 원본에 의해 결정됩니다. 데이터 원본의 날짜 속성을 참조하십시오.
  
- DATENAME(date_part, date, [start_of_week]) date의 date_part를 문자열로 반환합니다.
  - DATENAME('year', #2004-04-15#) = "2004"
  - DATENAME('month', #2004-04-15#) = "April"

- DATEPART(date_part, date, [start_of_week])
  - date의 date_part를 정수로 반환합니다.
  - DATEPART('year', #2004-04-15#) = 2004
  - DATEPART('month', #2004-04-15#) = 4

- MONTH(#2004-04-15#) = 4

- WEEK (#2004-04-15#) = 16

- YEAR(#2004-04-15#) = 2004

​    

# 논리함수

**expr1 IN expr2**

expr1의 값이 expr2의 값 중 하나와 일치하는 경우 TRUE를 반환합니다.

SUM([Cost]) IN (1000, 15, 200)

---

**IF expr1 AND expr2** 

**THEN then END** 

두 식에 대한 논리곱을 수행합니다.

IF (ATTR([Market]) = "Africa" AND SUM([Sales]) > [Emerging Threshold] )THEN "Well Performing"

---

**CASE (expression>** 

**WHEN (value1> THEN (return1>** 

**WHEN (value2> THEN (return2> ...**

**ELSE (default return>** 

**END**

논리 테스트를 수행하고 적절한 값을 반환합니다. CASE 함수는 expression을 평가하고 value1, value2 등의 일련의 값과 비교한 다음 결과를 반환합니다. expression과 일치하는 값이 있으면 CASE가 해당 반환 값을 반환합니다. 일치 항목이 없으면 기본 반환 식이 사용됩니다. 기본 반환이 없고 일치하는 값도 없으면 Null이 반환됩니다.

CASE [Region] 

WHEN 'West' THEN 1 

WHEN 'East' THEN 2 

ELSE 3 END



CASE LEFT(DATENAME('weekday',[Order Date]),3)

WHEN 'Sun' THEN 0 

WHEN 'Mon' THEN 1 

WHEN 'Tue' THEN 2 

WHEN 'Wed' THEN 3 

WHEN 'Thu' THEN 4 

WHEN 'Fri' THEN 5 

WHEN 'Sat' THEN 6 

END

---

**IF (expr) THEN (then)** 

**ELSE (else)** 

**END** 

일련의 식을 테스트하여 true인 첫 번째 (expr)에 대해 (then) 값을 반환합니다.

If [Profit] > 0 THEN 'Profitable' ELSE 'Loss' END

​    

---

**IF (expr) THEN (then)** 

**ELSEIF (expr2) THEN (then2)...**

**ELSE (else)** 

**END** 

일련의 식을 테스트하여 true인 첫 번째 (expr)에 대해 (then) 값을 반환합니다.



IF [Profit] > 0 THEN 'Profitable' 

ELSEIF [Profit] = 0 THEN 'Breakeven' 

ELSE 'Loss' END

---

**IFNULL(expr1, expr2)** 

null이 아니면 (expr1)을 반환하고, null이면 (expr2)를 반환합니다.

IFNULL([Profit], 0)

---

**IIF(test, then, else, [unknown])** 

조건이 충족되는지 여부를 확인하여, TRUE이면 첫 번째 값을 반환하고, FALSE이면 두 번째 값을 반환하며, 알 수 없는 값일 경우 선택적 입력 값인 세 번째 값 또는 NULL을 반환합니다.

IIF([Profit] > 0, 'Profit', 'Loss')

---

**ISNULL(expression)** 

식이 유효한 데이터를 포함하지 않는 경우(Null인 경우) true를 반환합니다.

ISNULL([Profit])

---

**NOT**

식에 대한 논리 부정을 수행합니다.

IF NOT [Profit] > 0 THEN "Unprofitable" 

END

---

**OR** 

두 식에 대한 논리합을 수행합니다.

IF [Profit] ( 0 OR [Profit] = 0 THEN "Needs Improvement" 

END

---

**ZN(expression)** 

null이 아니면 (expression)을 반환하고, 그렇지 않으면 0을 반환합니다.

ZN([Profit]) : Profit 에 Null 이 있을때, 0 으로 바꾸고 싶다면 ZN([Profit]) 을 새로 지정해줍니다.

ZN(LOOKUP(SUM([매출]),0)) : 만든 ‘테이블’ 에서, 공란이 나온경우(NA 떄문이 아니라 애초에 그 CELL 에 해당하는 값이 없었기 때문) 이렇게 Lookup 을 이용해 zn 으로 채워주면 lookup 은 순전히 ‘테이블 위의 값’ 만을 보고 계산하기 떄문에 0을 채울 수 있습니다. 



# 집계함수

​    

- AVG(expression)

식에서 모든 값의 평균을 반환합니다. AVG는 숫자 필드에서만 사용할 수 있습니다. Null 값은 무시됩니다.



- COUNT(expression)

그룹의 항목 수를 반환합니다. Null 값은 계산되지 않습니다.

  

- COUNTD(expression)

그룹의 고유 항목 수를 반환합니다. Null 값은 계산되지 않습니다.

​    

- MIN(expression)

모든 레코드에 대한 식의 최소값을 반환합니다. 식이 문자열 값이면 이 함수는 사전순으로 정의된 첫 번째 값을 반환합니다.

​    

- MAX(expression)

모든 레코드에 대한 식의 최대값을 반환합니다. 식이 문자열 값이면 이 함수는 사전순으로 정의된 마지막 값을 반환합니다.

​    

- MEDIAN(expression)

모든 레코드에 대한 식의 중앙값을 반환합니다. 중앙값은 숫자 필드에서만 사용할 수 있습니다. Null 값은 무시됩니다.

​    

- PERCENTILE(expression, number)

지정한 수에 해당하는 지정된 식에서 백분위수 값을 반환합니다. 수는 0과 1을 포함하여 0에서 1 사이(예: 0.66)의 숫자 상수여야 합니다.

​    

- STDEV(expression)

샘플 모집단을 기준으로 주어진 식에 있는 모든 값의 통계적 표준 편차를 반환합니다.

​    

- SUM(expression)

식에서 모든 값의 합계를 반환합니다. SUM은 숫자 필드에서만 사용할 수 있습니다. Null 값은 무시됩니다.

​    

- VAR(expression)

샘플 모집단을 기준으로 주어진 식에 있는 모든 값의 통계적 분산을 반환합니다.



# 테이블 계산 함수

- First()

  현재 행에서 파티션에 있는 첫번째 행까지의 행 수를 반환한다. (이 경우 measure 가 0까지와의 거리가 되어서, 행이 3 행일 경우 -2 가 출력된다.)

- Last()

  현재 행에서 마지막 행 까지의 행 수를 반환한다. 이 경우 measure 은 마지막 행까지의 거리가 된다. (양수)

- Lookup(expression,offset)

  현재 행 기준, 오프셋으로 지정된 대상 행에서, 식의 값을 반환한다.  