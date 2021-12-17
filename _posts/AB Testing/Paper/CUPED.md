---
title: "Improving the Sensitivity of Online Controlled Experiments by Utilizing Pre-Experiment Data"
excerpt: "Cuped 를 적용한 Improve Sensitivity Methods"
categories:
  - AB_Testing
last_modified_at: 2021-12-13

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

A/B Testing 에서 Proportion 검정하는방법
{: .notice--warning}

# [Abstract and Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## Abstract

- Online Controlled Experiment 는 Amazon, eBay , Zynga 등 다양한 회사에서 데이터 중심 결정을 내리는 핵심이 됩니다.
- 이때에 매우 작은 비율의 차이로도 주요 측정 기준 (OEC) 의 차이는 매우 중요한 비즈니스에 영향을 끼칠 수 있습니다.
  - 매우 큰 회사인 빙에서는 수천만달러가왔다갔다 하는 매우 중요한 실험을 수행하게 됩니다. 

- 이 논문에서는 메트릭 변동성을 줄이고, 따라서 더 나은 감도를 달성하기 위해 사전 실험 기간의 데이터를 활용하는 접근법인 CUPED 를 제안합니다.
- 이 기술은 주요 비즈니스 메트릭에 활용이 가능하고, 실용적이며 구현이 쉽습니다.
- 이러한 기술을 적용한 Bing 은 매우 성공적이였습니다. 사용자의 절반 또는 절반의 실험 기간으로도 동일한 통계적 능력을 달설할 수 있었습니다.

> ## Introduction

- 통제된 실험은 가장 오래되고 보편적으로 받아들여지는 방법론입니다.
- 현재 많은 기업에서 널리 사용되고, 재발견된 이 실험은 다음과 같이 다양한 이름으로 불리워지고 있습니다.
  - A/B test (Wikipedia) , a split test, a weblab (at Amazon), a live traffic experiment (at Google), a flight (at Microsoft) , and a bucket test (at Yahoo!). 
- 이 논문은 아마존, ebay 와 같은 온라인 비즈니스 사이트 및  포탈의 온라인 제어 실험에 촛점을 맞추고 있습니다.
  - 이때 온라인 제어 실험은 매우 중요합니다. 몆퍼센트 비율 차이는 비즈니스에게 막대한 영향을 끼치게 됩니다.


![jpg](/assets/images/Program/125_1.jpg)

- 우리는 위와 같은 방 찾기 예시부터 시작해 보겠습니다.
- 위 그림처럼 6가지의 방 찾기 위젯을 위한 6개의 후보가 있엇습니다. 
  - 왼쪽 맨 위가 Control 입니다.
  - 실험동안 사용자는 6 가지 Variant으 로 무작위로 나뉘었습니다.

- 우리는 위의 위젯을 통해서 파트너 사이트 방문을 늘리는것이 목표였습니다.
  - 우리는 사용자의 상호작용을 계측하고, 파트너 사이트로의 전 횟수를 늘리는것이 목표였습니다.
- 이 실험에서 승자인 Treatment 는 이전 대조군 대비 수익을 10% 증가시켰습니다.

> Controled Experiment

- 통제실험의 한가지 과제는 Treatment 효과가 실제로 존재할때 탐지하는 능력으로, 보통 Power , Sensitivity 라고 불립니다.
  - 이때 온라인 실험을 대규모로 실핼할 때는 Sensitivity 를 늘리는것이 매우 중요합니다.
  - 왜냐하면 성숙한 온라인 실험플랫폼은 연간 수천개의 실험을 진행하게 되고 ,  즉 Sensitivity 를 조금만 상승시키더라도, 규모의 경제에 대해서 이익이 엄청 커지기 때문입니다.

- 이떄 온라인 실험은 이미 매우 큰 표본 크기를 가지는 경향이 있고, 표본 크기를 늘리는것이 일반적으로 Power 를 향상시키는 매우 간단한 방법이기 때문에, 민감도를 강조할 필요가 없어 보일 수 있습니다.
- 하지만 현실에서는 많은 양의 트래픽이 있더라도, online 실험은 우리가 원하는 Statistical power 에 도달하지 못하는 경우가 있습니다. 
- 구글에서는 매달 100억건 이상의 검색을 수행하는데에도, 그들이 가진 트래픽 양에 만족하지 않는다고 합니다.
- 이렇게 늘 Sample 의 수에 허덕이는 이유는 다음과 같습니다.

> ## Sample is not enough

> 이유 1

- 우리가 탐지하고자 하는 Treatment 효과는 매우 작은 경향이 있다.
- 통제된 실험의 민감도는 제곱된 사용자 수에 반비례하므로, 작은 사이트에서 5% 의 delta 를 감지하려면 10000명의 사용자가 필요할 수 있습니다. 
  - 이때에 0.5% 의 delta 를 감지하려면 100만명의 사용자가 필요하게 됩니다. 
- 사용자당 0.5% 의 수익 변화만으로도 대형 온라인 사이트의 경우 수백만 달러에 해당한다는것을 기억하세요! 

> 이유 2. 

- 결과를 빨리 얻는것이 중요하다는 것입니다. 
  - 좋은 기능을 조기에 출시하고 싶을 수 있기 떄문입니다.
  - 또 더욱 중요한 이유는 Treatment 가 사용자에게 안좋은 영향을 미칠때 빨리 중단해야 한다는 것입니다.

> 이유3

- 낮은 Triggering rate 를 가진 실험이 있을때, 이러한 실험은 매우 적은 유저만이 실제로 Treatment 효과를 경험하게 됩니다.
- 예를 들어서 레시키 관련 쿼리에만 영향을 미치는 실험에서 대부분의 사람들은 레시피를 검색하지 않기 때문에 Variant 를 경험하지 않습니다.
- 즉 이러한 경우 유효한 표본 크기는 작을 수 있으며, 통계 분석의 Statistical Power 는 매우 낮을 수 있습니다.

> 이유 4

- 마지막으로 데이터 중심 문화에서는 혁신 속도에 맞추기 위하여 더 많은 실험을 항상 실험해야 하고, 이는 좋은 온라인 플랫폼의 경우 항상 샘플 사이즈 부족에 허덕일수밖에 없다는 의미입니다. 

> ## Variance Reduction

- 민감도를 개선하는 방식중에 하나는 분산 감소를 통해서 가능합니다. 
  - Kohavi et al. (2009b) 는 다른 평가 메트릭을 사용하거나, Treatment 의 영향을 받지 않는 사용자를 걸러냄으로서 더 낮은 분산을 달성할 수 있는 예시를 제공합니다. 
- Deng 등(2011) 은 페이지 수준 메트릭의 분산을 줄이기 위해서, 설계 단계에서 페이지 수준의 무작위화를 사용하는 방법을 제시합니다. 
  - 하지만 이러한 방법은 매우 특수한 경우에만 적용할 수 있습니다.
- 또한 기업은 쉽게 변경할 수 없는 핵심지표 (KPI) 를 가지기 때문에, 실제로 모든 메트릭에 적용할 수 있는 기술을 원합니다. (예를 들어서 인당 수익을 최대화 하고 싶은 기업의 경우 페이지 기준으로 계산하기 어렵습니다.)
- 또한 모델 가정이 신뢰할 수 없는 경향이 있고 한 메트릭에 대해 작동하는 모델이 다른 메트릭에 반드시 적용되는 것은 아니기 때문에 이 기법은 가급적 파라메트릭 모델에 기반해서는 안 된다.

> ## CUPED

- 이 논문에서 우리는 CUPED (사전 실험 데이터를 사용하여 제어된 실험) 이라는 기술을 제안합니다. 이 기술은 Control 및 Treatment 의 사용자를 위해 사전 실험 데이터를 사용해 메트릭을 조정하여서 메트릭의 변동성을 줄입니다. 
- 이러한 CUPED 방법론의 이점은 다음과 같습니다.
  - 사전 실험 데이터를 사용해 온라인 실험에 대한 분산을 줄이기 위한 방법으로서 실험의 Sensitivity 를 크게 높힐 수 있음
  - Non-user metric 애 대한 확장된 접근과 Partially Missing pre experiment data 에 대한 새로운 접근법 
  - 사전 실험에서 동일한 메트릭을 사용하면 일반적으로 가장 큰 분산 감소를 할 수 있다는 Emprical Result와 최적의 공변량을 선택하는 기준 제시
  - Bing에서 실행되는 실제 온라인 실험에 대한 결과의 검증은 약 50%의 분산 감소를 보여주며, 이는 트래픽을 두 배로 늘리거나 동일한 민감도를 얻기 위해 실험을 실행해야 하는 시간을 절반으로 줄이는 것과 같습니다.
  - pre experiment 를 사용할 경우 , 기간을 설정해야 되는데 이때 기간에 사용할 수 있는 최상의 길이를 결정하는 방법, 다수의 공변량 사용과 같은 방법론을 소개. 하고 성공적인 CUPED 방법론에 대해서 논의합니다.

# [2.Backgound and Related Workd](#link){: .btn .btn--primary}{: .align-center}

> ## 2.1 Analyzing Experiment

- 광범위한 적용 가능성 덕분에 우리의 논의는 2-표본 t-검정의 경우에 초점을 맞춘다(Student 1908; Wasserman 2003). 이 방법론은 온라인 실험 분석에서 가장 일반적으로 사용되는 프레임워크입니다. 
- 메트릭 Y(예: 사용자당 쿼리)에 관심이 있다고 가정합시다. 이때 t-test를 적용하기 위해, 우리는 Control 과 Treatment에 있는 사용자에 대해 관찰된 메트릭 값은 랜덤 변수 $Y^{(t)} $ 와 $Y^{(c)}$ 의 independent 한 realization 이라고 가정합니다.  
- 귀무 가설($H_0 $)은 $\mu_{Y^{(t)}} = \mu_{Y^{(c)}}$ 이라고 설정합니다. 대립가설은 $\mu_{Y^{(t)}} \not= \mu_{Y^{(c)}}$  이 됩니다. 이때 t-test 는 아래와 같은 통계량을 Based 로 실험이 진행됩니다.

$$\frac{\bar{Y}^{(t)}-\bar{Y}^{(c)}}{\sqrt{\operatorname{var}\left(\bar{Y}^{(t)}-\bar{Y}^{(c)}\right)}}$$

- 이때 $$\Delta=\bar{Y}^{(t)}-\bar{Y}^{(c)}$$ 는 평균의 이동 (Shift ) 에 대한 Unbiased Estimator 입니다. 
  - 그리고 t-Statistic 은 위, 평균의 이동(차이라고도 함) 에 대해 정규화된 버젼이라고 생각할 수 있습니니다. 

- t-test 의 경우 Y가 Normal 분포여야 한다는 가정이 필요합니다만, Online Experiment 의 경우 Sample 의 크기는 최소한 수천 단위 이므로 중심극한정리 덕분에 Y 에 대한 정규성 가정은 크게 필요하지 않습니다.

> Variance 

- 이때 샘플은 independent 이므로 $\Delta$ 에 대한 분산은 아래와 같이 계산됩니다.

$$\operatorname{var}(\Delta)=\operatorname{var}\left(\bar{Y}^{(t)}-\bar{Y}^{(c)}\right)=\operatorname{var}\left(\bar{Y}^{(t)}\right)+\operatorname{var}\left(\bar{Y}^{(c)}\right)$$

- 이 프레임워크에의 핵심은 평균 자체의 분산을 줄이는 데 있습니다. 
  - 섹션 3에서 볼 것처럼, 이것은 우리의 문제를 분산 감소를 통한 평균의 추정을 개선하기 위해 몬테카를로 샘플링에 사용되는 기술과 연결합니다.
- 매우 높은 Level에서 분산 감소에 대한 제안은 다음과 같습니다. 
  - 우리는 평소처럼 실험을 진행하지만 데이터를 분석할 때  $\Delta$ 를 사용하는게 아니라 수정된 델타 추정치 ($\Delta^{*}$) 를 계산합니다.

-  조정된 추정치 ∆∗는 다음과 같은 좋은 성질을 지닙니다.
  - $\Delta^{*}$ 는 여전히 Shift in mean 에 대한 Unbiased estimator 가 됩니다. ( $\Delta$ 도 Shift mean 에 대한 Unbiased mean 이라는것을 기억하세요! ) 
  - $\Delta^{*}$ 는 $\Delta$ 보다 적은 Variance를 가진다.
- 즉 정리하면 CUPED 를 적용한 조정된 추정치 ∆∗는 Unbiased Estimator 인데 Variance 까지 낮으니 매우 좋은 추정량이라고 할 수 있죠!

> ## 2.2 Linear model

- 분산 감소는 랜덤화된 실험을 분석하는데에 있어서 매우 오래된 과제였습니다. 
- 이 경우 가장 인기 있는 모수적 방법은 선형 모델링을 기반으로 합니다(Gelman and Hill 2006). 실험에 대한 선형 모형에서는 결과가 Covariates 항과 결합된 Treatment 효과의 선형 조합이라고 가정합니다.
  - $Y_i$  를 metric 의 outcome 이라고 합시다.
  - $Z_i$ 를 Treatment Assignment indicator 라고 합시다. 
  - $X_i$ 는 vector of covariates 라고 합시다. linear model 은 다음과 같은 사실을 가정합니다.


$$\mathbb{E}\left(Y_{i} \mid Z_{i}, \mathbf{X}_{i}\right)=\theta_{0}+\delta Z_{i}+\boldsymbol{\theta}^{T} \mathbf{X}_{i}$$

- 모형의 가정 하에서 선형 회귀 분석(공변량이 범주형 변수인 경우 ANCOVA라고도 함)은 평균 Treatment 효과에 대해 일관된 추정치를 제공하고 분산을 줄입니다. 

> Note : ANCOVA

- ANCOVA 는 독립변수가 종속변수에 어떻게 작용하는지를 살펴볼 수 있게 한다. ANCOVA 는 여러분이 살펴보고자 하는 변수가 아닌 **공변량의 영향을 모두 제거한다**. 예를 들어, 여러분이 교수 능력의 수준이 수학 과목에 있어서 학생의 학습 능력에 끼치는 영향에 대해 알아보고 싶어한다고 하자; 이러한 경우 학생들을 임의로 교실에 배정할 수 없을 수도 있다. 그렇다면 여러분은 다른 교실에 있는 학생들 사이에 계통적인 차이를 고려해야만 한다(예를 들어, 똑똑한 학생과 일반적인 학생 사이에 존재하는 수학 실력의 차이)
- Assumption 

1. **독립변수(최소 2개) 는 범주형이어야 한다**.
2. **종속변수와 공변량은 연속형이어야한다**(등간척도 또는 비율척도).
3. **공변량과 종속변수는** (**모든 수준**의 독립변수에서) **선형적으로 연관** 되어야 한다.
4. 자료는 각각의 독립변수 값에 대해 종속변수는 **등분산성** 을 가져야 한다.
5. **공변량과 독립변수는 교호작용이 없어야 한다**. 다른 말로 하자면, 회귀계수에 동차성(homogeneity) 을 만족해야 한다.

> Limitation

- 그러나 선형 모델은 일반적으로 모든 residual 은 동일하다는 가정을 하게 됩니다.
  - 또한 treatment 의 효와에 대해서 metric 의 효과는 선형적이라는 가정을 하게됩니다. 

- 선형 모델의 한계를 극복하기 위해 연구자들은 준모수 모델(Tsiatis 2006)이라고 불리는 덜 제한적인 모델을 개발했는데, 이 모델에 일반화된 추정 방정식(GE)이 사용됩니다. 
- 표준 선형 모델을 준모수 모델과 비교한 양(Yang)과 치아티스(Tsiatis)(2001)는 선형 모델(ANCOVA)과 GE가 덜 제한적인 준모수 모델에서 점근적으로 동일하고 둘 다 조정되지 않은 t-검정보다 평균 처리 효과에 대해 더 효율적인 추정치를 제공한다는 것을 보여주었다. 
- 레온 외. (2003년), 다비디안 외 연구진. (2005) 과 치아티스 외 연구진. (2008)은 준모수 통계 이론(Tsiatis 2006)을 사용하여 작업을 더욱 개선하고 평균 치료 효과에 대한 추정기 클래스의 분석 형태를 제공했다. 
  - 이 클래스는 평균 처리 효과에 대해 가능한 모든 RAL(정규 및 점근 선형) 추정기가 클래스 내 하나와 점근적으로 동일하다는 점에서 완전하다. 남은 문제는 학급에서 분산이 가장 작은 추정기를 찾는 것이고 그들은 일반적인 지침을 제공했습니다.

- 이 논문에서 우리는 문제를 다른 관점에서 바라봅니다. 무작위 실험의 분산 감소 문제를 몬테카를로 시뮬레이션의 유사한 문제와 연결함으로써 매우 강력한 결과를 도출할 수 있다. 
- 추상적 힐베르트 공간과 기능적 영향 곡선으로 다이빙하는 대신, 우리의 주장은 기본적인 확률만 포함한다. 특히 메트릭 변동성을 줄이기 위해 사전 실험 기간의 데이터를 사용할 것을 제안하며, 이는 매우 효과적이고 실제로 적용할 수 있는 것으로 밝혀졌다.

# [3.Variance Reduction](#link){: .btn .btn--primary}{: .align-center}

> ## 3.0 Variance reduction

- 분산 감소는 몬테카를로 샘플링의 일반적인 주제이며, 여기서 목표는 일반적으로 기본 분포에서 가능한 값을 반복적으로 시뮬레이션하여 매개 변수를 추정하는 것입니다.
  - 이때 몬테카를로 샘플링에서 사전 정보를 통합하여 분산을 줄이는 샘플링 체계를 사용하면 상당한 효율성 이득을 얻을 수 있다.
- 하지만 안정된 population 에서 샘플릉 진행하는 몬테카를로 시뮬레이션과 달리 온라인 실험의 세계에서는 모집단이 역동적이고 실험이 진행됨에 따라 데이터가 점진적으로 도착하게 됩니다. 
  - 이런 온라인 세계에서는 미리 샘플링 계획을 설계하고 그에 따라 데이터를 수집할 수 없습니다. 

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

- 온라인 세계에서는 시간이 지남에 따라 데이터를 수집하기 때문에 일반적으로 미리 형성된 계층에서 샘플을 추출할 수 없습니다. 
  - 하지만 우리는 데이터가 모인 후에 계층을 만드는것이 아니라, 우리는 모든 데이터가 수집된 후에도 계층을 구성할 수 있습니다. (for theoretical justification see Asmussen and Glynn (2008, Page 153)).

- 예를 들어, $Y_i$ 가 사용자 i에 대한 쿼리 수라면, 공변량 $X_i$는 사용자가 실험을 시작하기 전에 사용한 브라우저가 될 수 있습니다. 
  - 그리고 이 변수에 대해서 Stratify 를 진행한 뒤, 아래처럼   계층화 평균을 계산할 수 있습니다.


$$\widehat{Y}_{\text {strat }}=\sum_{k=1}^{K} w_{k} \bar{Y}_{k}=\sum_{k=1}^{K} w_{k}\left(\frac{1}{n_{k}} \sum_{i: X_{i}=k} Y_{i}\right)$$

- 이떄 Treatment 와 Control 을 표시하기 위하여 아래처럼 위첨자를 사용해 보았습니다. (t 는 Treatment , c 는 contol )

$$\Delta_{s t r a t}=\widehat{Y}_{s t r a t}^{(t)}-\widehat{Y}_{s t r a t}^{(c)}=\sum_{k=1}^{K} w_{k}\left(\bar{Y}_{k}^{(t)}-\bar{Y}_{k}^{(c)}\right)$$

- 위와 같이 차이에 대한 추정량은 계층화 평균을 사용하였으므로 , 동일한 로직으로 분산이 감소될 수 있습니다.
- 이떄 우리는 오로지 pre-experiment information 을 사용했다는것이 주목해야 합니다. 이렇게 하면 우리는 애초에 미리 실험한 정보만을 사용했으므로, 층화에 사용한 변수 $X_i$ 는 실험의 효과를 Peeking 하지 않았습니다. 즉 아는 $\Delta_{Strat}$ 는 가 Unbised 임을 보장합니다.
- 이떄 하나 더 고려할 점은 우리가 사용할 적절한 가중치 $w_k$ 를 항상 알고있지 않다는 사실입니다.
  - Online Experimental 맥락에서 이 값은 일반적으로, 실험에 포함되지 않은 사용자로부터 계산될 수 있습니다.


> ## 3.3 Control Variates

- 우리는 온라인 실험이 시뮬레이션 에서에서 널리 사용되는 계층화 기법의 이점을 어떻게 얻을 수 있는지 보여주었습니다.
- 이 섹션에서는 Control Variates이라고 하는 시뮬레이션에 사용되는 또 다른 분산 감소 기술이 온라인 실험에서 어떻게 활용될 수 있는지를 보여주려고 합니다.

> ## 3.4 Control Variates in Simulation

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

> ## 3.2.2 Control Variates in Online Experimentation

- 이전과 같이 분산을 줄이기 위해서 Control Variates 를 활용하는 방법론은 매우 일반적인 방법입니다.
  - 하지만 이것을 적용할때 어려운점중 하나는, Y 와 높은 상관관계가 있는 Control Variates $X$ 를 찾는것과 , $E(X)$를 찾는것입니다. 

- 이떄 $\mathbb{E}\left(X^{(t)}\right)$ and $\mathbb{E}\left(X^{(c)}\right)$ 를 알고있는 Control Variates $X$ 를 찾는것은 매우 어렵습니다.
  - 하지만 이때 중요하게 생각해야될 점은 pre-experiment 단계에서  $\mathbb{E}\left(X^{(t)}\right)-\mathbb{E}\left(X^{(c)}\right)=0$ 를 가지는 $X$ 를 찾는것은 크게 어렵지 않다는 사실입니다. 
- 우리는 Pre-experiments 단계에서의 정보만을 이용했으므로, 혹시나 결과를 봐서 생기는 편향을 예방할 수 있을 것입니다.
- Given  $\mathbb{E} X^{(t)}-\mathbb{E} X^{(c)}=0$ 라고 합시다. 그러면 쉽게 $$\Delta_{c v}=\widehat{Y}_{c v}^{(t)}-\widehat{Y}_{c v}^{(c)}$$ 는 $\delta=\mathbb{E}(\Delta)$ 에 대한 Unbiased Estimator 라는것을 알 수 있습니다.
  - $$\widehat{Y}^{(t)}_{c v}=\bar{Y}^{(t)}-\theta \bar{X}^{(t)}+\theta \mathbb{E} X^{(t)},$$
- 이떄 $\Delta_{c v}$ 는 $\mathbb{E}\left(X^{(t)}\right)$ 와 $\mathbb{E}\left(X^{(c)}\right)$ 의 값은 서로 상쇄되므로 depend 하지 않는다는것을 기억합시다.

- $\theta$ 에 대해서 Optimal Choice 를 하게 된다면 ($\theta=\operatorname{cov}(Y, X) / \operatorname{var}(X)$)  $\Delta_{c v}$ 는 아래와 같이 Variance 가 줄어들게 됩니다.

$$\operatorname{var}\left(\Delta_{c v}\right)=\operatorname{var}(\Delta)\left(1-\rho^{2}\right)$$

- 큰 상관관계를 얻고 분산 감소 최대화 하기 위하여 가장 분명한 접근 방식은 $X$를 $Y$와 동일하게 선택하는 것립니다.
  - 이는 자연스럽게 사전 실험 관찰 윈도우 동안 동일한 변수를 Control Variant 로서 사용하게 된다. 
  - 섹션 5의 경험적 결과에서 볼 수 있듯이, 이것은 실제로 Control Variant 방법론으로서 가장 효과적인 방법론으로 알려져 있습니다. 
- 하지만 여기에서는 살짝 지적할점이 있습니다. The pair $(Y, X)$ 는 Treatment 효과가 있을때 약간 Dsitribution 이 달라질 수 있습니다.  $\Delta_{c v}$ 가 Unbiased 이려면 Treatment 와 Control 모두에 대해서 같은 $\theta$ 를 사용해야 합니다. 
- 이를 추정하는 가장 쉬운 방법은 control 과 treatment 에 대한 Pooled population 으로부터 추정하는 것입니다. 
- variance reduction 에 대한 효과는 매우 미미할 수 있습니다. 우리는 general nonlinear control covariates Case 의 경우 우리는 same functional form in both $\widehat{Y}_{c v}^{(t)}$ and $\widehat{Y}_{c v}^{(c)}$ 가 되어야 합니다. 

> ## 3.3 Connection between Stratification and Control Variates

- 우리는 분산 감소를 달성하기 위해 Covariates 를 활용하는 두 가지 기술에 대해 논의했습니다. 
  - stratification 접근법은 Covariates을 사용하여 strata을 구성하고 Control Covariates 접근법은 회귀 변수로 사용한다. 

- stratification는 이산형(또는 이산형) 공변량을 사용하는 반면, Control Covariates는 연속형 변수로 더 자연스럽게 보입니다. 
- 그러나 이 두 가지 접근법이 밀접하게 관련되어 있다는 것은 놀라운 일이 아닙니다. 
  - 실제로 공변량 X가 범주형일 때(예: 이산형 값 1, . . . , K) 두 접근법이 동일한 추정치를 생성한다는 것을 보여 줄 수 있습니다. 

- 자세한 내용은 부록 A에 포함되어 있습니다. 기본 아이디어는 각 stratum 에 대해 지시 변수 $1_{X=k}$ 를 구성하고 평균이 stratum Weight 인 $w_k$인 관리 변수로 사용하는 것입니다. 이를 위해 제어 변동 기법은 연속 공변량과 이산 공변량이 모두 적용되는 계층화의 확장이다.
- 이 두 기술은 수학적으로 잘 연결되어 있지만, 분산 감소를 달성하는 이유와 방법을 이해하는 데 다른 통찰력을 제공한다.
- 층화는 성분 분포에 따라 표본을 분리하여 성분 간 분산을 효과적으로 제거하고 분산을 줄이는 것과 같습니다.
  - 따라서 표본을 더 잘 분류하고 기본 구조와 정렬할 수 있는 공변량이 더 좋습니다. 

- 반면에, 관리 변동 공식은 공변량과 변수 자체의 상관 관계에 대한 함수로 분산 감소의 양을 정량화합니다. 그것은 수학적으로 더 간단하고 우아하다. 공변량이 높을수록 상관 관계가 더 커야 합니다.

> ## 4. CUPED IN PRACTICE

- CUPED를 구현하는 간단하지만 효과적인 방법은 사전 실험 기간의 동일한 변수를 공변량과 함께 사용하는 것이다. 
  - 실제로, 이것이 빙의 실험 시스템을 위해 우리가 실제로 구현한 것입니다. 

- 하지만 이것이 불가능하거나 실용적이지 않은 상황이 있습니다. 
  - 예를 들어 사용자 유지율을 측정하거나 새로운 사용자를 대상으로 실험을 수행하려는 경우 작업할 사전 실험 데이터가 없습니다. 
  - 사실, 대부분의 온라인 실험에서 우리는 모든 사용자에 대한 사전 실험 정보를 가지고 있지 않을 수 있습니다. 분석 단위가 사용자가 아닌 메트릭에 대해 사전 실험 데이터를 어떻게 사용하는지도 추가적인 과제입니다. 

- 이 섹션은 빙의 실험 시스템을 사례 연구로 사용하여 이와 같은 실제 과제를 해결하는 데 전념한다.

> ## 4.1 Selecting Covariates

- 공변량의 선택은 분산 감소의 효과를 직접 결정하기 때문에 매우 중요합니다. 
- 올바른 변수를 선택하면 분산을 절반으로 줄일 수 있지만 잘못된 선택을 하면 분산을 거의 줄일 수 없습니다. 
- 어떤 사전 실험 변수가 가장 잘 작동하는지 이해하기 위해 가능한 사전 실험 변수를 많이 평가했다. 
- 큰 Class의 메트릭에 걸쳐, 우리의 결과는 공변량과 동일한 변수를 사용하는 것이 최상의 분산 감소를 제공하는 경향이 있다는 것을 일관되게 보여주었다. 
- 여기에 프리엑스피먼트의 길이와 실험 기간도 작용하게 됩니다. 
  - 실험 전 기간이 동일하다고 해서 실험의 길이를 늘린다고 해서 분산 감소율이 반드시 개선되는 것은 아닙니다. 
  - 반면에, 더 긴 사전 기간은 동일한 실험 기간에 대해 더 높은 감소를 제공하는 경향이 있습니다. 우리는 섹션 5의 경험적 사례의 맥락에서 더 많은 세부 사항을 논의한다.


> ## 4.2 handling missing

-  온라인 사이트에서는 실험의 모든 사용자에 대한 사전 실험 데이터가 없을 수 있습니다. 일부 사용자가 처음 방문하거나 사전 실험 기간에 나타날 정도로 사이트를 자주 방문하지 않기 때문에 발생할 수 있다. 
- 또한 사용자는 신뢰할 수 없고 "바꿀" 수 있는 쿠키로 식별되는 경우도 있습니다. (즉, 사용자가 쿠키를 삭제하여 변경됨). 
-  이것은 공변량을 구성하기 위해 사전 실험 정보를 사용하는 데 어려움을 제기한다.
   -  실험 중이지만 사전 실험 기간에 있지 않은 사용자의 경우 해당 공변량이 잘 정의되어 있지 않습니다. 

-  이를 해결하는 한 가지 방법은 사전 실험 기간에 사용자가 나타났는지 여부를 나타내는 또 다른 공변량을 정의하는 것이다. 
   -  이 추가 이항 공변량을 사용하여 결측 공변량 값을 원하는 상수로 설정할 수 있습니다. 

-  직관적으로 이것은 먼저 사용자를 실험 전 기간에 나타난 계층과 그렇지 않은 계층으로 나누는 것과 같습니다. 
   -  사전 실험 데이터를 가진 사용자 계층의 경우 사전 실험 공변량이 잘 정의되어 있으므로 이러한 공변량을 기반으로 한 추가적인 분산 감소가 가능하다. 
   -  또한, 이전 기간의 존재에 의한 계층화는 분산 감소의 추가적인 원천이다.


> ## 4.3 Beyond Pre-Experiment Data

- 지금까지 우리는 사전 실험 데이터를 사용하여 구성된 공변량을 기반으로 메트릭 변동성을 줄이는 것만 고려했습니다.
  - 사전 기간의 동일한 변수를 사용하면 분산 감소 효과가 가장 잘 나타날 뿐만 아니라 사전 실험 정보가 실험의 효과와 무관하게 보장돼 편향된 결과를 피하는데 매우 중요하기 때입니다.
- 이것을 수학적으로 증명하는 것은 아마도 제어 변형 제형으로 증명하는 것이 더 쉬울 것이다. 

$$\Delta_{c v}=\widehat{Y}_{c v}^{(t)}-\widehat{Y}_{c v}^{(c)}$$

$\Delta_{c v}$ is computed assuming $\mathbb{E}\left(X^{(t)}\right)=\mathbb{E}\left(X^{(c)}\right)$. 

- If there is truly a difference between control and treatment in terms of $X$ and this equality does not hold, $\Delta_{c v}$ will be biased. 
- 예를 들어, 페이지 로드 시간이 빠르면 일반적으로 검색 페이지를 더 많이 클릭하게 됩니다(Kohavi 등). 2009b). 
- 페이지 로드 시간을 개선하는 실험에서 클릭 수를 공변량으로 사용하는 경우, 개선의 일부가 공변량에 의해 "조정"되기 때문에 로드 시간에 대한 실험의 영향을 과소평가하게 됩니다. 
  - 여기에 설명된 요건을 위반하는 공변량을 사용함으로써 발생하는 편향 결과의 실제 예는 섹션 5를 참조하세요

- 그러나 이것이 프리엑스피먼트 데이터를 기반으로 한 공변량만이 유일한 선택이라는 것을 의미하지는 않습니다. 
  - 필요한 것은 공변량 X가 실험의 처리의 영향을 받지 않는 것입니다. 
- 자연적 확장은 사용자가 실험에 처음 나타날 때 수집된 정보를 사용하여 구성된 공변량의 종류입니다.
  - 예를 들어, 사용자가 실험에서 처음 관찰되는 요일은 실험 자체와 무관하다. 
  - 이러한 공변량은 분산 감소를 위한 강력한 추가 원인으로 작용할 수 있습니다. 
  - 이 아이디어를 더욱 확장하기 위해 사용자가 실제로 실험 기능을 트리거하기 전에 설정된 정보를 기반으로 한 공변량도 유효하다. 이 기능은 평가할 형상의 트리거 속도가 낮은 경우에 특히 유용할 수 있습니다.

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
- 다음으로 우리는 Treatment가 대조군과 동일하여 치료 효과가 0인 것으로 알려진 통제된 실험인 3주 A/A 테스트를 더 자세히 살펴본다. A/A 실험을 사용하여 실제 온라인 실험의 분산 감소 성공에 큰 영향을 미칠 수 있는 중요한 결정을 검토할 수 있다. 
- 마지막으로, 사용자 트리거링을 지나 실험에 부적절하게 공변량을 선택할 경우 편향된 추정치가 어떻게 발생하는지 보여준다.

> ## 5.1 Slowdown Wxperiment in bing

- 실제 실험에서 CUPED의 영향을 보여주기 위해 페이지 로드 시간과 사용자 참여 사이의 관계를 Bing에 테스트한 실험을 조사한다. 
- 수백 밀리초 정도의 지연은 사용자 참여를 손상시키는 것으로 알려져 있습니다((Kohavi et al. 2009b, Section 6.1.2)
- 이 실험에서는 Bing 쿼리에 대한 서버 응답을 의도적으로 250밀리초 지연시켰습니다. 
- 실험은 처음에 Bing 사용자 중 작은 부분을 대상으로 2주 동안 실행되었으며, 통계적으로 유의한 클릭률(CTR)에 대한 영향을 관찰했습니다.
- 이 경우에 p-값이 임계값 0.05보다 약간 낮았다. 이 메트릭에 대한 Treatment Effect가 False Positive 가 아닌 실제라는 것을 확인하기 위해, 우리는 더 큰 큰 실험을 진행했고 이것은 실제로 p-값 2e-13으로 실제 효과임을 확인할 수 있었습니다.

> Apply Cuped Methods

- 공변량으로 2주 전 기간부터 CTR을 사용하여 CUPED를 적용하였습니다.
- 결과는 인상적입니다: 델타 수치는 첫날부터 통계적으로 유의했습니다! 

![png](/assets/images/Stat/124_1.png)

- 위 그림은 시간 경과에 따른 p-값을 로그 척도로 보여줍니다. 검은색 수평선은 0.05 유의 막대입니다. 

> Interpret

- Cuped 를 적용하지 않은 실험에서 (빨간색 막대) t -test는 서서히 낮아지고 실험이 2주 만에 중단될 때쯤 되어서야 간신히 p-value 가 임계점 0.05 보다 낮아졌습니다.
- 하지만 같은 실험에 대해서 CUPED를 적용하면 전체 p-값 곡선이 막대 아래에 있습니다.
- 그림의 하단 그림은 CUPED가 사용자의 절반만 대상으로 실행될 때의 p-값 곡선을 비교합니다. CUPED는 사용자 절반이 실험에 노출되어도 더 민감한 테스트가 진행되고 있음을 알 수 있습니다.
- 실험 대부분이 사용자의 Experience 에 부정적이나 아무 영향도 미치지 않는다는 사실(Kohavi et al. 2009a; Manzi 2012) 에 비추어볼때, 우리는 위와 같이 같은 샘플을 이용하였더라도 기존의 실험보다 더  Statistical Power 가 높은 실험을 진행하는것은 CUPED 의 이점입니다.
- 위 실험뿐만 아니라 다른 실험을 수행하였을떄에도 CUPED 방법론은 비슷한 수준의 Statistical Power 상승 효과를 얻을 수 있었습니다.

> ##  5.2 Factors Affecting CUPED Effectiveness

- 이 섹션에서는 실제로 CUPED를 사용하는 데 큰 영향을 미칠 수 있는 요소를 살펴봅니다. 여기서 사용하는 데이터는 3주간의 A/A 실험에서 얻은 데이터입니다.

![png](/assets/images/Stat/124_2.png)

- 위 그림은 queries-per-user 라는 metric 에 대한 CUPED의 분산 감소율을 보여줍니다. 이때 공변량 (Covariates) 는 아래와 같이 2가지가 고려됩니다. 
  - (1) 사용자가 실험에 처음 나타나는 날을 나타내는 범주형 변수인 엔트리-데이
  - (2) 실험 전 1주 동안의 사용자당 쿼리-변수
-  엔트리-데이는 사전 실험 데이터는 아니지만, 치료 방법이 실험 중 사용자가 처음 오는 시간에 영향을 미치지 않기 때문에 4.3절에서 요구하는 조건을 만족한다.

> ## 

**reference**

- <http://rinterested.github.io/statistics/chi_square_same_as_z_test.html>
- https://bytepawn.com/reducing-variance-in-ab-testing-with-cuped.html



