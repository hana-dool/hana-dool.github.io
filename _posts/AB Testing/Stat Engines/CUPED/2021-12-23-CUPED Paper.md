---
title: "Improving the Sensitivity of Online Controlled Experiments by Utilizing Pre-Experiment Data"
excerpt: "Cuped 방법론을 제시한 Paper"
tags :
  - AB_Stat
last_modified_at: 2021-12-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

CUPED 방법론을 활용해서 Metric 의 Sensitivity 를 높히는 방법
{: .notice--warning}

# [Abstract and Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## Abstract

- Online Controlled Experiment 는 Amazon, eBay , Zynga 등 다양한 회사에서 데이터 중심 결정을 내리는 핵심이 됩니다.
- 이때에 매우 작은 비율의 차이로도 주요 측정 기준 (OEC) 의 차이는 매우 중요한 비즈니스에 영향을 끼칠 수 있습니다.
  - 매우 큰 회사인 빙에서는 수천만달러가왔다갔다 하는 매우 중요한 실험을 수행하고, 매우 많은 실험을 진행합니다.
  - 즉 OEC 의 측정을 약간만 개선하더라도, 회사 전제적으로 엄청난 이득을 볼 수 있겠죠?
- 이 논문에서는 메트릭 변동성을 줄이고, 따라서 더 나은 감도를 달성하기 위해 사전 실험 기간의 데이터를 활용하는 접근법인 CUPED 를 제안합니다.
  - 이 기술은 다양한 비즈니스 메트릭에 활용이 가능하고, 실용적이며 구현이 쉽습니다.

- 이러한 기술을 적용한 Bing 은 매우 성공적이였습니다. 사용자의 절반 또는 절반의 실험 기간으로도 동일한 통계적 능력을 달성할 수 있었습니다.

> ## Introduction

- Controlled Experiments는 가장 오래되고 보편적으로 받아들여지는 방법론입니다.
- 현재 많은 기업에서 널리 사용되고 있는 Controlled Experiments 는 다음과 같이 다양한 이름으로 불리워지고 있습니다.
  - A/B test (Wikipedia) , a split test, a weblab (at Amazon), a live traffic experiment (at Google), a flight (at Microsoft) , and a bucket test (at Yahoo!). 
- 이 논문은 아마존, ebay 와 같은 온라인 비즈니스 사이트 및  포탈의 온라인 제어 실험에 촛점을 맞추고 있습니다.
  - 이때 온라인 제어 실험은 매우 중요합니다. 몆퍼센트 비율 차이는 비즈니스에게 막대한 영향을 끼치게 됩니다.

> Examples


![jpg](/assets/images/Stat/125_1.jpg)

- 우리는 위와 같은 방 찾기 예시를 통해서 Oneline Experiemtns 가 어떻게 이루어지는지에 대해서 알아보도록 하겠습니다.
-  MSN Real Estate (http://realestate.msn.com) 사이트에서는 위 그림처럼 6가지의 `Find a home`위젯을 위한 6가지 후보가 있엇습니다. 
  - 왼쪽 맨 위 : Control  , 나머지는 Variants
- 실험동안 사용자는 6 가지 Variant 에 무작위로 배정받게 됩니다. 그를 통하여 사이트 방문을 늘리는것이 목표를 제일 잘 달성하는 Variant 를 선택하게 됩니다.
- 이 실험에서 승자인 Treatment 는 이전 대조군 대비 수익을 10% 증가시켰습니다.

> Controled Experiment

- Controlled Experiment 에서 ,실험의 질을 좌우하는 능력은 Treatment 효과가 실제로 존재할때 탐지하는 능력입니다. (보통 Power , Sensitivity 라고 불립니다.)
- 온라인 실험을 대규모로 실행할 때는 Sensitivity 를 늘리는것이 매우 중요합니다.
  - 왜냐하면 성숙한 온라인 실험플랫폼은 연간 수천개의 실험을 진행하게 되고 ,  즉 Sensitivity 를 조금만 상승시키더라도, 규모의 경제에 대해서 이익이 엄청 커지기 때문입니다.
- 이떄 Power 를 높히기 위한 제일 쉬운 방법은 표본 크기를 늘리는것입니다. 
  - 이때 온라인 실험은 이미 매우 큰 표본 크기를 가지므로, A/B Testing 에서 Power를 강조할 필요가 없어 보일 수 있습니다. 

- 하지만 정말로 Online 실험에서는 이미 샘플의 크기가 크므로 Sample 의 수를 고려하지 않아도 될까요?

> ## Sample is not enough

- 하지만 현실에서는 많은 양의 트래픽이 있더라도, online 실험은 우리가 원하는 Statistical power 에 도달하지 못하는 경우가 있습니다. 
  - 구글에서는 매달 100억건 이상의 검색을 수행하는데에도, 그들이 가진 트래픽 양에 만족하지 않는다고 합니다.
- 이제 샘플이 필요한 이유를 하나하나 알아봅시다.

> 이유 1 : Treatment 효과는 매우 적음

- 우리가 탐지하고자 하는 Treatment 효과는 매우 작은 경향이 있습니다. (항상 모든 기능이 혁신적이라 큰 Treatment 의 증가를 나타내는게 아니기 때문이죠.. )
- Contolled Experiment 의 Sensitivity (이 문단에서는 delta 의 수준을 의미하는듯 함.) 는 사용자 수 제곱에 반비례하므로, 작은 사이트에서 5% 의 delta 를 감지하려면 10000명의 사용자가 필요할 수 있습니다. 
  - 즉 0.5% 의 delta 를 감지하려면 1/10 으로 감소된 delta 를 감지해야 하므로 100만명의 사용자가 필요하게 됩니다. 
- 이때 0.5% 가 별거 아니라고 생각할 수 있는데, 큰 서비스에서는 사용자당 0.5% 의 수익 변화만으로도 대형 온라인 사이트의 경우 수백만 달러에 해당한다는것을 기억하세요! 

> 이유 2 :  결과를 빨리 얻는것이 중요

- 결과를 빨리 얻는것이 중요하기 떄문입니다. 왜 결과를 빨리 얻는것이 중요할까요? 
  - 좋은 기능을 조기에 출시하고 싶을 수 있기 떄문
  - Treatment 가 사용자에게 안좋은 영향을 미칠때 빨리 중단해야 하기 때문

- 그러므로 Sensitivity 가 큰 실험을 해야 조기중단에 대해서 더 큰 신뢰성을 얻을 수 있습니다.

> 이유 3 : 영향을 받는 유저가 적을수 있음

- 낮은 Triggering rate 를 가진 실험이 있을때, 이러한 실험은 매우 적은 유저만이 실제로 Treatment 효과를 경험하게 됩니다.
  - 예를 들어서 레시피 관련 쿼리에만 영향을 미치는 실험에서 대부분의 사람들은 레시피를 검색하지 않기 때문에 Variant 를 경험하지 않습니다.

- 즉 이러한 경우 유효한 표본 크기는 작을 수 있으며, 통계 분석의 Statistical Power 는 매우 낮을 수 있습니다.

> 이유 4 : 실험이 많아질수록 샘플이 적어짐

- 실험이 많아질수록 , 각 실험은 샘플 사이즈를 서로 나눠써야하기 때문에 한 실험이 가용할 수 있는 샘플의 수가 적어지게 됩니다.
  - 이때 다양한 실험을 동시에 진행한다고 하면 Interaction Effect 를 고려해야 해서 설계가 매우 어렵습니다.

- 그러므로 데이터 중심 문화가 제대로 잡힌 기업에서는 혁신 속도에 맞추기 위하여 더 많은 실험을 항상 실험해야 하고, 이는 좋은 온라인 플랫폼의 경우 항상 샘플 사이즈 부족에 허덕일수밖에 없다는 의미입니다. 

> ## Improve Sensitivity : Variance Reduction

- 자 그럼 위에서 Power 가 매우 중요하다는것을 알았습니다. 그러면 이떄 어떻게 해야 Power 를 높힐 수 있을까요?
- 민감도를 개선하는 방식중에 하나는 "분산 감소" 방법론입니다. 이러한 분산 감소를 어떻게 이루어낼 수 있을지 아래에서 알아보시다.

> 다른 평가 매트릭 사용하기

- Kohavi et al. (2009b) 는 다른 평가 메트릭을 사용할때에 더 낮은 분산을 가질 수 있다고 합니다.
- Revenue 와 같은 metric 은 매우 큰 분산을 가지기 때문에 이러한 메트릭은 Power 가 낮을 것입니다.

> Treatment 의 영향을 받지 않는 사용자 거르기

- Treatment 의 영향을 받지 않는 경우의 사용자는 Error(Noise) 로 작용하게 됩니다. 
  - 왜냐하면 이러한 사용자는 A,B 모두에 고르게 배치되고 같은 효과를 가지기 떄문입니다. 
- 그러므로 Treatment 의 영향을 받는 유저만으로 Filtering 하게 된다면 , 실험의 Power 를 높힐 수 있게됩니다.
  - Kohavi et al. (2009b) 참고

> Randomization

- Deng 등(2011) 은 페이지 수준 메트릭의 분산을 줄이기 위해서, 설계 단계에서 페이지 수준의 무작위화를 사용하는 방법을 제시합니다. 

> Note

- 하지만 위와 같은 방법론들은 매우 특수한 경우에만 적용할 수 있습니다.
- 또한 기업은 쉽게 변경할 수 없는 핵심지표 (KPI) 를 가지기 때문에, 실제로 모든 메트릭에 적용할 수 있는 기술을 원합니다. (예를 들어서 인당 수익을 최대화 하고 싶은 기업의 경우 페이지 기준으로 계산하기 어렵습니다.)
- 또한 모델 가정이 신뢰할 수 없는 경향이 있고 한 메트릭에 대해 작동하는 모델이 다른 메트릭에 반드시 적용되는 것은 아니기 때문에 이 기법은 가급적 파라메트릭 모델에 기반해서는 안됩니다.
- 그러므로 우리는 '다양한 방법론에 Globally' 하게 적용되는 방법론을 원합니다. 이러한 방법이 있을까요? 

> ## CUPED

- 이 논문에서 우리는 CUPED (사전 실험 데이터를 사용한 제어된 실험) 이라는 기술을 제안합니다. 
  - 이 기술은 Control 및 Treatment 의 사용자에 대하여서 사전 실험 데이터를 사용해 메트릭을 조정하여서 메트릭의 변동성을 줄입니다. 

- 이러한 CUPED 방법론의 이점은 다음과 같습니다.
  - 사전 실험 데이터를 사용해 온라인 실험에 대한 분산을 줄이기 위한 방법으로서 실험의 Sensitivity 를 크게 높힐 수 있음
  - Non-user metric 애 대한 확장된 접근과 Partially Missing pre experiment data 에 대한 새로운 접근법 
  - 사전 실험에서 동일한 메트릭을 사용하면 일반적으로 가장 큰 분산 감소를 할 수 있다는 Emprical Result와 최적의 공변량을 선택하는 기준 제시
  - Bing에서 실행되는 실제 온라인 실험에 대한 결과의 검증은 약 50%의 분산 감소를 보여주며, 이는 트래픽을 두 배로 늘리거나 동일한 민감도를 얻기 위해 실험을 실행해야 하는 시간을 절반으로 줄이는 것과 같습니다.
  - pre experiment 를 사용할 경우 , 기간을 설정해야 되는데 이때 기간에 사용할 수 있는 최상의 길이를 결정하는 방법, 다수의 공변량 사용과 같은 방법론을 소개
- 이제 이러한 CUPED 방법론에 대해서 자세히 알아보고 논의해보록 하겠습니다.

# [2.Backgound and Related Workd](#link){: .btn .btn--primary}{: .align-center}

> ## 2.1 Analyzing Experiment

> Two sample t test

- 광범위한 적용 가능성 덕분에 우리의 논의는 2-표본 t-검정의 경우에 초점을 맞춥니다(Student 1908; Wasserman 2003). 
  - 이 방법론은 온라인 실험 분석에서 가장 일반적으로 사용되는 프레임워크입니다. 

- 메트릭 Y(예: 사용자당 쿼리)에 관심이 있다고 가정합시다. 이때 t-test를 적용하기 위해, 우리는 Control 과 Treatment에 있는 사용자에 대해 관찰된 메트릭 값은 랜덤 변수 $Y^{(t)} $ 와 $Y^{(c)}$ 의 independent 한 realization 이라고 가정합니다.  
- 귀무 가설($H_0 $)은 $\mu_{Y^{(t)}} = \mu_{Y^{(c)}}$ 이라고 설정합니다. 대립가설은 $\mu_{Y^{(t)}} \not= \mu_{Y^{(c)}}$  이 됩니다. 이때 t-test 는 아래와 같은 통계량을 Based 로 실험이 진행됩니다.

$$\frac{\bar{Y}^{(t)}-\bar{Y}^{(c)}}{\sqrt{\operatorname{var}\left(\bar{Y}^{(t)}-\bar{Y}^{(c)}\right)}}$$

- 이때 $$\Delta=\bar{Y}^{(t)}-\bar{Y}^{(c)}$$ 는 평균의 이동 (Shift ) 에 대한 Unbiased Estimator 입니다. 
  - 그리고 t-Statistic 은 위, 평균의 이동(차이라고도 함) 에 대해 **정규화된 버젼**이라고 생각할 수 있습니니다. 

- t-test 의 경우 Y가 Normal 분포여야 한다는 가정이 필요합니다만, Online Experiment 의 경우 Sample 의 크기는 최소한 수천 단위 이므로 중심극한정리 덕분에 Y 에 대한 정규성 가정은 크게 필요하지 않습니다.

> Variance 

- 이때 샘플은 independent 이므로 $\Delta$ 에 대한 분산은 아래와 같이 계산됩니다.

$$\operatorname{var}(\Delta)=\operatorname{var}\left(\bar{Y}^{(t)}-\bar{Y}^{(c)}\right)=\operatorname{var}\left(\bar{Y}^{(t)}\right)+\operatorname{var}\left(\bar{Y}^{(c)}\right)$$

- 이 프레임워크에의 핵심은 평균 자체의 분산을 줄이는 데 있습니다. 
  - 섹션 3에서 볼 것처럼, 이것은 우리의 문제를 분산 감소를 통한 평균의 추정을 개선하기 위해 몬테카를로 샘플링에 사용되는 기술과 연결합니다.

> High level Reduction Veriance

- 분산 감소에 대한 아이디어는 다음과 같습니다.
  - 우리는 평소처럼 실험을 진행하지만 데이터를 분석할 때  $\Delta$ 를 사용하는게 아니라 수정된 델타 추정치 ($\Delta^{*}$) 를 계산하고, 이를 실험 검정에 사용하게 됩니다.
- 조정된 추정치 ∆∗는 다음과 같은 좋은 성질을 지닙니다.
  - $\Delta^{*}$ 는 여전히 Shift in mean 에 대한 Unbiased estimator 가 됩니다. ( $\Delta$ 도 Shift mean 에 대한 Unbiased mean 이라는것을 기억하세요! ) 
  - $\Delta^{*}$ 는 $\Delta$ 보다 적은 Variance를 가진다.
  - 즉 Unbiased + Lower Variance Estimator 으므로 차이에 대해서 $\Delta$ 보다 $\Delta^{*}$ 가 더 좋은 추정량이 됩니다.
- 즉 정리하면 CUPED 를 적용한 조정된 추정치 ∆∗는 Unbiased Estimator 인데 Variance 까지 낮으니 매우 좋은 추정량이라고 할 수 있죠! 
- 이러한 ∆∗ 는 어떻게 구할 수 있을까요?

> ## 2.2 Linear model

- 분산 감소는 랜덤화된 실험을 분석하는데에 있어서 매우 오래된 과제였습니다. 
- 이 경우 가장 인기 있는 모수적 방법은 선형 모델링을 기반으로 합니다(Gelman and Hill 2006). 실험에 대한 선형 모형에서는 결과가 Covariates 항과 결합된 Treatment 효과의 선형 조합이라고 가정합니다.
  - $Y_i$  를 metric 의 outcome 이라고 합시다.
  - $Z_i$ 를 Treatment Assignment indicator 라고 합시다. 
  - $X_i$ 는 vector of covariates 라고 합시다. linear model 은 다음과 같은 사실을 가정합니다.


$$\mathbb{E}\left(Y_{i} \mid Z_{i}, \mathbf{X}_{i}\right)=\theta_{0}+\delta Z_{i}+\boldsymbol{\theta}^{T} \mathbf{X}_{i}$$

- 모형의 가정 하에서 선형 회귀 분석(공변량이 범주형 변수인 경우 ANCOVA라고도 함)은 평균 Treatment 효과에 대해 일관된 추정치를 제공하고 분산을 줄입니다. 

> Note : ANCOVA

- ANCOVA 는 독립변수가 종속변수에 어떻게 작용하는지를 살펴볼 수 있게 해줍니다.
- ANCOVA 는 여러분이 살펴보고자 하는 변수가 아닌 **공변량의 영향을 모두 제거한다**. 
  - 예를 들어, 여러분이 교수 능력의 수준이 수학 과목에 있어서 학생의 학습 능력에 끼치는 영향에 대해 알아보고 싶어한다고 하자.
  - 이러한 경우 학생들을 임의로 교실에 배정할 수 없을 수도 있다. 
  - 그렇다면 여러분은 다른 교실에 있는 학생들 사이에 계통적인 차이를 고려해야만 한다(예를 들어, 똑똑한 학생과 일반적인 학생 사이에 존재하는 수학 실력의 차이)

- Assumption : ANCOVA 를 적용하기 위한 가정

1. **독립변수(최소 2개) 는 범주형이어야 한다**.
2. **종속변수와 공변량은 연속형이어야한다**(등간척도 또는 비율척도).
3. **공변량과 종속변수는** (**모든 수준**의 독립변수에서) **선형적으로 연관** 되어야 한다.
4. 자료는 각각의 독립변수 값에 대해 종속변수는 **등분산성** 을 가져야 한다.
5. **공변량과 독립변수는 교호작용이 없어야 한다**. 다른 말로 하자면, 회귀계수에 동차성(homogeneity) 을 만족해야 한다.

> ## 2.3 Semi Parameteric Models

- 그러나 선형 모델은 일반적으로 모든 residual 은 동일하다는 가정을 하게 됩니다. 또한 treatment 의 효와에 대해서 metric 의 효과는 선형적이라는 가정을 하게됩니다. 
- 이러한 선형 모델의 한계를 극복하기 위해 연구자들은 준모수 모델(Tsiatis 2006)이라고 불리는 덜 제한적인 모델을 개발했는데, 이 모델에 일반화된 추정 방정식(GE)이 사용됩니다. 
- 표준 선형 모델을 준모수 모델과 비교한 양(Yang)과 치아티스(Tsiatis)(2001)는 선형 모델(ANCOVA)과 GE가 덜 제한적인 준모수 모델에서 점근적으로 동일하고 둘 다 조정되지 않은 t-검정보다 평균 처리 효과에 대해 더 효율적인 추정치를 제공한다는 것을 보여주었습니다.
- 레온 외. (2003년), 다비디안 외 연구진. (2005) 과 치아티스 외 연구진. (2008)은 준모수 통계 이론(Tsiatis 2006)을 사용하여 작업을 더욱 개선하고 평균 치료 효과에 대한 추정기 클래스의 분석 형태를 제공했다. 
  - 이 클래스는 평균 처리 효과에 대해 가능한 모든 RAL(정규 및 점근 선형) 추정기가 클래스 내 하나와 점근적으로 동일하다는 점에서 완전하다. 남은 문제는 학급에서 분산이 가장 작은 추정기를 찾는 것이고 그들은 일반적인 지침을 제공했습니다.
- 하지만! 이 논문에서 우리는 문제를 위와 같이 Linear Model 을 쓰지는 않을것이고 다른 관점에서 바라봅니다.
  - 무작위 실험의 분산 감소 문제를 몬테카를로 시뮬레이션의 유사한 문제와 연결함으로써 매우 강력한 결과를 도출할 수 있다. 

- 메트릭 변동성을 줄이기 위해 사전 실험 기간의 데이터를 사용할 것을 제안하며, 이는 매우 효과적이고 실제로 적용할 수 있는 것으로 밝혀졌다.

# [3.Variance Reduction](#link){: .btn .btn--primary}{: .align-center}

> ## 3.0 Variance reduction

> Variance reduction in Montecarlo

- 몬테카를로 샘플링에서 추정에 대한 분산 감소는 매우 유명한 주제입니다. 여기서 목표는 일반적으로 기본 분포에서 가능한 값을 반복적으로 시뮬레이션하여 parameter를 추정하는 것입니다.
- 이때 몬테카를로 샘플링에서 사전 정보를 통합하여 분산을 줄이는 샘플링 체계를 사용하면 상당한 효율성 이득을 얻을 수 있다. ( 즉 사전에 우리가 알고 있는 정보들을 넣음으로서 분산을 줄이는 것이죠. )

> Variance reduction in AB testing

- 하지만 안정된 population 에서 샘플릉 진행하는 몬테카를로 시뮬레이션과 달리 온라인 실험의 세계에서는 모집단이 역동적이고 실험이 진행됨에 따라 데이터가 시계열적으로 도착하게 됩니다. 
  - 즉 이런 온라인 세계에서는 미리 사전 지식을 이용하여 샘플링 계획을 설계하고  데이터를 수집하고, 그에 따라 parameter 에 대해서 variance reduction 의 효과를 얻기 힘듭니다
- 그렇다면 우리는 몬테카를로 분산 기법을 사용할 수 없을까요? 그렇지 않습니다. 우리는 사전 실험 데이터가 있기 때문에 몬테카를로 분산 기법을 적용할 수 있다는 것을 보여줄 것입니다.
- 여기서 고려하는 두 가지 몬테카를로 분산 감소 기술은 stratification 와 control variates 방법입니다.
- 각 기술에 대해 기본 개념을 검토한 다음 온라인 실험 설정에 어떻게 적응할 수 있는지 보여줄 것입니다.


> ## 3.1 Stratification in simulation

> Introduction

- 층화(Stratification) 는 분산 감소를 달성하기 위해 몬테카를로 샘플링에 사용되는 일반적인 기법입니다. 이 섹션에서는 온라인 실험의 세계에서 이러한 기법이 어떻게 사용될 수 있는지에 대해서 알아보도록 하겠습니다.
- 계층화의 기본 아이디어는 표본 추출 영역을 층으로 나누고 각 층 내에서 별도로 표본 추출한 다음 개별 층의 결과를 함께 결합하여 전체적인 추정치를 합치는 방법입니다. 
  - 일반적으로 층화 추출을 하였을떄가, 안했을때보다 분산이 더 작습니다.


> MonteCarlo Mean Estimation

-  $Y$ 가 우리가 알기 원하는 변수라고 할때, 우리는 ,$\mathbb{E}(Y)$ 를 알고 싶습니다.
- 이때 standard Monte Carlo 방법론은 n 개의 independent samples $Y_{i}, i=1, \ldots, n$, 를 만들고, 이 n 개 샘플의 평균  $\bar{Y}$ 를 $\mathbb{E}(Y)$ 에 대한 estimator 로 삼습니다. 
  - 이때 $ . \bar{Y}$ 는 unbiased 이고 분산은 $\operatorname{var}(\bar{Y})=$ $\operatorname{var}(Y) / n$. 가 됩니다.

> Stratification

- 이제 층화추출의 개념에 대해서 알아봅시다. Y 에 대한 Sampling region 을 K 개로(strata) 쪼갠다고 합시다. (ex : 사람을 추출할때 10대 , 20대, 30대... 로 나누는것)
- 그리고 $w_{k}$ 는  $Y$ 가 $k$ th stratum, ($k=1, \ldots, K$) 에 할당될 확률이라고 정의합시다. 
  - 만일 우리가  $n_{k}=n \cdot w_{k}$, 로 정의한다면 stratified average 는 아래와 같이 정의됩니다. 

$$\widehat{Y}_{s t r a t}=\sum_{k=1}^{K} w_{k} \bar{Y}_{k}$$

where $\bar{Y}_{k}$ is the average within the $k$ th stratum.

- stratified average $\widehat{Y}_{s t r a t}$ 와 Standard average $\bar{Y}$ 는 같은 expectation 값을 가지지만, variance 는  $\widehat{Y}_{s t r a t}$ 가 더 작습니다. 
  - 이때 직관은 다음과 같습니다.  variance of $\bar{Y}$ 는  within-strata variance 와 the between-strata varianced  로 분해될 수 있습니다. 
  - 이때  between-strata varianced 는 계층화를 통해서 제거될 수 있습니다. 
  - 한 예시로 아이들의 경우 바로 키의 편차를 계산하게 된다면 그 편차는 매우 큽니다. 하지만 연령별로  Stratify를 시키게 된다면 .더 작은 분산을 가지게 됩니다.

$$\begin{aligned}
\operatorname{var}(\bar{Y}) &=\sum_{k=1}^{K} \frac{w_{k}}{n} \sigma_{k}^{2}+\sum_{k=1}^{K} \frac{w_{k}}{n}\left(\mu_{k}-\mu\right)^{2} \\
& \geq \sum_{k=1}^{K} \frac{w_{k}}{n} \sigma_{k}^{2}=\operatorname{var}\left(\widehat{Y}_{\text {strat }}\right)
\end{aligned}$$

where $\left(\mu_{k}, \sigma_{k}^{2}\right)$ denote the mean and variance for users in the $k$ th stratum. 

- 이것에 대한 더 자세한 증명은 standard Monte Carlo books (e.g. Asmussen and Glynn (2008)). 에서 찾을 수 있습니다. 
- 좋은 Stratification 은 데이터의 클러스터와 잘 맞는 계층화입니다. 이러한 클러스터를 계층으로 정의함으로서 이들에 의해 생겨날 수 있는 분산을 제거할 수 있습니다. 

> ## 3.2 Stratification in Online Experimentation

- 온라인 세계에서는 시간이 지남에 따라 데이터를 수집하기 때문에, 미리 형성된 Strata 에서 샘플을 각각 추출하는 Sampling Scheme 을 적용할 수 없습니다.
  - 하지만 우리는 데이터가 모인 후에 계층을 만드는것이 아니라, 우리는 모든 데이터가 수집된 후에도 계층을 구성할 수 있습니다. (for theoretical justification see Asmussen and Glynn (2008, Page 153)).

- 예를 들어, $Y_i$ 가 사용자 i에 대한 쿼리 수라면, 공변량 $X_i$는 **사용자가 실험을 시작하기 전**( preexperiment variables) 에 사용한 브라우저의 종류 (Categoricl vatiable) 가 될 수 있습니다. 
  - 그리고 이 변수에 대해서 Stratify 를 진행한 뒤, 아래처럼   계층화 평균을 계산할 수 있습니다.


$$\widehat{Y}_{\text {strat }}=\sum_{k=1}^{K} w_{k} \bar{Y}_{k}=\sum_{k=1}^{K} w_{k}\left(\frac{1}{n_{k}} \sum_{i: X_{i}=k} Y_{i}\right)$$

- 이떄 Treatment 와 Control 을 표시하기 위하여 아래처럼 위첨자를 사용해 보았습니다. (t 는 Treatment , c 는 contol )

$$\Delta_{s t r a t}=\widehat{Y}_{s t r a t}^{(t)}-\widehat{Y}_{s t r a t}^{(c)}=\sum_{k=1}^{K} w_{k}\left(\bar{Y}_{k}^{(t)}-\bar{Y}_{k}^{(c)}\right)$$

- 위와 같이 차이에 대한 추정량은 stratified average을 사용하였으므로 , 동일한 로직으로 분산이 감소될 수 있습니다.
- 이떄 우리는 오로지 pre-experiment information 을 사용했다는것이 주목해야 합니다. 이렇게 하면 우리는 애초에 미리 실험한 정보만을 사용했으므로, 층화에 사용한 변수 $X_i$ 는 independent of the experiment effect 라고 할 수 있습니다. 즉 이는 stratified delta 는 unbiased 임을 보장합니다.
- 이떄 하나 더 고려할 점은 우리가 사용할 적절한 가중치 $w_k$ 를 항상 알고있지 않다는 사실입니다.
  - Online Experimental 맥락에서 이 값은 일반적으로, 실험에 포함되지 않은 사용자로부터 추정될 수 있습니다. (대게 실험의 경우 모든 트래픽에 대해서 Treatment 를 할당하지 않으므로 계산할 수 있습니다.)


> ## 3.2 Control Variates

- 우리는 온라인 실험이 시뮬레이션 에서에서 널리 사용되는 계층화 기법의 이점을 어떻게 얻을 수 있는지 보여주었습니다.
- 이 섹션에서는 Control Variates이라고 하는 시뮬레이션에 사용되는 또 다른 분산 감소 기술이 온라인 실험에서 어떻게 활용될 수 있는지를 보여주려고 합니다.

> ### 3.2.1 Control Variates in Simulation

- control variates 를 통해서 Variance Reduction 을 하는 방법의 아이디어는 다음의 예시를 통해서 알 수 있습니다.
- $\mathbb{E}(X)$  가 알려진 another random variable $X$  를 생각해 봅시다.
- 그러면 우리는  independent pairs of $\left(Y_{i}, X_{i}\right), i=1, \ldots, n$. 를 생각해볼 수 있고, 아래의 식을 생각해 봅시다.

$$\widehat{Y}_{c v}=\bar{Y}-\theta \bar{X}+\theta \mathbb{E} X,$$

where $\theta$ is any constant.

- 이떄 $\widehat{Y}_{c v}$ 는  $\mathbb{E}(Y)$ 에 대한 Unbiased estimator 입니다. 왜냐하면 $-\theta \mathbb{E}(\bar{X})+\theta \mathbb{E}(X)=0$. 는 0이기 때문입니다. 

> Variance

- 이떄 The variance of $\widehat{Y}_{c v}$ 는  아래와 같이 계산됩니다.

$$\begin{aligned}
\operatorname{var}\left(\widehat{Y}_{c v}\right) &=\operatorname{var}(\bar{Y}-\theta \bar{X})=\operatorname{var}(Y-\theta X) / n \\
&=\frac{1}{n}\left(\operatorname{var}(Y)+\theta^{2} \operatorname{var}(X)-2 \theta \operatorname{cov}(Y, X)\right) .
\end{aligned}$$

- 위의 $\operatorname{var}\left(\widehat{Y}_{c v}\right)$ 는 아래와 같이 세타를 정의할때게 최솟값이 됩니다.

$$\theta=\operatorname{cov}(Y, X) / \operatorname{var}(X)$$

- 위와 같이 분산을 최소화 하는 $\theta$ 를 선택한다면 그 Variance 는 아래와 같습니다.

$$\operatorname{var}\left(\widehat{Y}_{c v}\right)=\operatorname{var}(\bar{Y})\left(1-\rho^{2}\right),$$

- where $\rho=\operatorname{cor}(Y, X)$ is the correlation between $Y$ and $X$. 
-  $\bar{Y}$ 의 분산과 비교해 볼 때에, 위 $\widehat{Y}_{c v}$ 의 분산은  1- $\rho^{2}$  의 비율만큼 작아집니다.
  - 즉 $\rho$ 값이 클수록 Variance reduction 의 효과가 큽니다. 
- 이떄 위는 단일 Covates를 사용한것으로 고려되었지만, 여러 변수를 포함하도록 쉽게 일반화할 수 있습니다.

> OLS relation

- 또한 이 경우에 OLS 와 쉽게 관련지어서 생각할 수 있습니다. 
- $\rho=\operatorname{cor}(Y, X)$ 는 Simple Linear regression 에서 OLS 의 해와 일치한다는 것을 기억합시다. 즉 이는 $R^2$ 를 OLS 의 결정계수라고 합시다. 그러면

$$\operatorname{var}\left(\widehat{Y}_{c v}\right)=\operatorname{var}(\bar{Y})\left(1-R^{2}\right),$$

- 위와 같이 해석될 수 있습니다. 

> Nonlinear Adjustments

- 이전에 Adjustment 를 계산할때 다음과 같이 계산되었음을 기억합시다.

$$\widehat{Y}_{c v}=\bar{Y}-\theta \bar{X}+\theta \mathbb{E} X,$$

- 하지만 위의 관계식은 Linear Adjustment 입니다. Linear 관계만 사용하는게 아니라 아래처럼 좀 더 복잡한 관계까지도 확장이 가능합니다.

$$\widehat{Y}_{c v}=\bar{Y}-\overline{f(X)}+\mathbb{E}(f(X)),$$

- 위와 같은 경우도, $$\operatorname{var}\left(\widehat{Y}_{c v}\right)$$ 를 낮출 수 있습니다. 이때 $f(X)$ 의 Optimal 한 Choice 는 $\mathbb{E}(Y \mid X)$ 가 됩니다.

> ### 3.2.2 Control Variates in Online Experimentation

- 이전과 같이 분산을 줄이기 위해서 Control Variates 를 활용하는 방법론은 매우 일반적인 방법입니다.
  - 하지만 이것을 적용할때 어려운점중 하나는, Y 와 높은 상관관계가 있는 Control Variates $X$ 를 찾는것과 , $E(X)$를 찾는것입니다. 
- 이떄 $\mathbb{E}\left(X^{(t)}\right)$ and $\mathbb{E}\left(X^{(c)}\right)$ 를 알고있는 Control Variates $X$ 를 찾는것은 매우 어렵습니다. 당연히 우리는 신이 아니므로 Expectation 이 같은 Variates 를 정하는건 쉽지 않기 때문입니다.
- 하지만 이때 중요하게 생각해야될 점은 pre-experiment 단계에서  $\mathbb{E}\left(X^{(t)}\right)-\mathbb{E}\left(X^{(c)}\right)=0$ 인 Covariates $X$ 는 찾기 쉽다는 것입니다. 왜냐하면 당연히 Preexperiment 에서는 아직 'Treatment 를 적용하지 않은 상태' 이기 때문에 treatment 와 Control 은 차이가 없는 상태이기 떄문이죠. 
- 우리는 Pre-experiments 단계에서의 정보만을 이용했으므로 나중에 우리가 
- Given  $\mathbb{E} X^{(t)}-\mathbb{E} X^{(c)}=0$ 라고 합시다. 그러면 쉽게 $$\Delta_{c v}=\widehat{Y}_{c v}^{(t)}-\widehat{Y}_{c v}^{(c)}$$ 는 $\delta=\mathbb{E}(\Delta)$ 에 대한 Unbiased Estimator 라는것을 알 수 있습니다.
  - $$\Delta_{c v}=\widehat{Y}_{c v}^{(t)}-\widehat{Y}_{c v}^{(c)}$$ = $$\bar{Y}^{(t)}-\theta \bar{X}^{(t)}+\theta \mathbb{E} X^{(t)} - \bar{Y}^{(c)}+\theta \bar{X}^{(c)}-\theta \mathbb{E} X^{(t)} $$ 
  - $$\Delta_{c v}=\widehat{Y}_{c v}^{(t)}-\widehat{Y}_{c v}^{(c)}$$ = $$\bar{Y}^{(t)}-\theta \bar{X}^{(t)}- \bar{Y}^{(c)}+\theta \bar{X}^{(c)}$$  (즉 계산 가능한 추정치)
- 이떄 위 식처럼 $\Delta_{c v}$ 는 $\mathbb{E}\left(X^{(t)}\right)$ 와 $\mathbb{E}\left(X^{(c)}\right)$ 의 값은 서로 상쇄되므로 depend 하지 않는다는것을 기억합시다! 그러므로 계산이 가능하죠.

> Choice of $\theta$

- $\theta$ 에 대해서 Optimal Choice 를 하게 된다면 ($\theta=\operatorname{cov}(Y, X) / \operatorname{var}(X)$)  $\Delta_{c v}$ 는 아래와 같이 Variance 가 줄어들게 됩니다.

$$\operatorname{var}\left(\Delta_{c v}\right)=\operatorname{var}(\Delta)\left(1-\rho^{2}\right)$$

- 위의 경우 $\rho$ 가 클수록 분산 감소의 효과가 크다는것을 알 수 있죠. 

> Choice of X

- 즉 큰 상관관계를 얻고 분산 감소 최대화 하기 위하여 가장 분명한 접근 방식은 $X$를 $Y$와 동일하게 선택하는 것립니다. (왜냐하면 이렇게 선택하는 경우 X 는 Pre experiment 데이터를 쓰게되고 Y 는 실험 데이터를 사용하게 되므로 그 상관관계가 엄청 크게 되기 때문이죠. 한 예시로 홍길동이라는 사용자가 실험 전에 평균 구매금액이 100만원이였다면, Treatment 를 적용한 실험 중에서도 100만원 전후의 구매를 할 것이라고 예측할 수 있습니다.)
- 그러므로 이는 자연스럽게 사전 실험 관찰 윈도우 동안 동일한 변수를 Control Variant 로서 사용하게 된다는것도 예측할 수 있습니다.. 
  - 즉 실험 기간이 3주였다면, X 는 Pre-experiment 기간동안의 3주 구매금액, Y 는 실험 기간동안의 3주 구매금액이 될 수 있습니다. 


> Note : Choice of $\theta$

- 이러한 방법론은 이것은 실제로 Control Variant 방법론으로서 가장 효과적인 방법론으로 알려져 있습니다. 
- 하지만 여기에서는 살짝 지적할점이 있습니다. The pair $(Y, X)$ 는 Treatment 효과가 있을때 약간 Dsitribution 이 달라질 수 있습니다. 그러므로 이는 $\theta$ 를 추정할때에 Cor$(Y, X)$  를 사용하게 되는데요, 이때  Treatment Sample 을 사용했을때와 Control Sample 을 사용했을때의 값이 다르다는 것이죠
-   $\Delta_{c v}$ 가 Unbiased 이려면 Treatment 와 Control 모두에 대해서 같은 $\theta$ 를 사용해야 합니다. 
  - $$\Delta_{c v}=\widehat{Y}_{c v}^{(t)}-\widehat{Y}_{c v}^{(c)}$$ = $$\bar{Y}^{(t)}-\theta \bar{X}^{(t)}- \bar{Y}^{(c)}+\theta \bar{X}^{(c)}$$  (즉 계산 가능한 추정치)
  - 위를 보면 당연히 $\theta$ 는 같아야 함을 알 수 있죠
- 그러므로 이를 추정하는 가장 쉬운 방법은 control 과 treatment 에 대한 Pooled population 으로부터 추정하는 것입니다. (즉 합친 샘플을 이용해서 세타를 추정해야한다는 의미)
- 만일 위처럼 Linear 과꼐가 아니라 general nonlinear control covariates Case 의 경우 우리는  $\widehat{Y}_{c v}^{(t)}$ and $\widehat{Y}_{c v}^{(c)}$ 에 대해서 같은 함수를 사용해야 합니다.
  - $$\widehat{Y}_{c v}=\bar{Y}-\overline{f(X)}+\mathbb{E}(f(X))$$ 로 추정되기 때문에 unbiased 가 되려면 당연한 이유이죠

> ## 3.3 Connection between Stratification and Control Variates

> Connection with Stratification and Control Variates

- 우리는 분산 감소를 달성하기 위해 Covariates 를 활용하는 두 가지 기술에 대해 논의했습니다. 
  - stratification 접근법은 Covariates을 사용하여 strata을 구성하고 Control Covariates 접근법은 회귀 변수로 사용한다. 
- stratification는 이산형(또는 이산형) 공변량을 사용하는 반면, Control Covariates는 연속형 변수를 아용하기 때문에 더 자연스럽게 보입니다. 
- 그러나 이 두 가지 접근법이 밀접하게 관련되어 있습니다.
  - 실제로 공변량 X가 범주형일 때(예: 이산형 값 1, . . . , K) 두 접근법이 동일한 추정치를 생성한다는 것을 보여 줄 수 있습니다. 
  - 자세한 내용은 부록 A에 포함되어 있습니다. 기본 아이디어는 각 stratum 에 대해 지시 변수 $1_{X=k}$ 를 구성하고 평균이 stratum Weight 인 $w_k$ 를  control variate 로 사용하는 것입니다. 
- 즉 더 확장하자면 control variates technique 은 extension of stratification 라고 할 수 있으며, Covariates 변수가 실수형이든, 범주형이든 적용이 가능합니다.

> Insight

- 두 기술( Stratification and Control Variates) 은 수학적으로 서로 연관이 매우 큽니다.  또한 각각의 방법론은 분산 감소를 가능하게 하는 이유와 방법을 이해하는 데 다른 통찰력을 제공합니다.
- Stratification는 Population 의 성질에 따라에 따라 Sampling 을 을 분리한 이후 component 간 분산을 효과적으로 제거하고 분산을 줄이게 됩니다.
  - 즉 소득에 대한 추정시에, 연령별로 나누어서 추정하여서 분산을 줄인다는것과 같습니다.
  - A better covariate 는 표본을 더 잘 분류하고 기본 구조를 잘 반영하는 것이 좋습니다. 
    - 공변량의 경우도 마구잡이로 선택할 수 없다는 것이죠.
- 반면에, control variates 방식은 공변량과 변수 자체의 상관 관계에 대한 함수로 분산 감소의 양을 정량화(수식화)합니다. 
  - 이 방법은 매우 수식적으로 간단하고, simple 합니다. 
  - 이떄 better covariate 는 상관 관계가(절댓값) 더 커야 합니다.

# [4. CUPED IN PRACTICE](#link){: .btn .btn--primary}{: .align-center}

- CUPED를 구현하는 간단합니다. 그 중에서 효과적인 방법은 사전 실험 기간의 동일한 변수를 Covariates 변수로 활용하는 것입니다.
  - 빙의 실험 시스템 에 대해서 실제로 우리는 이러한 방법론을 적용하였습니다. 
- 하지만 이것이 불가능하거나 실용적이지 않은 상황이 있습니다. 
  - 예를 들어 사용자 유지율을 측정하거나 새로운 사용자를 대상으로 실험을 수행하려는 경우 우리는 Covatiates 를 구성할 사전 데이터 (Pre-experiments data) 가 없으므로 아예 X 를 구성할 수 없습니다.
- 사실, 대부분의 온라인 실험에서 우리는 모든 사용자에 대한 사전 실험 정보를 가지고 있지 않을 수 있습니다.
- 또한 분석 단위가 사용자(User)가 아닌 메트릭에 대해 사전 실험 데이터를 어떻게 사용하는지도 문제가 됩니다.
- 이 Section은 Bing의 실험 시스템을 사례 연구로 사용하여 이와 같은 실제 과제를 해결하는것에 대해서 알어보려 합니다.

> ## 4.1 Selecting Covariates

> Selection pre-experiments Covariates Variable

- 공변량(Covariates)의 선택은 분산 감소의 효과를 직접 결정하기 때문에 매우 중요합니다. 
  - 올바른 변수를 선택하면 분산을 절반으로 줄일 수 있지만 잘못된 선택을 하면 분산을 거의 줄일 수 없습니다. 

- 우리는 어떤 Pre - expereiments 변수가 가장 잘 작동하는지 이해하기 위해 가능한 사전 실험 변수를 많이 평가해 보았습니다.
- 그 결과 우리의 결과는 공변량과 동일한 변수를 사용하는 것이 최상의 분산 감소를 제공하는 경향이 있다는 것을 일관되게 보여주었습니다.

> Experiments Length and Pre-Experiments Length

- Terminology
  - Experiment Length : 실험 기간 (Control vs Treatment 실험)
  - pre-Experiments Length : 사전 실험기간 (Covariates 를 계산하기 위해 고려하는 사전실험 기간)
- 이떄 실험 기간을 정하는게 중요합니다. 위의 기간을 어떻게 조절하는게 좋을까요?
  - pre-experiments 기간이 동일할때, Experiments 기간이 늘어난다고 해서 분산 감소율이 개선되지는 않았습니다. 
  - experiments 기간이 동일할때 pre-experiments 기간이 길수록 더 높은 분산 감소를 제공합니다. 
- 자세한 내용은 섹션 5에서 보도록 하겠습니다.


> ## 4.2 handling missing

> Problem

-  온라인 사이트에서는 실험의 모든 사용자에 대한 사전 실험(pre - experiments) 데이터가 없을 수 있습니다.
   -  일부 사용자는 실험기간 도중에 처음 방문할 수 있습니다. 이 경우에 pre-experiments 에는 정보가 없을것입니다.

-  또한 사용자를 식별할수 있는 key 가 유저별로 "바뀔"수 있는 쿠키로 식별되는 경우도 있습니다. (즉, 사용자가 쿠키를 삭제하면 변경됨). 
-  이것은 Covariates를 구성하기 위해 사전 실험 정보를 사용하는것을 어렵게 만듭니다.
   -  실험 중이지만 사전 실험 기간에 있지 않은 사용자의 경우 해당 공변량이 잘 정의되어 있지 않습니다. 


> Remedy

-  이를 해결하는 한 가지 방법은 사전 실험 기간에 사용자가 나타났는지 여부를 나타내는 또 다른 공변량(Covariates) 을 정의하는 것입니다.. 
   -  이 추가 binary covariate을 사용하여 Missing Covariates 값을 원하는 상수로 설정할 수 있습니다. 
-  직관적으로 이것은 사용자를 실험 전 기간에 나타난 Strata과 그렇지 않은 계층으로 나누는 것과 같습니다. 
   -  이렇게 나눈다면 우리는 사전 실험 데이터를 가진 사용자 Stratum의 경우 Pre-experiments Covariates가 잘 정의되어 있으므로 이러한 공변량을 기반으로 한 추가적인 분산 감소가 가능할 것입니다.


> ## 4.3 Beyond Pre-Experiment Data

- 지금까지 우리는 사전 실험 데이터를 사용하여 구성된 공변량을 기반으로 메트릭 변동성을 줄이는 것만 고려했습니다.
  - 사전 기간의 동일한 변수를 사용하면 분산 감소 효과가 가장 잘 나타날 뿐만 아니라 사전 실험의 정보를 이용하게 되므로,  실험의 효과와 independence 를 보장하고, 우리가 원하는 겨로가에 대해서 Unbiased 를 보장하기 떄문입니다.
- 이것을  control variates formulation 와 함께 보도록 하겠습니다..

> Formula

$$\Delta_{c v}=\widehat{Y}_{c v}^{(t)}-\widehat{Y}_{c v}^{(c)}$$

$\Delta_{c v}$ is computed assuming $\mathbb{E}\left(X^{(t)}\right)=\mathbb{E}\left(X^{(c)}\right)$. 

- 하지만 만일 difference between control and treatment in terms of $X$ 가 있었다면, 위의 equality 는 성립하지 않고, 이는 $\Delta_{c v}$ 가 biased 가 될 것이라는것을 의미합니다.

> Example

- 예를 들어, 페이지 로드 시간이 빠르면 일반적으로 검색 페이지를 더 많이 클릭하게 됩니다(Kohavi 등). 2009b). 
- 페이지 로드 시간을 개선하는 Experiments 에서의 (즉 pre-experiment 의 정보가 아님) 클릭 수를 Covariates으로 사용하는 경우, 개선(Improvement) 의 일부가 Covariates에 의해 “adjusted away"되기 때문에 로드 시간에 대한 실험의 영향을 과소평가하게 됩니다. 
  - 로드시간 개선 -> 클릭 수 개선 -> 조절되는 값 (- 로 빼지는 공변량 값) 도 커짐 -> 과소평가
  - 여기에 설명된 요건을 위반하는 공변량을 사용함으로써 발생하는 Biased 된 결과의 실제 예는 섹션 5를 참조하세요

> Beyond Pre-Experiments Data

- 그러나 이것이 Pre-experiments 데이터를 기반으로 한 공변량만이 유일한 선택이라는 것을 의미하지는 않습니다. 
  - 필요한 것은 공변량 X가 실험의 Treatment의 영향을 받지 않는 것입니다! 
- pre-experiment 외에 사용할 수 있는 공변량은 어떤게 있을까요? 
  - 사용자가 실험에 처음 나타날 때 수집된 정보를 사용하여 구성된 Covariates 를 활용할 수 있습니다.
  - 예를 들어, 사용자가 실험에서 처음 관찰되는 요일은 실험 자체와 무관합니다. 즉 이러한 공변량은 분산 감소를 위해서 쓸 수 있을것입니다.
- 이 아이디어를 확장하면 사용자가 실제로 experiment feature를 트리거하기 전에 설정된 정보를 기반으로 한 공변량도 유효하다. 
  - 이 기능은 평가할 Feature 의 트리거 속도가 낮은 경우에 특히 유용할 수 있습니다.

> ## 4.4 Handling Non-User metric

- 섹션 1에서 언급했듯이 온라인 실험에서 유저 기준이 아니라 Cookie 기준으로 Randomize  Uniit 을 사용하는 경우가 있습니다.  (또는 세션 단위 등이 될 수 있음)
  - ex : 추천 알고리즘을 바꾸는 경우에는 세션 단위로 Randomize unit 을 설정하면 실험 sample 수가 늘어나고, 실험의 품질이 늘어나게 됨
- 지금까지의 논의에서, 우리는 분석 유닛도 "사용자"라고 가정했습니다. 하지만 항상 그렇지는 않습니다.
  - 예를 들어 클릭 수를 총 페이지 수로 나눈 값으로 CTR를 계산할 수 있습니다. 여기 분석 단위는 사용자 대신 페이지입니다. 
- 분산 추정 자체는 분석 단위와 실험 단위가 일치하지 않을 때 더 어렵습니다. 
- 가장 일반적인 솔루션은 델타 방법을 사용하여 동일한 사용자의 페이지 상관관계를 고려한 정확한 분산 추정치를 생성하는 것입니다.(Deng et al. 2011; Tang et al. 2010b; Kohavi et al. 2009b).
- 이러한 비사용자 수준 메트릭에 대한 분산 감소를 달성하려면 델타 방법과 분산 감소 기술을 함께 결합해야 합니다. (자세한 내용은 부록 B에 나와 있습니다.) 
- 실제로 관심 메트릭(예: CTR)이 페이지 레벨일 뿐만 아니라 페이지 레벨 공변량도 가질 수 있습니다. 이렇게 하면 다음과 같은 페이지별 기능을 기반으로 하는 더 큰 클래스의 공변량을 사용할 수 있는 문이 열립니다.

# [5.Emprical Resultes](#link){: .btn .btn--primary}{: .align-center}

> ## 5. Empricical Results

- 이 섹션에서는 Microsoft Bing의 실험 시스템에 대한 CUPED의 효과를 보여주는 실제 예시들을보여주려 합니다.
- 먼저 우리는 CUPED가 bing에서 실험의 민감도(Power)를 어떻게 크게 향상시킬 수 있는지 보여준다. 
- 다음으로 우리는 Treatment가 대조군과 동일하여 치료 효과가 0인 것으로 알려진 통제된 실험인 3주 A/A 테스트를 더 자세히 살펴봅니다. A/A 실험을 사용하여 실제 온라인 실험의 분산 감소 성공에 큰 영향을 미칠 수 있는 중요한 결정을 검토해 보겠습니다. 
- 마지막으로 실험에 부적절하게 공변량을 선택할 경우 편향된 추정치가 어떻게 발생하는지 보여주려고 합니다.

> ## 5.1 Slowdown Wxperiment in bing

- 실제 실험에서 CUPED의 영향을 보여주기 위해 페이지 로드 시간과 user engagement 사이의 관계를 Bing에 테스트한 실험을 조사해 보았습니다.
- 이 실험에서는 Bing 쿼리에 대한 서버 응답을 의도적으로 250밀리초 지연시켰습니다. 
  - 이때 수백 밀리초 정도의 지연은 user engagement를 손상시키는 것으로 알려져 있습니다((Kohavi et al. 2009b, Section 6.1.2)

- 실험은 처음에 Bing 사용자 중 작은 비율의 데이터만을 대상으로 2주 동안 실행되었으며, 통계적으로 유의한 클릭률(CTR)에 대한 영향을 관찰했습니다.
- 이 경우에 p-값이 임계값 0.05보다 약간 낮았습니다. 이 메트릭에 대한 Treatment Effect가 False Positive 가 아닌 실제라는 것을 확인하기 위해, 우리는 더 큰 큰 실험을 진행했고 이것은 실제로 p-값 2e-13으로 실제 효과임을 확인할 수 있었습니다.

> Apply Cuped Methods

-  CTR from the 2-week preperiod 를 Pre-experiment Covariates 로 설정한 뒤에 Cuped 방법론을 적용하였습니다. 
- 결과는 인상적이였습니다. 델타 수치는 첫날부터 통계적으로 유의했습니다! 

![jpg](/assets/images/Stat/124_1.jpg)

- 위 그림은 시간 경과에 따른 p-값을 로그 척도로 보여줍니다. 검은색 수평선은 0.05 유의 막대입니다. 

> Interpret

- Cuped 를 적용하지 않은 실험에서 (빨간색 막대) t -test는 서서히 낮아지고 실험이 2주 만에 중단될 때쯤 되어서야 간신히 p-value 가 임계점 0.05 보다 낮아졌습니다.
- 하지만 같은 실험에 대해서 CUPED를 적용하면 전체 p-값 곡선이 막대 아래에 있습니다.
- 그림의 하단 그림은 CUPED가 사용자의 절반만 대상으로 실행될 때의 p-값 곡선을 비교합니다. CUPED는 사용자 절반이 실험에 노출되어도 더 민감한 테스트가 진행되고 있음을 알 수 있습니다.
- 실험 대부분이 사용자의 Experience 에 부정적이나 아무 영향도 미치지 않는다는 사실(Kohavi et al. 2009a; Manzi 2012) 에 비추어볼때, 우리는 위와 같이 같은 샘플을 이용하였더라도 기존의 실험보다 더  Statistical Power 가 높은 실험을 진행하는것은 CUPED 의 이점입니다.
- 위 실험뿐만 아니라 다른 실험을 수행하였을떄에도 CUPED 방법론은 비슷한 수준의 Statistical Power 상승 효과를 얻을 수 있었습니다.

> ##  5.2 Factors Affecting CUPED Effectiveness

- 이 섹션에서는 실제로 CUPED를 사용하는 데 큰 영향을 미칠 수 있는 요소를 살펴봅니다. 여기서 사용하는 데이터는 3주간의 A/A 실험에서 얻은 데이터입니다.

> ### 5.2.1 Covariates

- 위 그림은 queries-per-user 라는 metric 에 대한 CUPED의 분산 감소율을 보여줍니다. 이때 공변량 (Covariates) 는 아래와 같이 2가지가 고려됩니다. 
  - (1) 사용자가 실험에 처음 나타나는 날을 나타내는 범주형 변수인 Entry-day
  - (2) pre-experiments data 1주 동안의 사용자당 쿼리-변수
-  Entry-Day는 사전 실험 데이터는 아니지만, Treatment 가 실험 중 사용자가 처음 오는 시간에 영향을 미치지 않기 때문에 4.3절에서 요구하는 조건을 만족한다.

![jpg](/assets/images/Stat/124_2.jpg)

- 위에서 전체 실험은 3주동안 수행되었습니다.  이떄 감소율은 최대 3주까지 데이터가 축적되고, 평가되고 표시되고 있습니다.
- 위 그림에 대해서 'Variance Reduction Rate' 는, 일반적인 $\Delta$ 를 사용했을때의 Variance 와 Variance Reduction 을 사용했을떄 $\Delta^*$ 의 Variance 를 비교하여 얼마나 분산이 낮아졌는지를 나타내는 그래프입니다.

> Interpret

- 진입일(Entry-day) 를 공변량으로 사용할 경우 실험이 더 오래 실행되고 2주 후 이후에도 아주 조금씩이지만 Variance 가 reduction 되고 있는것을 볼 수 있습니다.
- 반면 Pre-experiments 기간중에 사용자당 쿼리 를 공변량으로 사용하면 분산 감소율이 45% 이상에 이른다는것을 볼 수 있습니다. 
- 두 공변량을 함께 결합하면, Pre-experiments 기간중에 사용자당 쿼리 만을 사용했을때 보다 2~3% 더 많은 추가 감소를 얻을 수 있다는것을 볼 수 있습니다.
- 이는 Pre-Experiments 기간에 계산된 동일한 메트릭이 Entry - day 보다 더 나은 단일 공변량임을 의미합니다. 
- 실험 기간과 실험 전 기간의 동일한 지표는 당연히 높은 상관관계를 가지기 때문에 높은 Variance Reduction 을 하게 되는것은 당한것이라고 볼 수 있습니다. 
- 이때 marginal variance reduction 효과만을 봅시다. 두 공변량을 함께 결합할 때 하나만 사용할때보다 분산 감소가 너무 작다는 사실은 Entry day 와 사용자당 쿼리 사이의 대부분의 상관 관계를 사용자당 Pre-experiment Queries 로 설명할 수있다는것을 의미한다.
  -  좀 더 정확히 말하면, 사용자당 Entry Day와 사용자당 쿼리의 부분적 상관관계가 낮다는것을 의미합니다.

> ### 5.2.2 Lengths of Experiment and Pre-Experiment

![jpg](/assets/images/Stat/124_3.jpg)

- 위 그림은 Covariates 의 효과 이외에도 Experiment Length 의 길이의 영향에 대한 직관을 제시합니다.

> Intuition

- 흥미로운 점은, 실험 기간이 증가함에 따라 Pre-experiments Covariates 를 사용했을때의 (녹색/삼각형)의 분산 감소율이 단조롭게 증가하지 않는다는 것입니다.
  - 약 2주 정도에 최대치에 도달한 후 서서히 감소하기 시작합니다.
- 위와 같은 현상을 좀 더 분석하기 위하여 우리는 Pre-experiments 의 기간이 3일에서 2주까지의 기간 길이를 갖는 4가지 방법에 대한 분산 감소율을 Plotting 해 보았습니다. 
  - 위 그림에서 볼 때 더 긴 Experiments Length 를 사용한경우가 더 높은 분산 감소율을 나타내느것을 볼 수 있습니다.

> Learning

- 이전에 살펴본 그림3과, 여기에서 본 그림4 에서 우리는 CUPED의 효과에 영향을 미치는 두가지 상반된 요소를 볼 수 있습니다. 
  - 상관관계 : 상관관계가 높을수록 분산 감소의 효과가 더 높습니다. 또한 Pre-experiments 의 길이를 늘리거나, Experiments 기간을 늘리면 사용자당 쿼리와 같은 "누적" 메트릭에 대한 상관 관계가 증가합니다. 왜냐하면 기간이 길수록 측정에 대한 Noise 가 적어지기 때문입니다.
  - Coverage : Coverage 는 Experiment 에 나타난 사용자에 대해서, Pre-experiment 에도 나타난 사용자의 비율입니다. 이러한 Coverage Rage 는 다음과 같이 결정됩니다. 
    - Experiment Duration : 실험 기간이 늘어날수록 Coverage 가 감소합니다. 왜냐하면 실험 초기에는 단골 방문객이 보이지만 (즉 Pre-experiment 유저가 존재), 실험 후기에는 새로운 사용자의 방문이 늘어나기 떄문입니다. Coverage Rate 가 감소할수록 Pre-experiment 정보를 사용해서 Variance Reduction 을 사용할 수 있는 유저가 줄어드므로, Variance Reduction 의 효과가 줄어듭니다.
    - Pre-Period Duration : Pre-Experiment 의 기간이 늘어난다면, Pre-period 의 유저 수도 많아지기 때문에, Variance Reduction 을 사용할 수 있는 유저도 늘어나기 때문입니다.

> ### 5.2.3 Metric of Interest

> Metric and CUPED

- 우리는 이전에 Covariates 를 어떤것을 선택하는것인지, Experiment 의 길이를 어떻게 정할지, Pre-experiment 길이를 어떻게 정할지에 따라서 살펴 보았습니다.
- 이떄 CUPED 의 효과는 pre-experiment metric(X) 와 experiment metric(Y) 간의 Correlation 의 크기에 따라서 효과가 달라집니다.
- 우리는 사용자당 클릭 수 , 사용자당 방문 수 와 같은 몇가지 메트릭에 대해 CUPED 을 적용해 보았습니다. 

> Cuped and Revenue

- 한 가지 주목할 만한 예외는 사용자당 수익으로, CUPED는 사전 실험 기간과 실험 기간 사이의 사용자당 수익의 상관관계가 낮기 때문에 Variance Reduction 의 효과가 5% 미만에 불과했습니다.

> CTR(Click Through Rate)

![jpg](/assets/images/Stat/124_4.jpg)

- 그림 5는 2주 전 실험 CTR을 CUPED 공변량으로 사용하여 클릭률(CTR) 감소율을 나타냅니다.

> Queries per User 

![jpg](/assets/images/Stat/124_5.jpg)

- 그림 6은 두 기간 사이의 상관관계에 대한 곡선을 나타냅니다.
- 이 경우에도 상관관계의 추이는 사용자당 쿼리와 유사하며 Variance Reduction 의 추이도 매우 비슷합니다.

> ## 5.3 Warning on Using Post-Triggering Data

- 이전 섹션 4에서 우리는 편향되지 않은 결과를 보장하기 위해 모든 공변량 X가 $E(X^{(t)}) = E(X^{(c)} ) $ 조건을 만족시켜야는것을 언급했습니다.

![jpg](/assets/images/Stat/124_6.jpg)

- 이 데이터는 사용자당 쿼리가 통계적으로 크게 증가한 다른 Bing 실험에서 얻은 것입니다
- 하지만 위의 데이터를 보면 기존의 실험 (Delta) 와 Cuped 를 적용한 실험 (Delta_cuped) 의 delta 방향이 다른것을 볼 수 있습니다. 
- 이런 경우에는 어떻게 된 것일까요?

> 다른 Covariates 변수 사용

- 우리는 queries-per-user 와 상관 관계가 높은 메트릭을 찾아보았습니다. 이때 나이브하게 생각한다면 pre-experiment queries-per-user 메트릭을 사용할 수 있을 것입니다. 
- 하지만 in-experiment Distinct Queries-peruser (DQ-per-user) 메트릭인 경우가 더 Correlation 가 더 높았습니다. 
  - DQ의 경우는 연속 중복된 쿼리가 제거된 후에 대한 사용자당 쿼리 수로 정의됩니다.
  - 결과적으로 DQ는 사용자당 쿼리(queries-per-user)보다 훨씬 매우 높은 상관관계를 가집니다. 
- 그러므로 공변량으로서의 사용자당 DQ는 좋은 아이디어인것처럼 보입니다. 그래서 우리는 DQ 를 사용하여 Covariates 를 구성하였고 $\Delta_{Cuped}$ 를 계산해 보있습니다.

> paradox : CUPED 를 적용하니 결과가 반대?

- 그 결과 그림 7은 CUPED 추정치 $\Delta_{C U P E D}$ 가 음수이고 신뢰 구간은 거의 항상 0 미만임을 보여줍니다. 
- 또한 신뢰 구간당 길이도 매우 짧은것도 볼 수 있습니다. 즉 사용자당 DQ 는 실제로 분산을 매우 많이 줄인것을 알 수 있습니다.
- 하지만 위의 결과를  $\Delta_{C U P E D}$ 를 이용해 해석하게 된다면 Control 과 Treatment 간의 사용자당 쿼리 차이가 95% 신뢰도로 음수이며, 그 결과는 알려진 효과와 방향적으로 반대임을 의미합니다! 

> 원인

- 이러한 모순은 사용자당 DQ가 $E(X^{(t)}) = E(X^{(c)} ) $ 를 만족시키지 않기 때문에 나타납니다.
- 사실 Treatment 에서는 사용자당 쿼리가 더 크기 때문에 사용자당 DQ도 더 큽니다.

$$\Delta_{c v}=\widehat{Y}_{c v}^{(t)}-\widehat{Y}_{c v}^{(c)}=\bar{Y}^{(t)}-\theta \bar{X}^{(t)}- \bar{Y}^{(c)}+\theta \bar{X}^{(c)}$$  

- 즉 위처럼 Treatment 의 $\bar{X}^{(t)}$ 가 과대추정 되었기 떄문에, $\Delta_{cv}$ 의 경우 값이 작아지게 됩니다. 즉  이러한 경우 공변량 델타도 양수이므로 CUPED 추정치가 0 아래로 내려갑니다. 
- 이러한 예시는 Pre-Experiment Data 를 사용하지 않고, In-Experiment 데이터 (즉 실험 도중의 데이터) 을 사용할때에 CUPED 의 Pitfall 을 나타냅니다.

# [6.Conclusion](#link){: .btn .btn--primary}{: .align-center}

> ## CONCLUSIONS

> Cuped 의 필요성

- Controlled Experiment 의 sensitivity 를 높히면 정확한 평가가 가능해지고, 더 적은 샘플과 더 적은 실험 기간을 가지고도 품질이 높은 실험을 진행할 수 있습니다.
- 우리는 사전 실험 데이터를 활용하여 Controlled Experiment 의 Sensitivity 를 높히는 새로운 기술은 CUPED 방법을 도입하였습니다. 
- CUPED 는 현재 Bing 의 Oneline Experiment System 에서 작동중입니다. 

> Cuped 적용 현황

- 최근 세 가지 중요한 실험에서 1주간의 실험과 1주일의 사전 실험 데이터로 45%, 52%, 49%의 분산 감소 효과를 얻을 수 있었습니다.
- 이는 CUPED가 사용자의 절반, 즉 지속 시간의 절반만으로 동일한 통계 능력을 효과적으로 달성하는 데 도움이 될 수 있음을 확신시켜 줍니다.
- CUPED는 단순성, 기존 시스템에 쉽게 추가할 수 있는 기능, 온라인 비즈니스에서 일반적으로 사용되는 메트릭에 대해 적용이 가능하다는 이점들 때문에  온라인 실험 시스템을 실행하는 조직에 광범위하게 적용할 수 있을 것입니다.
- Bing에서 CUPED를 적용한 경험을 바탕으로 온라인 실험에 CUPED를 적용하는 데 관심이 있는 다른 사람들을 위해 다음과 같은 권장 사항을 제공할 수 있습니다.

> Recommendataion for adaptation

- 분산 감소는 사용자 모집단에 따라 분포가 크게 다른 메트릭에 가장 적합합니다. 즉 Light 유저와 Heveay 유저의 경우 메트릭의 값이 매우 다른 경우입니다. 이러한 예시는 사용자당 쿼리 등이 될 수 있었습니다.
- 공변량을 정할떄에는 , 이전 기간에 측정된 메트릭을 공변량으로 사용하는 것이 일반적으로 최상의 분산 감소를 제공합니다.
- a pre-experiment period 기간은 1-2주를 사용하는 것이 분산 감소에 효과적입니다. 
  - 기간이 너무 짧으면 유저 매칭률이 너무 적습니다. (기간을 너무 짧게 하면 pre-experiment data 가 있는 유저의 수가 너무 적습니다.)
  - 기간이 너무 길면 실험 기간 동안 결과 메트릭과의 상관관계가 감소한다. (너무 옛날것까지 고려하면 최근 경향과는 다르므로)
- Treatment 의 영향을 받을 수 있는 공변량을 사용하면 결과가 편향될 수 있으므로 절대 사용하지 않는것을 추천드립니다. 
  - 우리는 이 요건을 위반할 경우 방향적으로 반대되는 결론이 나올 수 있는 예를 보여주었습니다. 

> ## Our Improvement Plan

- Cuped 의 경우 Oneline Experiment 의 Sensitivity 를 크게 향상시켰습니다. 이에 대해서 개선 사항을 더 살펴보도록 하겠습니다.

> Optimized Covariate Selection.

- CUPED를 확장하여 Covariates selection 에 대한 과정을 확장할 수 있습니다. 
  - 이떄 특정한 실험에 대해서, 적합한 Covariates 를 추천하는 시스템을 구축할 수 있을것입니다.

> multiple covariates

- 우리는 또한 대규모의 공변량 변수 라이브러리에서 다중 공변량의 선택을 최적화 하기 위해 연구하고 있습니다. 

> Incorporating Covariate Information into Assignment

- 실험이 완료된 후 데이터를 조정하는 대신, 공변량을 인식한 상태에서 Randomizaation 이 진행된다면  실험에 트래픽을 더 효율적으로 할당할 뿐만 아니라 실험의 민감도를 향상시킬 수 있습니다.

**reference**

- <http://rinterested.github.io/statistics/chi_square_same_as_z_test.html>
- https://bytepawn.com/reducing-variance-in-ab-testing-with-cuped.html



