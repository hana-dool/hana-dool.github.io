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

> ## Quasi Experiment

- 지금까지는 어떤 경우에 Quasi Experiemnt 를 디자인 할 수 있을지에 대해서 살펴보았습니다.
  - 자실 Quasi Experiment 는 말 그대로 Research Design
  - 그러면 이러한 Research Design 의 결과를 분석하는 방법이 필요
  
- 이러한 분석 방법에서 가장 대표적인 방법 두가지가 바로 Difference in Difference / Regression in Discontinuity 

> ## 이중차분법 : Difference in Difference (DID)

- 이중 차분법은 두번의 차분, 즉 두번의 뺼셈이 있는 구조입니다. 

$$\text { DID estimator }=\left(T_{A}-T_{B}\right)-\left(C_{A}-C_{B}\right)$$

- 첫번째 차분은 다음과 같습니다 .
  - Treatment group 내에서의 전 후의 변화 - Control group 내에서의 전 후의 변화 를 측정
- 분석의 방법은 매우 간단!
  - DID 분석은 이렇게 하는거야! 라고 하고 끝나는게 아니라 왜 DID 가 Potential Outcome Framework 하에서 인과추론을 위한 중요한 도구이닞에 대해서 개념적으로 이해해 봅시다. 
- 개념적으로 DID 의 분석은 매우매우 간단
  - DID 모델을 potential Framework 하에서 분석해보자. 

> Note

- Potential Framework 하에서 가장 중요한것은 바로 Counterfactual
  - Counterfactual : Treatment 가 없었다면 있었을 잠재적 결과
- 이러한 Counterfactore 를 $T_A'$ 라고 합시다. 

$$T_{B}+\left(T_{A}^{\prime}-T_{B}\right)$$

- 위처럼 구분했을떄, 시간에 따라 변하는값과 변하지 않는 값을 알 수 있음 
  - $T_B$ 는 Before Period 에 대해서 Treatment 에서의 outcome
  -  $$T_{A}^{\prime}-T_{B}$$ 는 Treatment 가 없을때 시간에 따라 변하는 변화량
- 이때 $T_{A}^{\prime}-T_{B}$ 는 관찰 할 수 없음 (Counter Factual 이여서)
- 그래서 DID 의 접근은, Counter Factual 과 가까운 Control 그룹을 찾아서 이 Treatment 가 없을때의 Treatment 그룸에서의 변화량을 ($T_{A}^{\prime}-T_{B}$ ) 비슷한 값을 찾게 된다면 대체하여서 Counter Factual 을 추정할 수 있지 않을까? 가 핵심

$$\begin{aligned}
\text { DID estimator } &=\left(T_{A}-T_{B}\right)-\left(C_{A}-C_{B}\right) \\
&=T_{A}-\left[T_{B}+\left(C_{A}-C_{B}\right)\right]
\end{aligned}$$

- Treatment 를 받지 않았을때의 Control 그룹의 차이를 치환해서 볼 수 있다는것이 핵심 ! 
- 실제 Counter Factual 은 아니지만, control 그룹이 Treatment 그룹과 가깝다면 Control 그룹을 통해서 Counter factual 을 추론하는것이 DID 방법

![image-20220102151555807](/Users/gorany/Desktop/Docs/Typora_Screenshot/image-20220102151555807.png)

- Treatment 가 없을때의 Treatment 그룹과 얼마나 비교 가능한지가 바로 DID 를 빋을 수 있는지 없는지가 됨

> Note

- 이때 왜 Before period 가 필요할까요 ?  
- 우리가 $T_A - T_A'$ 를 $T_A - C_A$ 로 바꿔서 생각할 수 있지 않을까요?  
  - 위 접근과 DID 접근의 차이를 봅시다. 
- DID 의 경우 Counter Facutal 의 전부를 치환하고 있지 않습니다.
  - 시간에 따른 변화량만 Control 그룹으로 치환하고 있습니다. 
  - 즉 $T_B$ (시간과 관계없는 이전값)는 그대로 Treatment 의 값을 쓰고 있습니다.
  - $T_A' \to T_{B}+\left(T_{A}^{\prime}-T_{B}\right) \to T_B +(C_A - C_B)$
- $T_A - T_A'$ 를 $T_A - C_A$  로 치환하게 되면, 시간에 따라 변하는 부분과 변하지않는 부분 모두 Control Group 으로 치환하고 있습니다.
  - 시간에 따라 변화하는 부분만 비슷하면 되는 DID 
  - Control 그룹이 모든면에서 Treatment 와 매우 비슷해야 $T_A - T_A'$ 를 $T_A - C_A$  로 치환하는게 먹힘
- 또한 시간에 따라 변화하는 양은 데이터를 통해 어느정도 검증할 수 있음 
  - After Period 만 있으면 우리는 검증하기 쉽지 않음 (counter factual 과 얼마나 가까운지)
  - 시간에 따라서 변화하는 양만 우리가 유사하게 바란다면, 충분히 이것은 검증 가능함
- 다시한번 강조를 하는 부분은, DID 분석은 Conrol 그룹과 Treatment 그룹이, Treatment가 없는 상황에서 모든면에서 유사한것을 요구하는건 아님
  - DID 분석의 핵심 가정은 Treatment 가 없을때 , Treatment 그룹과 control 그룹의 시간에 따라 변화하는 변화의 정도만 유사하면 충분히 DID 분석은 강력한 힘을 발휘할 수 있습니다. 
- 그래서 시간에 따라 변화하는 변화량이 같아야 한다는 가정을 우리는 Parallel trend assumption 이라고 부릅니다. 

![image-20220102153422325](/Users/gorany/Desktop/Docs/Typora_Screenshot/image-20220102153422325.png)

- 선택 편향을 없앨 수 있는 가정을 우리는 Identification Assumption 이라고 부릅니다 .
  - Parallel trend assumption 은 DID 분석에 대한 Identification Assumption 
  - Treatment 가 없을때 Treatment 와 control 이 동일해야한다는 가정이 아님 
  - 동일해야한다가 아니라, 시간에 따라서 두 그룹의 변화량이 비슷하고, 패턴이 유사해야 한다는것임 
  - 즉 시간에 따라서 평행하게 변화해야 한다는 의미가 되겠습니다.
- 한가지 예시를 들면 위 그림의 연구에서는 컨텐츠를 온라인 스트리밍 하는것의 인과적인 효과를 분석하고 있습니다.
  - 2007년에 미국의 가장 큰 방송사중에 하나인 NBC 가 애플과의 협강이 결렬이 되어서 아이튠즈에서 모든 NBC 컨텐츠가 내려간 적이 있었습니다.
- 이러한 사건을 Exogenous Shock 으로 이용해서 NBC 컨텐츠를 Treatment , 그 외의 컨텐츠를 Control 그룹으로 묶고 분석한 전형적인 Natural Experiment 입니다. 
  - 즉 NBC 와의 협상 결렬을 이용한 Natural Experiment 가 됩니다. 
- 여기서 보면, 중요한 부분은 지금 Treatment, 즉 협상이 결렬되서 컨텐츠가 아이튠즈에서 내려온 Treatment 와 Control 그룹에 평행한것을 보여주고 있습니다.
  - 이 값들이 겹쳤다는 사실이 중요한게 아님. 달라도 상관 없음
  - 더 중요한것은.. Treatment 그룹과 Control 그룹이 시간에 따라 변하는 값이 비슷해서 평행하게 이동한다는 사실이 중요 
  - 이러한 가정 하에서 Diff in diff 가 실험은 아니지만 Randomized Exeriment 와 비슷하게 강력한 인과추론의 힘을 가질 수 있게 되는것입니다. 
- 그래서 이러한 DID 가 Potential Outcome Framework 에서 유리한지에 대해서 조금 이해를 하셨을 것입니다. 
  - 그런데 여기에서 결국엔 Treatment 그룹과 Control 그룹이 Treatment 가 없을때 유사해야 하는 가정은 똑같음 
- 운이 좋아서 정말 이렇게 ceteris paribus 를 만족하는 Control 그룹을 찾을 수 있지만 그렇지 못하는 경우도 많음
  - Parallel trend 를 만족하는 경우도 매우 많음 
- 그러면 우리가 이 COmparable Control group 을 찾을 수 없을때는 어떻게 해야 할까요 ?
  - 이런 측면에서 활용할 수 있는 도구가 있음 

> ## Matching Techniques

- 우리가 가지고 있는 변수들을 활용해서 Treatment 그룹과 Control 그룹에서 이러한 변수들의 값이 평균적으로 유사한 샘플들만 서로 매칭을 해서 인위적으로 유사하게 만들어주는 기법 
  - 예를 들어서 남자는 남자와 매칭하고, 키큰 사람은 키큰 사람끼리만 매칭하는 등...
- 이런식으로 매칭한다면 Control 그룹과 Treatment 그룹간의 남녀 성비, 평균 키 등을 비슷하게 만들 수 있습니다. 
  - 이게 바로 전형적인 Matching 의 아이디어
- Matching 의 목적은 Treatment 가 없었을때 Counter Factual 을 만드는것... 
- 이런 Matching 에는 크게 두가지의 접근ㅇ 있음 
  - (i) Propensity score matching (PSM)
  - (ii) Coarsened exact matching (CEM)

![image-20220102201738521](/Users/gorany/Desktop/Docs/Typora_Screenshot/image-20220102201738521.png)

- Propensy score 를 먼저 계산하고, score 가 비슷한 사람끼리 매칭을 하겠다는 매칭
  - 여기에서 propensity score 는 Treatment 그룹에 속할 확률이라고 볼 수 있음 
- 우리는 Binary outcome 을 모델링할때는 logistic 또는 probhit 모델을 이용해서 모델링
  - Treatment 에 속하면 1 
  - Control 에 속하면 0 
- 우리가 가지고 있는 변수들을 independent variable 로 놓고 prophit 모델을 모델링한다면 Treatment 에 속할 Propensity score 를 계산할 수 있습니다. 
  - 이렇게 계산을 해서 쭈우욱 줄을 세운 다음에, 이런 score 가 유사한 샘플들끼리 매칭을 하고, 매칭된 샘플만 활용해서 분석을 한다면 훨씬 더 비교 가능한 대상이 될 것입니다. 
  - 적어도 우리가 활용한 변수에 대해서는 말이죠, 물론 우리가 관찰하지 못하는 변수에 대해서는 비교 불가능할수도 있겠죠....
- 이러한 매칭 방법이 DID 분석과 궁합이 잘 맞아서, 많은 연구들에서 DID 와 Matching 을 결합해서 활용하곤 합니다. 
  - 사실 Matching 관련해서는 Mathching 된 샘플만을 이용하기보다는 역확률 가중 법 등을 쓰기 도함 (이러한 방법론에 대해서는 나중에 깊이 있게 설명하려고 합니다.)
- 이런 PSM 가장 많이 활용되었던 매칭 방법이고, 여전히 많은 경우에 매우 효과적입니다. 
  - 하지만 한가지 단점이 있는데, 여기에서 보듯이, 모든 샘플을 이 Propensity score 를 계산해서 propensity 하나로만 매칭을 하고 있음
  - 그렇기 때문에 만약 변수가 굉장히 많으면 모든 변수에 대해서 매칭을 하는게 아니라 단일 스코어만으로만 매칭을 하는것이기 때문에 경우에 따라서는 어떤 변수에 대해서 차이가 많이 생길 수 있음 (즉 벨런스가 잘 안맞음...)
- 이런 한계점을 극복하기 위해 발전된게 바로 CEM 

> ## CEM

- CEM 은 이런 PSM 보다 훨씬 직관적
  - 모든 변수에 대해서 동일하게 해야 한다면 .... 모든 변수가 동일하도록 그냥 매칭을 하면 됩니다. 

![image-20220102202748508](/Users/gorany/Desktop/Docs/Typora_Screenshot/image-20220102202748508.png)

- 예를 들어서 남자이면서 키가 170인 사람은 또 다른 키가 170인 남자와 매칭을 하면 됩니다.
  - 정확하게 값이 똑같은 값인 사람을 매칭하게 되면 모든 변수에 대해서 값이 같을것
- 하지만 변수가 많아지만, 이런 변수들에 대해서 값이 똑같은 샘플을 찾기가 매우 어려울 것입니다.
  - 예를 들어서 지금 위 왼쪽에 보이는 그림에서 Age 와 Imcome 두 변수를 고려하여 만약 Exact Matching 을 한다면 두 변수에 대해서 값이 거의 동일한것의 경우 거의 없습니다..  (많은 샘플을 버리게 되고 있는것을 보고 있죠)
- 이러한 Exact Matching 은 거의 활용하기가 없음...
- 이러한 대안으로 나온게 바로 Coarsened Exact matching
  - 어떤 모든 변수에 대해서 정확한 값을 서로 매칭하기 보다는, 각 변수별로 몇개 구간을 나누고, 그 구간에 따라 모든 구간에서 일치하는 샘플끼리 매칭을 하자는것이 바로 CEM 의 아이디어 
- Coarsened : 거친 / 느슨한... 
  - 그렇기 때문에 느슨하게 값을 모든 변수에 대해서 Matching 하자는 개념이 되겠습니다.
- 예를 들어서 , Age 에 대한 변수를 3개의 구간으로 나누고 , 또 Income 에 대한 변수를 4개의 구간으로 나누어서 두 변수에서 모두 동일한 구간을 가진 샘플끼리 매칭을 하게 되면 비록 정확한 값이 완벽하게 매칭되지는 않지만 느슨하게 매칭된 값들을 매칭시킬 수 있게 됩니다.
  - 이게 바로 CEM 의 기본 아이디어이고, 사실 PSM 과 CEM 중 뭐가 좋은지는 여전히 갑론을박이 있는 상황
- 어떤것이 좋다! 라고는 여기에서 결론을 내리지는 않으려고 합니다.
  - 즉 두가지 방법을 모두 시험해보는게 좋을것입니다. 
- DID 와 Matching 방법론을 모두 설명했음
  - DID 와 Matching 은 Self Selection 과 Exogenous Shock 에 대해서 적합한 방법론

> ## Discontinuity

- Discontinuity 는 RRegression Discontinuity (RD) 라고 불리는 방식으로 분석을 할 수 있습니다. 
  - 여기에서 설명학자 하는 방법은, Regression Discontinuity 에 대한 오해가 많은것 같음...
- 왜냐하면 많은 사람들이 DID 와 RD 많이 헷갈려 하는것 같음 
  - 여기에서는 최대한 간략하게 RD 가 DID 과 어떻게 다르고 또 그러한 Identification Assumption ,(인과추론을 가능하게 하는 가정) 이 어떻게 다른지에 대해서 중점적으로 살펴보려 합니다. 
- Regression Discontinuity 는 아래 그림처럼 Discontinuity Jump 를 활용하는것입니다.
  - 여기서 중요한것은 Jump 가 일어난 변수입니다. 이를 우리는 흔히 Running Variable 또는 Assignment Variable 이라고 합니다. 
- Regression Discontinuiuty 가 전후 (cut off) 를 기점으로 Control 과 Treatment 를 나누어서 분석하는것이라 생각할 수 있음
  - 하지만 단순하게 둘로 나눠서 분석하는것은 DID 라고 보는게 더 적절함. 
  - RD 는 사실 Potential Outcome Framework 하에서는 DID 관점이 조금 다른 접근을 취하고 있음 
- Regression Discontinuiuty 관점은 Running Variable 에 대한 Modeling 이 핵심임 
  - 다시 설명하자면 Running Variable 과 Outcome Variable 간의 관계가 있을것입니다. 
  - 어떤 Treatment (Dicontinuiuty jump 가 없을때) 이러한 관계를 바로 Counterfactual 이라고 할 수 있습니다. 
- Running Variable 이 없을때의 상황을 모델링하여 Counter Factual 를 계산하고, Counter Factual 과 실제값과의 차이를 계산으로 Treatment effect 를 구하려고 하는게 바로 Regression Discontinuity
  - RD 의 색심은 바로 Running Variable 에 대한 모델링이고, 이를 통해서 Counterfactual 를 계산하려 함 

![image-20220102203810915](/Users/gorany/Desktop/Docs/Typora_Screenshot/image-20220102203810915.png)

- 위에 서 보면, 지금 가상의 데이터가 있다고 할때 , X 가 Running variable 이라 할 수 있습니다. 
  - Linear Funtion 으로 정의하면 이게 Counter Factual 이 될 것이지만.. 뭐... 
- 위처럼 생긴 

---

**Reference**

- https://www.youtube.com/watch?v=HKpkgluQypA&list=PLKKkeayRo4PWyV8Gr-RcbWcis26ltIyMN&index=4

