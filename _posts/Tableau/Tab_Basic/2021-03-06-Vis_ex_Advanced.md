---
title:  "Vis_Advanced_Ex"
excerpt: "시각화 고급 예시들"
categories:
  - Tableau
tags:
  - 3
last_modified_at: 2021-03-10

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# <center><font size="20"> 파레토 차트 </font></center>

파레토 차트는 막대와 라인그래프를 모두 포함하는 차트이다. 선 그래프는 누적 그래프가 되고, 막대 그래프는 각각의 값을 나타나게 된다. 

![png](/assets/images/Tableau/18_1.PNG)

이제 어떻게 만드는지 한번 같이 만들어보자. 

아래와 같이 하나의 범주에 대해서 수치값을 그리게 되면 막대그래프가 형성되게 된다.

![png](/assets/images/Tableau/18_2.PNG)

이제 같은 수치값을 Dual axis 로 붙여넣는다. 이때에는 매출이 될 것.

![png](/assets/images/Tableau/18_3.PNG)

붙여넣게 되면 다음과 같이 형성이 된다.(둘다 같은 수치형이라 Mark card 가 늘어난거 말고는 아무런 변화가 없다.)

![png](/assets/images/Tableau/18_4.PNG)

두개의 마크 카드 중 하나의 값에 대해서 Line 차트로 바꾸자

![png](/assets/images/Tableau/18_5.PNG)

이제 저 라인을 누적값으로 바꾸면 될 것이다. ROW 선반에서 Table calculation 을 추가하자.

![png](/assets/images/Tableau/18_6.PNG)

그리고 그 안에서 Running total 을 주요 calculation 으로 설정한다. 그 이후 Secondary Calculation 을 Percent of Total 로 지정한다. 

![png](/assets/images/Tableau/18_7.PNG)

그 이후 Line 의 색을 좀 더 보기좋게 설정하면 아래 그림과 같아진다. 

![png](/assets/images/Tableau/18_8.PNG)

<BR>

# <center><font size="20"> Betterfly 차트</font></center>

나비 차트란 아래와 같이 두개의 구분값에 대해 확연히 그 추이를 비교하면서 알 수 있게 해주는 차트이다.

![png](/assets/images/Tableau/18_17.PNG)

우선 우리가 시각화를 적용하려는 파일을 살펴보자

![png](/assets/images/Tableau/18_9.PNG)

우리가 원하는건 Gender 별로 위 예시에서와 같이 나비 차트를 나이의 구간별로 만들고싶다.  그러므로 아래 그림과 같이 Age 를 구간차원으로 만든다. 

![png](/assets/images/Tableau/18_10.PNG)

그리고 Bins 를 수정하는데 다음과 같이 이름을 알기 쉽게 수정하고, bins 의 사이즈를 10으로 조절한다.

![png](/assets/images/Tableau/18_11.PNG)

그 이후 위에서 조절한 구간차원을 적용하면 아래 그림과 같다.

![png](/assets/images/Tableau/18_12.PNG)

이제 남 / 여 를 구분하기 위해서 Gender 가 여자일때에는 여자인구 / 남자일때에는 남자인구를 출력해주는 Calculation field 를 구성한다.

![png](/assets/images/Tableau/18_13.PNG)

이제 위에서 수정한 Calculation field 를 col 선반에 올려놓으면 다음과 같아진다. 

![png](/assets/images/Tableau/18_14.PNG)

이제 남자 인구수를 반전시키면 딱 맞아보인다. 남자인구의 Axis에서 Edit 을 들어간다. 

![png](/assets/images/Tableau/18_15.PNG)

그 이후 Scale 을 Reversed 로 하게되면 그림과 같이 나비차트가 완성된다.

![png](/assets/images/Tableau/18_16.PNG)

이제 색상을 보기좋게 바꾸면 예시와 같이 완성~

![png](/assets/images/Tableau/18_17.PNG)



# <center><font size="20"> KPI 차트</font></center>

KPI(Key progress indicator) 를 표시하는 뷰를 만드는 방법을 보여준다. 다음과 같이 View 에서 매출과 제품 중분류 표를 보자. 여기에서 어느정도의 매출을 올리는 지역과/ 그렇지 않는 지역을 모양 차이를 통해 구분을 두고싶다.

![png](/assets/images/Tableau/18_19.PNG)

아래와 같이 Calculated Field 를 구성하여 매출을 2개로 구분되게 만든다. 

![png](/assets/images/Tableau/18_20.PNG)

그 이후 shape 에 올려놓게 되면 다음과 같이 두개의 기호로 구분되는것을 볼 수 있다.

![png](/assets/images/Tableau/18_21.PNG)

하지만 기호들의 생김새가 직관적이지 않아서 생각보다는 한눈에 알아보기 힘들다. 그러므로 모양을 다르게 적용해보자, 아래와 같이 shape 에서 뭔하는 shape 로 지정을 새로해주자. 

![png](/assets/images/Tableau/18_22.PNG)

그러면 아래 그림과 같이 내가 원하는 모양으로 이쁘게 구성되는것을 볼 수 있다.

![png](/assets/images/Tableau/18_23.PNG)



# <center><font size="20"> Bump 차트</font></center>



순위를 시각화 하기 매우 좋은 그래프이다. 다음과 같이 그래프를 구성하는것을 목적으로 삼자.

![png](/assets/images/Tableau/18_24.PNG)

우선 rank 함수를 새로 지정해주어야 하는데, 그 차이는 아래와 같다. 우리는 값이 같더라도, 위와같이 구별되는 rank 를 원하기 때문에 rank_unique 를 쓸 예정!

![png](/assets/images/Tableau/18_25.PNG)

다음과 같이 이익에 대한 rank_unique 를 구성한다.

![png](/assets/images/Tableau/18_26.PNG)

그리고 나서 아래와 같이 rank 를 올리게 되면 내가 예상한 차트가 나오지 않는데, 이는 기본적으로 연산이 across 이기 떄문이다.(즉 rank 를 지역별로 경기도 1위, 충남 2위 ... 가 아니라 경기도 내에서 5월일때가 매출 1위 .... 이런식으로 매긴다는 뜻) 그러므로 이를 조절해 주어야 한다.

![png](/assets/images/Tableau/18_27.PNG)

아래 그림과 같이 compute using 지역 을 클릭하여 내 rank 의 계산 기준이 지역이 되게 한다. 그러면 내가 원하는 rank 의 구성이 나오게 된다.

![png](/assets/images/Tableau/18_28.PNG)

그 이후에 rank 를 복사하고, 복사한 rank 를 string 의 typr 으로 만든다. (그런데 사실 이 작업은 해도 되고 안해도 되는듯..)

![png](/assets/images/Tableau/18_29.PNG)

![png](/assets/images/Tableau/18_30.PNG)

그러고 난 이후에 rank 를 row에서 하나 복사한 이후 dual axis 를 적용한다.

![png](/assets/images/Tableau/18_31.PNG)

복사한 두번째 뷰에 대해서 모양을 circle 로 주자. 그러고 난 뒤에 우리가 복사했던 rank (copy) 를 붙여넣는다. 그러면 아래 그림처럼 rank들이 또 across 로 계산되어서 제멋대로인것을 볼 수 있다. 이 떄에도 계산 기준을 바꾸어야한다.

![png](/assets/images/Tableau/18_33.PNG)

그러면 이제 우리가 원하는 방향으로 바뀐것을 볼 수 있다. 그런데 여기에서는 rank 가 reverse d 된 방향으로 정렬이 되어있다!(즉 rank 1위가 맨 위여야하는데, 값으로는 제일 작으므로 맨 아래에 위치하고 있는 현상) 이를 바꾸어 주어야 우리가 원하는 visualization 이 될것이다. 그를 위해서 우선 축을 Synchronized 시킨다.

![png](/assets/images/Tableau/18_34.PNG)

그 이후에 축을 Reversed 시킨다. 

![png](/assets/images/Tableau/18_35.PNG)

짜잔 내가 원하는 구성이 완성되었다. 

![png](/assets/images/Tableau/18_36.PNG)