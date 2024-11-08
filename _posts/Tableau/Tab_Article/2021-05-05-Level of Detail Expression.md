---
title:  "Level of Detail (LOD)"
excerpt: "태블로의 LOD"
categories:
  - Tab_Article
tags:
  - 3
last_modified_at: 2021-05-05

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
typora-root-url: ../../../../hana-dool.github.io
---



# Intro

Tableau 의 Alan Eldridge, Tara Walker 가 태블로 공식 홈페이지에 올린 LOD 에 대한 설명글에 대한 정리입니다. 

# Vis LOD

데이터 탐색의 핵심은 원본의 구조를 이해하는 데 있습니다. 예를 들어 가장 세부적인 수준이 주소별로 나열된 레스토랑 검사 데이터가 있다고 가정해 보겠습니다. 데이터를 집계하여 우편 번호, 구/군/시, 시/도 또는 국가별로 속성을 확인해 보려고 합니다. 

Tableau에서는 일반적으로 원하는 차원(예: 구/군/시, 시/도)을 뷰에 드롭하여 이러한 작업을 수행할 수 있습니다. 뷰에 추가하도록 선택한 차원에 따라 데이터가 ‘비주얼라이제이션 세부 수준’ 즉, 비주얼라이제이션 LOD (vis LOD) 로 집계됩니다.

아래와 같이 비쥬얼라이제이션 LOD 에 추가하는 방식은 데이터 테이블에서 View 로 필드를 옮겨놓는것을 통해 이루어집니다. 

![png](/assets/images/Tab_Article/3_1.png)

하지만 아래와 같이 페이지 / 필터 / 도구 설명에는 추가해도 vis LOD 수준을 변경하지 않습니다.

![png](/assets/images/Tab_Article/3_2.png)



# LOD expression

LOD 표현식을 사용하면 세부 수준(예: 차원) 을 비주얼라이제이션에 실제로 드롭하지 않고도 계산에서 사용되는 세부 수준을 결정할 수 있습니다. 비주얼라이제이션 LOD와 독립적으로 계산을 수행할 세부 수준을 정의할 수 있습니다. 

레스토랑 검사 데이터를 사용하는 다음 예의 경우 뷰에 다음 두 개의 차원을 추가되었습니다.(city 와 state)

![png](/assets/images/Tab_Article/3_3.png)

뷰에 있는 데이터는 비주얼라이제이션 LOD를 기반으로 집계되었습니다. 즉, 이 경우 city 와 state 로 구성되며 초기 데이터 원본에 비해 더 세부적으로 집계되었습니다. 이미지에서 선택된 지점은 에든버러 지역(state)의 뉴브리지(city)에 있는 모든 레스토랑의 평균 사용자층을 나타냅니다. 

뷰에 더욱 세부적인 차원을 추가하면 비주얼라이제이션 LOD의 집계 수준이 낮아집니다. 예를 들어, Business ID(비즈니스 ID)를 세부 정보 선반에 드롭하여 비주얼라이제이션에 추가하면 비즈니스별 평균 사용자층을 볼 수 있습니다. 이렇게 하면 비주얼라이제이션도 변경됩니다. 개별 비즈니스가 맵에서 원으로 표시됩니다. 

하지만 비주얼라이제이션을 변경하지 않으려면 어떻게 해야 할까요? 비즈니스 ID 별 총 고객층을 결정하고 city별 해당 값의 평균을 구하고 city별로 원을 하나씩만 표시하려면 어떻게 해야 할까요? city별 각 레스토랑의 평균 고객 수를 파악하려고 합니다.

이렇게 하려면 비주얼라이제이션에 차원을 드래그하지 않고 뷰에 차원을 추가해야 합니다. LOD 표현식을 사용하면 이 작업을 수행할 수 있습니다.

Fans per Business(비즈니스별 고객 수)라는 새 계산된 필드를 만들어 보겠습니다. 구문에 대한 간단한 소개는 다음과 같습니다

![png](/assets/images/Tab_Article/3_4.png)

이 표현식을 사용하면 비주얼라이제이션에 사용된 다른 차원과 관계없이 Tableau 에서 각 비즈니스 ID에 대한 집계를 수행합니다. LOD 표현식을 사용하여 Business ID(비즈니스 ID)별 총 User Fans(사용자 수)를 계산할 수 있습니다. 이 새 필드를 뷰에 드래그한 다음 city 별 해당 값에 대한 평균을 구할 수 있습니다.

![png](/assets/images/Tab_Article/3_5.png)

LOD 표현식에 FIXED 연산자를 사용하면 Business ID(비즈니스 ID)별로 평균 사용자 수가 더 많은 city에 대한 정보를 얻을 수 있습니다. 

즉, 파란색이 더 진한 city는 인기 있는 레스토랑이 더 많다(또는 해당 city의 인구가 더 많고 이에 따라 레스토랑별 사용자 수가 더 많음)는 것을 의미합니다 (비즈니스 ID 별로(즉 식당별로) 이용자수를 먼저 SUM 집계한 뒤에, 그 값을 AVG 취했으므로)

LOD 표현식 키워드에는 EXCLUDE, INCLUDE, FIXED 등 3가지 유형이 있으며 각 키워드로 LOD 표현식의 범위를 다르게 지정할 수 있습니다.

<br>

# Include : 낮은 세부 수준에서 계산

INCLUDE 키워드는 비주얼라이제이션 LOD에 비해 집계 수준이 낮은 ( 즉 , 더 세부적인) 표현식을 만듭니다. 지정된 차원은 계산이 수행되기 전에 vis_LOD에 먼저 추가됩니다.

![png](/assets/images/Tab_Article/3_6.png)

위의 식에서 꺾인 화살표는 점점 세부 수준으로 쪼개지는것을 의미한다고 보시면 됩니다. INCLUDE 를 통해서, 비주얼라이제이션 LOD에 비해 집계 수준이 낮은 표현식을 만듭니다. (Include Region 이라면, 평균, 합 등으로 표현되어야하는 vis_LOD 에 비해 한단계 낮아진 "지역별 수준" 으로 낮아집니다.) 그 이후에, 함수를 적용해 다시 집계합니다. 

<br>

# Exclude : 높은 세부 수준에서 계산

EXCLUDE 키워드의 핵심은 다음과 같습니다. Tableau에서는 먼저 비주얼라이제이션 LOD에서 제외된 차원을 삭제하고 해당 차원이 없는 것으로 간주하고 계산을 수행합니다. 그런 다음 그 결과가 시각적으로 표시됩니다. 다음 흐름 도표는 Tableau 에서 EXCLUDE LOD 표현식이 수행되는 방법에 대한 시각적인 설명입니다. 

![png](/assets/images/Tab_Article/3_7.png)

EXCLUDE{[region : SUM([sale])]} 을 생각해 보겠습니다. 이 경우 region 을 제외하고 집계하여 집계수준이 한단계 높아집니다. 그 이후에 그 값들을 각 region 마다 복사하여 대체합니다.  

<br>

# Fixed : 정확한 세부수준 지정

FIXED 키워드를 사용하면 계산의 집계 수준을 구체적으로 정의할 수 있습니다. INCLUDE 및 EXCLUDE와 달리 비주얼라이제이션에서 사용되는 차원과 독립적으로 수행됩니다. 

FIXED 표현식의 결과는 FIXED 차원과 비주얼라이제이션 LOD의 관계에 따라 비주얼라이제이션 LOD보다 광범위하거나 세부적일 수 있습니다.

![png](/assets/images/Tab_Article/3_8.png)