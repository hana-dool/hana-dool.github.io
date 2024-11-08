---
title:  "Optimization"
excerpt: "태블로 최적화"
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
typora-root-url: ../../../../hana-dool.github.io
---



- 뷰, 대시보드, 스토리와 같은 시각화를 제작할때에 한 화면에 많은 정보를 적절히 담는것도 중요합니다.
- 하지만 이 경우 계산식이 많거나 너무 복잡하다면 Visualization 의 속도가 저하될 수 있습니다. 

- 이런 경우 사용자가 시각화를 탐색하다가 나갈 수 있기 떄문에 매우 치명적입니다.

<br>

# <center><font size="15"> 범위 줄이기</font></center>

- 뷰, 대시보드, 스토리 등을 만들때에 많은 필드와 계산을 추가하여 많은 정보를 넣고싶을 수 있습니다.
- 각 워크시트는 데이터에 대해 하나 이상의 쿼리를 실행하기 떄문에 시트가 많을수록 Visualization 렌더링에 많은 시간이 걸리게 됩니다. 
- 즉 가능한 여러 Visualization 에 데이터를 나누어 표현하는게 좋습니다.
- 데이터 시트 / 데이터 원본의 수가 적을수록 개선됩니다. 

<br>

<br>

# <center><font size="15">표시되는 필터 수 제한</font></center>

- 뷰의 필터는 사용자에게 많은 interaction 이 가능해지게 합니다. 
- 하지만 뷰에 필터를 추가할 경우 각 뷰의 필터는 옵션을 위한 쿼리가 필요해집니다.
- 즉 필터수가 많을수록 계산식에 오랜 시간이 걸리게 됩니다

<br>

<br>

# <center><font size="15">마크 수 줄이기</font></center>

- 마크가 많을수록 Visualization 속도가 줄어들게 됩니다.
- 아래와 같이 뷰에 몇개의 마크가 있는지 볼 수 있습니다.

![png](/assets/images/Tableau/26_1.png)

- 이와 같이 마크의 수가 많아지게 된다면 랜더링에 시간이 걸리게 됩니다. 
- 이러한 문제를 방지하기 위해서는 종작 필터를 이용해, 데이터 탐색시 세부 뷰로 이동하여 적은 수의 마크를 탐색하도록 하면 됩니다.

<br>

<br>

# <center><font size="15">줌 인의 함정</font></center>

- 줌 인을 하게되면 적은 수의 마크와 시각화만 보게되므로 시각화가 빨라진다고 생각할 수 있습니다.
- 하지만 이때에 주의해야할것은, 줌 인을 하게된다 하여도, 줌 밖의 마크들은 필터링이 되지 않습니다. 
- 즉 줌 밖의 마크들도 동시에 성능에 영향을 끼치게 되기 때문에 주의해야합니다.

