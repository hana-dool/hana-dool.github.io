---
title:  "인과추론을 위한 연구 디자인"
excerpt: ""
categories:
  - Casual_Inference_Session2021
last_modified_at: 2021-12-20

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 Casual Inference 와 철학
{: .notice--warning}

> ## Causal Hierarchy

![jpg](/assets/images/Stat/134_1.jpg)

- 위의 그림은 인과추론의 레벨을 바탕으로 계층을 그린것
  - 가장 위에 있는것이 인과추론의 레벨이 가장 높다고 볼 수 있음
  - 아래로 갈수록 인과관계에 대한 신뢰와 증명이 어려워짐 

> Meta Analysis

- 맨 위의 meta analysis 는 단일 방법론이라기보다는 여러 인과추론의 결과를 종합적으로 분석하는 방법론
  - 여러 인과적 증거들을 종합하면 인과관계를 명확하게 알 수 있을것이므로 제일 수준이 높다고 할 수 있음
  - 다만 여러 인과적 증거를 종합하는거라 단일 방법이라고 하기는 어려움

> Randomized Experiment

- Potential Outcome Framework 에서 가장 수준이 높은 단일 방법론은 Radomized Experiment (RCT)

> Quasi - Experiment 

- 현실상황에서 Randomized Experiment 를 하기 힘든 경우가 많으므로, 실험과 매우 유사한 상황을 찾아서 분석하는 '준실험' 도 특정 가정 하에서는 Randmize Expreiment 와 비슷한 실험이 가능 

> Instrumental Variable

- 하지만 준실험(Quasi Exeriment) 이 불가능한 경우에도 있음

- 이럴때에 우리는 인위적인 도구를 활용할 수 있음. 그게 바로 도구변수 (instrumental Variable).

  -  도수변수는 인과추론을 방해하는 요인으로서 내생성을 이야기함. 내생성을 인위적으로 제거하기 위한 도구라고 이해하면 됨 

  - 이러한 도구변수를 항상 찾을 수 있는것은 아님 (이를 찾는것은 매우 어려움)

> Designed Regression

- Randomized Expreiment / Quasi - Experiment / Instrument Variable 도 찾기 어렵다면 인과추론을 포기해야 할까요? 
  - 이때에 적절한 통제변수의 디자인을 통해서 , Designed Regression 을 할 수 있을것. (모델은 일반적인 회귀분석 regression 이지만 어떤 통제 변수를 넣을지를 디자인 한다는 의미에서 Designed Regression 이라고 함) 
  - 이 경우에 Causal DIagram 이 매우 중요함

> Regression

- 이러한 통제변수에 대한 적절한 디자인이 없다면 (단순히 통제변수를 많이 포함한다고 해서 선택 편향을 없애는것은 매우 어려움) 
  - 그래서 모든변수를 단순히 활용하는 단순한 회귀는 제일 낮은 레벨 

> Descriptive Statistics 

- 그리고 제일 아랫단의 단순한 통계량 (평균, 중앙값 비교) 의 경우 결과에 영향을 미치는게 너무 많기떄문에 인과수준의 레벨에서는 너무나 낮음

---

**Reference**

- https://www.youtube.com/watch?v=HKpkgluQypA&list=PLKKkeayRo4PWyV8Gr-RcbWcis26ltIyMN&index=4

