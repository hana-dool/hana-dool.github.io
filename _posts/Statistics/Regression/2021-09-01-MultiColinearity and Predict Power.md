---
title:  "Multicollinearity and Predictive Power"
excerpt: "다중공산성은 예측 Power 에 큰 영향이 없다?"
categories:
  - Regression
tags:
  - 1
last_modified_at: 2021-09-01

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# 1. Intro

- 다중공선성이 있으면, '모델의 추정 계수가 불안해지긴 하지만 Predicitve Power 에는 영향이 없다' 라는 말을 볼 수 있습니다. 
  - 다중공선성이 있으면 '무조건 제거' 해야한다는 말을 듣고 살았는데 Predictive Power 에는 영향이 없다는 말은 어떤 의미일까요? 

![png](/assets/images/Stat/52_5.png)

- https://online.stat.psu.edu/stat501/lesson/12/12.3

![png](/assets/images/Stat/52_6.png)

- https://en.wikipedia.org/wiki/Multicollinearity#cite_ref-8

# 2. Example

- 체중(Weight) , 체표면적(BSA)으로 BP(혈압) 을 예측하는게 목적이라고 합시다.

![png](/assets/images/Stat/52_1.png)

- 위의 그림을 보게되면, 체중(Weight) 과 체표면적(BSA) 가 큰 관련이 있는것을 볼 수 있습니다. 
  - 즉 두 변수는 다중공선성 관계에 있음을 알 수 있습니다. 

![png](/assets/images/Stat/52_3.png)

- 다중 공선성의 Predictive 영향을 보기 위하여 위처럼 2,92 의 값을 예측하려 해 보았습니다. 
  - 이떄 모델은 3개로서 각각 
    - BSA 만 이용해서 예측 
    - Weight 만 이용해서 예측
    - BSA , Weight 둘다 이용해서 예측
- BSA, Weight 가 다중공선성이 존재하고 있으므로 , 두개 변수를 모두 이용하였을때에 그 예측이 이상해질까요?

![png](/assets/images/Stat/52_2.png)

- 위를 보시면 그 예측 차이 (Fit) 가 별로 없음을 알 수 있습니다. 
- 바로 이런 이유에서 '다중공선성이 있는 변수가 있어도, 그 예측값에는 큰 변화가 없다' 라는 것입니다.
  - 이런 맥락에서 'Predictive Power' 에는 영향이 없었다는 이야기입니다. 
- 하지만 다시말하면 , '다중공선성이 있어도 모델에는 큰 도움이 안된다' 라는 의미가 되기도 합니다.

# 3. Why ? 

## 왜 위의 실험에서 추정치는 별로 차이가 없었나? 

- 이런 일이 일어나게 된 이유는, 바로 '계수 추정은 기본적으로 LSE' 로 이루어지기 떄문입니다. 
- 이전에 ' 변수가 늘어날수록 $R^2$ 이 감소한다는것을 증명했었습니다.
- 즉 다중공선성이 심한 변수여도, 추가하게 되면 모델의 성능은 어느정도 증가하고 (LSE 입장에서) Linear line 도 약간 변하게 되는것입니다.  
  - 하지만 기본적으로 별 정보량이 없기때문에 그 예측에는 도움이 안됩니다.

## 그럼 놔두는게 좋은가?

- 아닙니다. 모델의 '예측' 관점에서 별 영향이 없는것은 맞지만 이는 '그 값이 데이터의 범위 내에 얌전하게 위치' 할 떄의 이야기 입니다. 

![png](/assets/images/Stat/52_7.png)

- 위의 공식은 '모델의 예측값에 대한 분산' 입니다. 
- 이를 보면  $X'X$ 의 inverse 는 다중공선성이 존재할때 매우 불안정하기 때문에 '데이터의 범위 내에서 얌전히 위치' 한다면 , Fitting 할때에 잘 예측하도록 해서 상관이 없으나 , 
- 예측을 데이터 범위 바깥에서 하거나, 살짝 다중공선성이 틀어지는 값에 대해 예측을 하게되면 이 모델은 완전히 이상한 예측을 내보내게 됩니다. 

# Refer

- https://stats.stackexchange.com/questions/306786/calculation-of-variance-of-prediction
- https://math.stackexchange.com/questions/2823248/why-multicollinearity-doesnt-affect-predictive-power-of-a-regression-model
- https://online.stat.psu.edu/stat501/lesson/12/12.3
- https://en.wikipedia.org/wiki/Multicollinearity#cite_ref-8
