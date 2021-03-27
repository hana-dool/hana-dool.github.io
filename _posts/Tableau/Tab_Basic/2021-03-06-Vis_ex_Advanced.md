---
title:  "Vis(Advanced Ex)"
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



# <center><font size="20"> Horizon 차트</font></center>

Horizon chart란 아래와 같이, 시간의 추이에 따른 변동을 색깔로 나타내주는것이다. 

![png](/assets/images/Tableau/18_49.PNG)

위 차트를 어떻게 구성하는지 알아보자! 우선 우리가 구성해볼 데이터시트를 살펴보자.

![png](/assets/images/Tableau/18_37.PNG)

날짜가 col 에 있어서 pivot 으로 형식을 변경해주어야 한다. 

![png](/assets/images/Tableau/18_38.PNG)

그 이후 날짜의 형식을 Date 로 바꾸어야 한다. 

![png](/assets/images/Tableau/18_39.PNG)

그러고 난 후, 이름을 바꾸어준다. 

![png](/assets/images/Tableau/18_40.PNG)

이제 Calculation field 를 만들어내야 한다.  아래와 같은 형식으로 계산된 식을 구성한다. 

![png](/assets/images/Tableau/18_41.PNG)

![png](/assets/images/Tableau/18_42.PNG)

![png](/assets/images/Tableau/18_43.PNG)

계산된 식을 Table 로 만들면 아래와 같다. 

![png](/assets/images/Tableau/18_44.PNG)

이제 Marks 를 Area 로 고치자. 그 이후에 Measure values 를 row 선반으로 올리자. 이 그래프를 보면 왜 우리가 Calculatation field 를 위와같이 설정했는지 감이 온다. 각 기준의 이상의 값을 가질때, 20으로 설정한것은 y 축의 최대값을 20으로만 구성하려고 하였기 때문이고, 그 내에서 '높이' 가 아니라 '색상' 으로 정도를 나타내려 하였기 떄문이다. 

![png](/assets/images/Tableau/18_45.PNG)

이 그래프를 보면, 색깔만 달리하고 겹쳐지는것이 우리가 원하는 그래프임을 알 수 있다.

![png](/assets/images/Tableau/18_46.PNG)

아래와 같이 구분된 색으로 그 정도를 측정할것이기 떄문에 Measure name 을 색깔 Marks 로 끌어내린다. 

![png](/assets/images/Tableau/18_47.PNG)

그 이후 아래와 같이 모든 나라들에 대해서 그 추이를 살펴볼 수 있다.

![png](/assets/images/Tableau/18_48.PNG)

Category 가 너무 많아 한눈에 보기 힘들다면(이 그래프의 장점은 y축이 짧더라도 많은 데이터를 보여줄 수 있다는 장점에 있다.) filter 에 Region 을 넣어서 아래와 같이 Catogory 를 줄일 수 있다.

![png](/assets/images/Tableau/18_49.PNG)



# <center><font size="20"> 달력 차트</font></center>

시각화를 달력에 하게된다면, 각각의 값에 대해서 어느정도의 값을 가지는지를 좀 더 효과적으로 알 수 있다. 먼저 아래와 같이 시간 정보를 끌어다가 놓는다. 이때, 시간에 대한 변수를 마우스 오른쪽 클릭 + 끌어놓음을 같이 하게 된다면(window) 아래 그림과 같이 Data field 를 선택하게 해주는 창이 나타난다. 이떄에 년/월 불연속값을 선택하자. 지금 추가한값은 필터로 걸리게 될 변수이다. (즉 2019년 9월 데이터만 Filter 로 거를것이다!)

![png](/assets/images/Tableau/18_50.PNG)

그러고 나서는, 옆에 WEEKDAY 라는 변수를 col 에 추가한다.

![png](/assets/images/Tableau/18_51.PNG)

그리고 week 이라는 변수를 rows 에 추가하면 아래와 같은 그래프가 나타나게 됨다.

![png](/assets/images/Tableau/18_52.PNG)

이제 Day(불연속) 를 Text 에 끌어놓는다. 이 때에도 오른쪽 클릭과 같이 끌어놓아야 우리가 원하는 불연속형의 데이터 형태로 나타나게 된다. 

 ![png](/assets/images/Tableau/18_53.PNG)

그러면 아래와 같이 날짜(day)가 text 의 형태로 나타나게 된다. 

![png](/assets/images/Tableau/18_54.PNG)

그 이후 Filter 를 추가하여, 우리가 원하는 월만 뽑아쓰자. 이 떄에는 2019년 6월 데이터만 보고자 한다.(물론 filter 를 show filter 를 통해서, 목록에서 고를 수 있다.)  

![png](/assets/images/Tableau/18_55.PNG)

![png](/assets/images/Tableau/18_56.PNG)

그 이후에 Entire view 로 전체보기로 한 후에, Mark 를 사각형으로 놓는다. 이러면 어느정도 구성이 된 것을 볼 수 있다.

![png](/assets/images/Tableau/18_57.PNG)

이제 색상에 sum(매출) 을 넣는다. 그렇다면 매출별로 색상이 나타나게 된다.(색상 조절은 사용자가 알아서! DIY) 

![png](/assets/images/Tableau/18_58.PNG)

그 이후 Label 에서 Allingment 를 조절하자. (색상 조절도 하면 깔끔함)

![png](/assets/images/Tableau/18_59.PNG)

그리고 color 의 border 를 조절하자. 아래와 같이 하얀색 margin 을 준다면 아래와 같이 잘 나오게 된다. 

![png](/assets/images/Tableau/18_60.PNG)

그런데 지금 일월화수목 의 순서인데 월화수목.. 의 형태로 만들고싶다. 그렇다면 아래처럼 date property 로 이동하여보자.(즉 시간의 property 를 고치겠다는 의미)

![png](/assets/images/Tableau/18_61.PNG)

이제 week start 를 monday 로 고치자.

![png](/assets/images/Tableau/18_62.PNG)

고치고나면 월 ~ 일 순서로 잘 바뀐것을 볼 수 있다.

![png](/assets/images/Tableau/18_63.PNG)

