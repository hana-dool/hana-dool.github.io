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

>테블로의 레이더 차트이다. PowerBI 에서는 디폴트로 있다고 하는데, 태블로에서는 힘들게 힘들게 구성해야한다.
>
>- https://www.pluralsight.com/guides/tableau-playbook-radar-chart
>- https://www.youtube.com/watch?v=HumFxNTIEGk
>- https://www.youtube.com/
>- https://www.youtube.com/watch?v=r2LI9Vq8F3g
>- https://www.thedataschool.co.uk/ellen-blackburn/a-simple-way-to-make-a-radar-chart
>
>위 항목들을 참고하였습니다. 아래의 구성을 할  수 있으려면, 모든 Value 값들의 Scale 이 통일되어야 한다는 점이 있습니다.

# <center><font size="15"> 시간별 Radar Chart </font></center>

- 우선 슈퍼스토어의 데이터로 실습을 해보자.
- 내 목표는 먼저 월별로 매출을 레이더 차트로 표현하는 것이다.
- 그러기 위해서는 아래와 같이 먼저 월을 계산하는 차트를 만들자.

![png](/assets/images/Tab_Vis/12_1.png)

- 레이터 차트를 위해서는 다음과 같이 4개의 계산식이 필요한데 하나하나 알아보자.

<br>

<Br>

## 계산식

### 1. 각도계산식

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

### 2. 중앙과의 거리식

![png](/assets/images/Tab_Vis/12_3.png)

- 이 경우에는 레이더 차트에 표기하고시픈 값을 넣는다. 나의 경우 매출이므로 이를 넣-었다.

<br>

### 3. X 좌표식

![png](/assets/images/Tab_Vis/12_4.png)

- X 좌표식은 다음과 같이 중앙과의 거리와 각도를 계산한 좌표를 넣는다.
- 2차원 원형좌표계를 생각하면 당연한 값이다.

<br>

### 4.Y 좌표식

![png](/assets/images/Tab_Vis/12_5.png)

- 이 경우에도 위와 같이 원형좌표계를 이용하여 Y 좌표를 계산한다.

<br>

<br>

## View 생성

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

## Dashboard 구성

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

<br>

<br>

# <center><font size="15"> 항목별 Radar chart</font></center>

- 위같이 시간별 레이더 차트를 항목화 할 수 있었다.
- 하지만 더 자주쓰이는것은 '항목별로(이를테면 공격력, 방어렫 등..)' 그린 레이더 차트이다.
- 이를 시각화 하는 방법을 알아보자.

## 데이터 구성 바꾸기

- 항목별로 레이더 차트를 구성하기 위해서는 Pivot 데이터로 구성해야한다. 
- 아래와 같은 형식의 데이터를 보자. Poketmon_data set 으로서 각각의 포켓몬에 대해 공격력, 방어력... 등이 나타나있다.
- 아래처럼 HP 를 복사하여 HP0 데이터를 만든다. 
- 이는 레이더차트가 시작과 끝이 있어야 하기 떄문에, 그것을 연결하는 역할을 한다.

![png](/assets/images/Tab_Vis/12_55.png)

![png](/assets/images/Tab_Vis/12_19.png)

- 먼저 아래와 같이 

- 하지만 이렇게 되어있으면, 시각화를 할 수 없다.
- 그러므로 우리가 '항목화 할 데이터' 를 Pivot 한다.

![png](/assets/images/Tab_Vis/12_20.png)

- 그러고 나서, 아래와 같이 Pivot 된 Name 과 Value 를 모두 조절한다.

![png](/assets/images/Tab_Vis/12_21.png)

<br>

## 데이터 Path 설정

- 그 이후에 아래와 같이 Path 를 정의한다. 
  - When 을 이용해서 시작과 끝을 정해준다. 
  - ELSE 는 HP0 일떄에 7이 나온다. 즉 HP 가 끝과 연결점이 되는것이다.

![png](/assets/images/Tab_Vis/12_22.png)

<br>

## 데이터 각도 설정

- 그 이후에 Radian , 즉 각도를 조정한다.
- 시작점이 pi/2 로서 12시 방향부터 시작한다.
- 그리고 6개 항목이므로 ([Path]-1)2 pi / 6 으로 계산한다.

![png](/assets/images/Tab_Vis/12_23.png)

<br>

## 데이터 X,Y 좌표 설정

- Value (피봇값) 와 Cos 값을 곱한것으로 X 좌표를 한다.

![png](/assets/images/Tab_Vis/12_24.png)

- 위와 같이 Y 좌표를 정의한다.(Y좌표는 Sin)

<br>

## View 구성

- 아래와 같이 X,Y 좌표를 추가한다.
- 그리고나서 Mark 를 Line 으로 정의한다.

![png](/assets/images/Tab_Vis/12_25.png)

- 그리고 Path 를 추가한뒤 Dimension 으로 추가한다.
- 그러면 아래와 같이 시각화가 나옴을 알 수 있다.

![png](/assets/images/Tab_Vis/12_26.png)

- 하지만 우리는 포켓몬별로 시각화를 하고싶지, 지금처럼 Agg 된 데이터로 하고싶지 않다.
- 그러므로 필터를 추가하여 여러 ID(포켓몬) 별로 보도록 하자.

![png](/assets/images/Tab_Vis/12_27.png)

- 그러고 나서 Name 을 COlor 로 놓는다.
- Color 와 id 는 다른 포켓몬에 대해서 구별자가 되기 떄문에 사실 id 나 Name 을 같이 필터와 컬러로 통일해도 상관없긴 하다.

![png](/assets/images/Tab_Vis/12_28.png)

<br>

## View 다듬기

- 아래와 같이 Sum(VAlue) 를 추가해보자. 각 값이 나온다. 도형 위에 나온다.

![png](/assets/images/Tab_Vis/12_29.png)

- 이렇게 겹치는 이유는 우리가 시작 / 끝을 정의하기 위해 같은 데이터를 한번 복제해서 사용했기 떄문이다.
- 즉 이런 경우를 방지하기 위해서, Aligment 를 Center 로 조절하자.

![png](/assets/images/Tab_Vis/12_30.png)

- 그 이후에 Axis 를 모두 통일한다.

![png](/assets/images/Tab_Vis/12_31.png)

- 그리고 그 이후에 모든 뷰를 꺠끗히 정리한다.

![png](/assets/images/Tab_Vis/12_32.png)

- 이제 id 를 FIlter 에서 추가하여 다양하게 살펴볼 수 있다.

![png](/assets/images/Tab_Vis/12_33.png)

<br>

<br>

# <center><font size="15">  Radar chart 의 배경설정</font></center>

- 레이더가 위처럼 휑 하면 , 어떤곳이 어떤값을 나타내고있는지가 헷갈린다.
- 기타 사이트에서 배경을 받는 방법도 있지만 아래에서처럼 태블로에서 해결할 수 있다.
- 아래와 같이 Ring1 ~ Ring5 라는 데이터를 추가한다.
  - 이는 우리 레이더 차트의 골조가 될 데이터이다.
  - 모두 같은 값을 가지게 데이터를 만든다.
  - 즉 최대값은 데이터의 최대값보다 조금 큰 값으로 설정하는것이 좋다.

## 뷰 안에서 배경설정

![png](/assets/images/Tab_Vis/12_34.png)

- 아래처럼 위에서 수행했던 시각화에서 id 로 color 와 디테일을 통일한다.

- 별 의도는 없다. 좀 더 관리하기 쉽게 하려고 그런것

![png](/assets/images/Tab_Vis/12_35.png)

- 아래처럼 Conditional Label 을 정의한다.
  - 우리가 추가한 Ring1 ~ Ring5 데이터의 id 는 1000 의 값이 넘는것을 생각하자.
  - 즉 아래처럼 정의하게 된다면, 우리가 추가한 데이터는 무시하는 Value 값이 된다.

![png](/assets/images/Tab_Vis/12_36.png)

- 아래와 같이 기존의 Value 를 대체한다
- 이렇게 되면, 기존의 데이터는 아무 영향을 받지 않게된다.

![png](/assets/images/Tab_Vis/12_37.png)

- 그 이후에 우리가 추가하였던 Ring1~5 데이터의 id 를 추가한다.
- 그러면 아래 그림처럼 그 값이 나오게 된다. 

![png](/assets/images/Tab_Vis/12_38.png)

- 이제 이 색깔을 좀 다르게 조절한다. 
- 무채색인 회색이 제일 좋은 선택이다.

![png](/assets/images/Tab_Vis/12_39.png)

![png](/assets/images/Tab_Vis/12_40.png)

- 이제 아래에서 처럼, ID=1005 일때에만 Attribute(피봇했던 col 이름) 을 출력하는 데이터를 만든다.
- 이 경우 HP0 의 경우는 겹치므로  제외시킨 것이다.

![png](/assets/images/Tab_Vis/12_41.png)

- 이를 Text 에 추가하게 된다면 아래와 같이 시각화가 된다.

![png](/assets/images/Tab_Vis/12_42.png)

- Attribute 로 변환하게 된다면 제대로 나타나게 된다.

![png](/assets/images/Tab_Vis/12_43.png)

<br>

## 뷰 밖에서 설정

- 위에서 했던 과정에서, 기존의 id 를 뺴고, 추가한 id 만 추가하자.
- 그러고 대시보드에 올리자. 
- Size 를 정사각형이 되게 조절하자.
- 그 이후 텍스트를 추가하게 된다면 아래와 같게 된다.

![png](/assets/images/Tab_Vis/12_44.png)

![png](/assets/images/Tab_Vis/12_46.png)

- 그 이후 이 그림을 저장하자. (Export image 또는 Print Scrin)
- 그리고 원래 데이터 시각화를 진행했던 뷰로 돌아가서 Background Image 를 추가하자.

![png](/assets/images/Tab_Vis/12_47.png)

![png](/assets/images/Tab_Vis/12_48.png)

- 이제 우리가 저장했던 이미지를 추가한다.
- 이 때에 X,Y 의 범위는 처음 VIew 를 구성했었을때의 범위와 같게 조절한다.

![png](/assets/images/Tab_Vis/12_49.png)

- 이제 아래와 같이 잘 구성된것을 볼 수 있다.

![png](/assets/images/Tab_Vis/12_50.png)

- 위와 다른점은 좀 더 섬세하게 이쁜 시각화가 가능하다는 점이다.

<br>

# <center><font size="15">  Radar chart 외곽선과 내부색칠</font></center>

- 아래와 같이 X 축을 하나 더 만들어내자.

![png](/assets/images/Tab_Vis/12_51.png)

- 그 이후에 Dual Axis 를 진행하다.

![png](/assets/images/Tab_Vis/12_52.png)

- 그 이후에 두개중 하나의 시각화를 Polygon 을 선택한다.
- 투명도를 조절하면 아래와 같이 나오게 된다.

![png](/assets/images/Tab_Vis/12_53.png)