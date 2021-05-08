---
title:  "Calculations"
excerpt: "태블로의 Calculation"
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
---



# Intro

Tableau 의 Zen Mater 인 Yven Fornes 가 블로그에 올리 글입니다. 태블로에서 제공하는 4가지 타입의 계산이 어떻게 이루어지고 있는지를 알려주고 있습니다. <https://www.tableau.com/about/blog/2019/9/understanding-how-tableau-calculation-types-work-together> 에서 글을 볼 수 있습니다. 제가 정리한 글인 Tab_Function 에서 Order of oprtation 과 함께 보셔도 좋을것입니다.



# Tableau 의 계산

테블로의 계산이 어떻게 이루어지는지 아는것은 매우 힘듭니다. 이는 Tableau 을 이해하는데에 큰 장애물이 됩니다. 이를 모두 이해하고, 편하게 쓰는데에는 몇년의 시간이 걸리기도 합니다. 아래 예시들을 보면서 Calculation 에 대해서 이해해보도록 합시다.

<Br>

## Row-level Calculations

Row level calculation 은 각 데이터 Row 들에 대해서 이루어지는 계산입니다.

![png](/assets/images/Tab_Article/2_1.png)

이제 [Quantity] * [Price] 에 대해서 계산하고, 이를 새로운 열 (Revenue) 로 추가하겠습니다. 이 계산은 수평적으로 일어납니다.

![png](/assets/images/Tab_Article/2_2.png)

<Br>

## Aggregation calculations

Row level 만으로는 정보의 수준이 너무 낮아서 우리가 원하는 정보를 얻기가 힘듭니다. (평균이라던지 합 등이 궁금함) 그러므로 이러한 연산을 해주는것을 Aggregate calculation 이라고 합니다.

이를 위해서 위에서 구했던 Revenue 를 Month 별로 sum 을 구하겠습니다. 즉 Sum([Revenue]) 를 구해보겠습니다. 이 계산은 수직적으로 일어납니다.

![png](/assets/images/Tab_Article/2_3.png)

<br>

## Table Calcultation

Table Calculation 은 '테이블에 나타난 값을 기준으로 하는 연산' 입니다. 즉  aggregation 된 이후에 일어납니다. 

우리는 월별 누적합(Running sum) 을 구해보겠습니다. 그럴 경우 식은 RUNNING_SUM(SUM([Revenue])) 가 됩니다. 이 식을 계산하기 위해서 태블로는 아래와 같은 과정을 거치게 됩니다. 

![png](/assets/images/Tab_Article/2_4.png)

위와 같은 계산의 순서에 익숙해지셔야 합니다. 



## Level of Detail(LOD) expression

LOD 표현식은 agg 계산이 다른 수준에서 이루어지기를 원할때 사용합니다. Fixed , Exclude , Include 를 사용하게 됩니다. 각각이 어떤것을 의미하는지는 Tab_Function 에서 LOD 를 봅시다. 



# Example

태블로를 사용하는사람들이 자주 묻는 질문중에 하나가, "왜 내가 의도한 계산의 결과가 나오지 않는지? " 이다. 이에 대한 원인중 제일 큰 요인은 계산 순서를 제대로 지키지 못한 경우입니다.  다음의 예시를 봅시다.

global percentage of GDP by country 를 계산하고 싶다고 합시다. 하지만 나라가 너무 많으므로 ,나라들에 대한 정보를 시각화에 나타내기 싫습니다. 그러므로 Table Calculaion 은 쓸 수 없습니다. 그럴 경우 식을 아래와 같이 구성할 수 있습니다.

![png](/assets/images/Tab_Article/2_5.png)

![png](/assets/images/Tab_Article/2_6.png)

위와 같이 시각화를 할 수 있습니다. 

