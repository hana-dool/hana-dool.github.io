---
title:  "Order of operation"
excerpt: "작동의 순서"
categories:
  - Tableau
tags:
  - 3
last_modified_at: 2021-04-18

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# intro

태블로는 각각의 operation 에 따른, 작동 순서가 정해져있습니다. 이를 잘 앍있어야 다양한 filter, action 등을 추가할때에 정확하게 추가할 수 있습니다. 아래 그림과 같이 여러 작동들의 순서가 얽히고 있는것을 볼 수 있습니다. 이러한 순서들을 잘 숙지하고있어야합니다.

![png](/assets/images/Tableau/23_0.png)

각각이 뭔지 알아야 잘 쓸 수 있겠죠? 각각이 뭔지 알아봅시다.

# 1.Extract Filter

Extract filter 란, 아래 그림과 같이 데이터를 불러올때 옆에 있는 Filter 를 말합니다. 즉 데이터를 불러옴과 동시에 바로 필터를 적용하는것이라, 순위가 최상단 일수밖에 없습니다!  아래 그림과 같이 Filter 를 추가할 수 있습니다.

![png](/assets/images/Tableau/24_1.png)

![png](/assets/images/Tableau/24_2.png)

새로 필터가 생긴것을 볼 수 있습니다. 아래 그림과 같이 서울 특별시의 데이터만 남아있는것을 확인할 수 있습니다.

![png](/assets/images/Tableau/24_3.png)



# 2.Row level calculation

Row level calculation 이란 데이터셋 row 각각에 대해 계산되는것을 말합니다. 아래 그림을 보면 각각 손냄에 대해 가격과, 그 수량이 매겨져 있습니다. 이를 Quantity * Price 의 연산으로 곱한 연산을 해줍니다. 그러면 

![png](/assets/images/Tableau/24_4.png)

아래와 같이 '각각의 row' 에 대해서 계산이 되는것을 볼 수 있습니다. 이런 연산을 row level caculation 이라고 합니다. 우리는 아래와 같이 태블로에게 새로운 계산열을 만들라고 명령을 하고 있는것입니다.

![png](/assets/images/Tableau/24_5.png)



# 3. Context Filter

컨텍스트 필터란 무엇일까? 태블로에서 모든 필터들은 독립적으로 적용된다. 즉 필터는 다른 필터들과 상관 없이, 데이터 원본 전체를 대상으로 각각 필터링한다. 하지만 A 를 컨텍스트 필터를 지정했다고 하자. 그러면 그 A 필터가 먼저! 적용된 이후 필터링된 데이터를 나머지 필터들이 필터하게 된다. 즉 필터의 왕이라고 생각하면 된다.

이를 사용하는 이유는 필터가 너무 많거나, 데이터 원본이 큰 경우에 performance 향상을 위해 컨텍스트 필터를 사용한다고 한다. 

아래와 같이 필터를 추가한 뒤에, 오른쪽 키를 누르고 Add to Context 를 선택하자. 그러면 이 필터는 필터중의 황제인 'Context Filter' 로 변신한다. 

![png](/assets/images/Tableau/24_6.png)

![png](/assets/images/Tableau/24_7.png)

#  4. { Fixed }

FIxed 란 뷰에 있는 차원과 상관없이, 계산된 필드에서 고정한(Fixed) 차원의 집계식을 계산한다. 

아래와 같은 경우를 생각해보자. 뷰가 어떻게되있건 상관없이 우선 제품 대분류로 묶고난 이후에, 매출을 계산하라는 의미이다. 

![png](/assets/images/Tableau/24_8.png)

그 이후에 표를 형성하게 되면 아래 그림과 같이 이미 Fixed 를 하고나서 형성하였기 때문에, 대분류별로는 값이 모두 같은것을 확인할 수 있다! 

![png](/assets/images/Tableau/24_9.png)

#  5. Set, Top N, Condition Filter

다음에~ 





https://www.tableau.com/about/blog/2019/9/understanding-how-tableau-calculation-types-work-together



