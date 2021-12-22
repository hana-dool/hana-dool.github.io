---
title:  "잠재적결과에 대한 프레임워크 (Potential Outcomes Frameworks)"
excerpt: ""
categories:
  - Casual_Inference_Session2021
last_modified_at: 2021-12-20

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Casual Inference 와 철학
{: .notice--warning}

> ## Causal Mindset

- 중요한것은 potential outcome framwork 하에서 인과 관계에 대한 마인드셋과 research design 에 대해서 알아가는것이 중요!

> ## Design-Based Approach Causation

- potential Outcomes Framworks 는 도널드 루빈이 만들어서 Rubin Causal model 이라고도 함 

"Without treatment definitions that specify actions to be performed on experimental units, we cannot unambiguously define causal effects of treatments." (Rubin 1978, p. 39)
{: .notice}

- 논문에서 실제 연구 대상에 행해질 수 있는 구체적인 Treatment 를 정의할 수 없다면, 그것의 인과적인 효과도 측정할 수 없다고 주장하고 있음
- 이러한 주장은 바로 Design Based Appraoch 의 핵심을 가지고 있음! 
- 즉 기본적으로 인위적으로 디자인될 수 있고, 그렇게 함으로서 연구 대상에 대한 조정과 intervension (개입)이 가능한 treatment 에 대해서 인과관계를 정의하고 측정할 수 있다고 보는 관점이 바로 Design Based Approach ! 

Researchers will be "successful at identifying the causal effect not because of the complex statistical methods that are applied to the data, but due to the effort in developing a design before data are collected." (Keele 2015, p. 331)
{: .notice}

- 즉 이러한 측면에서 research design 이 중요할수밖에 없는데, 논문에서 저자가 주장하는것처럼 potential outcome framework 하에서는 인과 추론을 위해 필요한건 빅데이터나 복잡한 통계 모형이아니라 더 중요한건 데이터를 모으기 전에 연구자가 얼마나 적절한 연구 디자인을 고안했는지 여부가 바로 인과 추론의 Quality 를 결정하는 요인이라고 말하고 있음
  - 이러한 관점도  design based appraoch 의 핵심!

- 이때 디자인이 가능한 treatment 에 대해서만 인과적 관계를 추정할 수 있다고 했는데, 구체적으로 그러면 특정 treatment 에 대한 인과관계를 어떻게 추정할 수 있을까요? 

> ## Potential Outcomes Framework

> Definition

- 특정 treatment 의 인과적인 효과에 대해서 잠재적 결과, 즉 potential outcome 의 차이로서 정의하는 관점이 Potential outcomes Framework 

- 우리는 늘 살면서 스무살에 알았더라면 좋았던것들 / 대학생떄 알았더라면 좋았던것등 등을 생각함

  - 즉 그때 어떤 상황과 그때 결정 원인이 되어서 지금의 결과로 이어졌기 떄문에 , 만약에 그때 다른 결정을 했다면 지금의 결과가 달라졌을까? 에 대해서 생각함.

- 사실 이러한 관점이 potential outcome framework 의 핵심 아이디어

  - 특정 treatment 의 인과적인 효과는 바로 treatment 를 받았을떄의 결과와 treatment 를 받지 않았을때의 potential outcome(잠재적 결과)간의 차이를 바탕으로 인과적 효과를 정의하고, 정량화할 수 있다라고 보는게 바로 potential outcomes Framework

  - Causal effect of the treatment $=($ Actual outcome for treated if treated $)$-(Potential outcome for treated if not treated)

> Example

![jpg](/assets/images/Stat/127_1.jpg)

- 만일 독서가 성적에 미치는 인과적인 효과를 알고싶다고 합시다.
- potential outcome framework 하에서 인과관계를 추정한다고 합시다. 책을 읽었을때의 성적과, 만약 책을 읽지 않았을때의 잠재적인 성적간의 차이를 통해서 독서의 인과적인 효과를 정의할 수 있을것입니다.
  - 즉 Causal effect of the treatment $=($ Actual outcome for treated if treated $)$-(Potential outcome for treated if not treated) 가 되는것이죠

- 여기에서 (Potential outcome for treated if not treated) 를 우리는 CounterFactual 이라고 부릅니다. 이는 potential outcome framework 에서 매우 중요한 개념임
- 또한 중요한점은, 이러한 결과는 같은 대상, 즉 treatment 그룹에서의 실제 결과와 그들의 잠재적 결과의 차이를 분석한다는 점입니다.
- 이런점에서 potential outcome frame work 하에서 측정한 causal effect 는 Average Treatment Effect (ATE) on the Treated (ATT)라고 불리는 부분에 대해서 우리는 측정을 할 수 있는것 
  - 왜냐하면 potential outcome framework 는 treated 그룹 하에서만 효과를 비교하는것이기 떄문에 다른 control 그룹 하에서도 적용이 될지에 대해서는 명확하지 않기 때문
- 여기에서 Average Treatment Effect (ATE) 는 Treatment 그룹과 또 다른 Control 그룹에서 모두 적용되는 효과를 의미함 
  - 그런데 위에서 보는것처럼 우리가 추정할 수 있는것은 항상 ATT 임.
- 그러면 중요한 질문이 하나 있음 ! 바로 언제 우리가 측정하는 ATT 가 실제 우리가 주장하고 싶은 ATE 가 될 것인지가 매우 중요한 부분 (다음에 더 자세히 논하도록 하자)
- 어쩃든 여기에서 제일 중요한것은, Potential Outcome framework 하에서는 같은 대상에 대한 잠재적 결과를 비교해야 한다는것인데, 이런 비교가 현실에서 가능할까요? 
  - 만약 불가능하다면 우리는 실제로 어떤 비교를 할 수밖에 없을까요? 

> ## Fundemental Problem of Casual inference

- Potential Outcome framwork 는 potential outcome 을 모두 관찰할 수 없다는 큰 문제가 있습니다. 이를 Fundamental Problem of Casual Inference 라고 함
- 즉 한 유저에 대해서 treatment 를 받으면 받은거고, 받지 않으면 받지 않은것이고, 두가지 모두의 경우에 대해서 potential Outcome 모두를 관찰할 수 없다는것입니다.

![jpg](/assets/images/Stat/127_2.jpg)

- 결국, 우리는 이러한 중첩상태가 불가능하므로, Treatment 를 받은 사람들의 outcome 과 treatment 를 받지 않은 사람의 outcome 을 비교할수밖에없음 
  - 이떄 우리는 treatment 를 받지 않은 사람들을 counterfactual 대신에 control 그룹이라고 부르게 됨
- 이 프레임워크가 중요한 이유는 Causal inference 를 어렵게 만드는게 어떤것인지 구체적으로 알려주고, 이러한 어려움을 극복할 방법도 구체화 해볼 수 있습니다.
  - 이때 우리는 인과추론을 위해 필요한것은 Counter Factual 인데, 우리가 가지고 있는것은 오로지 Control group 밖에 없음
  - 즉 인과추론이 어려운 이유는 Counter Factual 그룹과 Control 그룹의 차이에서 기인함
- 이게 바로 Potential Outcome Framework 관점에서의 인과추론 문제라고 할 수 있음
- 즉 Control 그룹을 Counter Factual 과 가장 가깝게 만들어야 하고, 이게 design baased approch 에서의 인과추론 문제라고 볼 수 있는것이죠. 

> ## selection biased

> definition

- 다시 정리하면 counterfactual 은 treatment 그룹에 대해서 treatment 가 없을떄의 결과라고 함
- control group 은 treatment 를 받지 않은 그룹
- 이 둘의 차이를 selection biased 라고 부름

> Selection Biased Biased

- 쉽게 말해서 우리가 어떤 실험들을 통해서 실험 대상을 랜덤하게 배정하지 않는 이상, 사람들은 알지 못하는 이유에서, Treatment 를 받을지, 받지 않을지를 스스로 선택하게 됨
  - 앞선 예시에서는 독서 행위가 treatment 가 될텐데, 책을 읽을지 말지는 사람들의 자발적인 선택일것임. 
  - 그렇기 때문에 책을 읽은 사람의 특징과, 책을 읽지 않은 사람의 특징은 다를수밖에 없고, 이를 Selection Biased(선택 편향) 이라고 함

> Decomposition

- 만일 책을 읽은 사람과 읽지 않은 사람간에 가정환경, 나이 등이 차이가 난다면 우리는 그들간의 다른 성적이 독서의 차이에서 나왔다고 단정할 수 있을까?
- 우리가 현실에서 관찰하는(Observed Effect of Treatment) 실제 추정 효과는 treatment 를 받은 사람의 outcome 과 treatment 를 받지 않은 사람의 차이입니다.

![jpg](/assets/images/Stat/127_3.jpg)

- 위처럼 우리가 관찰하는 값은 Casual effect + selection Biased 로 분해됩니다.
  - 그런데 우리는 Causal effect 만 추정하고 싶은데 ,뒤에 선택 편향(오류) 가 붙어있는 것이죠..
- 즉 treatment 가 없는 상태에서도 애초에 treatment 그룹과 untreatment 그룹이 차이가 있으면, 이를 선택 편향이라 할 수 있음
- 정리하면 causal effect 를 추정함에 있어서 최대의 적은 selection biased 
  - 이를 없앨 수 있다면, selection biased 가 상쇄되고, 우리가 관찰하는 값이 Causal effect 와 같아질 수 있음

> ## Mindset for Causal Inference (Causal Mindset)

- causal inference 가 potential outcome framework 하에서는 selection biased 를 없애는것과 같을것임
- 그러면 어떻게 이것을 추구할 수 있을까요? 

> How to?

- treatment 가 없을떄, 모든 요인들에서 평균적으로 비교 가능해야 한다는것
- 정리하자면 potential outcome framwork 는 cAsulsal inference 의 핵심 목표는바로  treatment 를 제외한 모든 요인에 있어서 비교 가능한 control 그룹 , 즉 실제 관찰할 수 없는 Counter Facual 에 대해서, 최대한 가까운 적절한 연구 디자인을 고안하는 것이 핵심 목표!!! 
- 그래서 이러한 목표를 우리는 ceteris paribus 라고 부름 즉 treatment 를 제외한 모든 다른 요인에 대해서 비교 가능해야 한다는 원칙
  -  potential outcome framwork 하에서 가장 중요한 원칙이라고 할 수 있음!  d

---

**Reference**

- <https://www.youtube.com/watch?v=3JUlFC1LuIk&list=PLKKkeayRo4PWyV8Gr-RcbWcis26ltIyMN&index=1>

