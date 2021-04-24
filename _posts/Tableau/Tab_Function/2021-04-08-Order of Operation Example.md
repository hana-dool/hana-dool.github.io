---
title:  "Order of operation [Example]"
excerpt: "작동의 순서 예시들"
categories:
  - Tab_Function
tags:
  - 3
last_modified_at: 2021-04-18

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# intro

태블로는 각각의 operation 에 따른, 작동 순서가 정해져있습니다. 이를 잘 앍있어야 다양한 filter, action 등을 추가할때에 정확하게 추가할 수 있습니다. 아래 그림과 같이 여러 작동들의 순서가 얽히고 있는것을 볼 수 있습니다. 이러한 순서들을 잘 숙지하고있어야합니다.

![png](/assets/images/Tableau/23_0.png)

Basic 에서 Filter 의 내용에도 같은 내용이 일부 들어있으므로 참고하세요!  아래 내용들은 <https://www.youtube.com/channel/UCaeomtvurRrHt_SWwCaOxfg> 의 내용을 적극 참조하였습니다.



# 날짜 차원 필터의 대체(LAST)

 다음과 같은 예제를 실행한다고 하자.  superstore 데이터를 이용해서 최근 2년간의 수익에 대한 12개월 이동 평균을 만들어내고 싶다고 하자. 우선 다음과 같이 주문일자와 수익의 그래프를 그리자. (https://www.youtube.com/watch?v=IRZAbkrkj60 를 참고하였습니다.)

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

무엇이 잘못된것일까? 아래 그림을 보면 알 수 있듯이, 최초 11개월은 MA 가 제대로 만들어지지 않는다. 그 이유는 MA 를 만들기 위해 필요한 값이 MA 가 만들어지기 전에 필터링되어서 빠져나갔기 떄문이다. 작동 순서를 살펴보면 아래와 같다.

![png](/assets/images/Tableau/0_3.PNG)

![png](/assets/images/Tableau/0_5.PNG)

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



#  문자열 차원 필터의 대체(Lookup)

날짜의 경우 위와 같이 Last 함수를 사용하여 Table calculation 을 사용하면 된다는것을 알았. 하지만 일반적인 문자열에 대해서는 어떻게 Table calculation 으로 filtering 할 수 있을까?

먼저 고객명을 선택하게 되면, 매출별로 ranking 을 매기고 싶은  상황을 가정하자. 우선 고객명과, 그 매출값에 따른 rank 를 매기도록 아래처럼 view 를 구성한다. 

![png](/assets/images/Tableau/0_22.PNG)

그리고 filtering 을 고객으로 하게 된다면 이 때에도 filtering 에 문제가 일어나게 된다. (테이블 계산은 dimension filtering 보다 순서가 늦기 떄문이다.)

![png](/assets/images/Tableau/0_23.PNG)

그래서 아래와 같이 고객을 filtering 하는것을 dimension 수준에서 table 수준으로 낮추고 싶다. 그럴때에는 아래와 같이 lookup 함수를 적용하자.  Lookup(Attr(고객이름),0) = 고객이 나열되어있는 리스트에서, 자기 자신의 값을 바라보자. 즉 별게 아니고 자기자신을 출력하라는 것임.

![png](/assets/images/Tableau/0_24.PNG)

그 이후에 위와 같이 계산된(table calculation 수준으로 낮추어진) 값을 이용해서 filtering 해보자. 

![png](/assets/images/Tableau/0_25.PNG)

그러면 아래와 같이, 내가 원하는 ranking 이 나오게 된다.

![png](/assets/images/Tableau/0_26.PNG)

이제 나아가서, 지역을 Filtering 하고싶을떄에는 어떻게 할까? 바로 아래 그림과 같이 위와 같은 과정을 지역에 반복해주면 된다. 

![png](/assets/images/Tableau/0_27.PNG)

이 값을 filter 에 올리고 계산하게 되면 제대로 값이 나오는것을 확인할 수 있다.

![png](/assets/images/Tableau/0_28.PNG)

![png](/assets/images/Tableau/0_29.PNG)



# Fixed LOD

아래와 같이 전체 매출의 평균이 선으로 표시되어있고, 이를 기준으로 다양한 지역을 고를때마다 그 지역의 매출의 평균이 어느정도인지를 알고싶다.

![png](/assets/images/Tableau/23_15.gif)

먼저 아래 그림처럼 지도를 시각화해주자.

![png](/assets/images/Tableau/23_1.png)

그리고 제품 대분류로 나눈 막대그래프를 시각화해보자.

![png](/assets/images/Tableau/23_2.png)

그 이후에 참조선을 각 Cell 마다 추가한다.

![png](/assets/images/Tableau/23_3.png)

그러면 아래 그림과 같이 각 Line 에 대해서 값이 나오는데, 이떄에 좀더 직관적으로 알아보기 위해서 Label 에 value 를 넣도록 하자. 

![png](/assets/images/Tableau/23_4.png)

그 이후 대시보드를 구성하면 아래와 같아진다. 

![png](/assets/images/Tableau/23_5.png)

이제 지도의 각 지역을 선택하면, 막대그래프가 그에따라 변하게 하기 위해서 아래와 같이 Filter 를 추가한다.

![png](/assets/images/Tableau/23_6.png)

하지만 이렇게 완성한 대시보드는 아래와 같이 각 나라를 클릭하게게 되면 '전체의 평균' 이 우리가 선택한 지역의 평균으로 형성되고있는것을 볼 수 있다. 

![png](/assets/images/Tableau/23_7.gif)

 그 이유는 아래와 같다. 결국 평균집계의 순서는 액션 필터보다 낮았기 떄문이다. 그러므로 전체 평균이란 '전체적인 값' 을 재는함수가 액션필터 이후에 적용되다 보니 전체값을 나타내지 못했던것이다.

![png](/assets/images/Tableau/23_8.png)

이를 고치기 위해서 다음과 같이 막대그래프로 가서, 참조선을 지우자. 현재 참조선은 Average line 으로 '집계' 이다. 즉 Action 이 있는한, 이 값이 전체평균을 나타낼수 있는 길은 없다.

![png](/assets/images/Tableau/23_9.png)

아래 그림과 같이 FIXED 를 활용하여 매출의 평균을 계산하자. FIXED 세부 수준 식은 뷰의 차원을 참조하지 않고 지정된 차원을 사용하여 값을 계산한다. 즉 우리는 제품 대분류룰 '고정' 하였으므로, 이 뒤의 filter, action 에 대해서 제품 대분류는 영향을 받지 않게된다. 즉 '전체에 대해서' 이 값은 평균을 내놓는다.  (자세한 내용은 Tab_func 참조)

![png](/assets/images/Tableau/23_10.png)

아래와 같이 Marks 에 이 변수를 올려놓는다. 우리가 참조선을 형성하려면, 데이터 패널에 있기만 해서는 사용할 수 없다. 결국 View 에 있는 값을 사용해야하기떄문이다. 이 떄에 가장 많이 이용되는것이 세부수준이다. 세부수준에 놓게되면 view 에 영향을 끼치지 않기 때문이다.

![png](/assets/images/Tableau/23_11.png)

그 이후에 Analyric 에서 Regerence Line 을 올려놓으면 우리가 생성한 값이 있음을 알 수 있다. (대분류를 고정한 평균매출) 이를 참조선으로 사용하자.

![png](/assets/images/Tableau/23_12.png)

![png](/assets/images/Tableau/23_13.png)

그러면 아래와 같이 막대가 전체에 대해서 생성되게 된다.

![png](/assets/images/Tableau/23_14.png)

이제 이를 확인해보자. 아래와 같이 '전체' 는 그대로인 상태에서, 내가 선택한 지역에 따른 매출이 나타나는것을 볼 수 있다.

![png](/assets/images/Tableau/23_15.gif)

<br>

**참고** : https://www.youtube.com/watch?v=k41o1m9xsR8

