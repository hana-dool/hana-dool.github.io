---
title:  "전 세계 인구의 중앙값"
excerpt: "인구 중앙값에 대한 시각화"
categories:
  - Tab_Dash
tags:
  - 3
last_modified_at: 2021-03-27

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# Intro

이 시각화는 <http://hdr.undp.org/en/data> un 에서 제공하는 지표에 대한 데이터를 사용하였습니다. 시각화의 완성본은 <https://public.tableau.com/profile/haninwook#!/?newProfile=&activeTab=0> 에서 볼 수 있습니다. 

시각화의 계기는 우리나라의 출산율 문제가 심각하여 인구 그래프가 피라미드 형태에서 팽이 모양으로 변하고있다는것을 들었습니다. 즉 나이의 중앙값이 20대에서 점점 30,40대로 옮겨가고 있음을 의미합니다. 이러한 현상이 다른나라에도 일어나고있는지를 알기 위해 나이의 중앙값을 살펴봄으로서 파악하고 싶었습니다.  결과물부터 보여주자면 아래와 같습니다.

![png](/assets/images/Tableau_ex/5_34.PNG)

# 말말말

이미 데이터를 받을떄에 어느정도 aggregated 가 되어있는 집계된 데이터라 별로 어렵지는 않았다. 다만 시트 하나에 여러 정보들이 혼재되어있어서 따로 나누어 주고, 분리하여서 시각화하는것이 약간 귀찮았습니다.

아래와 같이 나라별로 인구중위수가 표현되어있기도 하지만

![png](/assets/images/Tableau_ex/5_1.PNG)

같은 시트 안에 인구개발 / 지역별로 다른 인구 중위수가 표현되어있다. 

![png](/assets/images/Tableau_ex/5_2.PNG)



# 전처리

우선 전처리를 해야했습니다. 위에서 보았듯이, 같은 시트안에 여러 정보들이 혼재되어있었습니다.  이 데이터를 다른 시트로 옮겨담습니다. 아래 사진과 같이 3개의 시트로 나라별 / 지역별 / 개발 수준별로 나누어 담았습니다. 또한 사이사이 빈 공간을 없애게 처리하였습니다. (큰 데이터라면 파이썬으로 하는것이 간편하지만, 겨우 100kb 도 안되는 데이터인 경우는 엑셀을 이용하는것이 훨씬 편리합니다.)

![png](/assets/images/Tableau_ex/5_3.PNG)

이떄 주의할점! 저장할때에 csv 가 아니라 excel 파일로 저장해야합니다. 그렇지 않은경우 태블로가 다른 시트를 인식하지 못합니다. 아래 그림을 보면 알겠지만 원래 파일은 csv 이지만 엑셀파일로 저장하였습니다. 

![png](/assets/images/Tableau_ex/5_4.PNG)

이제 파일을 열어보면 다음과 같습니다. 왼쪽 SHEET 를 보면 우리가 만든 3개의 시트가 들어있는것을 확인할 수 있습니다. 그런데 열 이름을 제대로 인식하지 못하고있네요. 그런 경우에는 아래와 같이 first row 를 column name 으로 인식하도록 설정해주면 됩니다.

![png](/assets/images/Tableau_ex/5_5.PNG)

![png](/assets/images/Tableau_ex/5_6.PNG)

![png](/assets/images/Tableau_ex/5_7.PNG)

이제 아래와 같이 pivot 을 설정합니다

![png](/assets/images/Tableau_ex/5_8.PNG)

![png](/assets/images/Tableau_ex/5_9.PNG)

그리고 나머지 시트에 대해서도 같은 처리를 진행합니다.



# 시각화(map)

다음과 같이 맵 시각화를 진행해봅시다. 각 인구수 중위값을 지역별로 표기한것입니다. 

![png](/assets/images/Tableau_ex/5_10.PNG)

이때에 오른쪽 하단을 보게 되면 , unknown 데이터가 있는것을 볼 수 있다. 이는 맵핑이 실패한것으로, 국가 이름이 테블로에서 제공하는 형식과 맞지 않기 때문이다. 즉 아래와 같이 맵핑을 수동으로 처리하자. 

![png](/assets/images/Tableau_ex/5_11.PNG)

일일히 맵핑을 끝내고 나면 아래와 같이 진행된것을 볼 수 있다.

![png](/assets/images/Tableau_ex/5_12.PNG)

이때에 남극이나 북극처럼 필요없는 국가들이 있어서 위 아래로 쓸모없는 공간이 있는것을 볼 수 있다. 이 경우 안그래도 좁은 대시보드를 많이 차지하게 되어서 비효율적이다. 그러므로 Map 에서 레이아웃을 조절해 없애자.

![png](/assets/images/Tableau_ex/5_13.PNG)

이제 나이를 sum 이 아니라 Average 로 바꾸자. 그 이후에 color 를 다음과 같이 수정하자. 그냥 연속형으로 두기에는 색 대비의 효과가 극적으로 보이지 않기 떄문이다. 

![png](/assets/images/Tableau_ex/5_14.PNG)

이제 년도별로 살펴보자. 그냥 filter 에 넣고 그 필터를 표시할 수도 있다. 하지만 이는 년도별로 재생해보면서 어떻게 변하는지를 확인하는 애니메이션 효과가 없이 그저 내가 골라볼 수 밖에 없다. 그러므로 Year 변수를 Pages 에 올리자. 

![png](/assets/images/Tableau_ex/5_15.PNG)



# 시각화(ranking)

이제 랭킹차트를 구성하자. 우리는 아예 새로운 시트에 데이터가 있으므로 다른 시트의 데이터를 불러오기 위해서 Data 메뉴에서 새로운 데이터소스를 불러오자.

![png](/assets/images/Tableau_ex/5_16.PNG)

그 이후 내가 불러온 같은 엑셀 시트를 선택한다. 

![png](/assets/images/Tableau_ex/5_17.PNG)

그 이후 데이터 탭에서 새로운 시트인 regions 를 고르고 데이터를 정제한다.(위 전처리에서와 같이)

![png](/assets/images/Tableau_ex/5_18.PNG)

이제 시각화를 구성하자. year 과 age 를 view 로 끌어온다.

![png](/assets/images/Tableau_ex/5_19.PNG)

ranking 차트를 구성할것이므로 Quick Table Calculation 에서 Rank 를 선택한다. 

![png](/assets/images/Tableau_ex/5_20.PNG)

이제 Mark 의 세부사항에 지역을 올려넣고, rank 계산에 Table 이 아니라 Region 을 선택한다. 그 이유는 우리가 봐야할것은 '지역별 인구 ranking 이기 때문이다.'

![png](/assets/images/Tableau_ex/5_21.PNG)

이제 dual axis 를 구성한 뒤

![png](/assets/images/Tableau_ex/5_22.PNG)

axis 를 합치고. 두번째 view 에 대해서는 line 으로 mark 를 변경한다. 

![png](/assets/images/Tableau_ex/5_23.PNG)

1등이 맨 위에 와야하므로 scale 을 Reversed 로 조절한다. (dual axis 이므로 옆 axis 에게도 똑같이 적용)

![png](/assets/images/Tableau_ex/5_24.PNG)

이제 Region 의 색상을 구분해야하므로, 지역을 색상마크에 올려놓는다.

![png](/assets/images/Tableau_ex/5_25.PNG)

그리고 각각 지역을 legend 로 보기에는 너무 불편하므로 line 첫부분에 보이도록 조절하자. 이때에는 정렬과, mark 가 line  어느쪽에 올지, font 는 진하게 할것인지 등을 설정한다.

![png](/assets/images/Tableau_ex/5_26.PNG)

그리고 text 가 너무 길어서 왼쪽이 약간 짤리는 현상이 있다. 그러므로 글씨 앞에 빈공간을 추가하여, 짤리는 현상을 방지하자.  

![png](/assets/images/Tableau_ex/5_27.PNG)

완성된 뷰는 다음과 같다. 

![png](/assets/images/Tableau_ex/5_28.PNG)

# 시각화(Line)

이는 별로 할 말이 없다. 앞의 것을 응용하면 금방 할 수 있다! 

![png](/assets/images/Tableau_ex/5_29.PNG)



# 대시보드 구성

우선 대시보드 먼저 보여주자면 다음과 같이 구성할 것이다. 이를 구성하기 위해서 축을 없애거나, axis 를 회전시키는것 등등은 생략하자. 

![png](/assets/images/Tableau_ex/5_30.PNG)

우선 legend 를 구성할때에는 아래 그림과 같이 아래를 향한 세모를 누른 뒤, legend 나 show page control 을 누르면 해당 view 의 legend / pages 가 나오게 된다. 이를 부동(float) 으로 바꾼뒤 내가 놓을곳에 놓으면 된다.

![png](/assets/images/Tableau_ex/5_31.PNG)

그리고 Caption도 넣을 수 있는데 위와 같이 아래 세모를 클릭한 뒤, 

![png](/assets/images/Tableau_ex/5_32.PNG)

원하는 텍스트를 수정하면 된다. 

![png](/assets/images/Tableau_ex/5_33.PNG)



# Result

<iframe seamless frameborder="0" src="https://public.tableau.com/views/Book1_16166863190180/Dashboard1?:embed=yes&:display_count=yes&:showVizHome=no" width = '1000' height = '860' scrolling='yes' ></iframe>