---
title:  "이중차분법/회귀불연속 &#58;Difference-in-Differences & Regression Discontinuity"
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

# [Difference in Difference](#link){: .btn .btn--primary}{: .align-center}

> ## Quasi Experiment

- 지금까지는 어떤 경우에 Quasi Experiemnt 를 디자인 할 수 있을지에 대해서 살펴보았습니다.
  - 자실 Quasi Experiment 는 말 그대로 Research Design
  - 그러면 이러한 Research Design 의 결과를 분석하는 방법이 필요
  
- 이러한 분석 방법에서 가장 대표적인 방법 두가지가 바로 Difference in Difference / Regression in Discontinuity 

> ## 이중차분법 : Difference in Difference (DID)

- 이중 차분법은 두번의 차분, 즉 두번의 뺼셈이 있는 구조입니다. 

![jpg](/assets/images/Stat/145_1.jpg)

$$\text { DID estimator }=\left(T_{A}-T_{B}\right)-\left(C_{A}-C_{B}\right)$$

- Treatment group 내에서의 전 후의 변화 - Control group 내에서의 전 후의 변화 를 측정

- 매우 간단해 보이지만, DID 분석은 이렇게 하는거야! 라고 하고 끝나는게 아니라 왜 DID 가 Potential Outcome Framework 하에서 인과추론을 위한 중요한 도구인지에 대해서 개념적으로 알아봅시다.

> ## Example

- 경제 규제가 회사에 어떠한 impact 를 일으켰는지를 알려고 한다고 합시다.

![jpg](/assets/images/Stat/145_2.jpg)

- 이를 알아보기 위하여 위와 같이 Regulation 을 적용한 그룹(A) 와 그렇지 않은 그룹(B) 를 살펴보려고 하였습니다.

![jpg](/assets/images/Stat/145_3.jpg)

- 이때 인과관계를 분석하기 위해 두 그룹을 위와 같이 Regulation 전의 데이터도 살펴보았습니다.
  - before the regulation
  - after the regulation

![jpg](/assets/images/Stat/145_4.jpg)

- 그래서 regulation 전후의 매출을 위와 같이 측정하였습니다.

![jpg](/assets/images/Stat/145_5.jpg)

- 그 이후에 Diff in Diff 를 이용하여 위처럼 regulation 이전과 이후의 차이를 측정합니다. 

![jpg](/assets/images/Stat/145_6.jpg)

- 이때 Regulation 을 제외한 나머지 요인은 두 그룹 모두 같은 영향을 미치고 있습니다. 
  - 위 그림에서 보면 electronic payment 라는 요인은 모두 양쪽에 대해서 같은 영향을 미치고 있습니다. 

![jpg](/assets/images/Stat/145_7.jpg)

- 이때 위와 같이 Difference 에 대해서 살펴보게 됩니다.

![jpg](/assets/images/Stat/145_8.jpg)

![jpg](/assets/images/Stat/145_9.jpg)

- 위처럼 Diff in Diff 를 계산하게 되고, 이것을 regulation 의 영향이라고 측정하게 됩니다.

> ## Justification

![jpg](/assets/images/Stat/145_10.jpg)

- Potential Framework 하에서 가장 중요한것은 바로 Counterfactual  (Counterfactual : Treatment 가 없었다면 있었을 잠재적 결과 ) 
- 이러한 Counter factual 를 $T_A'$ 라고 합시다. 이러한 Counter Factual을 아래와 같이 다시 써 봅시다. (A : after , B : before)

$$T_{B}+\left(T_{A}^{\prime}-T_{B}\right)$$

- 위처럼 Counter Factual 을 분해하면 시간에 따라 변하는값과 변하지 않는 값을 알 수 있음 
  - $T_B$ 는 Before Period 에 대해서 Treatment의 결과값
  -  $$T_{A}^{\prime}-T_{B}$$ 는 Treatment 가 없을때 시간에 따라 변하는 변화량
- 이때 $T_{A}^{\prime}-T_{B}$ 는 관찰 할 수 없는 값입니다. 
- 그래서 DID 의 접근은, Counter Factual 과 가까운 Control 그룹을 찾아서 이 Treatment 가 없을때의 Treatment 그룸에서의 변화량과 ($T_{A}^{\prime}-T_{B}$ ) 비슷한 값을 찾게 된다면 대체하여서 Counter Factual 을 추정할 수 있지 않을까? 가 아이디어입니다.
  - 즉 $T_A' - T_B \to C_A-C_B$ 처럼 추정하겠다는 것입니다.


> DID estimator

- DID 가 원래 추정하고자 하는 값은 $T_A' - T_A$
- 이때 $T_A' - T_B \to C_A-C_B$ 를 이용하여 우리가 '실제로 추정 가능' 하게 바꾸면 추정치는 아래와 같습니다.

$$\begin{aligned}
\text { DID estimator } &=\left(T_{A}-T_{B}\right)-\left(C_{A}-C_{B}\right) \\
&=T_{A}-\left[T_{B}+\left(C_{A}-C_{B}\right)\right]
\end{aligned}$$

> Note

- 위 방법을 잘 보면 $T_A' - T_B \to C_A-C_B$ 가 핵심입니다. 
  - 즉 Control 그룹과 Treatment 그룹이 "유사" 하다고 가정한 것입니다.
- 실제 Counter Factual 은 아니지만, control 그룹이 Treatment 그룹과 가깝다면 Control 그룹을 통해서 Counter factual 을 추론하는것이 DID 방법
- 그러므로 핵심은 Treatment 가 없을때의 Treatment 그룹과 Control 그룹이 얼마나  비교 가능한지가 바로 DID 가 가능한지의 여부가 됩니다.

> ## Needs of Before Period

- 이때 왜 Before period 가 필요할까요 ?  
- Treatment 가 없을때에 Control 그룹과 Treatment 그룹이 유사하다는것이 가정이였ㅇ므로 $T_A - T_A'$ 를 $T_A - C_A$ 로 바꿔서 생각할 수 있지 않을까요?  

> DID : 시간에 따라 변하는 값만 치환

- DID 의 경우 Counter Facutal ($T_A'$) 의 전부를 치환하고 있지 않습니다.
  - 시간에 따른 변화량만 ( $T_A' - T_B \to C_A-C_B$ ) Control 그룹으로 치환하고 있습니다. 
  - 즉 $T_B$ (시간과 관계없는 이전값)는 그대로 Treatment 의 값을 쓰고 있습니다. ( $T_A' \to T_{B}+\left(T_{A}^{\prime}-T_{B}\right) \to T_B +(C_A - C_B)$ )
- 즉 시간에 따라 변화하는 부분만 일치하면 됩니다. 
- 즉 아래와 같은 경우에도 DID 를 쓸 수 있다는 것입니다.
  - Treatment = 10,11,12,13,14,15... 
  - Control = 1,2,3,4,5,6....

>  $T_A - T_A' \to T_A - C_A$ : 시간에 따라 변하는부분 / 변하지 않는 부분 모두 치환

- $T_A - T_A'$ 를 $T_A - C_A$  로 치환하게 되면, 시간에 따라 변하는 부분과 변하지않는 부분 모두 Control Group 으로 치환하고 있습니다.
  - $$T_A' = T_{B}+\left(T_{A}^{\prime}-T_{B}\right)$$ 에서 $T_B$ 는 변하지 않는 값 , $T_A'-T_B$ 는 시간에 따라 변하는 값 임을 기억합시다.
- 즉 위와 같은 경우는 Control 그룹이 모든면에서 Treatment 와 매우 비슷해야 $T_A - T_A'$ 를 $T_A - C_A$  로 치환하는게 먹힌다는 것이죠.
- 즉 아래와 같은 상황에서는 모두 치환하는 방식($T_A' \to C_A$) 을 쓸 수 없다는 것입니다. 
  - Control : 1,2,3,4,5,6 ....
  - Treatment : 10,11,12,13,14,15,16....

> 검증 (Validation)

- 또한 위와 같이 "모두 치환" 하는 방식이 안좋다는것은 "검증" 의 입장에서도 살펴볼 수 있습니다.
  - $T_A' \to C_A$ 로 변환하는것은 "변하는 부분" 과 "변하지 않는 부분" 모두를 바꾸는것이기 떄문에 이 부분을 데이터로 검증하기란 쉽지 않습니다.  
  - 하지만 $T_A' - T_B \to C_A-C_B$  처럼 시간에 따른 변화량만 대체하게 된다면 이 부분은 데이터로 검증하기가 상대적으로 쉽습니다.
- ex : 아래와 같이 Control 그룹과 Treatment 그룹의 매출 변화가 아래와 같다고 합시다.
  - Control : 1,2,3,4,5,6,7....
  - Treatment : 10,11,12,13,14,15,16,17....
- 그렇다면 위처럼 "시간에 따른 변화량" 이 일치하므로 , 우리는 "시간에 따른 Control 과 Treatment 의 변하는 부분이 일치" 한다고 검증할 수 있죠
- 하지만 시간에 따라 변하지 않는 부분 ($T_B = C_B$ 인가?) 에 대해서는 검증하기가 쉽지는 않다는 것입니다.
- 또한 시간에 따라 변화하는 양은 데이터를 통해 어느정도 검증할 수 있습니다.

> ## Parallel trend assumption

- 다시한번 강조를 하는 부분은, DID 분석은 Conrol 그룹과 Treatment 그룹이, Treatment가 없는 상황에서 모든면에서 유사한것을 요구하는건 아님
  - DID 분석의 핵심 가정은 Treatment 가 없을때 , Treatment 그룹과 control 그룹의 시간에 따라 변화하는 변화의 정도만 유사하면 충분히 DID 분석은 강력한 힘을 발휘할 수 있습니다. 
- 그래서 시간에 따라 변화하는 변화량이 같아야 한다는 가정을 우리는 Parallel trend assumption 이라고 부릅니다. 

> parallel trend assumption

- 선택 편향을 없앨 수 있는 가정을 우리는 Identification Assumption 이라고 부릅니다 .
  - Parallel trend assumption 은 DID 분석에 대한 Identification Assumption 
- parallel trend assumption 은 Treatment 가 없을때 Treatment 와 control 이 동일해야한다는 가정이 아님 
  - 동일해야한다가 아니라, 시간에 따라서 두 그룹의 변화량이 비슷하고, 패턴이 유사해야 한다는것임 
  - 즉 시간에 따라서 평행하게 변화해야 한다는 의미가 되겠습니다.

> ## Example 

![jpg](/assets/images/Stat/145_11.jpg)

- 위 그림의 연구에서는 컨텐츠를 온라인 스트리밍 하는것의 인과적인 효과를 분석하는 연구입니다.
- 2007년에 미국의 가장 큰 방송사중에 하나인 NBC 가 애플과의 협상이 결렬되어서 아이튠즈에서 모든 NBC 컨텐츠가 내려간 적이 있었습니다

> Experiment

- 이러한 사건을 Exogenous Shock 으로 이용해서 NBC 컨텐츠를 Treatment , 그 외의 컨텐츠를 Control 그룹으로 묶고 분석한 전형적인 Natural Experiment를 시행해 보았습니다. 
  - 즉 NBC 와의 협상 결렬을 이용한 Natural Experiment 가 됩니다. 
- 여기서 보면 중요한 부분은 Treatment (컨텐츠가 아이튠즈에 올리는것) 의 여부에 때해서 Control 그룹과 Treatment 그룹의 다운로드 수가 평행한것을 볼 수 있습니다.
  - DID 를 위해서라면 이 값들이 겹쳤다는 사실이 중요한게 아님. 달라도 상관 없음!
  - 더 중요한것은.. Treatment 그룹과 Control 그룹이 시간에 따라 변하는 값이 비슷해서 평행하게 이동한다는 사실이 중요함!
- 이러한 가정 하에서 Diff in diff 가 실험은 아니지만 Randomized Exeriment 와 비슷하게 강력한 인과추론의 힘을 가질 수 있게 되는것입니다. 

> ## why DID is strong?

- 그래서 이러한 DID 가 Potential Outcome Framework 에서 유리한지에 대해서 조금 이해를 하셨을 것입니다. 
- 그런데 여기에서 결국엔 Treatment 그룹과 Control 그룹이 Treatment 가 없을때 유사해야 한다는 가정 (ceteris paribus) 는 똑같음 
- 그런데 Causal experiment 는 self selection 에 의하던, Exogenuous Shock 에 의하던, 결국 Treatment 를 정하는것은 연구자가 아님.
  - 즉 운이 좋아서 정말 이렇게 ceteris paribus 를 만족하는 Control 그룹을 찾을 수 있지만 그렇지 못하는 경우도 많음
  - 예를 들어서 Parallel trend 를 만족하기 어려운 경우도 매우 많음 
- 그러면 우리가 이 Comparable Control group 을 찾을 수 없을때는 어떻게 해야 할까요 ?
  - 이런 측면에서 활용할 수 있는 도구가 있습니다!

# [Matching](#link){: .btn .btn--primary}{: .align-center}

> ## Matching Techniques

- 우리가 가지고 있는 변수들을 활용해서 Treatment 그룹과 Control 그룹에서 이러한 변수들의 값이 평균적으로 유사한 샘플들만 서로 매칭을 해서 인위적으로 유사하게 만들어주는 기법 
  - 예를 들어서 남자는 남자와 매칭하고, 키큰 사람은 키큰 사람끼리만 매칭하는 등...
- 이런식으로 매칭한다면 Control 그룹과 Treatment 그룹간의 남녀 성비, 평균 키 등을 비슷하게 만들 수 있습니다. 
  - 이러한 Matching 의 목적은 Treatment 그룹의 Counter Factual 을 만들고자 하는것입니다.

- 이런 Matching 에는 크게 두가지의 접근이 있습니다.
  - (i) Propensity score matching (PSM)
  - (ii) Coarsened exact matching (CEM)

> ##  Propensity score matching (PSM)

![jpg](/assets/images/Stat/145_12.jpg)

- Propensy score 를 먼저 계산하고, score 가 비슷한 사람끼리 매칭을 하겠다는 매칭
  - 여기에서 propensity score 는 Treatment 그룹에 속할 확률이라고 볼 수 있음 
- 우리는 Binary outcome 을 모델링할때는 logistic 또는 probhit 모델을 이용해서 모델링하게 됩니다.
  - Treatment 에 속하면 1 
  - Control 에 속하면 0 
- 우리가 가지고 있는 변수들을 independent variable 로 놓고 prophit 모델을 모델링한다면 Treatment 에 속할 Propensity score 를 계산할 수 있습니다. 
  - 이렇게 계산을 해서 쭈우욱 줄을 세운 다음에, 이런 score 가 유사한 샘플들끼리 매칭을 하고, 매칭된 샘플만 활용해서 분석을 한다면 훨씬 더 비교 가능한 대상이 될 것입니다. 
- 물론 우리가 예측에 사용한 변수에 대해서만 비교 가능하다는 유의점이 있습니다.우리가 관찰하지 못하는 변수에 대해서는 비교 불가능할수도 있겠죠....
- 이러한 매칭 방법이 DID 분석과 궁합이 잘 맞아서, 많은 연구들에서 DID 와 Matching 을 결합해서 활용하곤 합니다. 
- 사실 Matching 관련해서는 Mathching 된 샘플만을 이용하기보다는 역확률 가중법 등을 쓰기도함 (이러한 방법론에 대해서는 나중에 깊이 있게 설명하려고 합니다.)
- 이런 PSM 가장 많이 활용되었던 매칭 방법이고, 여전히 많은 경우에 매우 효과적입니다. 
  - 하지만 한가지 단점이 있는데, 여기에서 보듯이, 모든 샘플을 이 Propensity score 를 계산해서 이 스코어 기반으로만 매칭을 하고 있습니다.
  - 그렇기 때문에 만약 변수가 굉장히 많으면 모든 변수에 대해서 매칭을 하는게 아니라 단일 스코어만으로만 매칭을 하는것이기 때문에 경우에 따라서는 어떤 변수에 대해서 차이가 많이 생길 수 있음 (즉 벨런스가 잘 안맞음...)
- 이런 한계점을 극복하기 위해 발전된게 바로 CEM 

> ## Coarsened exact matching (CEM)

- CEM 은 이런 PSM 보다 훨씬 직관적입니다.

> Exact Matching

- 모든 변수에 대해서 동일하게 해야 한다면 가장 쉬운 방법은 그냥 모든 변수가 동일하도록 그냥 매칭을 하면 됩니다.

- 예를 들어서 남자이면서 키가 170인 사람은 또 다른 키가 170인 남자와 매칭을 하면 됩니다.
  - 정확하게 값이 똑같은 값인 사람을 매칭하게 되면 모든 변수에 대해서 값이 같을것입니다.

![jpg](/assets/images/Stat/145_13.jpg)

- 하지만 변수가 많아지면, 이런 변수들에 대해서 값이 똑같은 샘플을 찾기가 매우 어려울 것입니다.
- 예를 들어서 지금 위 왼쪽에 보이는 그림에서 Age 와 Imcome 두 변수를 고려하여 만약 Exact Matching 을 한다면 두 변수에 대해서 같은 값을 가지는  Matching이 거의 없는것을 볼 수 있죠.
- 그래서 Exact Matching 은 많은 샘플을 버리게 되기 때문에, 활용하기가 어렵다는 단점이 있습니다..

> Coarsened Exact matching

- 이러한 대안으로 나온게 바로 Coarsened Exact matching
- 어떤 모든 변수에 대해서 정확한 값을 서로 매칭하기 보다는, 각 변수별로 몇개 구간을 나누고, 모든 "구간"에서 일치하는 샘플끼리 매칭을 하자는것이 바로 CEM 의 아이디어.

![jpg](/assets/images/Stat/145_13.jpg)

- 예를 들어서 , Age 에 대한 변수를 3개의 구간으로 나누고, 또 Income 에 대한 변수를 4개의 구간으로 나누어서 두 변수에서 모두 동일한 구간을 가진 샘플끼리 매칭을 하게 되면 비록 정확한 값이 완벽하게 매칭되지는 않지만 느슨하게 매칭된 값들을 매칭시킬 수 있게 됩니다.
- 이게 바로 CEM 의 기본 아이디어이고, 사실 PSM 과 CEM 중 뭐가 좋은지는 여전히 갑론을박이 있는 상황
- 어떤 Matching 방법이 좋다! 라고는 여기에서 결론을 내리지는 않으려고 합니다.
  - 즉 두가지 방법을 모두 시험해보는게 좋을것입니다. 

> Conclusion

- DID 와 Matching 방법론을 모두 설명했습니다.
  - DID 와 Matching 은 Self Selection 과 Exogenous Shock 에 대해서 적합한 방법론

> ## Discontinuity

- Discontinuity 는 Regression Discontinuity (RD) 라고 불리는 방식으로 분석을 할 수 있습니다.
- 많은 사람들이 DID 와 RD 많이 헷갈려하는 부분이 있습니다.
  - 여기에서는 최대한 간략하게 RD 가 DID 과 어떻게 다르고 또 그러한 Identification Assumption(인과추론을 가능하게 하는 가정) 이 어떻게 다른지에 대해서 중점적으로 살펴보려 합니다. 

![jpg](/assets/images/Stat/145_14.jpg)

- Regression Discontinuity 는 위 그림처럼 Discontinuity Jump 를 활용하는것입니다.
  - Counterfactual 이 왼쪽 그림과 같은 모델링으로 진행이 되고, Treatment 는 오른쪽 그림과 같이 모델링이 될때에, Discontinuiuty jump 는 바로 그 효과라고 볼 습니다.
- 여기서 중요한것은 Jump 가 일어난 변수입니다. 이를 우리는 흔히 Running Variable 또는 Assignment Variable 이라고 합니다. 

> Misconcept

- 가장 큰 오해는 Regression Discontinuiuty 가 전후 (cut off) 를 기점으로 Control 과 Treatment 를 나누어서 분석하는것이라 생각할 수 있음
  - 하지만 단순하게 둘로 나눠서 분석하는것은 DID 라고 보는게 더 적절함. 
- RD 는 사실 Potential Outcome Framework 하에서는 DID 관점와는 조금 다른 접근을 취하고 있음 
  - Regression Discontinuiuty 관점은 Running Variable 에 대한 Modeling 이 핵심임.
- Counter Fatual 에서 Running Variable 과 Outcome Variable 간의 관계가 있을것입니다. (선형관계라던지, )
  - 이때 Discontinuiuty jump 가 없으므로 이러한 관계를 바로 Counterfactual 이라고 할 수 있습니다. 
- 그래서 Running Variable 에 대한 Discontinuiuty 가 없을때의 상황을 모델링하여 (점선의 선) Counter Factual 를 계산하고, Counter Factual 과 실제값과의 차이를 계산으로 Treatment effect 를 구하려고 하는게 바로 Regression Discontinuity
  - RD 의 색심은 바로 Running Variable 에 대한 모델링이고, 이를 통해서 Counterfactual 를 계산하려 함 

![jpg](/assets/images/Stat/145_15.jpg)

- 위에서 보면, 지금 가상의 데이터가 있다고 할때 , X 가 Running variable 이라 할 수 있습니다. 
- 이러한 Outcome 에 대해서 이러한 관계를 Liniear function 으로 정의할 수 있습니다.

![jpg](/assets/images/Stat/145_16.jpg)

- 위에서 점선과 같이 Counter Factual 을 정의할수도 있습니다. 
  - 만약에 linear function 으로 정의하게 되면 counter factual 과의 거리가 크기 때문에, Treatment Effect 가 크게 나오게 됩니다. 
- 반면에, 만약 running variable 을 nonlinear 로 정의하게되면 아무런 jump 도 일어나지 않습니다.
  - 그럼에 따라 treatment effect 가 일어나지 않음 
- 그러므로 regression discontinuiuty 는 running variable 에 대한 DID 와는 달리 Funtional Form 에 대해서 취약한 방법이라고 할 수 있습니다. 
  - 같은 데이터에 대해서도 linear 로 모델링하는지, nonlinear 로 모델링하는지에 대해서 확확 달라지게 됩니다. 

> ## Example

![jpg](/assets/images/Stat/145_17.jpg)

- 음주와 건강 이슈를 살펴봅시다. 
- Running Varable 은 age 입니다 .
  - $A_a$ 는 어디에서 Discontinuiuty 가 일어나는지에 대한 부분입니다. 
  - 21세 이상이면 1, 그렇지 않으면 0 으로 모델링 하게 됩니다. 
- 모델의 형태를 보면 age(a) 와 사망률($D_a$)과의 관계를 linear function 으로 정의하고 있음을 볼 수 있습니다.
- linear function 을 통해서 discontinuiuty jump 된 값을 바탕으로 treatment effect 로 정의함
- 물론 나이와 사망률과의 관계를 다른 함수로 정의한다면 결과는 완전히 달라질 수 있습니다.
- 즉 RD 의 문제는 Running variable 에 대한 정확한 funtional form 에 대해서 알기가 어렵다는 것입니다.
  - 많은 연구에서 활용하는 방식은 다항식을 활용하게 됩니다.
  - 3차함수까지도 많이 넣게 됩니다. 
- 이런 다양한 functional form 때문에 flexible 하긴 하지만, DID 에 비해서 identification assumption 을 증명하기가 어려움
  - 이런 discontinuiuty 가 있는 경우여도 DID 가 가능하다면 , 이것을 적용하는게 더 좋음... 

---

**Reference**

- https://www.youtube.com/watch?v=HKpkgluQypA&list=PLKKkeayRo4PWyV8Gr-RcbWcis26ltIyMN&index=4

