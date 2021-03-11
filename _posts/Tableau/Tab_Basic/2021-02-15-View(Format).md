---
title:  "View(Format)"
excerpt: "대시보드를 좀 더 보기 좋게 만드는 방법"
categories:
  - Tableau
tags:
  - 3
last_modified_at: 2021-02-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# Line 

- 데이터 뷰를 보다보면 그래프의 선들이 거슬릴 때가 있다. 

- Lines 에 대한 format 에 대한 구분은 다음과 같다.

  ![png](/assets/images/Tableau/15_1.png)

- Grid Lines(노란색 점선) : 그래프의 그리드를 조절한다.

  - 데이터가 얼마인지 쉽게 알 수 있다는 장점이 있지만, 자칫 너무 복잡해보일 수 있다.

- Zero Lines(검은색 굵은선) : 그래프의 0을 나타낸다.

  - 0이 큰 의미를 가지는 데이터에서(수익)는 중요하지만, 그렇지 않은경우는 별로 필요없는 선이다.

- Trend Lines(초록색 점선) : Analytic 에서 추세선을 추가하였을때에 Trend 를 나타내 준다.

- Ref Lines(하늘색 점선) : Analytic 에서 평균,상수선 등을 추가하였을 때의 참조선

- Axis Ruler(빨간색 점선) : x,y 축의 선

- Axis Ticks(검은색 실선) : Axis 의 값들을 구분시켜주는 짦은 검은색 실선

  - 이 값은 없애지 않으면 자칫 x,y 축이 고슴도치처럼 보여서 안좋아 보인다.

Sheet 에서 조절하지 않고 Rows/Columns 에서 조절하면 가로 / 세로 에 해당하는것만 조절할 수 있다.



# Border

- 경계선에 대한 Format 에 대한 구분은 아래와 같다. 

  ![png](/assets/images/Tableau/15_2.png)

- Row Divider
  - Pane(panel) : 파란색 점선 
  - Header : 빨간색 실선
  - Level : Row 의 레벨 수준을 나타냄. 높을수록 세세하게 선이 생긴다. 0으로 설정하면 row Axis 쪽에 구분(빨간색 실선) 이 생기지 않음

- Col Divider
  - Pane(panel) : 검은색 실선
  - Header : 초록색 실선
  - Level : Col 의 레벨 수준을 나타낸다. 높을수록 세세하게 선이 생김. 0 으로 설정하면 Row Axis 쪽에 구분(초록색 실선) 이 생기지 않는다.



# Shading

- 배경색에 대한 Format의 구분은 아래와 같다.

  ![png](/assets/images/Tableau/15_3.PNG)

- Default

  - Worksheet (살구색) : 맨 바탕의 색
  - Pane(하늘색) : 데이터 view 안쪽의 색

  - Header(회색) : 데이터 view 의 바깥쪽(header) 색

- Row/Col Banding

  - 각각 값이 변할때 마다 사진처럼 효과를 주는것
  - 이때 level / bandsize 조절을 통해 세세한 조절 가능

  