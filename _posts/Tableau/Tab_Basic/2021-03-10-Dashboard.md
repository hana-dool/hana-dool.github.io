---
title:  "Dashboard"
excerpt: "대시보드"
categories:
  - Tableau
tags:
  - 3
last_modified_at: 2021-03-12

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---



# 효율적인 대시보드

대시보드에 마구잡이로 view 를 넣는다고 해서 좋은 시각화가 되는것은 아니다. 목표와 대상을 파악하고, 이 visualization 으로 전하려는게 무엇인가? 어떤 의미가 있는지, 주제가 뭔지, 스토리가 뭔지, 그리고 어디에 활용하려는것인지 등의 목적에 따라 다르게 구성해야 한다. 

## 가장 많이 보는 지점 활용 

대시보드를 살펴볼때, 대부분 왼쪽 위부터 콘텐츠를 살펴본다. 즉 대시보드의 기본적인 용도를 파악했다면 가장중요한 뷰를 대시보드 왼쪽 위레다가 표시해야한다.

<https://help.tableau.com/current/pro/desktop/ko-kr/dashboards_best_practices.htm>

![png](/assets/images/Tableau/21_1.PNG)



## 현실에 맞는 크기

태블로는 대시보드의 고정크지 또는 크기를 자동으로 설정할 수 있습니다. 대시보드는 최종 사용자가 사용하게 되는 디스플레이 크기를 고려하여 그 크기를 설정해야합니다. 

![png](/assets/images/Tableau/21_2.PNG)



## 적당한 뷰의 수

일반적으로 대시보드에 포함되는 뷰의 갯수는 2~3개로 제한하는것이 좋다. 너무 많은 뷰를 추가하게 되면 시각적으로 명확성이 떨어지고, 내가 원하는 정보를 얻기 힘들어진다. 

![png](/assets/images/Tableau/21_3.gif)



## 상호작용 추가

필터를 사용하여 뷰에 표시할 데이터를 지정할 수 있다. 

![png](/assets/images/Tableau/21_4.PNG)

이러한 효과를 통해 사용자와 Interactive 한 시각화를 구성할 수 있다. 

![png](/assets/images/Tableau/21_5.PNG)

그 밖에 위와 같이 Highlighter를 이용하여 원하는 데이터를 선택하면 뷰에 표시되게 할 수 있다.

![png](/assets/images/Tableau/21_6.PNG)







# 대시보드 구성



## Filter 로 사용

아래와 같이 대시보드를 생성하고 Use as filter 를 사용하여 필터로 사용할 수 있다. 

![png](/assets/images/Tableau/21_7.PNG)



## 경계선 추가

아래와 같이 경계선을 추가할 수 있다. 

- Border 에서 경계선을 선택할 수 있다.
- Padding 에서 그 경계선의 padding 수준을 정할 수 있다.

![png](/assets/images/Tableau/21_8.PNG)



## 사진 배경

<https://www.pexels.com/ko-kr/> 나는 사진을 많이 수집했다. 사진을 resize 하는것이 다운로드할 때부터 가능해서 바로 테블로의 사이즈에 맞게 사진을 저장하여 이용하기 편헀다.

아래와 같이 사진 파일의 사이즈와 맞게 view 의 size 를 조절한다.

![png](/assets/images/Tableau/21_9.PNG)

그리고 Object 에서 이미지를 누른 후, 내가 넣고 싶은 사진을 클릭한 이후, Opstions 에서 Fit image 와 center image 를 클릭한다. 사진 정렬과 자동으로 fit 해주는 기능인데, 사실 내 사진 사이즈와 테블루에서 뷰를 생성할때 지정한 사이즈와 맞으면 별로 할 필요가 없는 기능이긴 하다.

![png](/assets/images/Tableau/21_10.PNG)

다음과 같이 사진이 알맞게 배경에 박힌것을 볼 수 있다. 이제 여기 위에다가 우리의 Visualization 을 넣을 차례이다. 먼제 Object 에서 Floating 을 설정한다. 이유는 배경 '위' 로 나의 시각화가 올라와야 하기 때문이다.

![png](/assets/images/Tableau/21_11.PNG)

우선 시각화를 추가하게 되면 위와같이 하얀 Layout 이 보이게 될 것이다. 하지만 우리가 원하는건 이게 아니라, 배경을 그래로 둔 상태에서 시각화만 투명하게 위로 올리고싶다.

![png](/assets/images/Tableau/21_12.PNG)

그를 위해서라면 view 를 선택한 상태에서 shading 을 지정하고, Default 를 None 으로 지정한다. 그러면 그래프의 배경(worksheet) 이 None 이 되면서 뒤까지 뚫려서 보이게 된다. 

![png](/assets/images/Tableau/21_13.PNG)

완성! 솔직히 잡기술이라 쓸 데가 있나싶긴한데, 보여주기식으로 구성할때에 쓰면 좋을거같기도?

![png](/assets/images/Tableau/21_14.PNG)