---
title:  "Data 형식"
excerpt: "날짜, 문자열, 등의 데이터형식"
categories:
  - SQL_Basic_Knowledge
tags:
  - 1
last_modified_at: 2021-05-31

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true 
---

# 데이터의 정의

데이터는 일반적으로 아래와 같이 정의가 된다. 즉 데이터의 구성 요소가 어떤 형식의 데이터를 가져야 하는지를 명시해주어야 한다는것이다. 이를 ORACLE 의 형태로 바꾸어주려면

![png](/assets/images/SQL_Basic/1_7.png)

아래 그림과 같이 CREATE TABLE MEMBER 와 괄호를 통해 정의해주면 된다. 

![png](/assets/images/SQL_Basic/1_8.png)



# 데이터의 유형

오라클은 다음과 같이 데이터 타입들이 있다. 우리는 Buit in data type 부터 보도록 하겠다. 맨 마지막의 파란색은 큰 데이터라는 의미이다. 

![png](/assets/images/SQL_Basic/1_9.png)

아래와 같이 데이터의 형식의 표현방식을 볼 수 있다. 문자형은 따움표를 통해서 문자라는것을 나타낸다. 날짜를 보면 시,분,초 까지 표현하면 Timestamp 가 된다.

![png](/assets/images/SQL_Basic/1_10.png)



## Character

이제 문자라는것을 표현하는 자료형은 어떻게 표현되는지 알아보아야한다. 

![png](/assets/images/SQL_Basic/2_1.png)

**1.CHAR**

- CHAR 은 가장 기본이다. 
- CHAR(size) # size 는 숫자로, 1은 1바이트를 저장할 수 있다. 
- ID에 이 형식을 넣을 수 있다. 그렇게 되면 size 에 크기를 할당한 만큼, ID 를 표현할 수 있게 된다.
- 생년월일, 성별 등에 대해서 이 형식을 쓸 수 있다.
- 하지만 ID 는 길이가 사용자마다 다르다. 이 경우 size 를 크게 해서 할당하면 되는것일까?
- 하지만 CHAR 의 경우 '고정 길이' 를 가진다. 즉 CHAR(3) 이라고 정의를 하게 된 순간, 이 데이터는 길이가 길건 작건 3바이트라는 공간을 차지하게 된다. 
- 즉 ID 를 CHAR 로 정의하게 될 경우, 불필요한 메모리 손실이 발생할 수 있다. 

**2.VARCHAR2**

- variabe character 는 위와 같은 상황에 매우 적절하다. 가변하는 문자열이라는 의미이다.
- VAR(3) 은 3 바이트의 공간을 다 쓰는게 아니다. 2바이트의 값이 들어오면 1바이트를 반환하게 된다. 즉 '최대 3바이트' 만 사용하겠다는 의미이다. 
- ID 같은 경우는 가변길이로 지정하면 좋을것이다.
- 모든 자료형을 가변으로 쓰면 되지 않을까? 이를 넣게되면 각각의 데이터가 길이가 가변이기때문에, 탐색시에 매우 느리다. (고정되어있을 경우, 어디에 데이터가 있을지 예측이 쉬워서 매우 빠름)

**3.NCHAR**

- 다양한 언어의 문자가 들어와야하는경우, National 하게 정의할 수 있다.
- 이렇게 되면, 문자마다 바이트가 다르므로, 많은 용량을 사용하게 된다. (3바이트)

**4.NVARCHAR2**

- 이 경우도 Natrional 하게 만들내는 가변길이이다



## Size

![png](/assets/images/SQL_Basic/2_1.png)

사이즈는 바이트로 측정하게 된다. 이때에 각각의 단어들은 1바이트가 한자리가 아니다 다음의 예시를 보자. 아래의 SELECT LENGTHB () FROM DUAL 은 () 안의 문자열의 바이트를 알려주는 명령어이다.

![png](/assets/images/SQL_Basic/2_2.png)

![png](/assets/images/SQL_Basic/2_3.png)

위를 보게되면, 영어의 경우 한자리당 1바이트가 할당되지만, 한국어의 경우 한자리당 3바이트가 할당되고있는것을 볼 수 있다. 즉 통상적으로 3글자인 사람 이름을 넣고싶다면 size 는 9가 필요함을 알 수 있다.

아래와 같이 테이블을 생성한 다음 살펴보자. 이때에 GENDER 의 경우, 2바이트를 넣은것을 볼 수 있다. 이때에 아래 INSERT 를 통해서 GENDER 라는곳에 VALUE 를 넣게되면 에러가 나게된다. 할당된 크기가 너무 작아, 남성이라는 단어가 못들어가는것이다. 

![png](/assets/images/SQL_Basic/2_4.png)

그래서 아래와 같이 SIZE 옆에 CHAR 를 쓰게되면 CHAR(2 CHAR) 바이트가 아니라 2글자를 넣으라는것이 된다. 아래와 같이 잘 쓰여지는것을 볼 수 있다.

![png](/assets/images/SQL_Basic/2_5.png) 

하지만 위의 경우는 바람직하지 않다. 이 이유는 NCHAR 보다 저장공간을 좀 더 차지하기 떄문이다. 아래와 같이 CHAR(2 CHAR) 로 형식을 지정하고, 그 안에 '남성' 을 넣게되면 몇바이트를 차지하는지 알아보자.  6바이트임을 볼 수 있다.

![png](/assets/images/SQL_Basic/2_6.png) 

하지만 NCHAR 로 지정하게 된다면, 4바이트로 매우 줄어든 모습을 볼 수 있다.

![png](/assets/images/SQL_Basic/2_7.png) 

이는 각각 할당하는 value 형식이 다르기 떄문인데 아래와 같이 character set 을 위해서와 Nchar character 를 저장하는 value 형식이 다른것을 볼 수 있다.

![png](/assets/images/SQL_Basic/2_8.png) 

즉 영어, 숫자가 아니고 다른나라의 언어를 쓰기 위해서는 CHAR(2,CHAR ): 문자를 캐렉터로 지정하고 저장하자 의 옵션보다는 NCHAR(2) 의 옵션이 훨씬 공간을 절약할 수 있다.

즉 우리의 Table 의 할당은 다음과 같이 정하자. 

![png](/assets/images/SQL_Basic/2_9.png) 


## Max size

![png](/assets/images/SQL_Basic/2_1.png)

위 그림을 보다시피, 환경변수가 Extended 면 약 3만 바이트까지 저장할 수 있고, Standard 일 경우에는 4000바이트가 최대값인것을 볼 수 있다. 

2000자까지 기록된다고 생각하면 된다. (나중에 이를 연장하는 옵션이 있음을 알 수 있다.)





# Ref

뉴렉쳐 유튜브 :https://www.youtube.com/channel/UC5-ixpj8DioZqmrasj6Ihpw

https://stackoverflow.com/questions/63342651/is-there-a-way-to-extract-data-from-a-mapvarchar-varchar-column-in-sql
