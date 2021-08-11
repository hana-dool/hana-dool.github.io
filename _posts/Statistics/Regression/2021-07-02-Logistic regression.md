---
title:  "Logistic Regression 1(~ing)"
excerpt: "Why Using Logistic?"
categories:
  - Regression
tags:
  - 1
last_modified_at: 2021-06-30

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# 1. Why not Linear regression?

- 회귀문제일때에는 Linear regression 을 제대로 사용할 수 있었습니다.
- 하지만 Classfication 문제에서는 Linear regression 이 제대로 작동하지 않습니다. 
- 왜 안되는지 한번, 억지로 Linear regression 을 적용해 봅시다. 

- 우선, Modeling 을 하기 위해서는 각 Label 에 '값' 을 부여해 실체화를 해야합니다. 
- 그러므로 우리가 분류하고자 하는 Class 에 대해 하나는 0, 하나는 1의 값을 줘 봅시다. 

![png](/assets/images/Stat/11_2.png)

- 선형 회귀를 해 보았을떄에 위와 같이 Fitting 이 됩니다.
  - 위를 보면, Extrapolation 의 경우 문제가 생깁니다. 
  - 즉 Fitting 되는 값 멀리 떨어지면 확률이 아닌 값이 나옵니다. 
- 그러면 제한을 주면 어떨까요? 예를들어, 1 이 넘는순간 모두 1로 해버리는것이죠! 
  - 이런식으로 모델에 사족(제한) 이 많아지면, 추정식을 일반화하여 정의하기 힘듭니다.
    - LSE 방법으로 추정한다 해도, 제한이 걸리는순간 식이 복잡해집니다.
    - Lasso 만 생각해봐도, Loss 에 식 하나 조금 더 붙었다고 Closed Form 이 없어지게 되는걸 보세요... 
  - 게다가 제한이 걸리게되면 각 변수에 대한 Sampling distribution 을 제대로 구할 수 없습니다. 
    - 왜냐하면 각 변수에 대한 추정이 딱 Closed 식으로 나오지 않거든요. 
    - 이러면 Sampling distribution 도 없고.. 그러면 당연히 Inference 도 불가해집니다. 
  - 그러면 해석력때문에 통계모델을 쓰는데, 로지스틱 모델을 쓸 이유가 없겠죠.. 
- 그래요. 그럼 백발 양보해서 한번 써 볼게요. 그런데 아래와 같은경우처럼 데이터를 추가하는 경우를 생각해봅시다. 

![png](/assets/images/Stat/11_3.png)

- 이 경우 우리 Line 이 제대로 확률을 근사하는것 처럼 보이나요? 
- 절대 아닙니다.. Outlier 에도 민감하고 해석도 안되는.. 너무나도 안좋은 모델입니다..

<br>

# 2. GLM

- 자 이제 Logistic regression 이 어떻게 탄생했는지 알아봅시다. 
- 우선 일반화 선형모형 (GLM) 에 대해서 알아보는것이 좋습니다. 
- Linear regression 의 경우, 선형모델은 어떤 가정을 따르게 될까요? 

> 1.y 와 X 간 관계는 선형이다.
>
> 2.error 는 iid Normal 을 따른다. 

- 위의 가정을 수식으로 표현하면 다음과 같습니다. 

> $E[Y \mid X] = X\beta$
>
> $\epsilon \sim N(0,\sigma^2)$ 

- 하지만 위 식은 y 와 X 가 선형일떄에나 잘 먹히는식입니다. 

<br>

- 일반화 선형모델은 위의 선형모델을 확장한 것입니다. 

>1.y 와 X 간 관계는 Link function g 를 매개로 선형이다.
>
>2.error 는 다른 분포를 따를 수 있다. 

- 수식으로 표현하면 아래와 같습니다. 

> $g(E[Y \mid X]) = X\beta$

- 위 GLM 모형에서 가정하는것은 아래와 같습니다. 

![png](/assets/images/Stat/11_5.png)

- 더 깊게 들어가면 좋을게 없으므로, 여기서 끊겠습니다.

<br>

# 3.Logistic Regression

- 이제 Logistic Regression 은 위와 무슨 상관이 있을까요? 
- Logistic Regression 은 link function $g(x) = ln(\frac{x}{1-x})$ 을 이용한, GLM 의 일종입니다. 
- 위와 같이 Link function 을 정의하게 되면 range 가 - 무한 ~ 무한이기 떄문에, 아무 제약 없이 linear regression 이 바로 가능합니다.

- 로지스틱 Regression 은, 분포가정이 y 가 Bernoulli 분포라는 가정만 들어가게 되고, 계수 추정은 MLE 로 진행하게 되며, 그에 따른 분포는 MLE 의 Assymptotic 을 이용하여 추정하게 됩니다. 
  - https://stats.stackexchange.com/questions/60074/wald-test-for-logistic-regression 


- 그에 따라 구한 계수는 MLE 이므로 Normal 분포임을 가정할 수 있습니다. (Assymptotic Normal) 그러므로 Inference가 가능합니다.

# 4. Interpret

![png](/assets/images/Stat/11_6.png)

- https://3months.tistory.com/category

# Goodness of fit

로지스틱 회귀분석의 경우, 생각보다 일반적인 regression 보다는 Assumption 체크를 빡세게 하지 않는다. 

그래도 어느정도는 해야되기에, 테스트가 존재하긴 한다. 아래 링크를 참고하면 Hosmer-Lemeshow 가 고안한 테스트를 볼 수 있다. 나중에 보자! 

<https://en.wikipedia.org/wiki/Hosmer%E2%80%93Lemeshow_test>

