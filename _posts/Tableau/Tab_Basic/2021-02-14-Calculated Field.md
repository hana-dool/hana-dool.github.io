---
title:  "Calculated Field"
excerpt: "Map 시각화 기초"
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

#<center> 사칙연산을 이용한 변수 생성</center>

아래와 같이 '비용' 이라는 데이터가 누락되어있는 경우, 아래와 같이 사칙연산을 간단히 적용하여 우리가 원하는 값을 만들어낼 수 있다. 

![png](/assets/images/Tableau/20_1.PNG)

위 말고도 사칙연산을 이용한 새로운 Field (매출 / 수량 = 1개당 평균 판매금액) 등을 얻어낼 수 있다. 

문법은 + / * - 를 적용하면 되므로 굳이 설명하지는 않겠다.



# <center>데이터의 분류</center>

예를 들어 visuaization 에서 색상을 사용하여 수익성이 있는것과 없는것을 구분하고 싶다고 하자. 

```
IF SUM([Profit]) > 0
THEN "Profitable"
ELSE "Nonprofitable"
END
```

위의 코드를 적용한 뒤, 색상으로 추가한다면 우리가 정의한대로 분류작업을 할 수 있다. 

![png](/assets/images/Tableau/20_3.PNG)

이익이 0 보다 낮은 물건에 대해서는 색을 다르게 주고싶다. 이 경우 Calculation Field 를 이용해 고치는게 좋다.

![png](/assets/images/Tableau/20_2.PNG)

