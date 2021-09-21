---
title:  "Linear regression"
excerpt: "선형성을 예측하는 제일 기본적인 모델"
categories:
  - Interpretable_Model
last_modified_at: 2021-09-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Linear regression 은 해석 가능한 전통적인 해석기법입니다. 여기에서는 심화적인 내용을 알아보고자 하는것이 아니므로 매우 짧게만 소개하고, 어떤것을 해석할 수 있고, 어떻게 해석할 수 있는지에 대해서 알아보도록 하겠습니다.
{: .notice--warning}

# [Linear regression](#link){: .btn .btn--primary}{: .align-center}

> ## Summary

- 선형 회귀 모델은 특성값(Feature) 의 입력과 가중치(Weight) 의 곱의 합을 이용하여 모델을 예측하는 것입니다.
- 이러한 선형성은 해석을 쉽게 만들어줍니다.

$$y=\beta_{0}+\beta_{1}x_{1}+\ldots+\beta_{p}x_{p}+\epsilon$$

- 위에서 $\epsilon$ 은 Normal 분포를 따른다고 가정하게 됩니다. 

$$\hat{\boldsymbol{\beta}}=\arg\!\min_{\beta_0,\ldots,\beta_p}\sum_{i=1}^n\left(y^{(i)}-\left(\beta_0+\sum_{j=1}^p\beta_jx^{(i)}_{j}\right)\right)^{2}$$

- 이러한 계수의 추정은 위와 같이 Least squared Method 를 이용하여 이루어집니다. 
- 이러한 선형 모델의 장점은 선형성입니다. 선형성은 추정 절차를 매우 단순하게 만들어줍니다.
  - 예측 가중치값은 통계적으로 신뢰구간으로 나타낼 수 있습니다.
  - 예를 들어서 $x_2$ 의 가중치가 $w_2$ 라고 가정합시다. 이 경우 95% 에 대한 신뢰구간이 1~3 이라 합시다. 
  - 샘플 데이터 (샘플은 R.V. 이므로 여러번 뽑을 수 있습니다.) 을 100회 뽑아서 각각 linear model 을 적합하였을떄 100개 모델중 95개의 신뢰구간이 실제 값을 포함하게 됩니다.
  - 즉 1~3의 신뢰구간은 95% 의 확률로 True 값을 포함한다고 볼 수 있습니다.
- 하지만 위와 같이 통계적으로 해석이 가능하고, 모델이 잘 작동하기 위해서는 여러 Assumption 을 만족해야 합니다. 

> ## Assumption 

> 선형성(Linearity)

- 선형회귀 모델은 y 가 X 들의 선형조합으로 형성된다고 가정합니다. 

> 정규성(Normality)

- 오차$\epsilon$ 은 Normal 을 따릅니다. 즉 , Feature 를 고정하였을떄에 Outcome (y) 의 분포는 Normal 이 된다는 것입니다.

> 등분산성(Homoscedasticity)

- 등분산성은 오차가 같은 분산을 가진다는 것입니다. 
- 즉, Feature 를 어떻게 고정하든 간에, Outcome(y) 의 분포는 동일하다는 것입니다.

> 독립성(Independence)

- 모든 Instance 는 다른 instance 들과 관계가 없다고 가정합니다. 
- 하지만, 환자당 여러번의 혈액 검사를 하는 경우와 같은경우, 각 데이터포인트는 독립적이지 않습니다.
- 이러한 데이터의 경우 GEE(Generalized Estimating equation) 과 같은 특수 선형회귀 모델이 필요할것입니다.

> 다중공선성이 없음

- 연관성이 있는 Feature 가 있게되면, Linear regression 의 해석은 망가질 수 있습니다.
- 특정한 변수가 , 다른 변수의 설명력을 가져간다거나, 추정치를 불안하게 만드는 등의 효과를 낳기 때문입니다.

> ## Interpret

- 선형 회귀의 해석은 각 특성값의 유형에 따라 달라지게 됩니다.

> Numerical 값

- 수치값을 가지는 Feature 일 경우, 1 단위를 늘리게 된다면 그 Weight 만큼 예측값이 증가합니다. 
- 하지만 이러한 경우, '현실적으로 하나의 Feature 만 증가' 시킨다는것은 불가능하기 때문에 문제가 될 수 있습니다. (자세한것은 제 블로그 다른 포스팅을 확인해주세요..)
  - $x,x^2,x^5$ 변수를 사용하여 Linear regression 을 적합하였다고 합시다. 
  - $x$ 변수의 계수가 10이라고 해서 , 이 $x$ 가 1 늘어날떄에 y 가 10 증가한다고 해석할 수는 없습니다. 

> Binary Feature 

- 이는 대체로, 두개의 특성을 가지는 Category 값을 one hot vector 로 바꾼 경우에 해당합니다.
- 우리가 가지는 데이터에 한국인 / 외국인 으로 구분되는 '국적' 변수가 있다고 합시다.
  - 그대로는 Linear regression 에 사용할수는 없으므로 한국인일떄 1 , 외국인일때 0 을 주는 '국적_onehot' 변수를 만들어낸다고 합시다.
  - 이러한 '국적_onehot' 변수의 계수가 10이라면 , 한국인일때에 y 의 예측치가 10 증가한다. 라고 해석할 수 있습니다.

> Categorical Feature 

- 이 경우 Category 값이 여러개인 경우입니다.
- 국적이 korea , japan , china 세개인 경우라고 합시다. 이 경우에 우리는 두개의 onehot vector 로 이러한 category 값을, Linear regression 이 이용 가능하도록 만들 수 있습니다.
  - korea_onehot , japan_onehot 두개의 변수를 만듭시다. 
    - korea_onehot 은 korea 국적일때에 1을 가집니다.
    - japan_onehot 은 japan 국적일때에 1을 가집니다.
    - china 국적을 가질떄에는 korea_onehot , japan_onehot 모두 1을 가집니다.
- 이러한 경우, 해석은 상대적인 값으로 해석됩니다. 
  - korea_onehot : 10 , japan_onehot : -5 의 계수를 가진다고 합시다. 
  - 이러한 경우 '중국 국적인 사람' 에 비해서 한국 국적을 가지는 사람의 y 값이 10 높다. 
  - '중국 국적인 사람에 비해서' 일본 국적을 가지는 사람의 y 값이 5 낮다. 
- 물론 그대로 onehot vector 를 3개 사용한다면 좀 더 해석이 쉬워집니다만, 이러한 경우 다중공선성 문제가 생기게 됩니다. 

> Intercept $\beta_0$

- 절편값은 '모든 수치적 특성값이 0' 이고, 카테고리 특성값이 기준 카테고리 (즉 drop 된 특성을 의미합니다.) 에 있을떄의 예측값 이 됩니다.
- 하지만 이러한 해석은 의미가 없는 경우가 많습니다. 모든 '수치적 특성값' 이 0 인 경우가 불가능할 경우가 많기 떄문입니다.
  - 예를 들어서 키 , 몸무게로 소득을 예측한다고 합시다. 키,몸무게가 0일 수 있을까요? 
- 이러한 intercept 의 해석이 가능하려면 모든 특성값이 표준화 되었을떄 (평균0, 표준편차1) 에나 의미가 있습니다. 
  - 그 떄의 해석은 '모든 수치값이 평균을 가지고 카테고리가 기준 카테고리를 가질떄의 예측값' 이 됩니다. 

> ## Feaure Importance

- Linear regression 의 Feature importance 를 재는 측도는 여러개가 있을 수 있습니다.

- 데이터 $X \in R^{n*d}$ 를 고려합시다.
- 모든 데이터를 살펴볼 수 없기 때문에, 특징이 다르고 중요한 데이터만을 뽑아서 생각한다.
- 살펴볼 데이터 budget B를 정한다. 이는 데이터를 총 몇 개 뽑아서, 내 데이터를 대표할 샘플로 만들지의 값이다
  - 이 값을 100개를 정한다면, 총 100개의 Sample 을 뽑게 됩니다.
- original representataion 으로부터, 해석가능한 표현   $X' \in R^{n*d'}$    를 만든다. 
- 데이터의 local 한 importance를 나타낼 matrix W 를 아래와 같이 정의합시다.
  - linear model을 explanation 으로 사용했다면 데이터 $x_i$ 에 대하여 explanation $g_i = \xi(x_i)$  를 얻을 수 있고, $W_{ij} = \mid w_{g_{ij}} \mid$  로 정의할 수 있습니다.
  - 이떄에, $g_{i}$ 는 데이터 $x_i$ 에 대한 Explainable model 입니다. (linear)
  - 그리고 $g_{ij}$ 는  linear model 의 j번째 feature 에 대한 계수입니다. 
- 추가적으로  $I_j$ (j column 의 global importance를 정의) $I_j = \sqrt{(\sum_i W_{ij})}$ 을 정의합니다.
  - 모든 instance i 에 대하서 , 설명 가능한 모델 $g_i$를 Construct 한 뒤에 , j 번째 feature 의 계수의 절댓값 모두 더한것입니다.
  - 당연히 '중요한 feature' 라면, 많은 샘플에 대해서, 왜 이런 예측을 하였는니? 에 대한 Local 적인 해석을 하더라도 계속 포함될 것입니다.
  - 예시로 월급을 예측한다고 할떄에 Feature 에 나이가 있다면,각 instance (철수, 영희,.....) 에 대한 월급 설명을 할때에 대부분 나이 변수가 크게 영향을 끼칠것이기 떄문입니다.
- 최대한 특징이 다르며 많은 정보를 포함하고 있는 데이터를 추출하기 위해서 $c(V,W,I) = \sum_{j=1}^{d'}1_{\exist i \in V : W_{ij}>0}I_j $라고 converge function 을 정의합니다.

![jpg](/assets/images/ML/14_3.png)

- 우선 위와 같이 예시를 들어보겠습니다. 
- 각 instance x_i 에 대하여, 설명모델은 가로줄과 같습니다. 
  - x1 은 $1\cdot f_1 + 1 \cdot f_2  = x_1$ 로 설명되고 있다고 보시면 됩니다. 
- $V=\{1,3\}$ 인 경우에 $c(V,W,I)$ = (1+4) + (4+2) 가 됩니다.
  - 그 이유는 $x_1$ 의 경우 $f_1, f_2$ 에 의해 설명이 되고, 각각의$I_1, I_2$ 는 1,4 이기 때문입니다.
  - $x_3$ 의 경우 $f_2,f_3$ 에 의해 설명이 되고, 각각의 $I_2, I_3$ 은 4,2 이기 떄문입니다.
- 이렇게 Coverage function 을 최대화 하는 집합 V 를 찾으면 중요한 데이터들을 쏙쏙 뽑아낼 수 있을것입니다.
  - 모두, 다양한 local 모델들에 대해서 중요하다고 생각되었던 Feature 들이기떄문에 중요한 데이터일것입니다.

$$Pick(\mathcal{W},I)=\underset{\mathcal{V},|\mathcal{V}|\leq B}{\operatorname{argmax}}c(\mathcal{V},\mathcal{W},I)$$

- 이러한 집합 V 를 찾아내는것은 위와 같이 정의됩니다. 

> ## SP Lime

- 하지만 , 위와 같이 , '최대화 하는 집합' 을 찾는것은 Global 한 optimization 문제로 매우 어렵습니다. 
- 그러므로 차선책으로 Greedy 하게 골라내려고 합니다. 

![jpg](/assets/images/ML/14_4.png)

- 그 방법론은 위와 같습니다.   

---

**Reference**

- <https://christophm.github.io/interpretable-ml-book/counterfactual.html>
- <https://tootouch.github.io/IML/counterfactual_explanations/>

 Global 한 해석을 가지기 위하여, Local 적인 해석에 맞춰져 있는 Lime 을 이용해 어떻게 하면, 모델을 해석할 수 있을지 탐구해본게 SP lime 입니다. 
{: .notice--success}

