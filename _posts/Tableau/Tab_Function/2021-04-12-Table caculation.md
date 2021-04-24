---
title:  "Table Calculation"
excerpt: "테이블 계산"
categories:
  - Tab_Function
tags:
  - 3
last_modified_at: 2021-04-12

use_math : true
---

# First

현재 행에서 첫번쨰 행까지의 행 수를 반환한다. lookup 과 같이 쓰이면, 늘 첫번째 값을 표현하게 된다.

![png](/assets/images/Tab_Fun/1_5.png)

# Last

마지막까지의 행 수를 반환한다. lookup 과 같이 쓰이면, 늘 마지막 값을 표현하게 된다.

![png](/assets/images/Tab_Fun/1_6.png)

# Index

현재 행의 인덱스를 반환한다.

![png](/assets/images/Tab_Fun/1_7.png)

# Lookup

그림을 다시 보게되면, 각각의 값에 대해서 어떻게 계산이 이루어지는지 가늠할 수 있다. LOOKUP(expression, [offset])  이란, 아래 그림처럼 현 행 기준으로 지정된 위치에서 offset 만큼 이동해서 그 값을 출력해주는것이다. 아래는 lookup(sum[sales],2) 를 적용한 함수이다. 

![png](/assets/images/Tab_Fun/1_2.png)

## Lookup + First, Last

다음과 같이 구성된 테이블을 보면서, first , last 와 lookup 이 같이 쓰이면 어떤 효과를 내는지 알아보자.

![png](/assets/images/Tab_Fun/1_1.png)

위 그림을 보게되면 각각의 measure values 에 대해서 정의한 값이 보인다. 정의는 아래와 같이 하였다.

- first : first()
- last : last()
- lookup_-1 : lookup(sum([매출]),-1)
- lookup_+1 : lookup(sum([매출]),+1)
- lookup_first : lookup(sum([매출]),first())
- lookup_last : lookup(sum([매출]),last())

![png](/assets/images/Tab_Fun/1_1.png)

위 그래프를 다시보자. first : 0을 처음행에 두고 뒤로갈수록 -1  , last : 0을 마지막 행에 두고 앞으로 올수록 + 1 임을 기억하자. 즉 lookup 과 함께 쓰이면 lookup_first 는 늘 첫쨰항을 출력하게 되고, lookup_last 는 늘 마지막항을 출력하게됨을 알 수 있다. 

## Compute using

lookup 을 할 때에도 행 기준으로 볼 것인지, 열 기준으로 볼 것인지에 따라 값이 다르게 된다. 다음과 같이 Compute using Table(acoss) 를 하게 된다면, 가로로 가로질러 (ㅎㅎ!) 계산하게 된다. 그러므로 lookup_first 를 통해 첫 값을 보라고 하면, 각 row 별로 첫번쨰 값을 보게된다.

![png](/assets/images/Tab_Fun/1_3.png)

그에 반해 다음과 같이 Compute using Table(down) 을 선택할 수 있다. 이 경우 세로로 보겠다는 뜻이다. 아래와 같이 각 분기별로 첫 값을 나타내고 있음을 볼 수 있다.

![png](/assets/images/Tab_Fun/1_4.png)

