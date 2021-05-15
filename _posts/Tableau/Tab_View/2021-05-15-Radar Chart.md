---
title:  "레이터 차트"
excerpt: "레이터 차트"
categories:
  - Tab_View
tags:
  - 3
last_modified_at: 2021-05-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true


---

<br>

# <center><font size="15"> Radar Chart </font></center>

- 우선 슈퍼스토어의 데이터로 실습을 해보자.
- 내 목표는 먼저 월별로 매출을 레이더 차트로 표현하는 것이다.
- 그러기 위해서는 아래와 같이 먼저 월을 계산하는 차트를 만들자.

![png](/assets/images/Tab_Vis/12_1.png)

- 레이터 차트를 위해서는 다음과 같이 4개의 계산식이 필요한데 하나하나 알아보자.

<br>

<Br>

# <center><font size="15"> 계산식 작성 </font></center>

## 1. 각도계산식

![png](/assets/images/Tab_Vis/12_2.png)

- 위의 계산식을 잘 보자.
- pi() 는 pi 값을 반환한다. 2*pi 가 360도 임을 기억하자.
- countd 는 그룹의 고유한 가짓수를 출력한다.
- Running_sum
  - 첫 번째 행에서 현재 행까지 주어진 식의 누계 합계를 반환합니다
- 즉 종합하면 고유한 가짓수가 변할때마다 누계합으로 각도값이 산출되고 있다.
  - 1.countd([월]) : 월의 고유한 가짓수, 즉 12를 출력한다. 이 경우 {} 로 감싸서 LOD 를 만들었다. 즉 '미리' 고유한 가짓수인 12를 출력한것이다. 
  - 2.min : 사실 이는 의미없는 값이다. 어짜피 12가 출력되기 떄문이다. (AVG , MAX 등 어떤것을 넣어도 상관없음) 하지만 이를 넣은 이유는 Running_sum 은 집계된 값을 필요로 하기때문에, 그 구색을 맞추려고 min 을 넣은것
  - 3.Running_sum : 누적합으로서, 월이 증가할때마다 누적해서 더한다. 즉 각도가 증가하는 상황과 맞다.
  - +pi()/2 : 이는 첫 시작위치를 잡기 위함이다. 12시 방향에서부터 출발하게 하기 위해서이다.

<br>

## 2. 중앙과의 거리식

![png](/assets/images/Tab_Vis/12_3.png)

- 이 경우에는 레이더 차트에 표기하고시픈 값을 넣는다. 나의 경우 매출이므로 이를 넣-었다.

<br>

## 3. X 좌표식

![png](/assets/images/Tab_Vis/12_4.png)

- X 좌표식은 다음과 같이 중앙과의 거리와 각도를 계산한 좌표를 넣는다.
- 2차원 원형좌표계를 생각하면 당연한 값이다.

<br>

## 4.Y 좌표식

![png](/assets/images/Tab_Vis/12_5.png)

- 이 경우에도 위와 같이 원형좌표계를 이용하여 Y 좌표를 계산한다.

<br>

<br>

# <center><font size="15"> View 생성 </font></center>

- 아래와 같이 월과 1.각도계산 식을 세부식에 넣는다.

![png](/assets/images/Tab_Vis/12_6.png)

- 그 이후 각도 계산을 Compute using 월 로 바꾼다. 
- 월을 기준으로 각도가 늘어나야 하기 때문이다.

![png](/assets/images/Tab_Vis/12_7.png)

- 그 이후 X,Y 좌표를 Row 와 Col 에 넣자.

![png](/assets/images/Tab_Vis/12_8.png)

- 그리고 모양을 polygon 으로 바꾸면 아래와 같아진다.

![png](/assets/images/Tab_Vis/12_9.png)

- 그리고 각도계산식을 Path 로 넣는다. 
- 그래야 Path 가 각도식을 훝으면서 Polygon 을 형성하게 된다.

![png](/assets/images/Tab_Vis/12_10.png)

- 이제 아래와 같이 주문년도를 구분하도록 Color 에 넣자.
  - 이 경우에 Filter 에 넣어도 된다. 사용자의 자유이다.

![png](/assets/images/Tab_Vis/12_11.png)

- 시각화를 하고나면 X,Y Axis 의 scale 을 맞추어 주어야 한다.
- 그래야만 왜곡을 줄일 수 있기 때문이다.

![png](/assets/images/Tab_Vis/12_12.png)

![png](/assets/images/Tab_Vis/12_13.png)

<br>

<br>

# <center><font size="15"> Dashboard 구성 </font></center>

- 시각화에 잘 보이게 하기 위해서, 투명도와 Outline 을 형성하자.

![png](/assets/images/Tab_Vis/12_14.png)

- 그 이후에는 아래와 같이 Tooltip 에 매출을 넣는다. 

![png](/assets/images/Tab_Vis/12_15.png)

- 이제 대시보드에 넣기 위해서 그리드를 제거한다.

![png](/assets/images/Tab_Vis/12_16.png)

- 대시보드에 이미지를 넣고, 배경에 눈금 이미지를 Floating 으로 겹쳐넣는다.

![png](/assets/images/Tab_Vis/12_17.png)

- 이 이미지 위에 잘 겹쳐지도록 조절하면 된다.

![png](/assets/images/Tab_Vis/12_18.png)