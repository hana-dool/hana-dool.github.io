---
title:  "Design Dasboard"
excerpt: "대시보드 디자인의 정석"
categories:
  - Tab_Article
tags:
  - 3
last_modified_at: 2021-05-04

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---



# Intro

Tableau 의 Zen Mater 인 Chantilly jaggernauth 의 강연을 듣고 정리한 내용입니다. <https://www.youtube.com/watch?v=bq0jeF9bv20> 에서 강연을 보실 수 있습니다. 대시보드의 기본이 얼마나 중요하고, 고려할게 많은지를 알 수 있게해주는 레전드 강연이라고 생각합니다.

#  목차

- Gather requirements
- Create a template
- Use icons and art to your advantage
- choose color
- Fonts

# Gather Requirement

- 먼저 프로젝트의 목표를 이해해야한다.
- 이 대시보드를 보는 사람들의 수준을 이해해야한다.
- 사용자들이 어떤것을 좋아하는지 파악한다.
  - 색깔 , 로고, 사이즈 .등등.
- 이 뷰를 통해서 어떤 질문에 대해 답하고 싶은지를 정하라.

![png](/assets/images/Tab_Article/1_1.png)

1. Dashboard overview
   - 대시보드의 전체적인것을 정해야한다.
   - 이름은 어떻게 정할까? 
   - 어떤 목표를 정해야할까?
   - 이 대시보드를 보는 사람들(사용자)은 시간을 얼마나 들일까?
2. Audience
   - 사용자들의 수준을 이해하자. 
   - 그 사람들은 대부분 태블로를 보르고, 처음 본 사람들일것이다.
3. Display Mode
   - 사람들이 핸드폰으로 볼지, 컴퓨터 화면으로 볼지 등에 따라 사이즈를 다르게 해야한다.
4. Use
   - 유저가 어떤 포멧의 시각화를 원할지를 파악해야한다.
   - 이미지 / pdf / 웹 등등....
5. Dashboard Filters / Notes...
   - 유저가 보고싶어할 만한 정보들을 정해본다.
   - 어떤색을 선호할지, 어떤 로고, 아이콘 등등..

![png](/assets/images/Tab_Article/1_2.png)

1. 차트가 어떤것에 집중할지를 정한다.
   - order, sales , profit, profit ratio for each region
2. 어떤 필드가 쓰여질지를 정한다.
   - Region / Customers / Orders / Sales / Profit / Profit Ratio
3. 어떤것을 Calculated 해야되는지를 결정한다.
   - Customers / Orders / Profit ratio
4. 어떤 Filter 를 쓸 것인지 정한다. 
   - 미정
5. 데이터 소스를 어떻게 연결할지 결정
   - SCV
6. 추가적 정보
   - 텍스트 테이블이 선호됨.

# Create Template

데이터를 분석하고, 유저들에게 전달할 insight 를 결정하고 나면, Grid-Like Template 를 구성하면 우리의 생각을 구성하는데에 큰 도움이 된다. (Chantilly - Jaggernauth)

![png](/assets/images/Tab_Article/1_3.png)

1. 필요로 하는것을 적어본다. 중요한 것만 사용하자.
   - 고객수, 주문수, 이익, 매출
   - Monthly sale per Region
   - Metric details per Region
   - Region Segment sales
   - Sales per State
   - Sales per Sub-category
2. 아웃라인을 종이, 펜 등을 이용해 구성해보기

3. Grid 를 디자인해보기
   - 위에서 그린 스케치대로 그리드를 대충 구상해본다. 

![png](/assets/images/Tab_Article/1_4.png)

4. incoporate banner 를 구성한다. (통합된 정보가 보여지는 값 박스)
   - 유저가 detail 에 접근하기 전에, summary 를 제공한다. 

![png](/assets/images/Tab_Article/1_5.png)

- 아래와 같이 왼쪽에 배너를 구성할 수도 있다.

![png](/assets/images/Tab_Article/1_6.png)

- 하지만 아래와 같이 아래쪽이나 오른쪽에는 구성하면 안된다.
- 그 이유는 사람들은 통상적으로 시선이 왼쪽 상단부터 우측 하단으로 향하기 떄문이다.

![png](/assets/images/Tab_Article/1_7.png)

5. 계층을 보여주기 위해서 위치와 사이즈를 조절하자.
   - 유저는 위에서 아래로, 왼쪽에서 오른쪽으로 시선이 이동하는것을 기억하자.
   - 필터는 맨 위에 구성한다. 
   - 아래와 같이 1~6 순서에 따라 중요한 순서대로 구성하자. 

![png](/assets/images/Tab_Article/1_8.png)

6. 아이콘과 색깔에 대해서 고민해보자. 
   - 너무 많이 아이콘을 사용하지 말자
   - 아래의 경우 왼쪽은 아이콘을 5개만 사용했지만 오른쪽은 너무 많이 사용해서 복잡해진다.

![png](/assets/images/Tab_Article/1_9.png)



# Fill the Template

![png](/assets/images/Tab_Article/1_10.png)



# Reuse Template

사용했던 탬블릿을 재사용하자. 아래의 경우 Template 은 같지만 내용을 다르게 해서 구성한 것이다.

![png](/assets/images/Tab_Article/1_11.png)

![png](/assets/images/Tab_Article/1_12.png)



# Using icon

아이콘을 잘 사용하게 된다면, 대시보드를 한번에 이해하는데에 도움을 준다.

![png](/assets/images/Tab_Article/1_14.png)

## 쉽고 직관적인 icon 사용

아래와 같이 직관적인 아이콘을 사용함으로서 한눈에 들어오도록 하고 있다.

![png](/assets/images/Tab_Article/1_13.png)

##  설명글을 같이 쓰기

아래와 같이, 아이콘 옆에 설명글을 같이 붙여, 사용자가 이 아이콘이 어떤의미를 지니는지 알게 해주어야 한다. 

![png](/assets/images/Tab_Article/1_15.png)

![png](/assets/images/Tab_Article/1_16.png)



## 창의적이지 말자

아래의 두 경우를 보자. 어떤경우가 더 좋은가? '모든사람이 쉽게 이해할만한 아이콘' 을 사용하는것이 좋다.

![png](/assets/images/Tab_Article/1_18.png)

![png](/assets/images/Tab_Article/1_17.png)



## 스타일을 통일하자.

아래를 보면 첫쨰줄은 괜찮다. 두번쨰줄은 3번째 아이콘이 다른것과 이질것이다. 세번쨰 줄은 두번쨰 아이콘이 이질적이다. 즉 Consistency 를 유지해야한다.

![png](/assets/images/Tab_Article/1_19.png)

아래는 사람의 시각화만 색으로 차있는것을 볼 수 있다. 이는 안좋은 대시보드이다. 

![png](/assets/images/Tab_Article/1_20.png)

아래 그림들은 좋은 아이콘들의 예시이다.

![png](/assets/images/Tab_Article/1_21.png)

![png](/assets/images/Tab_Article/1_22.png)



## 대시보드와 색을 통합하자.

아래의 경우를 보자. 색을 다양하게 줄 필요 없다.

![png](/assets/images/Tab_Article/1_23.png)

아래와 같이 이질적인 색이 끼어있다. 이는 별로 좋지 않다. 

![png](/assets/images/Tab_Article/1_24.png)

고객이 "다양한 색을 넣고싶어요! " 라고 해도, 넣지마라.. 



## 아이콘의 수준을 낮춰라

아래와 같은 경우를 보자. Graphic Design 이 복잡할 필요 없다. 심플하게, 우리가 알만한 경우로만 제한하는것이 좋다.

![png](/assets/images/Tab_Article/1_25.png)

아래를 보면 이 아이콘이 무슨소리 하는거지? 싶다..

![png](/assets/images/Tab_Article/1_26.png)



## Icon Reference

- <www.flaticon.com>
- <www.thenounproject.com>
- <www.icons8.com>



# Color

색상을 정하는것도 중요하다. 중요한은 절제와 균형이다. 너무 많은 색상을 사용하는것은 미관을 해치고 , 이해하기 힘들게 한다. 다음과 같은 사항들이 있고, 이를 차례차례 알아보자.

![png](/assets/images/Tab_Article/1_37.png)

## Brand Color

Dominant 한 색으로 Brand Color 을 이용하자. 이를 이용하여 대시보드를 구성하자. 아래의 경우를 보자. Linked in 의 색상에 맞추어서 색을 정하였다.

![png](/assets/images/Tab_Article/1_27.png)

아래의 경우는 Women's march 라는 로고 색상에 맞춰 대시보드를 구성한 예시이다.

![png](/assets/images/Tab_Article/1_28.png)



## 다른 Visualization 참고

health care 에 대한 Visualization 을 하려한다고 하자. 그럴떄에는 아래와 같이 구글링을 통해서 좋은 시각화를 찾는다. 

![png](/assets/images/Tab_Article/1_29.png)

그 이후에 아래와 같이 시각화를 진행할때에 색상을 참고하였다.

![png](/assets/images/Tab_Article/1_30.png)

또는 Tableau Public 을 이용할 수 있다.

![png](/assets/images/Tab_Article/1_31.png)

![png](/assets/images/Tab_Article/1_32.png)



## Dominant Color 를 제한

1~2개만을 추천한다. 

![png](/assets/images/Tab_Article/1_33.png)

![png](/assets/images/Tab_Article/1_34.png)

![png](/assets/images/Tab_Article/1_35.png)

아래와 같이 많은 색상을 사용한 경우, 집중력이 분산된다.

![png](/assets/images/Tab_Article/1_36.png)



## 다양한 Color 를 시험해보기

아래와 같이 다양한 색깔을 시험해보자. 한눈에 들어오는 색깔을 선택한다. 

![png](/assets/images/Tab_Article/1_38.png)

![png](/assets/images/Tab_Article/1_39.png)

하지만 아래의 경우는 옳지 않다. 

![png](/assets/images/Tab_Article/1_40.png)



## 컬러를 의도적으로 사용하라

아래의 경우 의도적으로 색을 사용하였다. 노란색은 가장 많이 태양빛에 대한 연관성을 나타내기 위해 사용하였고, 회색은, 적은 태양빛을 표현하기 위해 사용하였다. 

![png](/assets/images/Tab_Article/1_41.png)

아래의 경우는 강화를 위해 사용한 예시이다. 파란색은 1등 나라를 강화(강조) 하기 위해 사용하였다.

![png](/assets/images/Tab_Article/1_42.png)

아래의 경우는 다른색으로 freedom of free 를 나타낸 경우이다. 

![png](/assets/images/Tab_Article/1_43.png)



## 막히는 경우에는 Gray 로 먼저 구성해보기

아래와 같이 우선 단색으로 구성해본다.

![png](/assets/images/Tab_Article/1_44.png)

타이틀 , Filter , BAN 에 대해서 먼저 색을 구성해본다.

![png](/assets/images/Tab_Article/1_45.png)

아래와 같이, 색을 넣어보았다.양 옆은 각각 다른 색 구현을 보여준다. 

![png](/assets/images/Tab_Article/1_46.png)

그 이후에 각각 차트에 대한 시각화를 본다. 혹시 하이라이트는 필요하지 않을까?

![png](/assets/images/Tab_Article/1_48.png)

하이라이트는 표에 넣는게 효과적이므로, 2개의 표에 대해서 하이라이트를 넣어야 할 지 생각해보자. 중앙의 표는 Scale 이 다르다. 즉 하이라이트로 구성하게 되면 5개의 색이 필요할 것이다. 이는 부적절 하다. 즉 scale 이 동일한 맨 왼쪽 표에 대해서만 하이라이트를 적용하도록 하자.

![png](/assets/images/Tab_Article/1_49.png)

그리고 맵에 대해서도 색을 구성해보자. 이 역시 Dominant 한 보라색으로 시각화를 하는것이 좋을것이다.

![png](/assets/images/Tab_Article/1_50.png)

Bar 에 대해서는 이미 '길이' 로 크기를 나타내고 있기 떄문에 색상을 넣는것은 부적절하다. 그러므로, 연한 회색으로 통일하자. (검은색은 너무 강함) 

![png](/assets/images/Tab_Article/1_51.png)

그리고 미세한 부분들을 조절하면 된다. 

![png](/assets/images/Tab_Article/1_52.png)

이떄 각각의 소제목들에 대해서 모두 왼쪽처럼 강조처리를 해야할까? 그러지 말자. 강렬한 강조는 제목만으로 족하다.  그렇다면 오른쪽처럼 상자처리를 할까? 여전히 너무 강조되는 효과가 있다. 

![png](/assets/images/Tab_Article/1_53.png)

아래와 같이 산뜻하게 회색으로 Shade 를 주거나, 그냥 주지 않는법이 좋다. 

![png](/assets/images/Tab_Article/1_54.png)



# Font

태블로의 폰트도 중요한 사항이다. 기본적으로 다음과 같은 기본사항이 있다.

![png](/assets/images/Tab_Article/1_55.png)



## 하나의 가독성이 좋은 폰트를 사용

다음의 경우, 하나의 폰트를 사용하였으나, 가독성이 좋지가 않다. 

![png](/assets/images/Tab_Article/1_56.png)

다음과 같이 태블로 폰트로 통일하는것도 가독성이 좋다.

![png](/assets/images/Tab_Article/1_57.png)



## font size 는 4개이하로 제한

아래의 시각화를 보면, 사이즈를 4개로 제한한것을 볼 수 있다.

![png](/assets/images/Tab_Article/1_58.png)



## Custom font 는 피해라

아래를 보면 왼쪽은 Mac 의 Native font 이다. 이를 Tableau Online 에 올린다면 렌더링 문제로 인해서 다른 폰트를 얻게 된다. 즉 웬만하면 기본 폰트를 사용하는것이 좋다.

![png](/assets/images/Tab_Article/1_59.png)

다음과 같은 Tableau 와 Compatible 한 Font 들이 있다.

![png](/assets/images/Tab_Article/1_60.png)



## 배경색과 잘 맞는 폰트를 사용하자

<https://accessible-colors.com/> 에 가서 아래와 같은 시험을 할 수 있다.

![png](/assets/images/Tab_Article/1_61.png)

이를 이용해 아래와 같이 시험해볼 수 있다. 우측 사진의 실험을 보면 파란색 작은 글씨가 잘 보이는지 실험하고 있다.

![png](/assets/images/Tab_Article/1_62.png)

실험을 통해서, 약간 밝은 바탕색이 파란글씨가 더 가독성이 좋음을 알 수 있었따.

![png](/assets/images/Tab_Article/1_63.png)



## 강조를 위해 Bold 체 / 색깔 을 넣어라

아래의 경우는 볼드체를 통해서 특정 단어를 강조한 예시이다.

![png](/assets/images/Tab_Article/1_64.png)

아래의 경우는 다른 색깔을 통해서 강조한 예시이다.

![png](/assets/images/Tab_Article/1_65.png)



## 왼쪽 또는 오른쪽으로 Align 을 맞춰라

즉 center는 피해야 한다는 것이다. 왜 그럴까? 아래의 예시를 보자. 어느 Align 이 더 읽기가 쉬울까?

![png](/assets/images/Tab_Article/1_66.png)

아래를 보면 Center 로 맞춘 경우 Text 를 읽기가 약간 어려운것을 볼 수 있다.

![png](/assets/images/Tab_Article/1_67.png)





# Business Case

아래의 실제 예시를 보면서 우리가 배운것을 어떻게 적용하였는지 보자. 시각화 자체는 간단해 보이지만, 이를 위해서 얼마나 많은 공이 들어갔는지 알 수 있을것이다.

![png](/assets/images/Tab_Article/1_68.png)



# Summary

![png](/assets/images/Tab_Article/1_69.png)

Anyone Can be a Designer ! 