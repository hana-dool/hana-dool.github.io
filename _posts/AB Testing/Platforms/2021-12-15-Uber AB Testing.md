---
title: "Uber Experimentation Platform (2018)"
excerpt: "Uber 의 실험플랫폼"
categories:
  - AB_Platform
last_modified_at: 2021-12-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

우버의 실험 플랫폼
{: .notice--warning}

# [Uber’s Experimentation Platform](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

> 우버에서 실험플랫폼은 어떻게 진행되고 있을까?

- 우버에선 실험을 통해 고객 경험(UX)를 향상하려 합니다.
  - 새로운 기능 테스트 및 앱 디자인 향상 , 새로운 아이디어, 제품 feature, 마케팅 캠페인, promotion. 및 기계학습 모델의 효과 등을 추정할때에 사용
- 플랫폼은 앱 전반에 걸친 실험을 지원하며 A/B/N Test, 인과 분석, Multi-armed Bandit(MAB)에 기반하여 지속적인 실험을 실행하는데에 도움을 줍니다.

![jpg](/assets/images/Stat/123_1.jpg)

- 현재 플랫폼에서는 위와 같이 1000개 이상의 실험이 실행되고 있습니다.

>  우버의 Experimental Methods

![jpg](/assets/images/Stat/123_2.jpg)

- 위는 Experimentation Plaform 팀이 사용하는 실험 방법론을 요약한 차트입니다.
- Experimental 팀은 통계 방법을 크게 4가지로 사용하게 됩니다.
  - 고정된 horizon A/B/N Test(t-test, 카이제곱, rank-sum test)
  - Sequential probability ratio tests(SPRT)
  - causal inference test (synthetic control and diff-in-diff tests)
  - continuous A/B/N test using bandit algorithms(톰슨 샘플링, upper confidence bounds, contextual multi armed bandit test를 통한 베이지안 최적화)
- 유형 1, 유형 2 오류의 확률을 계산시에 편차 보정을 측정하는 회귀 방법을 사용하고, standard error를 측정하기 위해 block bootstrap와 delta methods 도 사용한다고 합니다.

> ## Classic AB Test

- 무작위 A/B 또는 A/B/N 테스트는 과학 분야에서 Treatment의 효과를 평가하기 위한 표준적인 방법입니다.
- Uber는 A/B 테스트(또는 A/B/N)를 적용하여 객관적이고 데이터를 기반으로 하는 비즈니스 결정을 내립니다. 
- 이때 A/B Testing 은 어떤것일까요? 

![jpg](/assets/images/Stat/123_3.jpg)

- 실험군과 대조군을 설정한 후, 그룹간 metric을 측정하여 Treatment 의 효과를 측정하게 됩니다.
  - 이러한 실험은 주로 Feature Release 실험시에 주로 사용되게 됩니다.

- 실험군과 대조군을 설정한 후, 그룹간 metric을 측정해 실험 효과를 측정
  - Feature release 실험시 주로 사용

![jpg](/assets/images/Stat/123_4.jpg)

- 위애서 보다시피 XP 분석 대시보드를 사용하면 데이터 과학자와 다른 사용자가 A/B 테스트 결과에 쉽게 액세스하고 해석할 수 있습니다.
- 위 대시보드를 보면, Sample 이 균형있게 잘 분배되고 있는지, Lift 가 우리가 원하는 수준만큼 향상되었는지 등을 점검하고 있음을 알 수 있습니다.

> ## Statiatical Engine

- 우리 팀의 주요 목표 중 하나는 회사 전체의 사용 사례에 적용할 수 있는 가장 보편적인 가설 테스트 방법론을 제공하는 것이였습니다. 
- 이를 달성하기 위해 여러 사람들과 함께 협력하여 통계 엔진을 구축했습니다.

![jpg](/assets/images/Stat/123_5.jpg)

- 무작위 A/B 테스트의 첫 번째 단계는 실험에 잘 맞는 Metric(예: 라이더 총 예약)을 선택하는 것입니다. 
- XP를 사용하면 실험자가 사전에 정의되었던 메트릭을 쉽게 재사용하고 데이터 수집 및 데이터 유효성 검사를 자동으로 처리할 수 있습니다. 
- 메트릭 유형에 따라 통계 엔진은 다양한 통계 가설 테스트 절차를 적용하고 읽기 쉬운 보고서를 생성합니다. 
- Uber는 방법론의 연구 및 검증에 막대한 투자를 하고 있으며 통계 엔진의 견고성과 효율성을 지속적으로 개선하고 있습니다.

> ## Two problem

- 데이터를 수집한 후 XP의 분석 플랫폼은 데이터를 검증하고 실험자가 A/B 실험에서 건강한 회의론을 관찰하고 유지해야 하는 두 가지 주요 문제를 감지합니다.

> Sample size imbalance

- Control 과 Treatment 사이에 표본 크기의 비율이 예상하는것과 다른 경우에 imbalance 가 존재한다고 합니다.
- 이런 imbalance 가 존재할 경우, 무작위 알고리즘을 다시 점검해야 합니다.

> Flickers (깜박임)

- Control 그룹과 Treatment 그룹 사이를 왔다갔다한 사용자를 나타낸 경우 
- Ex : 기종에 따라서 무작위가 결정되는 실험에 홍길동씨가 Control 에 할당되었다고 합시다. 그런데 최근에 iphone 을 사용하다가, Android 휴대전화로 바꾸어서 Control 에서 Treatment 로 할당 되었다고 합시다.
- 위와 같이 Control 에서 Treatment 로 전환된 (또는 그 반대) 사용자의 경우 실험 결과를 외곡시킬 수 있어서, 이런 깜박임 사용자를 제외하는것이 중요합니다. 

> ## Metric Definition

- User level 에서는 아래와 같이 세가지의 Metric 이 있습니다.
- Continuous metrics
  - 유저당 예약 비율같은 1가지 숫자로 나타낼 수 있는 지
- Proportion metrics
  - 여행을 완료한 사용자의 비율 과 같은 Proportion
- Ratio metrics
  - 2개의 숫자 값을 사용한 metric, 예를 들면 (총 트립 요구수/완료된 트립의 수)

> ## Improve A/B Test Quality

- AB Test의 퍼포먼스를 증대시키기 위한 전처리 방법은 다음과 같습니다. 

> Outlier detection

- Outlier 를 제거하면, 데이터에 존재하는 irregularity 를 제거하고, 그에 따라 분석 결과의 Robustness 를 향상합니다. 
- 클러스터링 기반 알고리즘을 사용하여 이상값 감지 및 제거를 수행합니다. (하지만 자세한 내용은... 안 알려줌!)

> Variance reduction

- 분산 감소는 Testing 의 통계적 검정력을 높히는데에 도움을 줍니다.
- 이는 특히 모든 실험에 대해서 매우 중요하긴 하지만, 특히 사용자가 적거나 정확성을 희생하지 않고 조기에 실험 끝낼 경우 유용합니다. 
- 이때에  [CUPED 방법](http://www.exp-platform.com/Documents/2013-02-CUPED-ImprovingSensitivityOfControlledExperiments.pdf) 을 활용한다면 추가 정보를 활용하고 의사 결정 매트릭스의 분산을 줄일 수 있습니다.

> Pre-experiment bias

- 다양한 유저가 존재하기 떄문에  그룹간 실험 편향을 교정할 필요가 있습니다. 
- diff-in-diff 방법론을 이용하여서 이러한 차이를 사전에 교정하려고 합니다.

Difference in differences (diff-in-diff) is a well-accepted method in quantitative research and we use it to correct pre-experiment bias between groups so as to produce reliable treatment effects estimation.
{: .notice}

> ## P-value and Testing method

- p value 값의 계산은 우리의 Stat Engine의 핵심입니다. 
- 우리는 p-값을 일반적인 A/B 테스트에서 원하는 False positive 비율(제1종 오류)(0.05) 을 설정한 뒤에 비교합니다..
- XP 는 아래의 테스트 방법론을 이용하여,  p-값 계산을 위한 다양한 방법론을 활용합니다. 

> Welch’s t test

- Continuous Test 를 테스트할때에 기초적인 방법론

> Mann-Whiteney U test 

- rank sum 을 활용한 비모수 테스트 test 
- 이 경우에 Outlier 가 rank 로 바뀌면 normalized 가 되는 효과가 있기 때문에 , Skewness 가 심한 경우에 매우 도움이 됩니다.
- 애초에 비모수 테스트기 때문에, t-test 보다 훨씬 적은 가정이 필요하며 skewed data 일 경우에 어느정도 잘 작동한다고 알려져 있습니다. 

> Chi-squared Test

- Proportion Test 를 검정할때에 사용하는 방법론
- 이때 2개의 평균을 비교하는 경우, Chi square Test 는 two sample proportion test 와 같습니다.

>  Delta method ([Deng et al. 2011](https://alexdeng.github.io/public/files/jsm2011-deng.pdf)) and bootstrap methods

- 위 방법론은 Assumption 이 two sample t test 보다 더 작기때문에 비율 메트릭, 또는 작은 샘플 크기의 경우에 사용됩니다.

> ## Correlation

> Multiple Correction

- 다중 테스트를 하다보면, False Positive Inflation 현상 때문에 두개 이상의 Treatment 그룹이 있는 경우 (A/B/C 또는 A/B/N...) 에 보정을 사용하게 됩니다.

> Power Calculation

- Power Calculation 을 이용한다면, 우리는 현재 샘플 수를 고려할때, 실험을 하게 된다면 어느정도의 Power 을 가지는 실험을 할 수 있는지를 계산할 수 있게 됩니다.
  - XP 에서 수행되는 검정력(Power) 계산은 항상 t-test 가 가정된 상태에서 계산됩니다. 
- 또는 반대로 Power를 고정한 상태에서 어느정도의 샘플 사이즈를 계산할 수 있을지도 계산할 수 있습니다.

> ## Metrics management

- XP의 경우에는 사용하는 메트릭의 수가 증가함에 따라(1,000개 이상의 메트릭 통합) 사용자가 실험의 성능을 평가하기 위해 적절한 메트릭을 결정하는 것이 점점 더 어려워집니다.
- 분석 도구의 신규 사용자가 이러한 메트릭을 더 쉽게 발견할 수 있도록 플랫폼에서 사용 가능한 메트릭의 검색을 용이하게 하는 추천 엔진을 구축했습니다!

> Metric Reccomendatation

- Uber에는 콘텐츠 추천에 사용되는 두 가지 일반적인 협업 필터링 방법이 있습니다. 
- 항목 기반 방법 (item-based)과 사용자 기반(user-based) 방법입니다. 
- 실험자의 특성 은 일반적으로 프로젝트에 큰 영향을 미치지 않기 때문에 주로  [item-based recommendation](https://en.wikipedia.org/wiki/Item-item_collaborative_filtering) 엔진을 사용합니다 .
  - 예를 들어서 실험 기획자가 Rider 팀에서 Uber Eats 팀으로 옮겨가는 경우 평가할 지표를 선택할 때 알고리즘이 Uber Eats에서 영감을 받은 이전 실험자를 검토할 필요가 없습니다.

> ## Recommendation engine methodology

- 두 Mtric이 서로 얼마나 상관관계가 있는지 확인하기 위해 popularity scores 와 absolute scores 를 시용하여서 메트릭간의 relationship 을 좀 더 자세하게 이해하려고 합니다. 
  - 이 점수를 계산하는 두 가지 기본 접근 방식은 다음과 같습니다.

> Popularity Score

- 여러 실험에서 두 메트릭이 함께 선택되는 빈도가 높을수록 관계에 더 높은 점수가 할당됩니다.
  - 이러한 경우에 우리는 [Jaccard Index](https://en.wikipedia.org/wiki/Jaccard_index) 를 사용하여 Metric 의 관계를 측정합니다.

> Absolute Score

- XP를 사용하여 사용자 샘플 풀을 생성 하고 그 풀에서 두 메트릭 의 [Pearson 상관 관계](https://en.wikipedia.org/wiki/Pearson_correlation_coefficient) 점수를 계산할 수 있습니다.
- 이는 우리가 생각하지 못했지만, 우리가 선택한 메트릭과 유사한 매트릭을 찾게 도와줍니다.
- 즉, 실험자는 직접적인 관련이 없기 때문에 실험에 메트릭을 추가하는 것을 고려하지 않았을 수 있지만 , 유사한 관련이 나왔다고 결과가 나온 메트릭을 고려할 수 있습니다

> Choice

- 이제, 두개의 Score 를 상대적 가중치를 이용해 계산합니다.
- 그 이후 첫 번째 측정 항목 선택을 기반으로 실험자에게 가장 높은 점수를 가진 측정 항목을 추천하게 됩니다.

> ## Insights discovery

- Uber의 규모가 계속 확장됨에 따라, 많은 메트릭 중에서 좋은 가치의 메트릭을 찾는것은 어려워지고 있습니다.
- 우리의 추천 엔진은 그들이 원하는 정보를 빠르게 제공하고,  이를 이용해 서비스 개선 하는것을 도와줍니다.

> Example

- 예를 들어서, 실험을 진행함에 따라서 우리는 특정 메트릭에 익숙해질 수있습니다.  나중이 되면 비슷한 메트릭만 사용하려 할 수 있습니다.
- 하지만 Metric Recommendation System 을 이용한다면 우리가 고려하지 못한 새로운 Metric 을 쓸 수 있습니다. 
- 여행 방정식의. 그러나 시장의 역동성 때문에 이 실험에서는 두 측정항목 모두 중요합니다. 우리의 추천 엔진은 데이터 과학자와 다른 사용자가 분명하지 않았을 수 있는 중요한 지표를 발견하는 데 도움이 됩니다.

> ## Sequential testing

![jpg](/assets/images/Stat/123_6.jpg)

- 기존의 A/B  Test 를 여러번 수행하게되면 제 1종 오류를 부풀리게 됩니다.
- 그에 비해서 순차적 테스트 (Sequential Testing) 는 주요한 비즈니스 메트릭을 지속적으로 모니터링하는 방법을 제공합니다.

> Note

- 이러한 순차적 순차 테스트가 우리 팀에 유용한 한 가지 사용 사례는 우리 플랫폼에서 실행되는 실험으로 인한 중단을 결정할때입니다.
- 안좋은 실험을 적용하게 되어서, 주요 메트릭의 저해를 초래한다고 합시다. 이 경우 A/B 테스트가 판단을 내리기까지의 충분한 샘플 크기를 수집할 때까지 기다리는 힘듭니다.
- 하지만 일반적으로 실험을 계속 바라보면서, 유의할때 바로 그만둬 버리는것은 Type 1 error 를 부풀리게 되므로 적절한 Sequential Testing 을 이용하여 Type 1 error 를 잘 조절하는것이 필요합니다.

> Methodologies

- Metrics 모니터링 목적으로는 [mSPRT](https://en.wikipedia.org/wiki/Sequential_probability_ratio_test)(mixed Sequential Probability Ratio Test)와 FDR을 사용한 분산 추정을 위한 테스팅을 활용하게 됩니다.

> ## Mixture Sequential Probability Ratio Test

- 위와 같은 Sequential Testing 을 가능하게 하는 일반적인 방법은 mSPRT 방법입니다. 이 테스트는 Likelihood Ratio Test 에 기반하고. incorporating an extra specification of [mixing distribution H.](http://www.kdd.org/kdd2017/papers/view/peeking-at-ab-tests-why-it-matters-and-what-to-do-about-it) 하는 방법론입니다. 
- mSPRT 의 방법론은 여기에서는 정말 간단히 맛만 보도록 하겠습니다.

>  MSPRT

- mixture of likelihood ratios against the null hypothesis that $\theta=\theta_{0}$  는 아래와 같습니다.

$$\Lambda_{n}^{H, \theta_{0}}=\int_{\Theta} \prod_{m=1}^{n} \frac{f_{\theta}\left(X_{m}\right)}{f_{\theta_{0}}\left(X_{m}\right)} h(\theta) d \theta$$

- 우리는 주로 large sample size 일 경우에 다루게 되므로 Central Limit Theorem 에 의하여 $H \sim N\left(0, \tau^{2}\right) $ 와 같이 가정할 수 있습니다.
- 위와 같은 가정을 통하여 우리는 $$\Lambda_{n}^{H, \theta_{0}}$$ 에 대해서 Closed form expression 을 만들어 낼 수 있습니다. 
- 또한 Another useful property about this method is under null hypothesis, $H_0$, is proven to be a [martingale ](http://www.kdd.org/kdd2017/papers/view/peeking-at-ab-tests-why-it-matters-and-what-to-do-about-it): $$\Lambda_{n}^{H, \theta_{0}}$$
- 위를 통해서 우리는 $(1-\alpha)$ 의 Confiidence interval 을 생성해낼 수 있습니다.

> ## Variance estimation with FDR control

- 순차 테스트를 올바르게 적용하기 위해 가능한 정확한 분산을 추정해야 합니다. 
- 비교군 대조군 그룹의 누적 차이를 모니터링하게 되는데 , 이떄 이러한 누적합은 같은 유저에 대해 Correlated 되고 이는 assumption of the mSPRT test 를 위배하게 됩니다.
  - 예를 들어서 CTR 을 계속 모니터링 중이라면, metric from one user across multiple days may be correlated
- 이러한 현상을 제거하기 위해 [delete-a-group jackknife variance estimation](http://www.sverigeisiffror.scb.se/contentassets/ca21efb41fee47d293bbee5bf7be7fb3/the-delete-a-group-jackknife.pdf)/block bootstrap methods to generalize mSPRT test under correlated data

> ## Multiple Correction

- 우리의 모니터링 시스템은 진행 중인 실험의 전반적인 상태를 평가하기를 원하기 때문에 많은 비즈니스 메트릭을 동시에 모니터링하여 잠재적으로 잘못된 경보로 이어질 수 있습니다
- 이론적으로 [Bonferroni 또는 BH 보정](https://en.wikipedia.org/wiki/Multiple_comparisons_problem) 를 이용할 수 있습니다.
- 그러나 potential loss of missing business degradations를 불러일으 킬 수 있습니다. 
- 우리는 BH 수정을 적용하고 다양한 수준의 중요도와 민감도를 가진 메트릭에 대한 매개변수(MDE, power, tolerance for practical significance, etc)를 유연하게 조절합니다.

![jpg](/assets/images/Stat/123_7.jpg)

Figure The sequential test methodology indicates a significant difference between our treatment and control groups, as identified in Plot B. In contrast, no significant difference is identified in Plot A. 

{: .notice}

-  위와 같이 특정 실험에 대한 주요 비즈니스 메트릭을 모니터링한다고 가정합니다.
- A와 B의 빨간색 선은 Control 과 Treatment 사이의 관찰된 누적 상대 차이를 나타냅니다.
  - 분홍색 밴드는 $1-\alpha$ Confidence interval 차이에 대한 신뢰 구간입니다.  

- 시간이 지남에 따라 더 많은 샘플을 측정하게 되고 그에 따라 신뢰 구간이 좁아지고 있는것을 볼 수 있습니다.
  - 그림 B(오른쪽)에서 신뢰 구간은 주어진 날짜(이 예에서는 11월 21일)부터 시작하여 일관되게 0에서 벗어나고 있습니다.
  - 대조적으로, 플롯 A의 신뢰 구간은 줄어들지만 항상 0을 포함합니다. 따라서 플롯 A에서는 충돌에 의한 regression 현상을 잡아내지 못하고 있습니다.

# [Uber’s Examples](#link){: .btn .btn--primary}{: .align-center}

> ## Continuous Experiments

![jpg](/assets/images/Stat/123_8.jpg)

- Uber의 데이터 과학 팀은 지속적인 실험을 통해 운전자, 탑승자, 식사자, 레스토랑 및 배달 파트너 들의 경험을 최적화하기 위해 항상 노력하고 있습니다. 
- 우리 팀은 관련 메트릭 성능의 지속적인 평가에서 반복적이고 빠르게 학습하기 위해 bandit 및 최적화 중심의 강화 학습 방법을 구현했습니다.
- 최근에 우리는 고객 참여를 향상시키기 위해 콘텐츠 최적화를 위한 bandit 기법을 사용한 실험을 완료했습니다. 이러한 기술은 고전적인 가설 테스트 방법에 비해 고객 참여를 개선하는 데 도움이 되었습니다. 

![jpg](/assets/images/Stat/123_9.jpg)

- 위 그림은 Ubers 의 다양한 Continuous Experiments use cases 를 나타내고 있습니다.

> ## Case study 1 

![jpg](/assets/images/Stat/123_12.jpg)

- Uber에서 이메일 캠페인을 최적화하고 라이더 참여를 향상시키는 데 어떻게 도움이 되었는지 간략하게 설명합니다. 
- 여기에서 유럽, 중동, 아프리카(EMEA)의 Uber Eats CRM(고객 관계 관리) 팀은 고객 라이프 사이클 초기에 주문 모멘텀을 장려하는 이메일 캠페인을 시작했습니다. 
- 실험자는 10개의 서로 다른 이메일 제목으로 캠페인을 실행하고 열린 비율과 열린 이메일 수 측면에서 가장 좋은 제목을 찾으려 했었습닌다.

> ## Case Study 2 

![jpg](/assets/images/Stat/123_10.jpg)

- 지속적인 실험을 활용하는 방법의 두 번째 예는 매개변수 조정입니다.
- 첫 번째 사례와 달리 두 번째 사례 연구는 통계적 실험과 머신 러닝 모델링을 결합한 보다 발전된bandit 알고리즘인 contextual multi-armed bandit 기법을 사용합니다. 상황별 MAB를 사용하여 기계 학습 모델에서 최상의 매개변수를 선택합니다.
- 위에서 볼 수 있듯이 Uber Eats 데이터 과학 팀은 MAB 테스트를 활용하여 MOO(다중 목표 최적화)라고 하는 선형 프로그래밍 모델을 만들었습니다. 
  - 이 모델은 Uber Eats 앱의 기본 피드에서 레스토랑의 순위를 지정합니다.
  - MOO 가 작동하는 알고리즘은 세션 전환율, 총 예약 수수료 및 사용자 유지율과 같은 여러 Metric 을 이용합니다. 
  - 우리가 이 알고리즘을 이용하기 위해서는 몇가지 하이퍼 파라미터를 넣어야 합니다. 이것을 어떻게 정해야 할까요?
- 이러한 실험에는 순위 알고리즘과 함께 사용할 수 있는 많은 매개변수 후보가 포함되어 있습니다. 
  - 순위 결과는 MOO 모델에 대해 선택한 하이퍼 매개변수에 따라 다릅니다. 
- 따라서 MOO 모델의 성능을 향상시키기 위해 multi-armed bandits 알고리즘을 통해 최상의 하이퍼 매개 변수를 파악하려 하였습니다.
- 기존의 A/B 테스트 프레임워크는 각 테스트를 처리하기에는 시간이 너무 많이 소요되므로 이러한 실험에 MAB 방법을 사용하기로 결정했습니다. 
  - MAB는 이러한 매개변수를 빠르게 조정할 수 있는 프레임워크를 제공할 수 있습니다.
- 우리는 블랙박스 함수 최적화 문제의 최대화기를 찾기 위해 상황별 MAB와 베이지안 최적화 방법을 선택했습니다. 아래 그림은 이 실험의 설정을 간략하게 보여줍니다.  

![j](/assets/images/Stat/123_11.jpg)

> ## Summary

- Uber 는 진짜 복잡한 Platform 을 쓰는것같네요.. 

---

**reference**

- <https://eng.uber.com/xp/>





