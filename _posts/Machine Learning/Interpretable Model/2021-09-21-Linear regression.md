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
  - 하지만, 어떠한 변수가 어떤 측면에서 중요할지는 매우 민감한 주제입니다.
  - 일반적으로 p-value , 계수값 등은 이용되어선 안될 것입니다.
- 이 책의 저자는 Linear regression 의 특성값의 중요도는 t-통계량의 절댓값으로 추정하고자 하였습니다. 

$$t_{\hat{\beta}_j}=\frac{\hat{\beta}_j}{SE(\hat{\beta}_j)}$$

- 위에서 볼 수 있듯이, t 통계량은 표준 오차로 크기가 조정된 추정 가중치값이 됩니다. 
- 계수가 아무리 크더라도, 추정된 분산값도 같이 크다면(불확실성이 크다면) 작은 importance를 지니게 됩니다.

> ## Example 

|                           | **Weight** | **SE** | **$\mid t \mid$** |
| ------------------------- | ---------- | ------ | ----------------- |
| (Intercept)               | 2399.4     | 238.3  | 10.1              |
| seasonSUMMER              | 899.3      | 122.3  | 7.4               |
| seasonFALL                | 138.2      | 161.7  | 0.9               |
| seasonWINTER              | 425.6      | 110.8  | 3.8               |
| holidayHOLIDAY            | -686.1     | 203.3  | 3.4               |
| workingdayWORKING DAY     | 124.9      | 73.3   | 1.7               |
| weathersitMISTY           | -379.4     | 87.6   | 4.3               |
| weathersitRAIN/SNOW/STORM | -1901.5    | 223.6  | 8.5               |
| temp                      | 110.7      | 7.0    | 15.7              |
| hum                       | -17.4      | 3.2    | 5.5               |
| windspeed                 | -42.5      | 6.9    | 6.2               |
| days_since_2011           | 4.9        | 0.2    | 28.5              |

- 위의 예제에서는 날씨와 시간적 정보를 이용하여 대여되는 자전거의 수를 예측하기 위한 모델입니다. 
- 특성값은 수치값 / 카테고리값이 섞여 있습니다. 
- 위의 결과를 다음과 같이 해석할 수 있을것입니다.
  - 온도가 1 상승하면 , 다른 변수가 고정되어 있을떄에 자전거 대여 수가 110.7 증가 
  - 비/눈/폭풍우 를 동반한 날씨일떄에 자건거 대여수는 맑을떄보다 1901개 감소 
    - 맑을때의 category 를 drop 한것으로 간주합니다.
- 위와 같이 쉽게 해석될 수 있는 이유는 , 각 모든 특성값들이 따로따로 + 로 연결되어있기 때문입니다. ( Linear model)
  - 이렇게 따로 떼어져 있기 떄문에 , '단독' 으로 위와 같이 해석할 수 있는것입니다.
  - 만일 모델이 $x_1 x_2 + x_3 + x_4^2 ..$ 와 같이 다양한 연산으로 이어져있다면, $x_1$ 의 1 단위 증가는 $x_2$ 의 수준에 따라 그 결과가 달라집니다. 즉 해석이 어려워지는 것입니다. 
- 위와 같은 단순한 Linear model 의 장점은 해석이 쉽다는 것이지만, 단점은 특성값들간의 상호작용을 무시한다는것에 있습니다.
  - 하나만 고정하고 늘릴 수 있다는것은 철저한 X 변수들간의 독립성을 가정한 것이기 떄문입니다. 

> ## Weight Comparison

![jpg](/assets/images/ML/15_1.png)

- 위 그림처럼 Weight 와 그에 대응되는 신뢰수준을 그림으로서 좀 더 확실한 해석을 할 수 있습니다.
  - 비,눈,폭풍 변수는 그 값이 매우 크고, 신뢰수준도 넓지만 무의미한 수준 (0을 포함하지 않으므로) 은 아닙니다. 즉 꽤 의미있는 변수라고 볼 수 있습니다.
- 하지만 위와 같이 단순 비교 할 경우 Weight 는 특성값의 스케일의 영향을 받게됩니다.
  - 온도가 섭씨가 아니라 화씨인 경우에는 다른 Weight 를 가지게 될 것입니다.
  - 즉 더 정확한 비교를 위해서 Scaling 한 이후에 Weight 를 비교할수도 있을것입니다.

> ## Effect Plot

- 선형회귀 모델에서, 가중치는 특성값(Feature) 의 척도에 따라 다르기떄문에 문제가 될 수 있었습니다.
  - 키를 미터 , cm 단위로 정함에 따라 단위가 달라지기 때문입니다.
- 또한 Feature 의 분포를 아는것 또한 중요합니다.
  - 어떠한 특성의 분산이 매우매우 낮다면, 그 변수는 계수가 유의할 지언정 효과가 미미할 것이기 떄문입니다. 
- 그러므로 위에 대한 고민 (단위에 따른 Weight 가 통일되지 않음 + Feature 의 분포도 알아야함) 을 해결하기 위해 아래와 같이 effect 를 정의할 수 있습니다.

$$\text{effect}_{j}^{(i)}=w_{j}x_{j}^{(i)}$$

- 즉 각 특성값의 가중치에 인스턴트 특성값을 곱한것을 effect 라 정의합니다.
  - 위 식은 $j$ 번쨰 특성에 대해, $i$ 번째 샘플의 effect 를 나타낸 것입니다. 

![jpg](/assets/images/ML/15_2.png)

- 위에 대한 effect 를 상자 그림으로 요약할 수 있습니다.
  - effect 를 각 특성별로 sample 의 수만큼 흩뿌려 상자그림을 그려보았습니다.
- 예상 대여 자전거 수에 가장 큰 영향을 주는것은 온도 특성값 , 일별 특성값임을 알 수 있습니다.
- 그 효과들이 비교적 Weight 의 단위와는 상관없이 같은 선상에서 비교되기 떄문에 훨씬 더 객관적인 비교 지표가 될 수 있을것입니다.

> ## Local Interpret

- 하나의 instance 에 대해서는 어떻게 해석되어야 할까요? 

| **Feature**     | **Value**   |
| --------------- | ----------- |
| season          | SPRING      |
| yr              | 2011        |
| mnth            | JAN         |
| holiday         | NO HOLIDAY  |
| weekday         | THU         |
| workingday      | WORKING DAY |
| weathersit      | GOOD        |
| temp            | 1.604356    |
| hum             | 51.8261     |
| windspeed       | 6.000868    |
| cnt             | 1606        |
| days_since_2011 | 5           |

- 위와 같은 인스턴트에 대해서 효과 분포를 나타내는 그림을 그려보겠습니다

![jpg](/assets/images/ML/15_3.png)

- 위와 같은 그림을 통하여, 현재 데이터가 어떤 변수에 의해 어떤 영향을 받고 있으며, 다른 sample 들과 비교할떄 어떤 데이터인지 알 수 있게해줍니다.
  - Train 데이터의 학습을 통한 예측의 평균은 4504 입니다.
  - 그에 반해서 instance 에 대한 예측은 1571로 매우 작습니다.
  - Effect plot 은 그 이유를 알려줍니다.
    - 이 instance 는 온도가 매우 낮았고 (온도의 계수가 양수임을 기억합시다.)
    - 2011년 초의 데이터 (days_since_2011 의 계수가 양수임을 기억합시다.) 이기 떄문입니다.

> ## Others 

- 그 밖에 Lasso , Ridge 와 같은 다양한 방법론이 존재하며 , 또는 Mltilevel regression 과 같은 방법도 가능합니다. 
- 그리고 Stepwise selection / Backward selection 과 같은 방법도 있습니다.
- 하지만 여기에서 다룰것은 'Linear regression' 이 어떤 방식으로 해석이 가능한지에 대해서 알아보는 'interpretability' 가 중심이므로 여기까지만 다루고 , 더 많은 이야기는 다른곳에서 알아보도록 하겠습니다.

---

**Reference**

- <https://christophm.github.io/interpretable-ml-book/limo.html>
- <https://tootouch.github.io>

 Linear regression 에 대한 이야기를 하자면 사실 , regression 만을 위한 책이 (1), (2) 까지 구성될 정도로 광할하고 어려운 분야이다. 그래서 여기에서는 그냥 OLS 만 다루었고, 그에대한 해석도 되게 짧게만 소개했다. 다음에 기회가 된다면, 좀 더 다양한 Model 을 소개하는것으로 하고 여기까지만 하는것으로!
{: .notice--success}

