---
title:  "달력 차트"
excerpt: "날짜 시각화"
categories:
  - Tab_View
tags:
  - 3
last_modified_at: 2021-03-10


use_math : true
---

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

