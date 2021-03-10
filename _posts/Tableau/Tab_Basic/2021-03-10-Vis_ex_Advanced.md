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


