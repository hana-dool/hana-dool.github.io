---
title: "Bootstrap AB Test at Criteo (2020)"
excerpt: "부트스트랩을 이용하는 A/B Testing"
categories:
  - AB_Platform
last_modified_at: 2021-11-14

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 Bootstrap 을 이용하여 Testing 을 진행하는 방법은 익히 알려져 있는데요, 이를 A/B Testing 에 어떻게 하면 적용할 수 있는지에 대해서 알아봅시다. (근데 뭐... 별로 이론적인 이야기를 하는것같지는 않네요)
{: .notice--warning}

# [Bootstrap A/B Testing](#link){: .btn .btn--primary}{: .align-center}

> ## A/B Testing in 0,1 Data

- Criteo 에서는 bainary metric 을 이용하여 A/B testing 의 결론을 내리는 경우가 많았습니다. 
  - 예를 들면, 전환율, 얼마나 사람들이 샀는지 등이 될 수 있습니다.

- 이러한 유형의 변수에 대해서 , 우리는 카이제곱 피어슨 검정을 사용하여 검정해 보았습니다.

$$\begin{array}{|l|l|l|l|}
\hline & \text { population A } & \text { population B } & \text { total } \\
\hline \text { number of buyers } & 105 & 45 & 150 \\
\hline \text { number of non-buyers } & 10000 & 5000 & 15000 \\
\hline
\end{array}$$

- 우선 $H_0$ 에서는 두 A,B 는 동일한 분포에서 샘플링 된다고 할 수 있습니다.
  - 그러므로 귀무가설에서는 1% 의 전환율을 얻습니다. 
  - 이 전환율을 사용하여, 우리는 A 와 B 에 대하여, Expected distribution of population A,B 를 얻을 수 있습니다. 

$$\begin{array}{|l|l|l|l|}
\hline & \text { population A } & \text { population B } & \text { total } \\
\hline \text { number of buyers } & 100 & 50 & 150 \\
\hline \text { number of non-buyers } & 10005 & 4995 & 15000 \\
\hline
\end{array}$$

- Chi square test 에 의하면, p-value sms 0.743 을 얻습니다.
  - 이는 $H_0$ 가설을 받아들여야 한다고 생각할 수 있을것입니다.

> ## A/B Testing in Continuous Data

- 데이터가 0,1 로만 이루어지지 않은 경우에는 중심극한 정리를 사용하여 메트릭의 신뢰 구간을 만들어낼 수 있습니다
- A/B Testing 의 경우 두개의 합을 비교하게 되므로, Welch two sample t test 를 이용할 수 있습니다. 
  - 이 경우에두 집단에 대한 평균과 분산만 가지고 테스팅이 가능하므로 매우 효율적이라 할 수 있습니다. 

> ## BOotstrap Method

- 하지만 위처럼 Exact 한 분포에 기반한 testing 이 아니라, sampling 에 근거한 통계 방법을 알아보겠습니다.
- 1979년 efron 에 의해 개척된 분야로서, 단순한것부터 , 복잡한것까지 모두 측정할 수 있다는 장점이 있습니다. 
  - CLT 를 적용할 수 없는 측정 항목에 대하여, (중앙값 , 분위수 등..) 우리는 부트스트랩 방법을 이용하여 테스팅을 진행할 수 있습니다. 

> How to? 

1. 먼저 사용하려는 부트스트랩 의 수 *k* 를 결정 합니다. k 는 최소한 100개 이상이여야 합니다. 
2. 각각 부트스트랩 procedure 마다 resampling 을 통하여 원래와 똑같은 크기의 샘플을 generating 합니다.
3. 이 새로운 데이터 세트에  metric of interest (중앙값 등) 를 계산합니다. 
4. k 개의 메트릭을 이용하여, Statistical Significant 를 계산합니다. 

> ## Bootstrap in A/B Testing 

> How to?

- 부트스트랩 방법을 사용한다면, 한개의 bootstrap sample 에서 계산되어지는게 아니라 두 모집단 모두에서 bootstrap 되어야 합니다. 
  - 즉 어떤 의미냐면, 평균을 비교한다면 A 와 B 에 대해서 $Sample_{A} , Sample _B$  로부터 각각 천개의 평균을 만들어내야 합니다.

> Example

- A/B test 에 부트스트랩 방법을 사용해보도록 하겠습니다. 
- A 와 B 는 각각 100만명의 사용자를 가지고 있습니다. 그리고 우리는 제품을 구매한 사람들의 비율을 비교하고자 합니다. 
  - 모집단 A 에서의 전환율은 정확히 1% 입니다. 그리고 모집단 B 에서의 전환율은 1.03% 입니다.
- 두 데이터를 Simulation 하기 위해서 Bernoulli 시행을 사용하여 두 데이터 Set 을 시뮬레이션 해 보았습니다. 
  - A 는 10109 명의 구매자 , B 는 10318 명의 구매자로 이루어져 있습니다. 
- 우리는 천개의 Bootstrap 을 사용하여 두 모집단의 구매자 수에 대한 Bootstrap 분포를 만들어 보았습니다 . ($S_A , S_B$ 라고 하겠습니다.) 

![png](/assets/images/Stat/103_1.png)

- 위는 모집단 A,B 에 대한 구매자 수의 합에 대한 Empirical Distribution 입니다. 

![png](/assets/images/Stat/103_2.png)

- 이때 우리는 위에서 계산된 평균들에 대해서, pop A 에서 하나를 고르고, pop B 에서 하나를 고른 뒤,  $S_A - S_B$ 를 여러개 만들어내어서 위와 같은 분포를 만들어 낼 수 있습니다.
- 위의 분포를 보면, 1000개중에서 74개가 0 이상인것을 볼 수 있습니다. 
  - 즉 이는 겨우 7.4 %의 bootstrap sample 이 $S_A > S_B$ 라는것을 의미합니다.
- 즉 우리는 $H_0$ 을 기각할 수 없습니다..

> ## Bootstrap method Problem

- 대규모 데이터에 대해서 작업할때에 다음과 같은 일이 일어날 수 있습니다. 

1. 데이터 세트가 여러 시스템에 분산되어있어서, 단일 시스템에 맞지 않을 수 있습니다.
2. 데이터 세트를 포함해서, 관찰값도 여러 시스템에 분산되어있을 수 있습니다. 예를 들어서 우리가 관심있어하는 metric 이, 사용자가 지난 7일동안 지출한 금액 이라고 할 때에, 원본 로그를 사용자 수준으로 다시 데이터를 말아야하는데 이러한 작업은 시간이 많이 들 수 있습니다.

---

**reference**

- <https://medium.com/criteo-engineering/why-your-ab-test-needs-confidence-intervals-bec9fe18db41>

  

