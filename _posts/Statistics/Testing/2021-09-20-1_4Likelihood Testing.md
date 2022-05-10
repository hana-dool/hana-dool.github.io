---
title:  "Likelihood Testing Comparison"
excerpt: "서로 다른 3가지의 Testing 비교"
categories:
  - Stat_Testing
date : 2021-09-20 18:00:00 +0900
last_modified_at: 2021-09-20

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 Likelihood Test 3개를 짧게 소개해보고 비교해보는 시간을 가져봅시다.
{: .notice--warning}

# [Likelihood Testing](#link){: .btn .btn--primary}{: .align-center}

> ## Idea

![png](/assets/images/Stat/62_1.png)

- Idea 는 위와 같이 간단합니다. 
- 우리는 $H_0 : \theta = \theta_0$ 과 $H_1 : \theta \not= \theta_0$ 을 테스트 하려한다고 합시다.
- likelihood function $l(\theta)$ 에 대해서 $\hat{\theta_n}$ 을 MLE 라고 합시다. (또는 Consistent root of Likelihood equation)
- 우리는 직관적으로, $\hat{\theta_n}$ 이 $\theta_0$ 과 멀다면, 이는 Null hypothesis 를 기각해야 할 것입니다.
  - 왜냐하면 , MLE 는 현재 '데이터를 고려할때에 가장 그럴듯한 추정량' 이기 떄문입니다.
- 하지만 이떄에 '얼마나 멀때에' 기각해야 할까요? 결국에는 분포를 알아야하는 문제가 됩니다. 
- 이러한 'far enough' 를 측정하기 위해서 만들어진 3개의 테스트가 바로 우리가 배운 LR Test, Rao SCore Test , Wald Test 입니다.

> ## Comparison

- Wald Test
  - $\sqrt{n}I^{1/2}(\hat{\theta_n})(\hat{\theta_n} - \theta_0) \sim N(0,1^2)$
  - $nI(\hat{\theta_n})(\hat{\theta_n} - \theta_0)^2 \sim \chi^2(1)$
- LRT Test 
  - $2[l(\hat{\theta_n}) - l(\theta_0))] \sim \chi^2(1)$
- Rao score Test
  - $n^{-1/2}I^{-1/2}(\theta_0)l'(\theta_0) \sim N(0,1^2)$
  - $n^{-1}I^{-1}(\theta_0)l'(\theta_0)^2 \sim \chi_1^2$

![png](/assets/images/Stat/62_2.png)

- 사실 3개의 테스트는 Likelihood 의 서로 다른것을 본 것입니다.

> Wald : MLE 와 $\theta_0$ 간의 거리비교

- 이는 통계량 생김새에서 명확히 드러납니다.
  - $W = nI(\hat{\theta_n})(\hat{\theta_n} - \theta_0)^2 \sim \chi^2(1)$

- 위의 추정량은 다음과 같이 해석됩니다. 
  - mle 는 $\sqrt{n}(\hat{\theta} - \theta_0) \xrightarrow{D} N(0,1/I(\theta_0))$  가 성립하기 떄문에 $W = \frac{(\hat{\theta_n} - \theta_0)^2}{var(\hat\theta)}$ 가 됩니다.
- 즉. 둘간의 거리를 Scaling 시킨 후에 (분산이 1 되도록) 비교한것이라고 볼 수 있습니다.

> LRT : log likelihood 간의 거리 비교 

- 이는 LRT 의 통계량을 본다면 바로 해결되는 문제입니다. 
  - $\Lambda = 2[l(\hat{\theta_n}) - l(\theta_0))] \sim \chi^2(1)$
  - 위와 같이 likelihood 와, Null hypothesis 의 likelihood 를 직접 비교하고 있습니다.

> Rao Score : log likelihood 의 기울기

- 이 또한 통계량에서 엿볼 수 있습니다. 
  - $R = n^{-1/2}I^{-1/2}(\theta_0)l'(\theta_0) \sim N(0,1^2)$
  - 위 값을 살펴보면, $\theta_0$ 의 loglikelihood 기울기가 통계량을 변하게 합니다.
  - 즉 이 값이 크다는것은, Likelihood 가 크게 변하는 과정중에 있다는 것이고, 그것은 지금 Null hypothesis 의 $\theta_0$ 위치가 MLE 와는 멀다는 것입니다.

> ## Difference

> Wald 와 Rao ,LR 는 Assymptoic 동일

![png](/assets/images/Stat/62_3.png)

- 위를 보신다면, $\hat\theta_n$ 이 MLE 라면, Rao 와 Wald 의 통계량은 같게 됩니다.
  - Wald : $\sqrt{n}I^{1/2}(\hat{\theta_n})(\hat{\theta_n} - \theta_0)$
  - Rao : $n^{-1/2}I^{-1/2}(\theta_0)l'(\theta_0)$
- 또한 Assymptotic 하게 3개의 테스트는 모두 같습니다.
  - 모두 'Likelihood Based Model 이기 때문입니다.'

> 하지만 다른 결론을 내릴 수 있다.

![png](/assets/images/Stat/62_4.png)

- 위와 같이, 각각의 Test 는 Approximation 을 다르게 이용하기 떄문입니다.

> 주로 Scoe test 가 선호된다.

- 그 이유는 Consistent Estimator 를 사용하지 않기 떄문입니다.

---

**Reference**

- https://www.cs.ubc.ca/~arnaud/stat461/lecture_stat461_WaldRaoLRtests_handouts_2008.pdf
- https://www.researchgate.net/publication/269286125_The_Three_Plus_One_Likelihood-Based_Test_Statistics_Unified_Geometrical_and_Graphical_Interpretations
- https://stats.idre.ucla.edu/other/mult-pkg/faq/general/faqhow-are-the-likelihood-ratio-wald-and-lagrange-multiplier-score-tests-different-andor-similar/
- 연세대학교 수리통계학(2) 강의
- WIkipedia 

 3가지 테스트에 대해서 살펴보았습니다. Likelihood Test 는 사실 세 형제라고 기억하시는게 편할거 같습니다.
{: .notice--success}

