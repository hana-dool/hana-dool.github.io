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

- <https://www.youtube.com/watch?v=yEApDIou2hg>

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

<br>

<br>

# <center><font size="15"> parameter 와 마크 연결 </font></center>

- 아래의 예시는 마크와 parameter 를 연결하는 방식입니다. (제 대시보드인 Us crime 에서 따왔습니다. )
- 아이콘을 클릭' 하였을때에 변하는 시각화를 만들고 싶다고 합시다.

![png](/assets/images/Tableau_ex/8_22.png)

- 이를 위해서는 "파라미터" 와 Icon 을 연결할 수 있어야 합니다.

- 먼저 아래와 같이 빈 view 에 8개의 avg(0) 을 만듭니다.

![png](/assets/images/Tableau_ex/8_23.png)

- 그 이후에 각 아이콘 수마다 대응될 String 을 생성합니다.
- 그 떄에 내용은 단순히 String 만 형성되면 되니다.

![png](/assets/images/Tableau_ex/8_24.png)

- 그리고 나서 Mark 를 Shape 로  바꿉니다.

![png](/assets/images/Tableau_ex/8_25.png)

- 그러고 나서 8개에 대해서 하나하나 선택한 이후에
- 각각 다른 이름을 Mapping 합니다. 
- 이 경우에 _arsons / _assault .... _rape 를 맵핑했습니다.

![png](/assets/images/Tableau_ex/8_26.png)

![png](/assets/images/Tableau_ex/8_27.png)

![png](/assets/images/Tableau_ex/8_28.png)

- 모두 맵핑을 다르게 하고 나면 다음과 같은 아이콘이 나오게 됩니다.

![png](/assets/images/Tableau_ex/8_29.png)

- 현재 위에서 시각화한것을 dash 보드에 옮긴 상태이다.
- 하지만 이는 그저 각각이 다른 Calulated Field 에서 정의되어있다.
- 즉 아무 의미없이 흩어져 있는 상태이다.

![png](/assets/images/Tableau_ex/8_30.png)

- 이를 연결하기 위해서 어떻게 해야될지 다음과 같이 연결합니다.
- 먼저 대시보드에서 액션을 추가합니다. (paramter action 을 추가합니다.)

![png](/assets/images/Tableau_ex/8_31.png)

![png](/assets/images/Tableau_ex/8_34.png)

- 그 이후에 아래 그림처럼 선택 아이콘을 Source sheet 로 지정합니다.
  - 선택 아이콘 시트란, 우리가지정했던 8개의 아이콘이 일렬로 있는 시트입니다.
    - 이 경우 Parameter 은 우리가 '조절하고 싶은 parameter 를 지정합니다.'
    - 우리는 p.범죄변화 라는 파라미터를 통해서 시각화를 조절했던것을 기억합시다.
  - 즉 Target parameter 는 다음과 같이 p.범죄변화 로 고쳐야 합니다.
  - Field 는 각 아이콘마다 다를것입니다. 이 경우 Filed 를 _arsons (즉 우리가 추가하였던 그저 'arsons' 를 내보내는 Field 를 추가합니다. )
  - arsons 의 아이콘만 parameter action 을 부여한 상태이므로 8개 아이콘에 대해서도 같은 작업을 진행합니다.
  - 아래를 보면 시트가 4개이고, 각 8개의 아이콘이 있으므로 총 32개의parameter action 을 추가한것을 볼 수 있습니다.

![png](/assets/images/Tableau_ex/8_32.png)

![png](/assets/images/Tableau_ex/8_33.png)

- 위의 작업을 끝내고 나면 Parameter 와 아이콘을 결합하여 반응형 대시보드를 제작할 수 있었습니다.

<br>

# <center><font size="15"> 마크 하이라이트 없애기</font></center>

