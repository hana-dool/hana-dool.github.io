---
title: "Key Platform Features for Trustworthy A/B-testing (2018)"
excerpt: "A/B Testing 설계에서의 Key Platform Features"
categories:
  - AB_Paper
last_modified_at: 2021-10-16

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 비록 학사 논문이지만, 그 수준이나 연구 내용이 매우 광범위하고 깊어서 리뷰해 보았습니다.  
{: .notice--warning}

# [Trustworthy Principles in Experiments](#link){: .btn .btn--primary}{: .align-center}

> ## Experiments Phase

- 많은 문헌의 연구로부터 세가지 실험 단계들을 확립할 수 있었습니다. 

![png](/assets/images/Stat/83_1.png)

- 그 순서도는 위와 같습니다. 설계단계 / 실행단계 / 분석단계 입니다. 
- 신뢰성있는 실험을 위해서라면 각 단계에서 어떤일을 할 수 있을지에 대해서 알아보겠습니다. 

> ## Experimentation Design Phase

- 첫번쨰 단계는 실험의 설계 단계입니다. 
  - 이 단계에서는 Treatment variation 이 디자인되고, metric 을 결정하며 sample size 가 결정하는 단계입니다. 
- 이 단계내에서 살펴봐야 할 것들은 다음과 같습니다. 

> Hypothesis given upfront

- 누구에게 실험을 하고, 언제 하는지, 어떤것을 실허마는지 등의 '구체적인 가설을 결정' 해야 한다는 것입니다. 
  - 이는 '가설을 먼저 결정' 해야 그 뒤에 이 가설에 맞는 metric 을 적절히 선택할 수 있기 때문입니다. 
- 나이브하게  실험에서 어떤것을 볼지와 상관 없이 중요해보이는 (클릭당 세션 수 등) 만 선택하는것은 실험의 품질을 낮춥니다.

> Correct Sample SIze 

- 올바른 표본 크기를 설정해야만 합니다. 
- 표본 크기가 크면 클수록 메트릭에 대한 Power 가 커집니다. 다만 너무 크기만 하면 많은 실험을 진행할 수 없습니다.
- 즉 적절한 표본 크기를 선정하는것이 중요합니다. 

> Reliable experiment users

- 특정한 Experiment System 은 'Bucket System' 을 이용합니다. 
  - 즉 사용자를 버킷으로 나누어 실험에 각 버킷을 할당하는 구조입니다 
- 하지만 이렇게 된다면, 이는 carryover effect 를 일으킬 수 있는 다음 실험에 사용될 수 있습니다. 
  - 이러한 연속 실험에서, 두 실험이 큰 상호작용을 일으키는 경우라면 문제가 될 수 있습니다. 
- Ex) 버킷1 , 버킷2 의 사용자를 '빨간 배경' 이라는 Treatment 에 적용하였다고 합시다. 이 실험이 끝난 이후 이 버켓을 모두 후속 실험인 '빨간 버튼' 이라는 실험에 넣었다고 합시다. 이때에 '빨간색에 익숙해진 사용자' (Carry over effect) 로 인하여 실험의 결과가 왜곡될 수 있습니다.

> ## Experimentation Execution Phase

- 이제 실험의 적용 단계에서는 이미 metric 은 결정되었고 실험이 진행중이라 합시다. 
- 이 단계에서는 Control / Treatment 간의 metric 값들이 계속 기록됩니다. 
- 이 떄에 실험이 잘못된 경우 실험을 중단할 수 있습니다. 

> Variation assignment monitoring

- 실험이 2개가 진행될 경우 50% / 50% 를 분할해야 하는것처럼 이러한 Sample 분할은 정확해야 합니다. 
- 신뢰할 수 있는 실험을 위해서라면 이러한 '정확한 분할' 이 잘 일어나고 있는지를 잘 감시하는게 중요하며 치우치면 안됩니다. 
- 이는 늘 사용자에 대해서 모니터링 되어야 하며, 변동이 과한 경우 심하면 실험을 중단해야 합니다.

> Error Detection 

- 실험 실행 단계에서, 메트릭과 변수에 대한 많은 데이터가 수집됩니다. 
- 하지만 일부 에러에 의하여 데이터가 손실되거나 (사용자의 연결 끊김으로 인한 Nan) 부정확한 결과가 나올 수 있습니다.
- 이러한 데이터를 식별할 수 있는 메커니즘을 구성하는것이 중요합니다. 

> Metric monitoring

- 실험의 Metric 을 지속적으로 모니터링하는것도 중요합니다. 
- Guardrail Metric 이 지나치게 안좋아진다거나, 있을 수 없는 움직임이 있는 등의 경우 즉각적으로 중단하거나 점검하는것이 필요합니다. 
- 또는 Guardrail metric 뿐만 아니라 Metric 이동 자체가 불가능한 경우에도 Detection 을 꾸준히 하는것이 좋습니다. 

> ## Experimentation Analysis Phase

- 이 단계에서는 주요 Metric 이 기록되었고, 실험이 중단된 단계에서의 결과 분석과 평가 단계입니다. 

> High Quality Data

- 데이터가 '좋은 품질' 로 잘 모아졌는지를 검사합니다.
- 이 경우에는 주로 SRM 을 사용합니다. 

> Presentation and Feedback 

- 실험 플랫폼에서의 실행 결과에 대해서 평가되고, 분석되어야 합니다.
- 만일 문제가 있었던 경우, 이는 Expereiment 하는 사람에게 피드백으로 제공되어야 합니다. 

> Use of correct statistical method

- 정확한 통계적 방법론을 이용하여 해석해야 합니다. 
  - 이는 metric 의 Type (conversion / continuous) 에 따라서 달라질 수 있습니다. 
- Treatment 와 Control 의 차이를 측정하기 위한 많은 방법 (T-test / Delta Method) 이 있으므로 올바른 방법을 사용하는것이 중요합니다.

![png](/assets/images/Stat/83_2.png)

# [Trustworthy Principles in Flatform Feature](#link){: .btn .btn--primary}{: .align-center}

- 이 경우에는 A/B Testing 의 신뢰성을 위하여 구현되는 플랫폼 기능에 대해서 알아보려 합니다.

> ## Flatform Features

> A/A Tests

- AA 테스트는 Experimental Sysytem 이 잘 작동하는지에 대해 체크하기 위해 사용합니다.
- 또는 이전 실험의 Carry over effect 가 있는지 없는지에 대해서 확인하는데에도 사용할 수도 있습니다.
  - R Kohavi et al “Trustworthy Online Controlled Experiments: Five Puzzling Outcomes Explained”.

> Power Analysis 

- Power Analysis 는 minimal samplesize 를 계산하기 위해 필요한 기능입니다. 
- 이를 통하여 duration 을 결정하거나 , control / Treatment 에 대한 traffic 비율을 결정할 수 있습니다.

> SRM - Test

- SRM 은 Split 이 잘 이루어졌는지를 감시하는 테스트입니다.

> Outlier Filtering

- 메트릭이 특이치가 있는 경우, 이러한 지표는 Control 과 Treatment 의 효과를 제대로 해석하는데에 어려움을 줍니다.
- 예를 들어 아마존은 한 사용자가 엄청난 수의 책을 주문했다는것을 알았고, 이는 도서관 계정에서 나온것으로 밝혀졌습니다.
  - 이러한 사용자가 어느곳 (Control or Treatment) 에 할당되느냐에 따라서 전체 검정 결과를 왜곡할 수 있습니다. 
- 그러므로 신뢰성 있는 결과를 얻기 위해서라면 이러한 특이치를 필터링할 수 있는 기능이 필요합니다.

> Randomization algorithm

- 무작위 알고리즘은 매우 중요합니다.
- 사용자를 Treatment 와 Control 로, 어떠한 bias 없이 잘 나누어야 합니다.

> Alerting / Near real-time Alerting

- Experiment 가 실행이후 / 실행도중 metric 에 대한 부정적인 움직임이 있으면 알람을 보내는 기능이 있어야 합니다.
- 또는 이를 잘 캐치할 수 있도록 실험자에게 별도의 경고를 보낼 수 있어야합니다.

> Auto Shutdown

- 중요한 Metric 이 갑자기 매우 감소할경우, 자동으로 실험을 중단할 수 있는 시스템을 만들어야 합니다. 
- 왜냐하면 모든 실험을 실험자가 맨날 감시할 수 없기 떄문입니다.

> Accurate Peeking 

- 우리는 실험의 peeking 의 경우 심하면 문제가 될 수 있습니다. 
- 그러므로 플랫폼이 실험자에게 이러한 성급한 결정을 내리지 않도록 안내하는것이 매우 중요합니다. 

> Interaction detection

- 사용자가 여러 실험에 탐지하는 경우도 있습니다. 
- 사용자가 상관관계가 있는 두개 이상에 참가하는 경우, 일부 실험 조합은 사용자에게 해를 입히고 결과를 왜곡할 수 있습니다. 
  - 빨간색 글씨를 적용하는 실험과 빨간색 배경을 적용하는 실험 2개가 같이 적용되면 그 사용자는 매우 끔찍한 경험을 하게 될 것입니다. (실험간의 상호작용으로 사용자가 끔찍한 경험을 하게됨)
- 이 기능은 이러한 상호작용을 탐지하고 실험자에게 경고하게 됩니다. 

> Analytic presentation

- 이러한 결과를 분석하고 정확하게 제시하ㅡㄴ 기능이 있습니다. 

> Conditional Trigerring 

- Online Controlled Experiment 에서 수집된 데이터는 그 변동성이 매우 큰 경우가 있습니다. 
- 즉 이러한 '소음' 을 분리할 수 있는 기능이 필요합니다.
  - 만일 'Help' 메뉴에 대해서 Treatment 를 적용할 경우에 Help 메뉴를 이용하지 않은 사람은 단순히 소음으로 작용합니다. 그러므로 help 메뉴를 이용한 사람만으로 Population 을 제한해야 합니다.

> Missing data detection

- 예를 들어 Wifi 를 통해 전송되는 데이터는 항상 손실되는 위험이 있습니다.
- 만약 Control 이나 Treatment 한쪽에서 데이터 손실이 크다면, 이러한 imbalance 는 실험의 유의성에 영향을 끼치므로 이를 탐지하는 기능이필요합니다.

> Novelty and primacy effect detection

- Novelty 나 primacy effect 는 실험에 영향을 끼칠 수 있습니다. 
  - 이러한 영향이 있는 경우에 대해서 detection 할 수 있는 기능이 필요할 수 있씁니다. 

> Use correct statistical test

- 정확한 통계적 방법론을 사용해야하는것은 물론 말할 필요가 없겠죠? 

> Heterogeneous treatment effect detection

- 이질적인 치료 효과는 특정 사용자 그룹에게 적용한 결과가 다를때에 사용합니다. 
- 예를 들어 추가된 기능은 웹 브라우저 A를 사용하는 사용자에게 긍정적인 영향을 미칠 수 있지만 브라우저 B를 사용하는 사용자에게 부정적인 영향을 미칠 수 있습니다. 
- 평균적으로는 좋을 수 있지만, 이러한 Feature 가 적용되면 브라우저 B를 사용하는 사용자에게 부정적인 영향을 미칩니다.
- 즉  이질적인 치료 효과를 감지하여 실험자에게 알려주는 기능이 필요합니다.

![png](/assets/images/Stat/83_3.png)

# [Mapping of Trustworthy Principles to Platform Features](#link){: .btn .btn--primary}{: .align-center}

- 이전에서는 신뢰할 수 있는 실험을 위한 원칙(principles) 과 플랫폼 특징을살펴보았습니다. 
- 여기에서는 그러한 원칙과 플랫폼 기능 (features) 이 어떻게 관련되어 있을 수 있는지에 대해서 알아보겠습니다.

![png](/assets/images/Stat/83_2.png)

![png](/assets/images/Stat/83_3.png)

> ## Mapping 

- 위 매핑에 대한 자세한 설명은 "Key Platform Features for Trustworthy A/B-testing" (reference) 를 참고하시면 됩니다. 
  - 여기는 사실 짝지어서 설명할뿐이라 생략하였습니다.

![png](/assets/images/Stat/83_4.png)

# [Platform Evaluation](#link){: .btn .btn--primary}{: .align-center}

- 많은 회사들이 자체 플랫폼을 개발했습니다만, 상용 및 오픈소수 모두에서 A/B Test 에 사용할 수 있는 플랫폼이 많이 있습니다.
- 여기에서는 Optimezly 와 VWO(Visual Website Optimizer) 두 플랫폼에 구현되어있는 기능에 대한 비교 / 정보를 제공하려 합니다. 
- ● 는 현재 그러한 기능을 사용할 수 있음을 의미합니다.
- ✖ 는 현재 그러한 기능을 사용할 수 없음을 의미합니다.
- ▲는 현재 그러한 기능을 부분적으로만 사용할 수 있음을 의미합니다.

> ## Optimizely

- Optimzely 는 large - scale commercial experimentation software 를 제공합니다. 
- market 에서 가장 인기있는 A/B TEst 플랫폼중 하나인 Optimizely X 를 개발하였습니다. 
  - 이는 A/B Test 및 MVT (3가지 이상의 변형) 을 위한 도구도 포함되어 있습니다. 

> ## VWO

- Visual Website Optimizer (VWO) 는 소프트웨어 개발 업체인 Wingify 의 제품중 하나입니다.
- A/B 테스트의 두가지 플랫폼인 VWO  Conversion Optimization Platform 과 VWO Testing Platform 을 운영합니다.
- 웹과 모바일 장치에 대해서 A/B Test 및 MVT 를 제공합니다. 

> ## Evaluation

- Optimizely 와 VWO 에 대해서, 우리가 진행했던 기능들에 대해서 얼마나 구현되어있는지에 대해서 평가를 진행해 보았습니다.

![png](/assets/images/Stat/83_5.png)

**reference**

- <http://ls00012.mah.se/bitstream/handle/2043/28349/Olle%20Caspersson.pdf?sequence=1&isAllowed=y>

 분명 그 깊이는 한계가 있지만, 광범위하게 A/B Testing 을 조사하고, 인터뷰까지 진행한 논문이라 리뷰해 보았습니다. 이 기능들을 모두 적용할 수 있다면 정말 좋은 플랫폼이 되겠네요! 한국은 아직 갈 길이 먼듯.... 
{: .notice--success}

