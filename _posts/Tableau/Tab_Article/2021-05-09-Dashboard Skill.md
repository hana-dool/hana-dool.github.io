---
title:  "Dashboard Skill"
excerpt: "태블로 대시보드 구성시 알아두면 좋은 Skill"
categories:
  - Tab_Article
tags:
  - 3
last_modified_at: 2021-05-09

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

<br>

> 아래 내용들은 탬플로의 대시보드를 구성하면서, 알면 좋은 스킬들을 수록하였습니다.

# <center><font size="15"> Mark 색변경 </font></center>

- 시각화를 하다보면, Mark 를 '우리가 원하는 색상' 으로 변경시키는것이 필요하다. 
- Mark 이미지를 다운받기 전에 색상변경을 할 수 있을것이다. 
- 하지만 그러한일이 불가능하거나 귀찮을 때에 다음과 같이 하면 쉽게 색을 부여할 수 있다.

먼저 아래와 같이 새로운 변수를 만든다. View 는 차원이 있어야 시각화가 가능해지기 때문이다.

![png](/assets/images/Tab_Article/6_1.png)

그 이후에 만들어진 shape 변수를 색상에 넣고, Mark 를 shape 로 변경한다.

![png](/assets/images/Tab_Article/6_2.png)

그 이후에 shape 를 custom shape 로 변경한다. 

![png](/assets/images/Tab_Article/6_3.png)

이제 색상을 변경한다. shape 의 값은 '' 으로 늘 일정한 차원값이기 때문에, 이 때에 assign 한 색상은 대시보드가 어떻게 변하든 일정하다. 

![png](/assets/images/Tab_Article/6_4.png) 

![png](/assets/images/Tab_Article/6_5.png)

이제 대시보드에 올려보면 올바른 색깔로 잘 나온다. (Legend 는 삭제하면 된다.)

![png](/assets/images/Tab_Article/6_6.png)

