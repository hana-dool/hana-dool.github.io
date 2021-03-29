---
title:  "나비 차트"
excerpt: "두개 구분값 시각화"
categories:
  - Tab_View
tags:
  - 3
last_modified_at: 2021-03-10


use_math : true
---

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
