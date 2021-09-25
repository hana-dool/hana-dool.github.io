---
title:  "Bayesian Statistic and Conjugate"
excerpt: "베이지안 통계 개요와 Conjugate"
categories:
  - Bayes
last_modified_at: 2021-03-14

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 통계를 하게되면 확률에 대한 두가지 관점인 베이지안과 Frequentist 두가지 관점에 대해서 배우게 됩니다. 두개의 차이에 대해서 짧게 알아보도록 합니다. 
{: .notice--warning}

# [Overview of Two main Tasks of Statistics](#link){: .btn .btn--primary}{: .align-center}

> ## Inference and Prediction

![png](/assets/images/Stat/65_1.png)

> Basic Setting and Terms

- Freauentist 에서는 모집단의 특성을 수치로 나타낸 모수 $\theta$ 를 Constant 라고 가정합니다.
- 데이터 $x_1...x_n$ 을 모으고 각각은 iid 라고 가정합니다. 
- 또한 Statistic(통계량) T 를 정합니다. 이러한 통계량은 Median , Mean 등이 될 수 있습니다. 
  - 통계량이 '추정' 목적이면 (즉 우리가 관심있는 대상 그 자체) Estimator 이라 합니다.
  - 통계량이 'Test' 가 목적이면 Test statistic 이라고 합니다.
- Sampling distribution 은 $T$ 의 분포가 됩니다. 

> Two main tasks of Statistics 

- Inference : 데이터를 이용하여 모델을 생성한 뒤에 $\theta$ 에 대한 추론
  - 설명 가능성이 매우 중요. (parameter 에 대한 추론을 한다는것은 데이터를 설명한다는 것과 같기 떄문에)
  - parameter 를 100개씩 두고 inference 를 하게 된다면, 각각의 $\theta$ 에 대한 해석은 모호해질수밖에 없음
- Prediction : 데이터를 사용하여 모델 생성 후, 새로운 $x_{new}$ 에 대한 추론

> ## Frequentsis and Bayesian View 

![png](/assets/images/Stat/65_2.png)

> Frequentist 의 View

- 데이터를 압축해 설명하는 Parameter 는 constant 라고 가정 (scalr or vector)
- 데이터로부터 , Estimator 를 만듭니다. 
  - 이 경우 주로 CLT 기반의 Limiting Distribution 을 활용
- inference 는 Estimation 과 Testing 두가지로 나뉩니다.
  - Estimation : 95% CI 를 형성합니다. (신뢰구간 = 고정된 parameter 를 커버할 확률이 95%)
  - Hypothesis Test : Parameter space 를 $H_0, H_1$ 둘로 양분한뒤 $H_0$ 이 맞다는 가정 하에서 Test statistic 의 분포를 구함. 그 이후 이 분포가 $H_1$ 쪽으로 얼마나 극단적인 방향인지 비교 
- prediction 은 기본적으로 $x_{new} \sim f(x,\hat{\theta})$ 라고 가정한 이후에, $x_{new}$ 를 추정  

> Bayesian 의 View

- 데이터를 설명하는 parameter $\theta$ 자체를 Random Variable 이라고 생각함 
- 이러한 $\theta$ 에 대해너 Prior 를 정하고, 이 Prior 는 데이터를 만나 posterior 로 업데이트됨
- Inference 는 그냥 'Posterior Distribution' 을 이용
- predict 의 경우에는 Prediction Predictive distribution 을 활용합니다.

# [Bayesian Statistics](#link){: .btn .btn--primary}{: .align-center}

> ## Belief and Bayes Theorem

![png](/assets/images/Stat/65_4.png)

- 베이즈에서는 주관적 믿음을 확률로 표현합니다.
  - 이러한 주관적 믿음을 확률로 쓸 수 있을까요? 
  - 믿음에 기대하는 속성과, probability 의 Axiom 과 겹친다는 것을 보여서 정당성을 확보합니다. 
- Bayesian Theorem 은 위 그림에서 보다시피 Partition 과 Rule of Total Probabiity 에 의해 성립합니다. 

> ## Bayesian Statistics Framework

![png](/assets/images/Stat/65_5.png)

- 우리의 믿음을 Prior $P(\theta)$ 로 표현합니다. 
- 그 이후에 데이터를 iid 샘플이라고 가정하였으므로 , 이로부터 Likelihood 를 구해냅니다. 
- 위 두 정보를 이용하여 Posterior 분포를 구해냅니다.
  - 분모는 Normalizing Constant 로 여긴 상태에서 계산될 수 있습니다. ($\theta$ 에 의해 적분되므로)

> inference

- inference 는 Posterior distribution 으로 바로 가능하다. 
  - Confidence Interval 을 대신할 Credible interval 을 정의. 이 구간은, $\theta$ 가 구간에 속할 확률이 95% 이 된다. (Frequantist 와의 차이를 알아두자!)
  - Hypothesis Test 는 그냥 Posterior 만 보고 알 수 있음. $P(\theta<0 \mid Data)$ 의 확률을 이용하여 $\theta<0$ 의 테스트를 직접 검정할 수 있음

> Prediction

- Prior predictive 라는것은 데이터를 모으기 전에 얻을 수 있는 분포 
  -  $p(x_{new,prior})= \int_\theta p(x_{new}\mid \theta)p(\theta)d\theta$ 
  - $p(x_{new}\mid \theta)$ 를 모든 $\theta$ 를 고려할때에 가중치로 평쥰을 냄. 즉 $p(\theta)$ 가 가중치인 Weighted mean 이라 볼 수 있음
  - 데이터를 보기 전에도, 믿음만 가지고도 데이터에 대한 분포를 어느정도 형성할 수 있음
- Posterior predicive 는 Data 가 given 했을떄의 확률
  - $p(x_{new,post}\mid data) = \int_\theta p(x_{new}\mid \theta)p(\theta \mid data)d\theta$
  - 이 경우에는 $p(\theta\mid data)$ 를 가중치로 둔 weighted mean 이라 볼 수있음

> Example 

- 시행횟수가 10인 이항분포를 따르는 확률 변수 X가 있다. 이항분포의 모수가 균일분포을 따를 때, 확률 변수 X의 사전예측분포를 구하여라.

![png](/assets/images/Stat/66_1.png)

- 동전을 던졌을 때, 앞면이 나올 확률이 균일분포를 따른다. 동전을 던졌더니 앞면이 나왔을 때, 이 결과를 이용하여 사후예측분포를 구하여라. 이때, 각 시행은 독립적이다.

![png](/assets/images/Stat/66_2.png)

> ## Frequentist Problem

![png](/assets/images/Stat/65_6.png)

- 위의 경우, 신장암의 발현 비율을 예측하는 문제가 있다고 하자. 
- Frequentist view 에서는 n 이 작으면 그 추정(mle) 이 문제가 생긴다.
  - n = 100 일때 발병자가 0 명이면 mle 는 발병률이 0이 된다.
  - n=100 일떄 재수없게도 발병자가 1명이면 mle 는 발병률이 1%가된다(엄청나게 높은 확률)
- 즉 위와 같은 현상의 '방파제' 역할을 할 수 있도록 prior 를 설정합니다.

> ## Why independent? 

![png](/assets/images/Stat/66_3.png)

![png](/assets/images/Stat/66_4.png)

- 우리가 베이즈 정리를 전개할떄에 위와 같은 식을 많이 보게 됩니다.
- 위와 같이 식을 짤 수 있는 이유는 바로 Exchangeablility 와 de finetti Thm 덕분입니다. 
  - 자세히는 Justification 글에서 살펴보도록 하겠습니다.

> ## Bayesian Inference 

![png](/assets/images/Stat/66_5.png)

- 데이터를 관찰을 하게되면 정보량이 생기고 이를 Theta 에 더 추가하여 Uncertainty 를 낮추는게 베이즈 Update 고정입니다. 
- 하지만 위의 과정에서 제일 어려운 과정은 Constant 를 Normalizing 하는 단계가 매우 어려운 단계입니다. 
  - 분모의 적분을 하는것은 거의 불가능에 가까움
  - 이러한 적분을 해결하기 위해서 몇가지 방법론이 있습니다.
    - Conjugate Prior 쓰기
    - MCMC 방법론 이용하기 
    - Approximation 이용하기 

> ## Conjugacy 

![png](/assets/images/Stat/66_8.png)

![png](/assets/images/Stat/66_9.png)

- 위와 같이, 특정한 Likelihood 에 대해서 특정한 Prior 를 사용하게 되면 Posterior 와 Prior 의 형태가 같게 됩니다. 
- 이렇게 posterior 와 prior 가 같은 class 를 가지는 분포를 Conjugate 분포라 합니다.  

> ## More

![png](/assets/images/Stat/66_10.png)

- 위와 같이 Exponential Family 의 분포를 가지는 경우에는 conjugate 로 잘 업데이트가 됨을 볼 수 있습니다.
  - 이러한 Conjugate 에 대해서는 뒤에 더 잘 알아보도록 하겠습니다.

---

**Reference**

- <https://www.youtube.com/watch?v=8WTSe0St3io>
  - 연세대학교 통계학회 ESC Session 1
- https://rooney-song.tistory.com/9

 베이즈 통계에 대해서 알아보았습니다. 앞으로 베이즈에 대해서 더 알아보도록 하겠습니다~ ! 사실 이전에 3월즈음에 정리를 해 놓았어는데, 초창기에 정리해놓아서 마음에 안들더라구요. 그래서 다시 정리하려고 합니다.
{: .notice--success}

