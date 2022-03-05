---
title:  "실험같은 준실험 &#58; Quasi-Experiment"
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

> ## Quasi Experiment

- Random Assignment 가 중요하다는것은 이해를 했을 것입니다.
  - 하지만 이런 실험이 불가능한 경우도 많습니다.

- 그러면 이러한 상황에서는 인과추론을 어떻게 해야할까요? 
  - 비록 Random Assignment 를 이용한 실험은 아니지만, 실험과 유사한 상황을 찾아서 실험과 비슷한 분석을 할 수 있을것입니다.
- 우리는 이것을 Quasi Experiment 라고 부릅니다. 

> ## 1단계 : Random 배정이 가능한가?

> Yes : Randomized Controlled Trial

![jpg](/assets/images/Stat/137_1.jpg)

- 우리 연구의 목적이 단순한 예측이라 한다면, 굳이 인과추론의 방법과 Research Design 을 고민할 필요가 없음 (그냥 모델 Fitting , Predict 하세요~)
- 하지만 만약 인과추론, 즉 어떤 원인과 그것의 직접적인 결과에 대해서 탐구하고 메커니즘에 대해 탐구하고자 한다면,  Research Design 에 대해서 더 진지하게 고민해야합니다.
- 인과 추론의 gold standard 는 random assignment 이기 떄문에, 이러한 random assignment 가 가능한지 부터 고민해야함
  - 만약 Randomized Assign 이 가능하다면 고민할것 없이 Randomized Controlled Trial 을 사용하는게 가장 좋음! 

> No : 2단계로 이동..

> ## 2 단계 Treatment 가 명확할때

![jpg](/assets/images/Stat/137_1.jpg)

- Randomzie 실험은 못하지만 우리가 관심있는 원인변수, 즉 Treatment 를 분명하게 정의할 수 있고, treatment 를 받은 그룹과 그렇지 않은 Control 그룹을 구분할 수 있는지에 대한 여부를 따져봐야 합니다.

> Yes

- 이때 만약 Treatment 그룹과 Control 그룹을 나눌 수 있다면, 추가적으로 생각해봐야될 것은 Treatment 전 후의 데이터를 모두 관찰할 수 있는지의 여부 
  - Treatment 와 Control 그룹을 구분할 수 있고, 전 후의 데이터가 모두 있다고 하면 우리는 비로소 준 실험 (Quasi Experiment ) 를 활용할 수 있음 
- Randomized Experiment 와 Quasi Experiment 의 유일한 차이는 바로 Treatment 에 대한 Assignment 방법입니다.
  - Randomized Experiment 는 Random Assignment 
  - Quasi Experiment 는 다른 방법으로 Assignment

> ## 3단계 : Quasi Experiment

![jpg](/assets/images/Stat/137_1.jpg)

- Treatment Assignment 의 유형에 따라서 Quasi Experiment 는 세가지 종류로 구분이 될 수 있습니다.
  - Self-selection : 연구 대상들이 스스로 Treatment 를 받을지 말지를 결정하는것 
  - Exogenous Shock : 연구 대상들이 비록 Random 하게 배정되지는 않지만, 외부 요인에 의해서 Treatment 그룹과 Control 그룹이 나눠질 수 있음. (예를 들어서 예상치 못한 외부의 Shock / Event 에 의해서 Treatment 그룹과 Control 그룹이 나눠질 수 있음)  이를 Exogenous Shock 이라고 부름
  - Discontinuity : 임의의 경계값 (threshold / Cutoff) 를 기준으로 Treatment 그룹과 Control 그룹을 나누기도 함. 이를 DisContinuity 라고 함

> Note : Natural Experiment

- Exogenous Shock 을 기반으로 하는 Experiment 를 Natural Experiment(자연실험) 라고도 부릅니다.
  - Quasi Experiment 를 구성할 수 있는 상황이라면, 그나마 인과추론에 유리한 상황이라고 할 수 있음 왜냐하면 이런 상황에 특화된 방법론이 이미 잘 개발이 되어있어서
- Quasi Experiment 가 가능하다면 다양한 방법론을 사용할 수 있음!
  - DID (Difference in Difference) / Matching / Regression Discontinuity...

> ## 2 단계 Treatment 가 명확하지 않을때

![jpg](/assets/images/Stat/137_1.jpg)

- 그런데 많은 경우에 사실 Treatment 그룹과 Contorl 그룹을 명확하게 나누는게 어려울때도 있음
  - 예로 Covid - 19 의 발생 현황이 지역 경제에 어떤 영향을 미치는지를 알아보고자 합시다. 하지만 이때, 모든 지역에서 적어도 1명 이상의 Covid 환자가 있음.. 즉 Covid 환자가 있는 Treamtnet 그룹과, 그렇지 않은 Control 그룹을 나누는것이 쉽지가 않다는것 
- 또한 Treatment 와 Control 그룹을 나눌 수 있다고 하더라도, 전 후의 데이터를 관찰할 수 없다면, 앞서 언급한 Causal Inference 의 세팅을 활용하기가 어려울것입니다.

> ## 3 단계 : Instrument Variable

![jpg](/assets/images/Stat/137_1.jpg)

- 이럴 경우에 다음으로 생각할 수 있는 질문은 원인변수 (treatment) 를 예측할 수 있고 동시에 오차항과 연관성이 없는 변수를 찾을 수 있는지에 대한 여부
  - 여기서 오차항이라함은, 쉽게 말하면 결과에 영향을 줄 수 있지만, 우리가 관찰할 수 없는 모든 변수를 포함하는 부분이라 말할 수 있습니다.
- 만약에 이런 변수를 우리 연구 세팅에서 찾을 수 있다면 , 우리는 이런 변수를 Instrumental Variable 이라 부르며 활용할 수 있을것입니다.
  - 하지만 경우에 따라서는, 도구 변수로 활용하는게 쉽지 않을 수 있습니다.

> ## 3단계 : Selection on Observable

- 그래서, 만약에 이런 도구변수도 활용하기 어렵면 최후의 방법은 Selection on Observavles
  - 우리가 가지고 있는 변수들, 관찰 가능한 변수들만 가지고 선택편향을 모두 통제해보자!
- 이러한 방법론으로는 우리가잘 아는 Matching 방법과 Regression 이 있음
  - Matching 과 Regression 이 아예 다르다고 생각하는사람도 있는데, 인과추론 입장에서 Matching 과 Regression 모두 동일한 역할을 한다고 봐도 무방합니다. 
  - 두 방법론 모두 마찬가지로, 우리가 가지고 있는 변수들을 통제하고자 하는 역할임
- 그런데 이 둘의 한가지 차이점이 있다면, 우리가 가지고 있는 변수와 그리고 결과변수간의관계에 대한 가정이 다름

> Regression

- regression 은 흔히 우리가 통제변수를 추가함으로서 변수를 통제함
- 이떄 통제변수와 결과변수간의 어떤 특정 Functional Form 이 있다라고 가정하게 됨 
  - 예를 들어서 Linear Regression 같은 경우, 통제 변수와 결과 변수간의 선형관계(Linear Relation) 을 가정하게 됨
  - 이러한 접근의 장점은, Functional Form 을 잘 캡쳐할 수 있다면, 훨씬더 효율적인 추정이 가능함
  - 또한 샘플의 수를 그대로 유지하면서 그대로 추정할 수 있기 떄문에, 통계적 추정을 할 때에 훨씬 더 효율적입니다.

> Matching

- 하지만 경우에 따라서, Funtional Form 을 모를수도 있음
  - 이럴때에는 Matching 방법론이 더 효율적일 수 있음
  - Matching 은 우리가 가지고 있는 변수들을 양 집단간의 어떤 균일하게 만들어줌으로서, 그 변수의 효과를 통제하고자 하는 방법 
  - 그렇기 때문에, 어떤 특정 Functional Form 을 가정하지 않고, 그 값 자체를 평균적으로 균일하게 맞추어 줌으로서 통제하고자 함
  - 이것의 장점은 , 어떤Functional Form 에 대한 가정이 필요 없다는 장점
  - 하지만 Matching 과정에서 샘플 수가 줄어든다는 단점 즉 샘플수가 충분하지 않면 Mathing 방법론이 안좋을수도 있습니다.

> Causal Structure

- 그런데 사실. matching 이나 Regression 이나 모두 우리가 관찰 가능한, 우리가 가지고 있는 변수만 통제를 하고자 하는 것이기 떄문에, 이런 변수를 통제한다고 해서 모든 Selection Biased 를 통제하는것은 쉽지가 않을 것입니다.
- 그래서 Causal Diagram 을 활용해, Causal Structure 를 구조화 하고, 어떤 변수를 통제함으로서 , 어떤 원인변수가 결과변수에 영향을 줄 수 있는 모든 (흔히 Backdoor Path 라고 많이 부르는) 선택 편향의 원인에 대해서 통제 변수만 가지고 통제할 수 있는지에 대해서 충분히 우리들이 설명한다면, 통제 변수를 디자인 함으로서, regression 을 이용해서도 충분히 좋은 인과추론을 할 수 있다!
- 자세한것들은 뒤에서 제대로 다루게 될 것입니다 .

> ## Self Selection

![jpg](/assets/images/Stat/137_2.jpg)

- 앞서 말했듯이, Randomized Experiment 와 quasi Inference 의 차이점은 Control 과 Treatment 을 어떻게 배정하는지만 다름
- 하지만 Potential Outcome Framework 하에서 목표는 동일. 즉 ceteris paribus  를 만족하는 (비교 가능한) Control / Treatment 를 구성하는게 목표
  - 하지만 Random Assignment 의 경우는  ceteris paribus 를 만족하기 쉬운 반면에, Quasi Experiment 는 랜덤으로 Treatment 를 배정하지 않아서 ceteris paribus 한지에 대해서 우리가 명시적으로 증명해야하는 어려움이 있음...

> ## Example : Exogenous Shock 

![jpg](/assets/images/Stat/137_3.jpg)

- 이 논문에서는 local finance 에 대한 접근이 창업에 미치는 인과적인 효과를 연구한것
- 이러한 상황은 실험이 불가능할것이라는것을 알 수 있음
  - 특정 지역만 random 하게 대출 규제를 풀거나, 늘리는게 어렵기 떄문입니다. 

![jpg](/assets/images/Stat/137_8.jpg)

- 그러므로 이러한 실험 대신에 Quasi Experiment 를 디자인 즉 바로 미국에서 셰일가스 붐을 Exogenous Shock 으로 활용하여 Treatment 와 Control 그룹을 구분하였습니다.
- 이 연구에서 셰일의 유전이 발전하고, 이 지역에서 개발이 되었다면 에너지 회사들이 돈을 많이 벌게되고, 이 돈은 지역은행에 예치하게 됨
  - 그러면 셰일붐이 있었던 지역의 은행은 예금이 늘게 되고, 기업들에게 대출해줄 수 있는 여력이 크게 증가했을것! 
- 위가 이 논문에서의 Research Design 의 핵심논리
  - 셰일가스 유전이 발견되지 않은 지역(finance 접근성 상대적으로 작음) : Control Group 로 지정
  - 셰일가스 유전이 발전된 지역(fiannce 접근성 상대적으로 큼) : Treatment Group 로 지정

> Truthworthy?

- 이제 이 연구 디자인이 인과추론에 있어서 믿을만한지 판단하는 기준은, 셰일 붐에 의해 적용된 Control group 과 treatment group 이 local finance 에 대한 접근성을 제외하고 다른 요인에 있어서 얼마나 유사한지 여부가 될 것임
- 이런 관점에서 Exogenous Shock 이 유리한점이 있는데, 이런 Exogenuous Shock 은 언제 어디에서 발생할지 아무도 예측할 수 없음.
  - 그러므로 Random 배정한것은 아니지만, Exogenuous Shock 은 어느정도 Random 하게 배정한것과 유사한 효과를 낸다고 말할 수 있을것입니다.
- 사실 생각해보면 석유나 천영가스는 수천년동안 지하에서 , 땅에서 누적되고 축적되어온것이기 때문에 어느 지역에 세일가스와 셰일 오일이 묻혀있을지 아무도 예상하기가 어려움 !
  - 셰일가스가 묻혀있는 지역과 그렇지 않은 지역간에는 평균적으로 크게 차이가 나지 않을것!
- Natural Experiment 는 상대적으로 Randomize Experiment 에 매우 가까운 실험설계라고 할 수 있습니다. 

> ## Example : Self Selection

![jpg](/assets/images/Stat/137_4.jpg)

- 여기에서의 연구에서는, 소비자들이 기업 소셜미디어에 댓글을 남긴다더나 like 를 누른다거나 등, 참여를 한다는것이 회사 웹사이트를 방문하는 빈도에 어떻게 영향을 미치는지를 분석한 논문
- 여기에서는 , 기업 소셜미디어 참여가 Treatment 가 되게 됨
  - 그렇게 떄문에 우리는 Treatment 그룹과 Control 그룹을 소비자들의 선택에 따라서 쉽게 나눌 수 있음 
- 하지만 이런 Treatment 는 연구자가 배정하거나, 외부의 어떤 Shock 에 의해서 수동적으로 배정되는게 아니고, 소비자들이 직접 연구 대상을 선택 (즉 Treatment 를 선택) 하게 되므로 전형적인 Self selection 방법
- Treatment 와 Control 그룹을 구분할 수 있지만, 소비자들이 어떤 의도를 가지고 회사의 소셜 미디어 페이지에 참여를 했는지에 대해서 알 수 없음
  - 그렇기 때문에 두 집단이 서로 비교 가능한지에 대해서는 조금 더 의구심이 들수밖에 없음
  - 그래서 Randomize Experiment 나 Exogenous SHock 을 활용한 Experiment 에 비해서 조금 더 엄밀하게 ceteris paribus (비교 가능성) 에 대해서 많은 노력이 필요함

> ## Comparison of Exogenous Shock and Self selection

- Quasi Experiment 는 최대한 비교 가능하게 만드는게 중요

![jpg](/assets/images/Stat/137_6.jpg)

- 위처럼 Ceteris Paribus 를 증명해야 하는 부담감은 위와 같음
  - Ceteris Paribus 의 증명에 대한 강도의 차이로 이해하면 좋다.

> ## Example Discontinuity

![jpg](/assets/images/Stat/137_7.jpg)

- 음주와 건강 문제
  - 미국에서는 음주 가능 연령이 21세
  - 이것은 법에 의해 임의로 정한것 (21세가 어떤 의미가 있지는 않음)
- 그런데 이 시점을 기준으로 어떤 사망률 등의 차이가 생긴다면, 음주가 미치는 인과적인 효과라고 말할 수 있을것 
  - 즉 이렇게 임의의 어떤 값을 바탕으로 또다른 Causal Inference 를 디자인 할 수 있을것 

---

**Reference**

- https://www.youtube.com/watch?v=HKpkgluQypA&list=PLKKkeayRo4PWyV8Gr-RcbWcis26ltIyMN&index=4

