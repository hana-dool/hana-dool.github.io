---
title:  "Coefficient of Determination"
excerpt: "결정 계수와 상관계수"
categories:
  - Regression
tags:
  - 1
last_modified_at: 2021-07-29

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# 1. Coefficient of Determination

![png](/assets/images/Stat/20_2.png)

- 정의는 위와 같습니다.

![png](/assets/images/Stat/20_1.png)

- https://www.researchgate.net/figure/Visualization-of-SSE-SSR-SST_fig17_322398615

- 하지만 위와 같은 그림이 제일 잘 설명한다고 생각합니다. 
- 모델링한 값에 대해서, 1 - 에러 변동합/ 전체 변동량 을 한 값입니다. 

![png](/assets/images/Stat/20_5.png)

![png](/assets/images/Stat/20_4.png)

- 위 정의는 다시 위와 같이 설명할 수도 있습니다. (SST = SSE + SSR)
  - 즉, 전체 데이터의 변동에 대헤서, 회귀선에 의해 설명되는 변동의 양 입니다. 

- 즉 1 에 가까울수록 좋은 값입니다.

<br>

# 2. 상관계수(r) 과의 관계

- R^2 를 계산할때에 회귀 모델을 사용하였고, 그리고 모델의 변수는 2개 (x,y) 라고 합시다.
- 위와 같은 경우 $r^2 = R^2$ 이 성립합니다. 이를 증명하면 아래와 같습니다.

![png](/assets/images/Stat/20_3.png)

- https://datalabbit.tistory.com/54

<br>

# 3. 상관계수 대신 R^2

- 우리는 흔히 상관계수의 값을 이용해 변수들간의 관계를 요약합니다.
  - X1 과 X2 의 상관계수는 0.8 이니까 선형성이 강력할거야~ 
  - X1 과 X2 의 상관계수는 0.2 이니까 선형성이 약할거야 ~ 
- 하지만 위의 상관계수가 0.8 , 0.2 라는것은 어떤것을 의미하길래 위와 같이 선형성을 말할 수 있는것일까요?

- 상관 계수는 $r = Cov(X,Y) / \sqrt{var(X)var(Y)}$ 으로 요약됩니다. 
- 물론 X,Y 가 선형성을 띤다면 옆 값이 1 또는 -1 에 가깝게 됩니다만.. 아직도 이게 대체 의미하는게 뭔데? 라고 물어보면 공식 말고는 제시할 게 없어보입니다.
- 이 해석을 도와줄 수 있는것이 바로 위에서 살펴본 $r^2 = R^2$ 공식입니다. 
- X,Y 의 상관계수가 0.8 이라는것은 , 두 변수에 대해서 regression 을 진행하였을때에 결정계수가 0.8^2 = 0.64 라는 의미이고, 이는 선형 모델에 대해서 설명되는 데이터 변동량이 64% 라는것을 의미합니다.
- 위와 같이 적절한 해석이 가능하기떄문에, 상관계수를 말하기 보다는 그 제곱값을 report 하는것을 더 추천드립니다.

- 우리는 흔히 결정계수를 이용하면 다음과 같이 말할 수 있는것입니다.
  - X1 과 X2 의 상관계수는 0.8 이니까, 둘을 회귀로 모델링하면 모델은 변동량의 64% 를 설명해
  - X1 과 X2 의 상관계수는 0.2 이니까, 둘을 회귀로 모델링하면 모델은 변동량의 4% 를 설명해

<br>

# 4. 변수의 수와 결정계수

- 다음과 같은 regression model 을 생각하여보자. 

- $y_i = \beta_0 + \beta_1 x_{1i} + ... +\beta_k x_{ki} + \epsilon _i$
- 이떄 $R^2 = 1- \frac{SSE}{SST} = 1-\frac{\sum(y_i-\hat{y})^2}{\sum (y_i - \bar{y})^2}$  이 된다. 
- 이제 약간 화제를 돌려보자. 우리가 $\beta$ 를 fitting 할때 어떻게 할까?
-  $\beta = min_\beta (y_i - X_i \beta)^2 =  min_\beta \sum \epsilon_i ^2 = min_\beta SSE$ 라는 것이다. 
- 즉 이는 원래 beta 를 fitting 할때부터 sse를 최소화 하려고 하는것이다. 
- 이는 X 변수가 많아질수록 SSE 는 무조건 같거나 작아진다는것을 의미한다. 
- 즉 R^2 는 아무리 안좋은 변수를 넣더라도 '증가' 하게 된다.

<br>

# 5. 음수가 나오기도.?

- 음수가 나올수도 있다.
- 그 경우는 모조리 평균으로 예측한거보다 안좋은 예측일경우이다.

# Refer

- <https://journals.lww.com/anesthesia-analgesia/fulltext/2018/05000/correlation_coefficients__appropriate_use_and.50.aspx>

  - 꼭 읽으세요..!

  
