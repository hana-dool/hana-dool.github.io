---
title:  "Beyond Power Analysis &#58; Metric Sensitivity Analysis in A/B Tests"
excerpt: "Microsoft Teams 에서 수행한 Metric 평가분석과 Remedy 방법 알아보기"
categories:
  - AB_Microsoft
last_modified_at: 2021-10-08

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 AB Test 시에 Metric 에 대해서 이 녀석이 얼마나 좋은 Metric 인지 궁금하지 않나요? 이에 대해서 Microsoft Teams 에서 어떻게 Metric 을 평가하고 , 안좋은 녀석에 대해서는 어떻게 조치하였는지에 대해서 알아봅시다! 
{: .notice--warning}

# [Metric Sensitivity in A/B Tests](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

- A/B Test 는 공통적으로 다음과 테스트할 가설을 설정하며, 이에 대해 Treatment 를 설계하며 AB Testing 을 수행합니다. 
  - A/B Testing 이 끝난 이후에는 이 결과를 해석하면서 효과가 있었는지 없었는지를 검정하게 됩니다. 
- 하지만 그 결과로 Metric 에 유의한 움직임이 없었다고 합시다. 이러한 경우 두가지 시나리오를 생각할 수 있습니다.
  - 실제로 Treatment 가 사용자에게 아무런 효과가 없었던 경우 
  - Treatment 가 사용자에게 효과가 있었지만 Metric 이 움직이지 않았던 경우 
- 우리는 메트릭이, 효과가 있다면 그러한 움직임을 잘 측정해주기를 바랍니다. 
- 우리는 이러한 Metric 의 Sensitivity 를 두가지 방법으로 추정해볼 수 있습니다. 
  - MDE 기반 또는의 Power analysis
    - Treatment 의 metric 이 MDE 만큼 변했다는 가정 하에서 계산되는 Power  
  - Movement Probability 
    - Treatment 에 따라 실제로 metric 이 변하는지에 대한 확률 
- Experiment 는 기본적으로 Statistical Power 에 초점을 맞춥니다만 Movement Probability 가 metric 의 Sensitivity 를 측정할때에 중요한 역할을 하게됩니다. 
- 여기에서는 다음과 같은 사항을 이야기 하고자 합니다.
  - metric 의 Sensitivity 를 이해하기 위해서 Statistical Power 롸 Movement Probability 로 이해하기
  - 어떻게 하면 Metric 이 Feature 의 impact 를 잡아낼만큼 Sensitive 한지 아닌지를 측정하는법
  - Sensitive Metric 을 설계하기 위한 Tip

# [Decomposing Metric Sensitivity](#link){: .btn .btn--primary}{: .align-center}

> ## Decomposing Metric Sensitivity

- Metric 분석에서 Deng 과 Shi 는 Sensitivty 를 두가지 구성 요소로 분해하였습니다. 
  - Statistical Power 와 Movement Probability 입니다. 
- 이 두개의 구성 요소는 feature 의 impact 를 측정하는데에 모두 중요한 역할을 합니다. 
- Feature 가 Metric 에 영향을 준다고 합시다. (즉 다시 말하면 대립가설이 맞을때 입니다.)
  - 그렇다면 Under Alternative Hypothesis $H_1$ 에 대해서 
- Prob[Detecting the treatment effect on the metric] =$ Prob(H_1)Prob(p<0.05\mid H_1)$

> $Prob(p<0.05\mid H_1)$ 

- $Prob(p < 0.05\mid H_1)$ 은 Statistical Power 를 나타냅니다. 
  - 즉 $H_1$ 이 맞을때 $H_1$ 을 선택할 확률이 됩니다.
  - 이는 Sample size , Effect size , Significant level 에 의해 결정됩니다. 
- Experiment 는 주로 MDE 에 기초하여 significant level, sample size 등을 고정한 상태에서 power 를 계산하게 됩니다. 
  - 또는 power 를 고정한 상태에서 Sample size 등을 계산하기도 합니다. 

> $Prob(H_1)$

- 위와 같은 $H_1$ term 은 Movement Probability 입니다. 
  - 이는 feature 가 $H_1$ 하에서 Metric 의 이동 확률을 나타냅니다. 

> ## Power Analysis 

- Power analysis 의 결과를 통해서 , Feature Team 과 함께 Metric 의 MDE 를 달성 가능한지 논의할 수 있습니다.
  - 일반적으로 백분율 값이면 , 절대적인 값으로 변환하여 (즉 % 가 아니라 vlaue로) 변화의 정도를 파악할 수 있습니다. 
- 최소 MDE 가 A/B Test 에서 예상하는 차이보다 보다 훨씬 높은 경우에는 Metric 이 잘 이동하지 않을것입니다. 
  - Microsoft Teams 의 경우 Time in App 매트릭의 경우 1주일 Traffic (Sample 수) 을 이용한다면 Minimum MDE 가 0.3%입니다.
  - Microsoft Teams 에서는 이러한 차이를 실제 차이와 비교해본 결과 이러한 MDE 는 달성 가능한것으로 여겨졌고, 즉 좋은 메트릭임을 알 수 있었습니다. 

> ## Movement Analysis 

- Metric 의 Sensitivity 를 알고싶다면, 과거 A/B Test 결과에 대한 Metric 의 움직임을 살펴봐야 합니다. 
- 이떄에 Historical A/B Test 는 Metric 을 평가하기 위한 좋은 tool 입니다
  - 이 떄에 Historical A/B Test 는 Experimental Corpus 라 불리우는 실험 Set 을 이용해 A/B Test를 하는것을 말합니다. 
  - 더 많은 HIstorical A/B Test 가 가능할수록 , 신뢰성 높고 다양한 테스트가 가능합니다. 
- 이를 어떻게 수행할 수 있는지는 아래에서 더 자세하게 알아보겠습니다.

# [Movement Analysis Deailed](#link){: .btn .btn--primary}{: .align-center}

> ## Movement Confusion Matrix

- Confusion matrix 는 metric 의 움직임에 대해서 이해하는데에 도움을 줍니다. 

![png](/assets/images/Stat/71_1.png)

- 위와 같이 Label 이 지정된 실험들이 히스토리에 저장되어 있다면 위와 같이 Confusion matrix 를 구성할 수 있습니다. 
  - columns 는 각 A/B Test 에서 '실제적인 Treatment 효과가 있었는지 없었는지' 를 알고있는 labeled Corpus 입니다. 
  - 이는, 이러한 방법을 제안한 논문을 보시면 알겠지만 , label 을 매기는 작업은 매우 힘든 작업입니다. 
- metric 의 움직임이 있었을때에는 실제 기대되는 direction 과 맞는지 검사해야합니다. 
  - metric 의 movement 가 정반대의 위치라면 더 많은 조사가 필요할 것입니다. 
    1. Experiment 의 Labeling 이 잘못된 경우 : 라벨을 업데이트
    2. Meric 이 실제와 반대로 움직인 경우 : Meric 을 교체 또는 수정 
- Matrix 에서는 Labeled 된 Experiment 를 통하여 Metric 의 움직임을 평가할 수 있습니다. 
  - Metric 이 Sensitive 한 metric 이라면 $N_1 / (N_1 + N_2)$ 가 큰 값을 가질것입니다.
  - Metric 이 Robust 한 Metric 이라면 (즉 Noise Movement 에 Robust) $N_3 /(N_3+ N_4)$ 가 Significant Level 에 수렴할 것입니다.
- Microsoft Teams 는 Time in Apps 메트릭에 대해  위와 같은 테스트를 수행해 보았습니다.
  - 그 결과는 $N_1 / (N_1 + N_2)$ 가 0 에 가까웠습니다. 

> ## Observed Movement Probability

- Labeled Corpus 가 매우 유용할 수 있겠지만 이러한 Labeling 에는 매우 시간과 노력이 많이 듭니다. 
  - 그래서 대안으로 Unlabelded Corpus 방법이 쓰일 수 있습니다.
- 이 경우 Deng 과 Shi 가 Data-Driven Metric Development for Online Controlled Experiments: Seven Lessons Learned 에서 추천하기를 이러한 비교를 위해서는 Observed Movement Probability 를 추정해야 한다고 하였습니다.
  - Observed Movement Probability 란 Metric 의 Movement 가 통계적으로 유의한(P<0.05) 실험의 수를의 비율을 나타냅니다. 
- 이러한 비율 (Probability) 을 Unlabeled Corpus 를 측정할떄에는  위 Confusion Metric 에서, Label 은 없는것으로 생각해야됩니다.
  - 즉 $(N_1 + N_3) /(N_1+N_2+N_3 +N_4)$ 를 측정하게 됩니다. 
  - 우리가 측정한 값을 분해해 보면 아래의 식과 같습니다. 

$$Prob(H_1)Prob(p<0.05|H_1) + Prob(H_0)Prob(p<0.05|H_0)$$

- 첫번쨰 Term 은 Treatment effect 가 존재하여 metric 에 영향을 주었고, 그것을 detect 할 확률입니다.    
- 두번쨰 Term 은 Treatment effect 가 metric 에 영향을 주지 못했지만 그것을 detect 했다고 잘못 말할 확률입니다. 
  - 이러한 Second Term 은 Biased Term 이라 할 수 있습니다. 하지만 이때에 $Prob(p<0.05\mid H_0$ 을 0.05 로 제한하여 식을 설계하였기 떄문에 Second Term 은 0.05 에 Bounded 됩니다. 
- Microsoft Teams 는 수십개의 A/B Tests 들을 모아보았고 , Time in App 에 대한 Observed Movement Probability 를 계산해 보았습니다. 
  - 이 값은 다른 매트릭값보다 훨씬 낮은 Observed Movement Probability 를 가지고 있었습니다. 
- 그러므로 이러한 Metric 에 대해서 Sensitivity 를 높히기 위하여, 다양한 조치가 필요할 수 있습니다.
  - 이러한 조치에 어떤것이 있을지는 아래에서 알아보도록 하겠습니다.

# [Tips for designing sensitive metrics](#link){: .btn .btn--primary}{: .align-center}

- 위에서의 Sensitive Analysis 에서 Metric 이 매우 안좋게 나왔다고 합시다. 
  - 이러한 메트릭을 버려야 할까요? 
  - 버릴 수 없는 메트릭 (사용자의 너무 좋은 부분을 Summary 하는 메트릭) 일 경우에는 어떻게 할까요? 
- 즉 이러한 상황을 위하여 , 우리는 메트릭을 약간 변형하더라도, Sensitivity 를 높히는 방법에 대해서 알아보려고 합니다.

> ## Apply a transformation to the metric value

- 한 방법은 Metric 의 Outlier 의 임팩트를 낮추어 sensitivity 를 높히는 방식입니다. 
  - Metric 의 Outlier 가 많으면 분산이 증가하고 통계량 (t , z ..) 이 감소하기 때문입니다. 
- 이러한 방식의 예시는 다음과 같습니다. 

> Capping

- 특정한 값 이상을 가지는 Metric 은 Outlier 취급을 하여 삭제하거나 다른 값으로 대체 

> Apply log

- log 변환 (x -> log(x+1)) 을 통하여 Skewed 된 분포를 조금 완화시킬 수 있습니다. 

> Change metric Aggregation level

- 메트릭의 집계 수준을 변화하는 방법입니다. 
- 이에 대해서는 . Li *et al.*, “Why Tenant-Randomized A/B Test is Challenging and Tenant-Pairing May Not Work.” 를 참고하세요

> ## Use Alternative Metric Type

- 일반적으로 A/B Metric 은 Randomized Unit 에 대해서 Average 를 합니다. 
  - 평균 앱 사용시간 등이 있습니다. 
- 하지만 다른 매트릭 타입을 사용하면 민감도를 높힐 수있습니다. 

> Proportion metics 

- 특정한 값에 대한 비율 메트릭을 사용하게 된다면 Sensitivity 를 높힐 수 있습니다.
  - 성공한 세션수의 비율 등이 있습니다. 

> Conditional Average metric 

- 이는 평균과 비슷하나, unit based 가 condition 되어있는 경우입니다. 
  - 예시로는 그냥 User 에 대한 평균 클릭 수 가 아니라, Active User 에 대한 평균 클릭 수 을 이용하는 경우입니다.
- Nemerate 와 Denominator 가 서로 관련있는 경우 Statistical Power 는 올라갈 것입니다 .
  - 위 예시에서 '그냥 유저' 를 분모로 하는 경우 Inactive user (가만히 있는 유저, 동영상 보는 유저..) 와 같은 경우에도 Sample 로 잡히게 됩니다.
  - 이러한 경우 , 이런 유저는 Treatment 가 효과가 있던 없건 , 클릭수가 발생하지 않기때문에 Noise 로 작용하게 됩니다.
  - 즉 Active user 라고 Conditional 을 줌으로서 좀 더 정밀한 측정이 가능해지는 것입니다. (Sensitivity 상승)

> ## Variance Reduction 

- CUPED (Controlled-experiment Using Pre-Experiment Data)  는 이전 실험 데이터를 이용하여 Test 의 분산을 감소시키는 방법 중 하나입니다.
  -  A. Deng, Y. Xu, R. Kohavi, and T. Walker, “Improving the sensitivity of online controlled experiments by utilizing pre-experiment data,”
- 이 효과성이 입증되었으며 , Microsoft 의 A/B Test 에서 널리 사용되고 있습니다. 
- Microsoft Teams 는 다양한 Metric 에 대하여 Variance Reduction 을 시도하였습니다.
  - Microsoft Teams 는 마침내 Log of Capped Time in Apps 를 Time in Apps 매트릭의 대안으로 삼아서 Sensitivity 를 상승시켰습니다. 
- 또한 A/B Test 시에 variance Reducttion 을 항상 수행한다고 합니다. 

---

**Reference**

- <https://www.microsoft.com/en-us/research/group/experimentation-platform-exp/articles/beyond-power-analysis-metric-sensitivity-in-a-b-tests/>
- <https://www.kdd.org/kdd2016/papers/files/adf0853-dengA.pdf>

실험을 하게되면 결국에 데이터는 쌓이게 되고, 이러한 데이터를 이용해 A/B Test 의 Metric 에 대해서 의미있는 평가를 할 수 있다는 부분은 정말 좋은 부분 같습니다. 또 더 마음에 들었던 부분은 쓸모없는 Metric 을 버리는게 아니라, sensitivity 를 높히는 여러가지 방법을 고안해서 살릴수도 있다는게 참 좋네요. 이러한 테크닉에 대한 논문이 Reference 에 많던데, 차근차근 하나씩 읽으면서 정리해야겠네요. 
{: .notice--success}

