---
title:  "Rounded barh 차트"
excerpt: "끝이 둥근 바 그래프"
categories:
  - Tab_View
tags:
  - 3
last_modified_at: 2021-04-24

use_math : true
---

![png](/assets/images/Tab_Vis/7_9.png)

위와 같이, 그래프의 양단을 둥글게 처리하고 싶다고 하자. 

# Rounded 바 차트

먼저 다음과 같이 차트를 구성한다. 딱딱한 막대의 모서리를 둥글게 만드는게 우리의 목표이다.

![png](/assets/images/Tab_Vis/7_1.png)

columns 에 avg(0) 을 추가한다.

![png](/assets/images/Tab_Vis/7_2.png)

그러면 다음과 같이 avg(0) 이 옆쪽에 나오게 된다. 이 경우에 avg 를 측정값 열에 추가하여 보자.

![png](/assets/images/Tab_Vis/7_3.png)

![png](/assets/images/Tab_Vis/7_4.png)

그러면 아래와 같이 2개의 축을 표시하고 있기 떄문에, 각 제품 중축에도 avg(0) 이라는 분류가 늘어난것을 볼 수 있다.

![png](/assets/images/Tab_Vis/7_5.png)

이때 Mark 에서 line 을 선택하여 둘을 연결해보자. 

![png](/assets/images/Tab_Vis/7_6.png)

그 이후에, Measure Names 를 Path 로 옮기자. 이 이유는 현재 Measure names 에는 sum(a매출) 과 avg(0) 이 있는 상황이다. 이 둘을 이어주어야 (0 ~ 매출합) 선 그래프를 그릴 수 있기 때문이다. 그러므로 Path 로 이동시키는것이다. (쓸데없이 y 축에 avg(0) 이 있는것도 없앨 수 있다. )

![png](/assets/images/Tab_Vis/7_7png)

![png](/assets/images/Tab_Vis/7_8.png)

이제 사이즈를 조절해주면 된다.

![png](/assets/images/Tab_Vis/7_9.png)