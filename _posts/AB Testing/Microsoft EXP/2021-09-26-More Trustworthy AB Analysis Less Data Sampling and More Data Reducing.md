---
title:  "More Trustworthy A/B Analysis &#58; Less Data Sampling and More Data Reducing"
excerpt: "Microsoft Experimentation Platform 에서 추천하는 Data 줄이는 방법"
categories:
  - AB_Microsoft
last_modified_at: 2021-09-26

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 어떻게 하면 적은 데이터로도 신뢰있는 결과를 이끌어낼 수 있을지에 대해서 알아봅시다.
{: .notice--warning}

# [Less Data Sampling](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

![png](/assets/images/Stat/70_1.png)

- 위 그림처럼 일반적으로 A/B Testing 은 유저로부터 데이터를 모아서, 그 데이터를 적재한 후에 데이터를 이용해 A/B Testing 을 하게됩니다.
- 하지만 이러한 데이터 볼륨이 증가할수록 저장 및 계산 비용이 급증하게 됩니다. 
  - 또한 데이터 볼륨이 한계를 초과하면 시스템 에러가 날 수 있습니다. 
- 그러므로 데이터의 일부만 수집하여 데이터 볼륨을 줄일 수 있습니다.
  - 하지만 '어떻게 줄일 수 있을까요?'
- 여기에서는 데이터 축소에 대해서 다음과 같이 알아보려 합니다.
  - 부적절한 데이터 축소가 분석의 품질을 어떻게 낮추게 되는지 알아보자.
  - 분석의 품질을 유지하면서 데이터의 볼륨을 감소시키는 효율적인 방법을 알아보자.
  - 마이크로 소프트 팀의 경험을 바탕으로 추천하는 3가지 데이터 축소 전략을 알아보자.

> ## improper data reduction 

![png](/assets/images/Stat/70_2.png)

- 우리는 위처럼 로그 데이터를 나타낼수 있습니다. 
  - 각각의 Row 는 Individual User 를 나타냅니다. 
  - 각각의 Col 은 각 Event 에 대한 데이터를 나타냅니다.
    - 이떄에 각 이벤트란 페이지 로드 타임 , 등이 돌될 수 있습니다. 
- 만약 모든 데이터를 수집하고자 하자면 위의 모든 데이터를 이용하게 됩니다. 
- 하지만 우리는 데이터의 양이 너무 많아 Sampling 하고자 한다고 합니다. 
  - 샘플링은 데이터 볼륨을 줄이기 위해 유저의 일부만 사용하는것입니다. 

- 사람들은 대부분 위와 같은 Simple Random Sample 을 사용합니다.
  - 또는 Quata Sampling 을 이용하기도 합니다. 

> ## Simple Random Sampling

![png](/assets/images/Stat/70_3.png) 

- Simple Random Sampling 은 그저 랜덤하게 유저를 뽑아내는것을 말합니다.

> ## Quata Sampling 

- Quata Sampling 은 모집단이 갖는 특성에 대한 비율에 맞추어 표본을 추출하는 방법입니다. 
  - 예를 들면 성별 , 교육 수준과 같은 특성에 따라 적절하게 표본을 선택하는것을 말합니다.
  - 이 경우에 모집단의 특성을 정확하게 알아야하는 어려움이 따릅니다.

![png](/assets/images/Stat/70_4.png)

- 위 오른쪽 그림과 같이 Quata Sampling 을 할때에는 유저와 Event 에 대해서 기준을 설정할 수 있습니다. 
  - 각 기준에 따라서 Mutually exclusive 한 subgroup 으로 나눈 뒤에 각 subgroup 에서 원하는 비율만큼 sampling 을 하게 됩니다.
- User Based segmentation 의 경우 각 유저의 subgroup 은 위 그림의 색깔처럼 Segmentation 이 나뉩니다. 
  - 그 이후 66% 만큼 subgroup 에서 샘플링을 하게되면 왼쪽 그림처럼 샘플링이 됩니다. 
- Event Based Segmentation 의 경우 각  Event 의 Subgroup 은 색깔별로 나뉘게 됩니다. 
  - Event 1, 2 는 10% 만 Sampling 을 하고 3,4,5 의 경우에는 50% 를 샘플링 하였습니다. 
-  전체 Population 을 Event 에 대해서  mutually exclusive 하게 subgroup 으로 나눕니다.
  - 그 이후에 나눈 subgroup 에 대해서  각각 사전에 정한 비율만큼 Event 를 추출합니다. 

> ## Impact on Analysis

- 위와 같은 설계는 A/B Test 분석에 영향을 줄 수 있습니다. 
- Simple Random Sampling 은 Metric 의 Power 를 크게 손상시킬 수 있습니다. 
  - Metric 을 첫 실행 경험 으로 잡았다고 합시다.
  - 이 경우 신규 유저만 '첫 실행 경험' 이라는 데이터를 생성하게 되므로 매우 드문 Traffic 이 됩니다.
  - 즉, 전체 데이터를 사용해도 가뜩이나 데이터가 부족한데, Sampling 을 하게 되어서 더더욱 관련 메트릭의 값이 부족해지는것을 의미합니다. 
- Quata Sampling 에서는 Event 별로 다르게 수집되고 이는 편향을 일으킬 수 있습니다.
  - 예시로 어떤 이벤트의 80% 는 Desktop 에서 발생하고, 20% 는 모바일에서 발생한다고 합시다.
  - Data volume 을 줄이기 위하여 Desktop 은 25% 만 샘플링하고, 모바일은 100% 그대로 사용한다고 합시다. 
  - 하지만 이는 모바일 데이터를 과대추정하게 됩니다. 즉 Event Type 에 대해서 다른 비율로 수집하게 될 경우 특정한 모집단을 과대 / 과소 추정하는 Biased 를 일으킬 수 있다는 뜻입니다.

# [Practical design for data volume reduction](#link){: .btn .btn--primary}{: .align-center}

- 우리는 데이터 축소를 어떻게 해야되는지 단계별로 알아봅시다.

> Reconcile existing logging for importance and validity

- 각각 데이터에 대한 중요성이 다를 수 있습니다. 
  - 어떠한 데이터는 줄이기를 원치 않을 수 있습니다. (매우 Critical 한 실험 등)
- 그러므로 데이터에 대해 중요성을 매기고 Reduce 할것을 정하는것이 중욯ㅂ니다. 

> Choose between sampling or summarization to reduce data

- 사실 '데이터를 줄이는방법' 도 있지만 , Summarization 하는 방법도 있습니다. 
  - 요약하는 방법은 데이터에 대한 요약 통계량을 형성하는 방법입니다. 
    - 이 방법을 선택한다면, 이 이 뒤의 스텝은 건너뛰어도 됩니다.  
- 데이터를 줄이는 방법을 선택한다면 이 아래 Step 을 계속 진행해주세요 

> Choose the sampling unit

- 실험하고자 하는 Feature 가 일반적으로 User level 에서 Randomized 하게 노출된다고 합시다.
- 그러면 이런 경우 randomized Unit 인 유저 level 이상의 level 로 Sampling Unit 을 정하는것이 좋습니다.
  - 즉 유저 이상 (유저 혹은 집단단위) 으로 Sampling unit 을 설정하라는 이야기입니다.
- Ranomized unit 과 Sampling unit 이 일치하지 않는경우 분석이 매우 복잡해지기 떄문입니다.
  - 만약 Sampling unit 이 Session 처럼 하위레벨이 된다면 각 Data 는 Independence 를 위배하게 됩니다.

> Choose a sampling method

- 단순히 Simple Random Sampling 을 선택하는것이 편합니다.
  - 이 방법은 Metric 을 바꿀 필요가 없습니다.
- Quata Sampling 은 좀 더 유연합니다.
  - 하지만 metric 별로 각 비율을 결정하고 조절할 필요가 있습니다. (추가적인 작업...)
    - 많은 Sample size 를 요구하는 둔감한 Metric 의 경우 많은 데이터가 필요할것입니다.
- 비즈니스에서 요구하고자 하는 방법을 잘 이용하는게 중요합니다. 

> Estimate the sample rates

- Sampling 된 데이터는 매트릭별로 요구하는 Power 를 잘 만족하는지에 대해서 알아두어야 합니다.
- A/B Test 가 얼마나 수행되고 있고, 그에 따라 요구되는 Sample size 도 잘 파악해야 합니다.
  - 너무 적게 Sampling 하면 각 테스트의 품질은 떨어질것입니다. 
- 아마 low traffic 을 가지는 sample 에 대해서는 데이터를 더 Sampling 해야할 수 도 있습니다.
  - 위 예시에서처럼 '첫 실행 경험' 을 Metric 으로 삼는 특수한 메트릭이 있는경우에는 트래픽이 적은 신규 유저에 대해서는 높은 비율로 Samlpling 전략을 짜야할 수 있습니다.

> Test sampling validity

- Sampling 전략에 따라서 각 Segment 에 대한 영향을 과대  , 과소 평가할 수 있습니다.
  - biased 된 데이터에 대해 분석하게 되면 그 결과를 밎을 수 없게됩니다. 
- Biased 가 있는지 없는지를 알아보기 위해서는 counterfactual sampling 를 수행할 수 있습니다.
  - 그리고 sampled 된 데이터와 unsampled 된 데이터간의 차이를 평가할 수 있습니다. 
  - 이에 대해서는 뒤에 더 자세하게 알아보겠습니다. 

> Assess impact on STEDI of metrics

- Metric 의 Sensitivity, Trustworthiness, Efficiency, Debuggability and Interpretability 를 STEDI 라 합니다. 
- 메트릭들이 Sampling 된 데이터의 경우에도 위와 같은 성능이 잘 유지되는지 살펴보세요

> Re-randomize to avoid residual effects

- 유저가 점점 다양한 테스트에 노출될수록(residual effect) , 시간이 지날수록 유저의 구성은 달라집니다. 
- 그러므로 우리는 다시 randomizing 하고 샘플을 다시 선택하는것을 추천드립니다.

# [3 recommended data reduction strategies based on our learnings](#link){: .btn .btn--primary}{: .align-center}

- Data reduction 은 다양한 방법이 가능할것입니다.
- 우리는 Data reduction 을 위한 3가지 방법을 제안합니다. 

> ## Summarization

- 유저가 detailed 된 raw data 를 보내는것이 아니라 Summary 를 남기는것을 말합니다.
- HOw to? 
  - 클라이언트는 유저의 세션이 끝날때에 주기적으로 요약 데이터를 보냅니다. 
  - 설계시에 데이터를 어떻게 요약할것인지, 로그에 어떻게 표시할것인지 등을 고려해야합니다. 
  - 요약 데이터를 보내는 빈도는 어떻게 해야할지? 
- 장점은 메트릭 계산시 필요한 정보량을 잃지 않습니다. 
- 단점은 로그 계산이 제대로 이루어지는지 검사가 철저히 필요합니다. 
  - 또한 요약 데이터는 '사전에 요약하기로 정한 값' 에 대해서는 정보손실이 없지만 나머지 로그들을 통쨰로 없애므로 전체 이벤트에 대한 정보 손실이 있습니다.
  - 그래서 고급 분석이 제한될 수 있습니다.
    - 요약된 데이터만 보기 떄문에 , 남성만 Segmentation 해서 분석한다던지 다양한 Metric 을 시험하는 등의 분석이 제한적입니다. 

> ## Full Analysis Population 

- 중요한 Event 에 대해서는 모든 유저가 Metric 을 계산한 결과를 보내는 방법입니다.

![png](/assets/images/Stat/70_5.png)

- 이 전략은 Event 를 중요한 이벤트와 별로 중요하지 않은 이벤트로 나눕니다.
  - 중요한 Event 는Key metric 의 계산에 사용될것입니다. 
  - 중요하지 않은 Event 는 디버그 매트릭처럼 비교적 순위가 밀리는 MEtric 의 계산에 쓰입니다.
- 그 이후에 Full Analysis Popultation 을 정의합니다. 
  - 이 Population 에 속하는 유저는 Critical / Non Cretical Event 모두 대해서 로그를 보내게 됩니다.
  - 이 Population 은 A/B Test 에서 대부분의 분석을 합리적으로 수행할 수 있을만큼 커야합니다. 
- 위에서 Full analysis Population 을 이용해서 특정한 Event의 샘플사이즈가 적을 경우에는 위 오른쪽 그림의 빨간색 박스처럼 모든 user 를 이용하여 수집합니다.
  - 또한 Key metric 에 사용되는 Event 의 경우 모든 User 를 사용해서 수집합니다
- Full Analysis Population 은 이전의 전체 모집단의 특성과 일치해야 합니다.
  - 이는 counterfactual sampling 을 통해 체크할 수 있습니다. 
    - Control : Full Analysis Population , Treatment : 나머지 User 로 설정 후 두 차이를 검정하는 방법으로 체크합니다. 
  - 주기적으로 Full Analysis Population 을 Reset 하는것이 중요합니다.

> Pros

- 기본적으로 Simple Random Sampling 을 통하여 Full Analysis Population 을 형성하기 때문에 기존의 Metric 을 바꿀 필요가 없습니다. 

> Cons

- sampling Full Analysis Population 은 모든 Event Type 에 대해 로그를 남기게 됩니다.
  - 이는 다양한 Event 의 특징을 잘 잡지 못한다는 단점이 있습니다.
  - 모든 유저가 로그를 남기는 페이지 로드 시간은 Full Analaysis Population 이 작기를 원합니다.
  - 적은 유저가 로그를 남기는 구매율은 Full Analysis Population 이 크기를 원합니다. 

> ## Event Sampling Adjustment

- 이 방법은 각 Event 에 대해서 다른 비율의 Population 이 Sampling 됩니다. 

![png](/assets/images/Stat/70_5.png)

- 위처럼 매우 중요한 Metric 에 쓰이는 이벤트거나 많은 샘플이 필요한 경우 빨간색 박스처럼 전체 User 에 대해서 계산됩니다. 
- 이와 같이 Sampling 을 하는경우 이전에서도 언급하였듯이, Sampling rate 에 대한 Sampling Biased 를 늘 확인해야 합니다.

> Pros 

- 이 방법론은 각 이벤트별로 유연한 샘플링을 통해서 최적의 실험을 진행할 수 있는 장점이 있습니다. 

> Cons

- 하지만 이 경우 구현이 매우 복잡합니다. 
- 또한 다양한 Event 를 사용한 metric 의 경우 사용자가 섞여있기 떄문에 해석이 어렵습니다. 

# [Summary ](#link){: .btn .btn--primary}{: .align-center}

![png](/assets/images/Stat/70_6.png)

| Strategy                  | Pros                                                         | Cons                                                         |
| ------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Summarization             | – Little information loss. <br />– No impact on metric sensitivity. | – Need to change client code, validate the pipeline, and create metrics consuming new data format. <br />– The data size may be still large. <br />– The impact of data loss can be great. <br />– May have limitations with advanced analysis. |
| Full Analysis Population  | – No information loss for Critical Metrics. <br />– No need to adjust metric definition. | – Can greatly impact metric sensitivity if the size of the sample size for Full Analysis is small. <br />– Non-Critical Events are sampled at fixed rate.<br /> – When the second stage is needed, it takes time to run the additional A/B test. |
| Event Sampling Adjustment | – No information loss for Critical Metrics. <br />– Allow Non-Critical Events to get sampled at different rates. | – The logic to adjust user base in metric definition might be complicated and maintenance high. <br />– Can be hard to debug and interpret analysis results. |

---

**Reference**

- <https://www.microsoft.com/en-us/research/group/experimentation-platform-exp/articles/more-trustworthy-a-b-analysis-less-data-sampling-and-more-data-reducing/>

데이터 적재가 힘들만큼 큰 서비스 기업(구글같은) 이 아니면 데이터가 넘쳐서 힘들다는 말은 잘 안나올거같아서 이 방법론을 어디에 활용할 수 있을지는 모르겠네요. Historical Data 적재가 힘든 경우에는 그냥 Summarization 을 사용해서 Metric 에 대한 Raw Data 형식으로만 남겨도 좋을것같아요. 원본 log 데이터를 삭제하면 크게 용량이 줄겠죠. 그 밖에 Online 실험에서 실시간으로 오는 Log data는 적재가 힘들어서 Sampling 을 하는 경우는 거의 없어서 이 방법론을 잘 안쓰지 않을까요? 방법론 자체는 어느정도 흥미롭긴 했는데 , Event Sampling Adjustment 방법론은 너무 구현법이 귀찮고 안정성이 떨어져서 안쓸것같고, 그나마 Full Analysis Population 이 실제에서 쓰일만할것같아요.
{: .notice--success}

