---
title:  "Tableau Structure"
excerpt: "테블로의 기초에 대해 알아보자"
categories:
  - Tableau
tags:
  - 3
last_modified_at: 2021-02-13

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# 데이터 유형

- 테블로에는 여러 데이터 유형이 있다.

  - 여러 유형의 데이터를 아이콘으로 보여주게 된다.
  - 이때에 파란색은 차원을 의미하고(categorical data) 초록색은 측정값(values)를 의미한다.

  ![png](/assets/images/Tableau/0_2.PNG)

- 각 아이콘에 대한 의미는 아래와 같다.

  ![png](/assets/images/Tableau/0_1.PNG)

- 각 데이터를 유형에 맞게 변형시켜서 사용해야할 것이다.
  - ex) 시/도 는 지리적 역활을 부여해야한다.
  - ex) 년도는 날짜적 역활을 부여해야한다.



# 작동 순서

기본적인 작업의 순서는 아래 그림과 같다. 태블로는 아래의 파이프라인의 순서를 따르면서 작업을 수행하게 된다. 계산과 필터의 작동 순서는 복잡하지만 체계적으로 구조화 되어있다. 아래 Last 필터를 적용하는것을 보면서 작동 순서가 어떻게 되는지에 대해서 알아보자.  (이 부분은 Filter 에도 추가하였습니다.) (https://www.youtube.com/watch?v=IRZAbkrkj60 를 참고하였습니다.)

![png](/assets/images/Tableau/0_3.PNG)

![png](/assets/images/Tableau/0_5.PNG)

위를 잘 이해하기 위해서, 다음과 같은 예제를 실행한다고 하자.  superstore 데이터를 이용해서 최근 2년간의 수익에 대한 12개월 이동 평균을 만들어내고 싶다고 하자. 우선 다음과 같이 주문일자와 수익의 그래프를 그리자.

 ![png](/assets/images/Tableau/0_6.PNG)

이제 이동평균이였으므로 수익의 table calculation 을 add 하자. (add 라고 되어있지만 고치는것임)

 ![png](/assets/images/Tableau/0_7.PNG)

이제 아래에서 Moving everage 를 선택한다. 그리고 prev 11 을 선택하다. (이때 prev 11 을 선택할때에 아래에 Current value 에 체크하는 란이 있다. 여기에 체크하면 본인을 포함한다는 의미이므로 12개월에 대한 이동평균이 된다.)

![png](/assets/images/Tableau/0_8.PNG)

그 이후에 아래와 같이 2017 ~ 2018 년의 변화만 보고싶기에 filter 를 추가한다.

![png](/assets/images/Tableau/0_9.PNG)

그러면 아래와 같이 값이 나오게 된다... 그런데! 이때 이 값이 과연 잘 나온 값일까?

![png](/assets/images/Tableau/0_10.PNG)

Moving average 가 잘 작동되는지 조사하기 위해 아래 그림처럼 Table 을 만들어 보았다.

![png](/assets/images/Tableau/0_11.PNG)

무엇이 잘못된것일까? 아래 그림을 보면 알 수 있듯이, 최초 11개월은 MA 가 제대로 만들어지지 않는다. 그 이유는 MA 를 만들기 위해 필요한 값이 MA 가 만들어지기 전에 필터링되어서 빠져나갔기 떄문이다.

![png](/assets/images/Tableau/0_12.PNG)

테이블 계산식은 작동 순서가 늦은편이다. 이 이유는 단순한데, 아래 그림처럼 먼저 '집계' 가 이루어진 이후에나 테이블 계산이 만들어질 수 있기 떄문이다. 

![png](/assets/images/Tableau/0_13.PNG)

이 이유는 필터 와 calculation 적용 순서 표에서도 알 수 있는데, 아래 그림과 같이 dimension filter 가 먼저 적용되어서 뒤의 Table Calculation 이 제대로 작동되지 않은것이다.

![png](/assets/images/Tableau/0_14.PNG)

그렇다면 어떻게 해야할까? 바로 filter 를 계산하기 전에 먹이는게 아니라, 계산 이후에 필터를 먹여야 한다. 즉 Table calculation 이후에 Table calculation filter 를 먹여주면 된다.

![png](/assets/images/Tableau/0_15.PNG)

![png](/assets/images/Tableau/0_16.PNG)

우선 아래 그림과 같이 Last 라는 함수를 생성한다. 이는 Table 함수로, Table 에 나타나는 순서에 따라서 순위를 표시한다. 

![png](/assets/images/Tableau/0_16.PNG)

![png](/assets/images/Tableau/0_17.PNG)

![png](/assets/images/Tableau/0_18.PNG)

이때에 우리는 Dimension filter 가 아니라,  Table calculation filter 를 사용해야 한다. 그러므로  Last() 라는 변수르 12~35까지 filtering 하면 될 것이다.

 ![png](/assets/images/Tableau/0_19.PNG)

이제 filter 를 통해서 범위를 지정해준다. (year/month 로 이루어진 필터는 버려버린다!)

![png](/assets/images/Tableau/0_20.PNG)

그럼 드디어 제대로 이동평균이 구성되어있는것을 볼 수 있다. table calulation filter 는 table 계산이 이루어진 이후에 적용되기 떄문이다. 

![png](/assets/images/Tableau/0_21.PNG)