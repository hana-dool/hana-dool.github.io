---
title: "Principles for the Design of Online A/B Metrics"
excerpt: "Bing 의 Metric Design 을 할 떄의 원칙에 대한 논문"
categories:
  - AB_Testing
last_modified_at: 2021-10-09

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 이 논문에서는 A/B Testing 에서 Metric 의 설계 원칙을 설명합니다. 실험을 설계할때에 나타나는 몇개의 문제점을 공유하고 이러한 함정을 피하기 위한 해결책을 공유하려 합니다.
{: .notice--warning}

# [Principles for the Design](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction 

- A/B 테스팅은 데이터를 기반으로 올바른 결정을 하게 해준다는 점에서 매우 중요합니다. 
- 이떄에 A/B Testing 은 '정해진 metric' 의 행동을 살펴보면서 결정을 내린다는 점에서 좋은 Metric 은 매우 중요합니다. 
  - 우리는 잘못된 metric 선정으로 인하여, 잘못된 결정을 하는 경우가 흔합니다. 
  - 그러므로 expressive / robust / trushworthy 한 metric 을 설계하는것이 중요합니다. 
- 이 논문에서 우리는 Bing.com 을 위한 A/B Testing metric 을 설계하면서 배운 몇가지 교휸을 공유하려고 합니다. 
  - 온라인 A/B Testing metric 을 설계할떄에 고려해야 할 많은 측면에 대해서 설명할 것입니다. 

> ## 1. THE A/B METRIC PROBLEM

- A/B Testing 에서는 특히 OEC(Overall Evaluation Criterion) 을 살펴보게 됩니다. 
  - 이 OEC 는 Treatment 가 좋은지 Contol 이 더 좋은지에 대해서 알려주게 됩니다. 
  - 웹 search 서비스 입장에서 보자면, 이러한 OEC 를 이용하여 사용자가 만족된 경험을 하였는지 아닌지에 대해서 살펴보게 됩니다.
- 이렇게 중요한 A/B metric 을 설계할떄에 드는 의문이 있습니다. "어떻게 하면 좋은 metric 을 고를 수 있을까요? "
- 전통적으로 이러한 문제는 prediction problem 으로 여겨졌습니다.
  - 즉 , 유저에 대한 로그 데이터와, 유저에 대한 true label 을 설정합니다. 
  - 그 이후에 true label 를 예측하는 모델들을 구성한 뒤에 recall / precision 등의 입장에서 제일 좋은 모델을 선택합니다 
  - 그리고 최고의 predictor 가 , 최고의 A/B metric 이 될 것이라는 것입니다. 
- 물론 위와 같은 방법은 처음 A/B Testing 의 metric 을 설계할때에는 합리적인듯 보이지만, 결함이 있는 metric 을 설계하게 될 가능성이 있습니다. 이유는 다음과 같습니다 .

> change 에 대해서 blind

- metric 을 설계할때에는 Treatment 의 변화를 효과적으로 감지하고 민감해야 합니다. 
- 아무리 우수한 predictor 라 하더라도, 특정 유저에 대해서 A/B 차이를 측정하는데에 실패할 수 있습니다.
- 또한 모델링시에 predicto 의 과적합을 피하기 위해 제거될 수 있습니다.  
- 또한 매우 드문 사용패턴의 경우, 과

**Reference**

- <https://www.microsoft.com/en-us/research/group/experimentation-platform-exp/articles/patterns-of-trustworthy-experimentation-during-experiment-stage/>

Alert 시스템을 어떻게 구성했는지에 대해서 말해주는 좋은 Article 이였던것 같습니다. 다만 False Positive 문제때문에 p-value 를 거의 0.001 수준으로 설정해야할것 같은데, 이것을 어떻게 잘 ㅈ절하는 방법이 있는지는 더 찾아봐야 겠네요. (Reference 링크에 들어가면 더 많이 나오기는 하는데.. 논문 타고타고 읽을것이 너무 많네요...... 시간은 없고... ) 
{: .notice--success}

