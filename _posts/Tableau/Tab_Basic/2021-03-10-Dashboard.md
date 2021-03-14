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

![png](/assets/images/Tableau/21_4.png)

이러한 효과를 통해 사용자와 Interactive 한 시각화를 구성할 수 있다. 

![png](/assets/images/Tableau/21_5.png)

그 밖에 위와 같이 Highlighter를 이용하여 원하는 데이터를 선택하면 뷰에 표시되게 할 수 있다.

![png](/assets/images/Tableau/21_6.png)





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





#가독성이 좋은 대시보드

가독성이 좋은 대시보드를 만들기 위해서는 완성된 통합 문서로부터 거꾸로 작업하여 접근성을 좀 더 높힐 수 있다

먼저 아래와 같은 대비소드를 좀 더 가독성이 좋게 수정하려 한다고 하자.

![png](/assets/images/Tableau/21_15.png)

.

## 색 조절

색의 대비가 클 수록 더 집중할 수 있는 효과가 있다. 즉 명암비의 차이를 최대화 하기 위해서 배경을 흰색으로 만들고, 검은색 굵은 글씨로 Text 를 변경하자.

먼저 대시보드의 format 에 들어가 Default 색상을 none 으로 교체한다.

![png](/assets/images/Tableau/21_16.png)

그 이후 폰트의 색깔을 바꿔야 한다. 그런데 이때, 각각의 워크시트를 클릭한 뒤 , Format 에서 각각 서식 지정을 해 주어야 할까? 물론 이렇게 해도 되지만 많은 view(워크시트) 들을 한번에 바꾸고 싶을것이다. 이럴때에는 Format(서식)>Workbook(통합문서) 를 선택한다. 그 이후 worbook 의 폰트를 변경하면 모든 대시보드에 대해서 적용된다. 

![png](/assets/images/Tableau/21_17.png)

이제 아래와 같이 배경색이나, Text 들의 대비가 안좋아서 한눈에 보기 힘들었던 대시보드가 어느정도 가독성이 좋아졌다. 

![png](/assets/images/Tableau/21_18.png)



## Group 을 이용한 카테고리 수 조절

대시보드를 구성하다보면 전달하려는 양이 너무 많아지는 경우가 있다. 위 대시보드를 보자. 맨 위의 막대그래프는 지역과 Category 에 대한 분류가 너무 많아서, 한눈에 정보가 들어오지 않는 모습이다.  (분절되어있는 막대의 경우, 별로 추천하지 않는 방법)

![png](/assets/images/Tableau/21_19.png)

아래와 같이 많은 카테고리를 하나로 통합하기 위해서 Grouping 을 진행하자. Grouping 을 통해서 많은 카테고리들을 적은 카테고리로 줄일 수 있다 그러면 아래와 같이 좀더 알기 쉬운 형태로 변하게 된다.

![png](/assets/images/Tableau/21_20.png)

![png](/assets/images/Tableau/21_21.png)



## 중복 정보 제거

아래의 데이터를 보자. 막대그래프를 한눈에 보더라도 매출의 차이를 한눈에 볼 수 있다. 하지만 음영의 차이로도 그 매출의 차이를 확인시키고 있다. 이렇게 같은 정보가 겹칠 필요가 있을까? 답은 NO! 괜히 막대의 높낮이 정보와음영의 정보가 중복되고 있는 것이다. 이러한 경우 하나의 것을 없애주는것이 가독성을 높여준다.

![png](/assets/images/Tableau/21_22.png)



## 색맹을 위한 색상

정상적인 사람은 해당되지 않으나, 색맹이 있는 사람의 경우 색상을 잘 구분하지 못한다. 그러므로 우리가 색을 선택할 떄에도 그러한 점을 고려해야 한다. 다행히 Tableau 에서는 색맹을 위한 색상표를 제공학 있으며 이를 이용한다면 색맹인 사람들도 색을 잘 구별할 수 있게 해준다. 아래의 꺾은선 그래프는 색맹인사람이 구별하지 못할 수 있다. 

![png](/assets/images/Tableau/21_23.png)

Color 조절에서 color palette 로 들어가 color blind 로 들어간다. 아래 색상표를 적용하게 된다면 색맹인 사람에도 잘 구분할 수 있게 해준다. 

![png](/assets/images/Tableau/21_24.png)





## 구분이 더 잘되는 그래프 

아래의 그래프를 보자. 시간에 따라서 각 Product type 에 대한 추이가 나오고 있다. 하지만 Product 가 너무 많아서 겹치는 정보가 너무 많은탓에 잘 구분이 되지 않는다. 

![png](/assets/images/Tableau/21_23.png)

위에서 중복 정보는 제거하라고 하였지만, 위처럼 '구분이 되지 않는' 경우에는 잘 구분되게 하기 위해서 색상 말고도 '마크' 를 이용해서 좀 더 구분되게 할 수 있다. 아래와 같이 shape 의 정보를 추가한 뒤, 색상 마크에서 shape 를 선택하자 . 그러면 각 마크에 대해 2개의 차트가 생긴다(마크로 구분되는 차트와 색으로 구분되는 차트) 이 둘을 이중축을 이용해 합치자.

![png](/assets/images/Tableau/21_25.png)

![png](/assets/images/Tableau/21_26.png)

그러면 아래와 같이 좀더 구분이 잘 되는 View 가 된 것을 볼 수 있다. 

![png](/assets/images/Tableau/21_27.png)



## Filter 를 이용한 카테고리 수 조절

아래 그림과 같이 그래프에 너무나 많은 Category 들이 겹쳐있다. 이런 경우 너무 정보가 많아 제대로 추이를 보기 힘들다는것이 문제이다. 이럴때에 해결법중 하나는 Group화를 시키는 것이였다. 하지만 정보의 손실을 어느정도 감수해야하기 떄문에 꺼려질 수 있다. 이런 경우 Filter 를 이용하여 처리할 수 있다.

![png](/assets/images/Tableau/21_28.png)

먼저 제품 중분류 별로 정보가 너무 많았기 떄문에, 제품 대분류와 제품 중분류를 묶어 계층을 만든다. (여기서 사용한 '제품 대분류' 같은 분류가 없을시에는, group화 시켜서 새로운 변수를 만든 후, 그 변수를 상위 분류로 놓아 계층을 만들면 된다.) 그리고 이 계층을 필터에 두게되면, 제품 대분류가 필터로 들어간다. 

![png](/assets/images/Tableau/21_29.png)

이제 필터의 값을 선택하면서 우리가 원하는 카테고리만 선택적으로 얻을 수 있다.

![png](/assets/images/Tableau/21_30.png)