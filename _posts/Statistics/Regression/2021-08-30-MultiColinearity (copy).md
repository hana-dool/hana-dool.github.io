---
title:  "Multicollinearity"
excerpt: "왜 OLS 에서 다중공선성이 문제가 되는가?"
categories:
  - Regression
tags:
  - 1
last_modified_at: 2021-08-30

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# 1. 맞는 해석이 여러개일 수 있음

![png](/assets/images/Stat/49_1.png)

![png](/assets/images/Stat/49_2.png)

- 위를 보면, 퍼팩트한 Multicollinearity 의 상황에서는, 위와 같이 하나의 변수에 대해서 여러가지 해석이 가능합니다. 
- 즉 , 다중공선성이 존재한다면 해석력에 안좋은 영향을 끼칠것입니다.

# 2. 해가 존재하지 않음

- 위의 말은 'OLS' 의 해가 없어진다는 것입니다. 

![png](/assets/images/Stat/49_3.png)

- 위와 같이 OLS 의 Solution 에는 $X'X$ 의 역함수가 있습니다.
- 즉 , 다중공선성이 있으면, 이 해를 구하지 못하게 됩니다. 

# 3. 불안정한 추정치

![png](/assets/images/Stat/49_4.png)

- 위와 같이, 우리의 OLS 계수 추정치 $\beta$ 의 분산을 잘 보면 분모에 $X'X$ 의 역수가 들어가있습니다.
- 이는 즉,  다중공선성이 어느정도 존재하면 $det(X'X) \approx 0$ 이며, 이는 추정치에 대한 엄청난 분산을 일으킵니다.

![png](/assets/images/Stat/49_5.png)

- 즉, 다중공선성이 존재하면 계수에 대한 분산이 어마어마하게 커져서 '조금만 변해도' 해석이 천차만별로 변하게 됩니다. 
- 이는 저희가 바라는 상황이 아닙니다..

# Refer

- 다중공선성에 대한 연구 = (A) study of multicollinearity in multiple regression analysis
  - http://www.riss.kr/search/detail/DetailView.do?p_mat_type=be54d9b8bc7cdb09&control_no=a4c0e81273f7f0d9



