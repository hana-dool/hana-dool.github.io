---
title:  "년별 농가소득 대시보드"
excerpt: "농촌의 경우 소득은 어떻게 되어있을까"
categories:
  - Tab_Dash
tags:
  - 3
last_modified_at: 2021-05-19

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

<br>

농촌의 경우, 특수작물을 재배하지 않는 이상 진짜 돈을 못번다. 우리 아버지도 농부시고, 엄청난 고생을 하시면서 쌀농사를 지어오셨는데, 그 수입이 노력에 비해 최저시급도 나오지 않는 정도였다. 과연 다른 지역도 이런지, 연령별로 수입의 차이가 있는지 등이 궁금해졌고, 그에 따라 대시보드를 구성하게 되었습니다. (From 21-05-19~)

<br>

<br>

# <center><font size="15"> Data Collection </font></center>

- 데이터는 공신력이 있어야 한다. 그러므로 데이터 소스는 되도록이면 공신력이 있는 사이트 기준으로 고르려 하였다
- <https://kosis.kr/statHtml/statHtml.do?orgId=101&tblId=DT_1EA1501&conn_path=I3>
- 위의 링크에서 데이터를 가져왔다. Kosis 의 농가소득에 관한 데이터이다.

![png](/assets/images/Tableau_ex/7_1.png)

- 위 데이터를 이용해서 시각화를 진행해 보겠다. Collection 과정이 크게 어렵지는 않았다.

<br>

<br>

# <center><font size="15"> Data Preprocessing </font></center>

- 데이터가 가로는 년별 / 세로는 분류별로 나누어져있다. 
- 

# <center><font size="15"> Outline </font></center>

- 먼저 Fatig 에서 아래와 같이 대충 아웃라인을 구성하였다.

![png](/assets/images/Tableau_ex/6_4.png)

- 중점을 둔 사안은 다음과 같다.
  - 최대한 로고의 이미지 색을 이용할것
  - 색을 많이 쓰지 말것
  - 각 제품별로 버튼을 만들어야 하므로, 6개의 버튼이 들어갈 공간은 냅둘것
  - 텍스트 설명이 들어가고 싶으므로 그 자리도 비워둘것
- 사실 이 부분은 시각화를 진행하면서 계속 바뀌어야 하는 부분이다.
- 결과적으로 최종 대시보드는 아래와 같이 구성되었다.

![png](/assets/images/Tableau_ex/6_5.png)

- 그리고 리뷰는 다음과 같이 시각화 한 다음 Export 하였다.

![png](/assets/images/Tableau_ex/6_6.png)

- 레이더 차트를 구성할것이기 때문에, 그 Outline 이 되는 배경도 만들었다.

![png](/assets/images/Tableau_ex/6_7.png)

- 그리고 버튼 모양도 다음과 같이 만들었다.

![png](/assets/images/Tableau_ex/6_8.png)

<br>

<br>

# <center><font size="15"> 버튼구성 </font></center>

- 먼저 버튼을 만들어보자. 다음과 같이 데이터가 구성되어있을것이다.

![png](/assets/images/Tableau_ex/6_9.png)

- 그 이후에 텍스트를 중앙에 Align 하는 방식으로 버튼을 구성한다.

![png](/assets/images/Tableau_ex/6_10.png)

![png](/assets/images/Tableau_ex/6_11.png)

<br>

<br>

# <center><font size="15"> 레이더 차트 </font></center>

- 레이더 차트를 구성하기 위해서는, 그 Scale 이 맞아야한다.
- 그러므로 최대가 1이 되도록 구성하였다.

![png](/assets/images/Tableau_ex/6_12.png)

- 그 이후에는 아래와 같이 시각화를 하게 될 Col 을 잡아서 Pivot 처리를 하였다.

![png](/assets/images/Tableau_ex/6_13.png)

![png](/assets/images/Tableau_ex/6_14.png)

- 이제 레이더차트에 필요한 4가지 변수를 구성하였다.

![png](/assets/images/Tableau_ex/6_15.png)

![png](/assets/images/Tableau_ex/6_16.png)

- X,Y 변수 2개를 구성하였다.

![png](/assets/images/Tableau_ex/6_17.png)

- 그 이후 아래와 같이 Path 에 대해서 Dimension 설정을 하면 레이터차트가 아래와 같아진다.

![png](/assets/images/Tableau_ex/6_18.png)

- 우리는 제품명에 대해서 보고싶으므로 제품명을 추가한다.

![png](/assets/images/Tableau_ex/6_19.png)

- 이떄에 0 선은 남겨두자. 그래야만 아래와 같이 레이더차트를 구성할때에 중심을 맞추어가면서 조절하기 쉽기 때문

![png](/assets/images/Tableau_ex/6_20.png)

![png](/assets/images/Tableau_ex/6_21.png)

- 색을 바꾸어주자. 그러면 아래와 같아진다.

![png](/assets/images/Tableau_ex/6_22.png)

<br>

<br>

# <center><font size="15"> 리뷰 </font></center>

- 그림을 사용하여 변하는 Dinamic 한 사진을 구현하자.
- 아래와 같이 각 제품명에 대해서 shape 를 형성하자.

![png](/assets/images/Tableau_ex/6_24.png)

- 그 이후에 Mark 를 이용해 시각화 하고자 하는 그림을 매칭한다.

![png](/assets/images/Tableau_ex/6_25.png)

- 그 이후에 보면 내가 리뷰로 넣고자 하는 이미지가 구현된 것을 볼 수 있다.

![png](/assets/images/Tableau_ex/6_26.png)

- 이를 DashBoard 에 알맞은 크기로 넣으면 된다.

![png](/assets/images/Tableau_ex/6_27.png)

<br>

<br>

# <center><font size="15"> 투명 버튼 </font></center>

- 아래와 같이 투명 버튼을 생성하기 전에, 클릭하면 변할 모양을 그 위에 겹쳐넣는다.

![png](/assets/images/Tableau_ex/6_28.png)

- 그 이후 투명버튼과 같은 크기의 상자를 준비하고, 그 위에 겹쳐본다.

![png](/assets/images/Tableau_ex/6_29.png)

![png](/assets/images/Tableau_ex/6_30.png)

- 잘 맞는다면 Filter 를 형성하고 

![png](/assets/images/Tableau_ex/6_31.png)

- 같은 규격의 투명한 버튼으로 바꾼다.

![png](/assets/images/Tableau_ex/6_32.png)

- 하지만 이 경우 아래처럼 에러가 나는것을 볼 수 있는데

![png](/assets/images/Tableau_ex/6_33.png)

- 이 이유는 아래처럼 변하는 버튼의 View 가 변해버렸기 떄문이다.
- 즉 선택되지 않은 버튼은 무시하기 떄문

![png](/assets/images/Tableau_ex/6_34.png)

- 이는 아래와 같이 Table Layout 에서 Empty row 에서 Show empty row 를 통ㅎ서 해결할 수 있다.

![png](/assets/images/Tableau_ex/6_35.png)

- 그 이후에 선택이 제대로 되는것을 볼 수 있다.

![png](/assets/images/Tableau_ex/6_36.png)

<br>

<br>

#<center><font size="15"> 가격 </font></center>

- 가격 텍스트를 마지막으로 넣는다.

![png](/assets/images/Tableau_ex/6_37.png)

![png](/assets/images/Tableau_ex/6_38.png)

<br>

<br>

#<center><font size="15"> Final Result </font></center>

<iframe seamless frameborder="0" src=" https://public.tableau.com/views/_16211024672920/Dashboard1?:embed=yes&:display_count=yes&:showVizHome=no" width = '774' height = '506' scrolling='yes' ></iframe>

<br>

<br>

# 아쉬웠던점 + Update

- Shape 의 해상도가 최대 지원이 Witdth 200 까지밖에 안된다고 하더라.
- 나는 Figma 에서 Review 를 한번에 만들고, 이를 Mark 를 통해서 다이나믹한 이미지를 구현하려 했는데, 위와 같이 해상도 문제로 인해 글자가 Blurry 하게 만들어졌다.
- 그리고 생각보다, 0인값이 많아서 레이더 차트를 구성할때에 별로 효과적이지 못하였다.
- 많은 시각화를 넣어보려 하였는데, 시간문제로 하나만 하는거에 만족해야했다.
- 5개의 값을 상대적으로 비교한거라, 당류가 별로 안들어있는 육개장이 당류가 많아보인다.. 

- 레이더차트의 순서와, 대 뒤 배경의 순서가 맞지 않아서 중간 수정이 있었습니다.
  - 그래서 대시보드와 사진의 순서가 약간 다릅니다.