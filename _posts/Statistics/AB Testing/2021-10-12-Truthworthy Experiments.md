---
title: "Patterns of Trustworthy Experimentation  &#58; Pre-Experiment Stage"
excerpt: "Truthworthy Experiment 를 위한 실험 전 세팅"
categories:
  - AB_Testing
last_modified_at: 2021-10-12

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 신뢰성 있는 실험을 하기 위하여, 실험 전에는 어떠한 세팅을 할 수 있는지에 대해서 알아봅시다.
{: .notice--warning}

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

- 신뢰할 수 있는(truth worthy) 데이터분석은 A/B Test 를 통해 비즈니스 결정을 내리는데에 매우 중요합니다.
- 실험 플랫폼을 출히한 이후, 14년 이상의 연구를 통하여 여러 Microsoft 제품에 대한 A/B Testing 을 진행하고, 확장하였습니다.
- 이러한 맥락 속에서 각 팀들이 요구하는 공통적인 요구사항은 바로 '신뢰성' 이였습니다.
- 실험 결과를 신뢰할 수 없으면 엔지니어링 , 분석의 노력들이 낭비가 되고, 조직은 실험에 대한 신뢰를 잃게 됩니다.
  - 그러므로 신뢰할 수 있는 실험을 만드는것은 이 업계에서 가장 큰 과제로 남아 있습니다. 
- 이러한 연구는 다양하게 이루어져 있습니다. 
  - broad overview of experimentation systems and challenges [1]–[3]
  - having a right overall evaluation criteria [4]–[8]
  - pitfalls in interpretation of experiment results [9],[10]
  - and designing metrics [7],[11].

- 이 시리즈에서 우리는 A/B Test 결과의 신뢰성을 높히기 위하여 Microsoft 에서 사용하는 실험 설계 및 분석 패턴을 공유합니다. 
- 이러한 process 는 실험 결과의 신뢰도에 영향을 끼치는 문제를 탐지하고, 예방하는데에 도움이 됩니다. 
- 결과적으로 Feature Team 은 관찰된 결과로부터 자신있게 decision 을 내릴 수 있고, 이로부터 향후 개발을 위해 학습할 수 있습니다.
- 우리는 이러한 A/B 실험의 사이클을 추적하고 관리하기 위하여 3가지 단계로 나눕니다. 
  - 사전 실험 단계
  - 실험 모니터링 및 분석 단계
  - 사후실험 단계 
- 이 포스팅에서는 사전 실험 단계에 초점을 맞추겠습니다.

![png](/assets/images/Stat/81_1.png)

# [Forming a Hypothesis and Selecting Users](#link){: .btn .btn--primary}{: .align-center}

> ## Formulate your Hypothesis and Success Metrics

- A/B 실험을 설계하는 첫 단계는 명확한 가설을 세우는것입니다. 
  - 이때에 가설은 Treatment 에 의해 발생되는 변화의 효과를 포함하고 간단해야 합니다. 
  - 만약 treament 가 여러 복잡한 변경을 포함하고 있다면, 각각을 break down 하여 간단한 개별 요소로 나누어 가설을 세우는것이 좋습니다.
- 또한 가설에는 제품에 도입된 변경사항(treatment) 이 미치는 영향을 측정하기 위한 metric 또한 포함하고 있어야 합니다. 
  - 한 예시로 "브랜드 효과가 높아질것이다." 와 같은 가설은 수치화 하여 측정할 수없기떄문에 이러한 가설은 안좋습니다.
- Treatment 의 효과를 정확하게 측정하려면 실험에 적합한 metric 을 선택하는것이 중요합니다.
- 또한 Core metric 에는 다음과 같은 메트릭이 있으며, 이 메트릭은 어떤 가설이던지 포함되는것이 좋습니다. (핵심적인 지표들이므로)
  - user satisfaction metric 
  - guardrail metric 
  - feature ans engagement metric 
  - data quality metric 
- 또한 가설을 설정할때 중요한 사항은 측정 metirc 의 예상되는 변화를 탐지하는 A/B TEst 의 power 입니다.
  - power analysis 를 통하여 필요한 트래픽의 하한을 설정하고, 우리 트래픽이 이러한 하한을 잘 만족하는지를 살피는게 중요합니다.

> ## Unit of randomization

- 여러가지 유형의 사용자 식별자 (id) 가 Unit of randomization 으로 사용됩니다.
  - 이떄에 우리 실험 환경에 어떤것이 가능하고 불가능한지를 잘 파악하는것이 중요합니다. 
- 아래는 Microsoft 에서 randomization unit 을 선택할때 사용하게 되는 세가지가 있습니다. 아래에서 알아봅시다.

> 1.Stability of the ID 

- Web 에서 사용자는 쿠키 기반의 id 를 사용하여 추적됩니다.
- 이러한 id 는 구현 및 추적이 쉽지만 안정적이지 않습니다. 
  - 쿠키를 지우고 다시 실험에 참가하게 된다면 , 다른 Varianct 에 할당될 수 있기 떄문입니다. 
- 그러므로 이러한 쿠키 ID 를 사용한다면, 모집단이 변동되지 않도록 단기적인 실험에만 사용하는것을 추천드립니다. 

> 2.Network Effect 

- 이 경우에는 Treatment 의 효과가 유저의 네트워크를 탁 서로 유저끼리 영향을 끼치는 경우에 일어나는 효과입니다.
- 이는 SUTVA 가정을 위배하게 됩니다. 

![png](/assets/images/Stat/80_2.png)

- 이를 위하여 위처럼 클러스터 수준에서 randomization unit 을 정하기도 합니다. 
  - 이렇게 cluster 수준에서의 randomization 은 단순 randomization unit 보다 훨씬 biased 되지 않은 estimation 을 내놓게 됩니다.

> 3.Enterprise Constraints

- 제약으로 인하여, randomization unit 의 선택에 제한이 있을 수 있습니다. 
- 그러므로 전체 enterprise 에 대하여 feature 가 적용될 수 있습니다. 
- 이러한 경우 사용자별 randomization 으 불가능하고, enterprise level 에서의 randomization 이 가능합니다.
  - 이에 대해서는 특별한 고려사항이 있습니다.
  - Enterprise-Level Controlled Experiments at Scale: Challenges and Solutions 참고
- 위와 같이 A/B Testing 을 위한 radnomization 에 유의합니다. 
  - 우리는 모든 feature 를 늘 같은 randomization unit 으로 실험할 수 없습니다. 
  - 가설에 따라 다양한 identifier 를 이용하여 randomization 을 유연하게 선택해야할 것입니다.

> ## Check and Account for Pre-Experiment Bias

- 우리는 최근의 한 실험에서 Edge 브라우저에 대한 새롱운 feature 를 테스트 하였습니다. 
  - 이 기능은 일부 데이터가 내부적으로 저장되는 형식을 변경하는것이라 유저에게는 아무 영향이 없을것이라 예상되었습니다. 
- 하지만 실험 결과 user engagement metric 이 p-value 0.01 로 통계적으로 유의한 감소가 나타났습니다.
  - 하지만 이러한 저하를 설명할만한 다른 metric 의 경우에는 움직임이 없었습니다. 
- 이러한 경우에는 이러한 metric 의 이동이 단순한 False Positive 라고 어떻게 확신할 수 있을까요? 
  - 재실행은 확실한 방법중 하나이지만 시간이 너무 오래 걸리며, 때로는 불가능할 수도 있습니다. 
- 과거 데이터는 실험 전에 이러한 biased 를 탐지하고 완화하는데에 매우 유용한것으로 밝혀졌습니다. 다음 3가지는 Microsoft 에서 사용하는 세가지 방법입니다.

> 1.Retrospective-AA Analysis

- 이 방법은 실험이 시작되기 전 기간에 대해서 Treatment , control group 에 대하여 동일한 메트릭을 계산해 봅니다. 
- 이러한 방법으로 metric 의 Treatment 와 Control 그룹간에 어떠한 편향이 있었는지 없었는지를 확인하게 됩니다.
- 만일 이러한 Retro A/A 분석에서 메트릭의 Statistically Significant Movement 를 발견하는 경우에 우리는 Randomization 으로 이러한 잘못된 False positive 가 발생한다고 예측할 수 있습니다. 
  - 위와 같은 예시에서 User engagement metric 이 Retrospective AA Test 에서 통계적으로 유의한 움직임을 보였다면 우리는 위 실험이 False Positive 라고 확신을 가질 수 있습니다. 
- 이러한 Retrospective AA Test 는 무작위화로 인한 metric 의 bias 를 검정하는 결정적인 테스트는 아니지만, 별다른 방법론이 없을떄에 매우 유용한 방법론입니다.

> 2.Seed Finder

- Retrospective A-A Analysis 는 A/B Test 결과에서 False Positive 를 식별하는데에 도움을 줍니다다만 이는 bias 를 식별하는데에 뒤떨어진 방법론입니다. 
  - 실험을 시작하기 전에 이러한 bias 를 가질 가능성을 어떻게 줄일 수 있을까요? 이는 Seedfinder 를 통해 가능합니다. 
- 일반적으로 A/B Test 실험의 경우 해싷함수와 시드를 사용하여 실험자를 Control 과 Treatment 로 할당합니다. 
- 실험을 시작하기 전에 Seedfnider 를 사용하여 많은 시드에 대해 Contol / Treatment 를 나누고 이 샘플에 대하여 metric 의 유의성을 검정한 metric set 를 구성합니다. 
  - 그 이후에 유의한 metric 차이를 가장 적게 관찰하게 되는 최적의 시드를 선택합니다. 
  - 우리는 몇백개의 시드를 생성하는것을 제안하지만 이는 product 와 고른 metric 에 따라서 달라질 수 있습니다. 
- 이러한 재 randomization 은 treatment 의 효과와 무관한 metric 의 노이즈를 줄이고 treatment 효과의 정밀도를 향상시킵니다.
-  random 을 했지만 Control 과 Treatment 의 유저의 특성이 다르게 할당될 수 있기 떄문에 '랜덤을 정할때' 유저가 잘 나뉘도록 Random 을 잘 구성하는 방법론입니다. 
  - '잘 나누어 졌느냐?' 는 metric 이 통계적으로 차이가 없는지를 통하여 검정하게 되고, 이러한이유로 'metric' 차이를 가장 적게 관찰하게 되는 seed 로 구성하는 것입니다.

> 3.Variance Reduction

- 이 방법은 metric 의 Sensitivity 를 높히는 분산 감소 방법입니다.
- 이 기법은 Noise 가 많고, Outlier 가 많아 sensitivty 하지 못한 여러 metric 에 대해서 적용되었습니다. 

<br>

- 일반적으로 위의 세가지 방법을 모두 사용하여 실험의 신뢰성을 올리기를 권장합니다. 

1. Seedfinder 를 이용하여 실험기간동안 주요 메트릭의 편향이 없는 좋은 무작위 seed 를 찾습니다. 
2. VR 을 통하여 메트릭의 민감도를 높힙니다.
3. Retropective AA 를 통하여 Seedfinder 로 최적화되지 않았던 다른 metric 의 이동을 조사해봅니다.

# [Pre-Experiment Engineering Design Plan](#link){: .btn .btn--primary}{: .align-center}

- 다음은 실험의 신뢰성을 높히기 위하여 Microsoft 에서 사용되는 몇가지 엔지니어링 과정에 대해서 알아보겠습니다.

> ## Set up Counterfactual logging

- A/B TEst 를 실행할때에 variants 에 속하는 모든 사용자가 treatment 에 노출되지는 않습니다. 
  - 특정한 featrure 를 업데이트 한 경우에는 특정한 의도 / 행동을 한 사람들만을 대상으로 하게 됩니다. 
  - 예시로 날씨 예보에 대한 답을 추가하는 A/B Testing 을 실행할때에, 이는 오로지 날씨 관련 검색을 하는 사람에게만 Treatment 가 적용되므로, 전체적으로 테스트할때에 의미있는 움직임을 감지할 수 없었습니다. 
  - 즉, 사용자의 대부분은(날씨 검색을 하지 않은) 노이즈로만 작용하여 테스트에서 의미있는 metric 의 움직임을 보지 못한것입니다. 
- 우리에게 필요한것은 날씨 관련 검색을 한 사용자로 zoom in 하는것이 중요합니다.
  - 하지만 어떻게 이러한 사용자로 확대할 수 있을까요? 
  - 날씨 답변 요청을 받게되면 그때, Treatment 에 속하는 유저였다면 날씨 관련 답변을 하고 , 그렇지 않으면(control 에 속하면) 답을 하지 않습니다. 그리고 이렇게 요청을 받게 된 유저는 마크를 해 놓습니다.
- 마크를 한 유저에 대해서만 제한하여 살펴본다면, 이는 'Treatment 에 대해서 영향받는 유저' 만 집어서 확인할 수 있으므로 Sensitivity 가 올라가게 됩니다.
- 이때 이러한 zoom in 으로 인해 누락되는 사용자가 없게 하기 위하여 SRM 을 확인하는것도 좋은 방법입니다.
- 이것을 구현할때에, 시스템상 지연을 야기할수도 있으므로 , 최적화 방법을 통하여 잘 구현해야 합니다. (여기는 시스템 얘기라 무슨소리인지 모르겠음.. ㅜㅜ )

> ## Have Custom Control and Standard Control

- Microsoft 의 Featrue Team 은 custom comtrol 을 만들어야할 때가 있습니다. (custom control 은 이전 날씨를 검색한 유저로 control 을 한정했던것과 같이, 유저를 Treatment 의 영향을 받는 범위로 좁히는 등의 'Custom' 처리를 한 control 집단)

  - 하지만 Treatment 의 효과를 평가하기 위하여 custom control 에만 의존하는것은 untruthworthy 한 결과를 불러들일 수 있습니다. 

- Microsoft News 는 페이지의 UI 에 사소한 변화를 주는 실험을 구성하였습니다 

  - 에러가 발생하여 (Custom)Control 과 Treatment 에 대해서 검색 상자가 없어졌습니다. 

  - 이로 인하여 사용자의 경험에 큰 영향을 미쳤습니다. 

- 하지만 이 경우에 Treatment 와 Conrtrol 모두에게 영향을 끼쳤기 떄문에, Treatment 와 Control 을 비교할때에 감지해낼만한 변화가 없었습니다. 

  - 이러한 변화는 production user (standard control) 과 비교될떄에만 감지되었던 차이였습니다. 
  - 이러한 Standard control 의 유저는 Experiemtn 의 어떠한 코드에도 영향을 받지 않았기 떄문입니다.

- 이제 우리가 추가한 코드에 영향을 받는 custom control 과 standard control 을 비교하여 metric 이 큰 이동을 일으키는지 아닌지를 테스트할 수 있습니다.

  - 이를 이용하면 custom control 에 큰 문제가 있음을 알 수 있고 더이상 피해를 주지 않고 신속히 실험을 종료할 수 있습니다. 

- 모든 규모의 실험에서 , 이러한 standard control 을 구현하는것은 쉬운일이 아닙니다. 

  - 상당한 양의 트래픽을 격리된 상태로 (code 의 영향을 받지 않게) 유지해야 하며, 각 실험의 트레픽 설정을 고려하여 사이즈를 고려해야 합니다.

> ## Review Engineering Design Choices to Avoid Bias

- 이 부분은 너무나 시스템적인 부분이라 Pass.... 

# [Pre-Validation by Progressing Through Populations](#link){: .btn .btn--primary}{: .align-center}

- 제품에 대한 모든 Treatment 는 사용자에게 노출되기 전에 이중 / 삼중으로 체크를 하게 됩니다. 
  - 하지만 여전히 이러한 change 에 대한 불확실성은 존재합니다. 
- 실험에 유저가 많이 포함될수록 실험의 불확실성을 줄일 수 있으나, 잘못된 Treatment 일 경우, risk 가 커지기 떄문에 이러한 Treatment 의 배포에 있어서는 rist 와 uncertainty 간의 Trade off 가 있다고 할 수 있습니다.
- 많은 사용자에게 Treatment 배포
  - 장점 : treatment 의 효과를 정확하게 측정할 수 있음
  - 단점 : 많은 사용자에게 안좋은 Treatment 를 적용하게 되면 큰 손해를 불러일으킴
- 적은 사용자에게 Treatment 배포
  - 장점 : treatment 가 안좋을지라도, 적용되는 사용자 수가 적으므로 손해가 작음
  - 단점 : Treatment 의 효과를 정확히 측정할 수 없음
- 이러한 Trade off 를 잘 조절하는 방법은 user population 에 대해서 점진적으로 treatment 의 할당 비율을 증가시키는 것입니다.
  - 실험 설계상 10% 까지 treatment 를 적용하고자 했으면 1% -> 2% ..... 10% 로 증가시킴

> ## Gradual Rollout Across Differenct User Population

- 큰 모집단에게 실험하기 전에 특수한 사용자 집단에 대해서 변화를 실험하는 것입니다. 
- 예시로 베타 사용자 집단에 대해서 Treatment 를 적용하는것입니다. 
  - 이러한 Subset 모집단에게 Treatment 를 실험하였을때에 사용자 경험에 안좋은 변화를 주게 된다면 , 전체 population 에 대해서도 안좋은 영향을 줄 확률이 높습니다. 

> ## Gradual Rollout within a User Population

- 일반적인 user population 에게 실험을 하기로 결정하게 되는 경우, 모집단의 일부에게만 노출하면서 점진적으로 높혀나가는 방법이 있습니다.
  - 먼저 트래픽의 1% 에 treatment 를 노출하고 , 5% , 10% 이런식으로 원하는 트래픽까지 점진적으로 높힐 수 있습니다.
- 이러한 ramp up 단계에서 , treatment 에 할당되는 유저수가 많아지고, treatment 의 효과에 대한 power 가 증가하여 예상치 못한 사용자 경험 감소를 잡아낼 수 있을것입니다. 
  - 이렇게 Treatment 를 점진적으로 적용하는 단계를 통하여 User 의 경험에 불필요한 해를 미치지 않을 수 있습니다.

**reference**

- <https://www.microsoft.com/en-us/research/group/experimentation-platform-exp/articles/patterns-of-trustworthy-experimentation-pre-experiment-stage/>

 실험의 신뢰성을 높히기 위하여 어떻게 행동할지에 대한 Article 입니다.
{: .notice--success}

