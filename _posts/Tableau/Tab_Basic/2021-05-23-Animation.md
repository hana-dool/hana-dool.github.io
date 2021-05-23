---
title:  "Animation"
excerpt: "태블로 애니메이션"
categories:
  - Tableau
tags:
  - 3
last_modified_at: 2021-05-23

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---



# <center><font size="15"> Animation 유형 </font></center>

Animation 유형

Ref: <https://help.tableau.com/current/pro/desktop/ko-kr/formatting_animations.htm>

- 태블로는 뷰가 변할떄에 바로 변하는게 아니라 애니메이션 설정을 통해서 시각화의 효과를 바꿀 수 있습니다.
- 아래와 같이 Fromat 의 Animation 에서 변경할 수 있습니다.

![png](/assets/images/Tableau/25_1.png)

- 위를 보면 Workbook Default 가 있습니다. 이를 off 에서 on 으로 바꾸면 애니메이션이 적용되는것입니다.
- Duration 은 애니메이션이 몇초동안 변하는지를 나타낸것입니다. (클수록 느리게 바뀌겠죠?)
- Style 은 순차적으로 변할지 아니면 급박하게 한번에 변할지 선택하는것입니다.

<br>

## Style : Simultanious

![png](/assets/images/Tableau/25_1.gif)

<br>

## Style : Sequential 

![png](/assets/images/Tableau/25_2.gif)

<br>

<br>

# <center><font size="15"> 미작동 이슈 </font></center>

- 애니메이션이 잘 작동되지 않을 수 있습니다. 
- 이런 경우 비쥬얼라이제이션에 filter 가 너무 많거나 계산식이 많은 등 복잡성이 크기 떄문일 수 있습니다.
- 이런 경우 view 의 복잡성을 줄이는것이 하나의 방법이 될 수 있습니다.
- 또는 Tableau Public 에 올리는것보다는 Local 에서 태블로 파일을 돌리는게 훨씬 빠르게 작동하기떄문에 효율적입니다.

