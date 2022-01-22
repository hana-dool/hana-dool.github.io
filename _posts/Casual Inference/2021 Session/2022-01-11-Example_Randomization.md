---
title:  "무작위 통제실험 연구사례 &#58; 출근시간 타겟 마케팅의 인과적 효과"
excerpt: ""
categories:
  - Casual_Inference_Session2021
last_modified_at: 2022-01-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3142835 의 논문 리뷰 
{: .notice--warning}

# [Contextual Targeting](#link){: .btn .btn--primary}{: .align-center}

> ## Contextual Targeting

- 온라인 쿠폰이 매우 많이 쓰이고 있지만 redemption rate (모바일 쿠폰을 받았을때 실물로 교환하는 비율) 은 매우 낮은 현상이 있습니다. (16% 의 유저만 사용)
- 온라인 쿠폰은 paper coupon 대비하여, 온라인 쿠폰의 사용량은 적었는데요, 이러한 온라인 쿠폰의 redepmtion rate 를 높히기 위해서 어떻게 할 수 있을지를 탐구한 연구입니다.

> 모바일에서 활용 가능한 부분

- 모바일폰은 항상 들고다니기때문에, 내가 언제든지 원하는 시간에 고객에게 뿌리기 가능
- 모바일 폰의 location 정보가 있으므로, 고객이 어디있는지 알 수 있으므로 지리적 정보를 이용해 쿠폰 추천이 가능
- 즉 고객의 temporal aspect , geographical aspect 를 활용하여 모바일 쿠폰을 타게팅 할 수 있다는 것입니다.
  - Temporal : 오전에 특정 사용자를 타겟하기 ...
  - Geographic : 영화관에 현재 들어온 사용자만을 타겟하기 ...
- 위와 같은 2개의 Aspect 들을 결합하는것을 Context Aspect 라고 합니다.
  - Context : 오전에 영화관에 간 사용자에 대해서 조조영화 쿠폰 등 추천 ... 

> context targeting

- 모바일 마케팅에서 이러한 contextual Targeting 이 중요해지고 있음 

![jpg](/assets/images/Stat/147_1.jpg)

- 이러한 contextual targetting 이 중요해지고 있는 이유는 이유는 , 사용자들이 점점 개인정보에 관심을 가지면서, 위치기반의 수집을 못하게 막음으로서, 위치기반의 마케팅을 못하게 하고 있기 떄문입니다.
  - 한 예시로 65% 의 사용자들에 대한 마케팅이 , 부적절한 위치 정보를 기반으로 이루어지고 있다는 말도 있습니다. 
- 그러므로 위치정보과 시간정보를 최대한 활용해서 모바일 쿠폰을 추천해주는것이 필요할 것입니다.

> ## Commuting 

- 그러면 어떠한 Context 내에서 모바일쿠폰을 추천해야할까요?
  - 대표적으로 Commuting 의 경우가 있을것입니다.
- Commuting(통근) 은 세계적으로 발생하는 현상으로서 대부분의 사람들이 경험하는 Context 입니다. 
  - 또한 이러한 Context 에 있는 사람들은 스마트폰과의 engagement 가 높습니다. 
- 그러므로 Commuting 을 쿠폰 추천에 적극적으로 이용할 수 있을것입니다.

> ## research question

- 위와 같이 Commuting 이라는 Context 를 고려하기로 하였는데요, 다음과 같은 질문들이 자연스럽게 도출될 것입니다.	
  - Commuting 이라는 context 가 모바일 쿠폰의 반응과 관련이 있는가?
  - 그러면 어떠한 관련이 있는가? 

> background

- 기본적으로  통근중에 얼마나 큰 스트레스를 받는지에 대해서 선행 연구가 되어 왔습니다.
  - commuting 에서 발생하는 스트레스가 모바일 쿠폰에 대한 반응률과 어떤 관련이 있을까요? 

![jpg](/assets/images/Stat/147_2.jpg)

- 위와 같이 2가지 관점에 대해서 기전을 주장하려 합니다.
- 사용자가 스트레스를 받으면 식욕이 증가한다. 
  - 만성(매일매일 가해지는) / 급성(갑자기 오는) 스트레스가 있는데 만성의 경우 식욕을 증가시키고, 급성은 저하시킴
  - commuting 은 맨날 겪는 스트레스이므로, 이 경우에 식욕이 높다! 라고 생각할 수 있습니다. 
  - 그러면 Commuting stree 를 받는 사람의 경우 , 음식 추천을 하면 redemption rate 가 높을것이라 예측할 수 있습니다.
- psychology
  - 어떤 종류의 스트레스(내가 컨트롤할 수없는 요소에 의한 압박)를 받게되면, outcome 을 얻을 수 있는 류의 행동을 보이게 됨. (예를 들면 충동 구매 등 ) 
  - 그러면 commuting stress 를 받고있는 사용자에게 outcome 이 예측되는 쿠폰을 추천하면 redemtion rate 가 높을 것입니다. 

![jpg](/assets/images/Stat/147_3.jpg)

> ## Research setting

- 한국의 T map 이라는 앱에서 수행됨 (카카오맵같은거)
  - 이 앱은 내가 어떤 목적지를 찍고, 그 목적지를 어떻게 가야하는지, 대중교통에 타고 있는상태면 언제 내려야되고 환승해야되는지를 알려주는 앱
  - 이 앱을 이용하면 사용자의 위치 정보를 활용할 수  있었음
- 물론 모든 사용자의 위치를 추적하고 있지는 않기 때문에, 어떻게 구체적으로 위치 정보를 얻을 수 있을까요?
- 사용자는 앱을 설치할때 두가지 경로를 입력해야합니다. 
  - 집과 학교(또는 직장) 주소를 입력하게 됩니다. 
- 이때 집 -> 직장 / 직장 -> 집 으로 경로 가이던스를 하는 버튼이 있는데요 이 버튼을 누른 로그가 있는 유저의 경우는 commuting route 라고 정의 / 그 외를 모두 non-commuting 으로 설정할 수 있습니다.

![jpg](/assets/images/Stat/147_4.jpg)

- 위처럼 got me home 또는 got me to work 를 누르게 되면 commuting 루트라고 할 수 있음 (treatment)
- got me somewhere (non-commuting route) 는 commuting 하는 사람이 아닐것이라고 생각할 수 있음 (control)

> Experiment

- 이제 각각의 Treatment , Control 유저에 대해서 랜덤으로 쿠폰 추천창을 보여주게 됩니다.
  - Check the gift 를 누르면 사진이 뜸 
  - 이 사진을 매장에 가면 실물과 교환할 수 있음

![jpg](/assets/images/Stat/147_5.jpg)

- 이떄 준 상품은 위와 같이 도넛, 머핀, 커피, 김밥 등이 있음 
  - 수량은 매우 많이 주었고, 유효기간은 1달짜리로 진행 
- 이때 특정 사용자는 쿠폰을 Commuting route 에서 받은 경우 / Commuting route 에서도 받은 경우가 있어서 제외함
- 10000명 정도의 유저가 15000개정도의 쿠폰을 받았음 
  - Treatment : commuting 에서 쿠폰을 받음 (약 1107명)
  - Control : non-commuting route 에서 쿠폰을 받음 (약 8821명)

# [Analysis : one coupon](#link){: .btn .btn--primary}{: .align-center}

> ## Analysis Method

- 분석은 두가지로 진행하게 되었습니다.
- 쿠폰을 하나만 받은 고객들로 filtering 한 다음에 Control 과 Treatment 그룹을 나누어서 분석
  - 즉 '쿠폰의 갯수' 에 대한 영향력을 줄일 수 있으므로 순수하게 Control / Treatment 를 비교할 수 있음
- 두개 이상의 쿠폰을 받았을때의 고객도 모두 포함해서 분석
  - 얼마나 쿠폰을 줘야하는지? 등도 볼 수 있게 되었습니다.
- 여기에서는 하나의 쿠폰을 받은 유저로 filtering 하여서 분석을 수행해 보겠습니다.

> ## Variable

- dependent variable
  - 쿠폰을 교환(Redeem) 을 했는지 안했는지
- key Independent Variable
  - Commuting 할때 받았는지, 아니면 다른 경우에 받았는지 
- 실험의 유효성을 위해서 Controls 한 변수
  - Parts of the day dummies (어떤 시간?)
  - Day of Week dummies (어떤 요일?)
  - Product dummies, (김밥 , 머핀 등 어떤 상품? )
  - Days to expiration of coupons (쿠폰을 받았을때 유효기간 얼마나 남음?)
  - Usage amount, Usage frequency, Average usage amount (사용자의 특성을 컨트롤 하기 위해 , Tmap 이라는 대중교통 앱을 쿠폰받기 직전 주에 총 몇회, 몇일, 얼마나 사용했는지에 대한 변수 )

> ## Experimental Design

- logistic regression 이용 
  - Experiment 종류는 아래와같이 3가지의 심볼로 표현 가능
- $\mathbf{X}=$ exposure of a group to an experimental treatment
- $\mathbf{O}=$ observation or measurement of the dependent variable
- $\mathbf{R}=$ random assignment of test units;

> 1. Pretest-Posttest Control Group Design (Natural Experiment)

![jpg](/assets/images/Stat/147_6.jpg)

- 위의 실험 디자인은 정말 ideal 한 디자인의 실험
  - Treatment 과 Control 를 랜덤하게 배정 ($\mathbf R$)
  - 실험 이전에 각각의 효과 ($O_1,O_3$) 을 측정 
  - 그 이후에는 실험을 적용한 이후의 효과 ($O_4,O_3$) 를 이용해서, Experiment 의 효과를 측
- Effect of the experimental treatment equals

$$\left(\mathrm{O}_{2}-\mathrm{O}_{1}\right)-\left(\mathrm{O}_{4}-\mathrm{O}_{3}\right)$$

![jpg](/assets/images/Stat/147_7.jpg)

- 그래서 $\left(\mathrm{O}_{2}-\mathrm{O}_{1}\right)-\left(\mathrm{O}_{4}-\mathrm{O}_{3}\right)$ 를 매져하기 위해 DID 모델을 사용하였습니다.
  - Treatment_1 은 treatment 그룹인지 아닌지를 결정 (1,0 의 더미변수)
  - posttrt : 실험 전인지 후인지를 결정 (1,0 의 더미변수)
- 위와 같은 모델에서 결국 $$\left(\mathrm{O}_{2}-\mathrm{O}_{1}\right)-\left(\mathrm{O}_{4}-\mathrm{O}_{3}\right)$$ 값은 $\beta_3$ 이 됩니다.

> 2. Posttest-Only Control Group Design

![jpg](/assets/images/Stat/147_8.jpg)

- 우리가 따르고자 하는 디자인은 위와 같은 디자인입니다.
  - 위 디자인의 특징은Treatment 이전의 효과는 관찰하지 않았습니다.
- 왜 위처럼 Treatment 이전의 효과는 보지 않았을까요? 
  - Treatment 이전의 효과는 바로 쿠폰을 주기 전에 이 사용자가 쿠폰의 redemption rate 가 얼마나 될까? 입니다.
  - 즉 쿠폰을 주기 전에 이 사용자가 쿠폰을 사용하는지 아닌지? 이것을 알수가 없다는 것입니다. (before treatment 효과를 알수가 없음) 

> Logistic regression

- 우리가 사용한 model 은 바로 logistic regression 입니다.

![jpg](/assets/images/Stat/147_9.jpg)

- outcome 이 binary 변수 (1,0) 이므로, 위와 같은 logistic regression 을 사용하였습니다. 
  - Treatment  - Control 의 차이의 위와 같이 $\beta_0$ 으로 세팅됩니다.
  - 즉 redemption likelihood 는 $U_i$ 로 모델링 되고, 이러한 $U_i$ 는 Treatment 의 영향을 받게됩니다.

> ## Experimental Design Summary

![jpg](/assets/images/Stat/147_10.jpg)

- 위에서 비교하고 있는것은 commuter 와 non-commuter target 의 효과(redemption rate)를 비교
- 하지만 이때 commter target 과 non-commuter target 방법간이 비교 가능한지 의문이 될 수 있음
  - 아무리 random assign 했지만 사용자의 구성이 다를 수 있기 때문입니다.

> ## matching

- 그래서 위의 Comparable 을 비교하기 위해서, Matching 방법론을 사용하였습니다.
- Propensity score matching 
  - propensity score 를 각각의 유저에 대해서 계산하게 됩니다. 
- marchign variabale
  - 쿠폰 사용에 대한 변수
    - Usage amount 
    - Usage frequency
    - Average usage Amount
  - 타겟(쿠폰) 에 대한 변수
    - Parts of the day dummies (Morning, Afternoon, Evening, and Night) 
    - Day of Week dummies (어떤날에 받은 쿠폰인지)
    - Product dummies (어떤 물건에 대한 쿠폰인지)
    - Days to expiration of coupons

![jpg](/assets/images/Stat/147_11.jpg)

- 그 결과는 위와 같습니다. 
  - 매칭 전과 후의 경우에 각 두 그룹의 mean difference 가 있는지 없는지에 대한 t- test 를 수행해 봄. 
  - 차이가 없으므로 모두 잘 분배되었음을 알 수 있음
- 이러한 matching 을 점검할때에는 대게 볼떄에 T-Test 를 사용해서 Mean 을 비교합니다!

> Matching method results

- Matching 방법론의 결과는 아래와 같습니다.

![jpg](/assets/images/Stat/147_12.jpg)

- Matching 이후에는 위와 같이 propensity score 가 상당히 비슷한것을 볼 수 있습니다.
- 매칭 전의 경우에는 score 가 연한 회색으로 엄청 차이가 나는듯 했는데, matcing 이후에는 잘 비교되는것을 볼 수 있습니다.

> ## Results

![jpg](/assets/images/Stat/147_13.jpg)

- matched sample을 이용하여 모델링을 수행해 보았습니다. 
- Control 그룹 변수를 어떤 조합을 사용해서 썼느냐? 에 따라서 5개의 모델을 볼 수 있습니다.
  - Application Usage Behavior : 어플리케이션 사용 유형
  - Day to Expiration : 쿠폰이 끝나는 기간 
  - .... 
- control 변수를 어떻게 정할지에 따라서 다양한 모델을 비교해 보았는데, 그 결과는 비슷했습니다.
  - Commuter Target 이 훨씬 좋다는 결과를 보여주고 있습니다.

![jpg](/assets/images/Stat/147_14.jpg)

- redemption rate 가 두세배 차이가 나는 모습을 볼 수 있음

# [Analysis 2 ](#link){: .btn .btn--primary}{: .align-center}

> ## One or more coupon user

- 하나 이상의 쿠폰을 받은 유저까지 포함해서 분석한다고 합시다. 
- 이 경우에, 매칭은 아래와 같이 이루어집니다.

![jpg](/assets/images/Stat/147_15.jpg)

> Static Matching

- Static matching 은 사용자의 모든 시점에서 Treatment 사용자와 Control 사용자의 matching 이 변하지 않고 계속 동일하게 유지
  - matching 하기가 편함

> Dynamic Matching

- 매 시점에서 가장 유사한 Control - Treatment 유저를 매칭하게 됨
  - 즉 시간이 달라질수록 매칭되는 유저가 달라집니다.

> ## Matching

- 매칭 방법은 Static Matching 과 Dynamic Matching 을 사용하였습니다.
  - Parts of the day dummies
  - Day of Week dummies
  - Product dummies
  - Days to expiration of coupons
  - Number of prior redemptions,
  - Usage amount, Usage frequency, Average usage amount

- 위와 같은 변수를 매칭 변수로 사용하였습니다. 그 결과는 아래와 같습니다.

> Static Matching

![jpg](/assets/images/Stat/147_16.jpg)

> Dynamic Matcing

![jpg](/assets/images/Stat/147_17.jpg)

> ## Comparison Matching : Covariate balance

$d_{X}=\frac{\mid M_{X_{t}}-M_{X_{p}}\mid}{\sqrt{\frac{S_{X_{t}}^{2}+S_{X_{p}}^{2}}{2}}}$ and $d_{X m}=\frac{\mid M_{X_{t}}-M_{X_{C}}\mid}{\sqrt{\frac{S_{X_{t}}^{2}+S_{X_{C}}^{2}}{2}}}$

- Control 그룹과 Treatment 그룹간의 mean 차이가 얼마나 큰지를 matching 전과 후에 대해서  테스트 해 보았습니다.

![jpg](/assets/images/Stat/147_18.jpg)

- 위처럼 Covariate balace 관점에서, 다양한 변수들을 비교해 보았을때, Dynamic Matching 의 결과가 좋은것을 볼 수 있습니다.
  - 그래서 우리는 다이나믹 매칭을 쓰기로 하였습니다.

> ## Results : 쿠폰의 수

![jpg](/assets/images/Stat/147_19.jpg)

- 결과는 위와 같습니다.
  - Treatment Effect (Positive) : 즉 commuter target 이 효과가 좋음
  - Number of Coupon (Positive) : 즉 쿠폰 많이줄수록 효과 좋음
  - Number of Coupon $*$ Treatment (Neg): commuter target 은 쿠폰을 많이 주었을때에도 그 효과가 다소 작다는것을 알 수 있음
- 어떤 Control 변수를 사용하던지 결과는 Consistency 하게 나옵니다.
  - 가장 마지막 (모든 변수를 넣은 모델) 에 초점을 나누어서 뒤의 설명을 진행하겠습니다.

![jpg](/assets/images/Stat/147_20.jpg)

- x 축 : 몇번쨰 쿠폰이냐 
- y 축 : response rate 가 얼마냐
- 첫 쿠폰에는 거의 3배 이상 차이가 남.
- 하지만 여러개 쿠폰을 줄때 commuter 의 효과는 별로 없음.. 
  - 많이 주다보면 commuter 보다 non - commuter 에게 더 좋음

> note

- 많은 쿠폰을 주는 전략이 non-commuter 에게는 효과적이지만 commuter 한테는 쿠폰 많이 주는게 별로 효과적이지 않더라! 라는 직관을 얻을 수 있습니다.

> ## Results : Day to Expriation유효기간

![jpg](/assets/images/Stat/147_21.jpg)

- Day to Expiration 을 보면 Positive 의 관계임을 볼 수 있습니다.

- 이때 Day to Expiration $*$ Treatment 가 음수인것을 볼 수 있습니다.

- 그런데 이때 Day to Expiration $*$ Treatment 의 계수가 더 큰것을 알 수 있습니다. (Day to Expiration 보다)

  - ex : Static Matching 의 모델3 의 경우 main effect (0.0439) 보다 interaction 값이 더 큼 (-0.437)

  - 즉 Commuter 의 경우 오히려 기간이 오래 남은 쿠폰을 줄수록 안좋은 효과를 불러일으킨다는 것입니다.

![jpg](/assets/images/Stat/147_22.jpg)

- 위처럼 non-commuter 그룹은 쿠폰의 기간이 오래 남은것을 주는게 효과적이라는것을 알 수 있습니다. 
  - 그에 반해서 treatment 그룹은 그 반대임!

> ## Results : Number of prior redemption (이전에 얼마나 교환했는지)

![jpg](/assets/images/Stat/147_23.jpg)

- 효과가 늘 음수이므로, 이전에 교환한 쿠폰이 많을수록 현재 쿠폰에 대한 교환율이 떨어지게 됩니다.

> ## Key Findif

- Commuter Target 이 non commuter target 보다 좋음
- 쿠폰을 많이 주게될 경우 non commter 가 더 반응이 좋음
- 쿠폰의 잔여 기간이 짧게 남은게 더 반응이 좋음 commuter 에게 반응이 더 좋음
  - 그에 반해 non-commuter : 기간이 길게 남은게 반응이 더 좋음 
- 이전 교환 횟수 (prior redemption )는 현재의 반응에 대해서 악영향이 있음!

# [Robustness check](#link){: .btn .btn--primary}{: .align-center}

> ## demographic 정보

- 데모그라픽 정보를 메인 분석에서 컨트롤 할 수 없었던 이유는 optional 한 서베이에서 측정되었기 때문에 50% 가 넘는 사용자가 응답을 하지 않음 

> Demographic

- robustness check으로 확인을 해 보았는데, 이때 응답하지 않은 (demographic 정보가 없는) 사람을 base line (control) 으로 설정하고 컨트롤 해 보았습니다.
  - 더미 변수를 설정하면 
  - 응답 안함 : 0 / 남자 : 1 / 여자 : 2 로 설정 후 컨트롤

> location

- location 의 경우 로그에 실제 location 정보는 없었음. 하지만 사용자가 쿠폰을 교환한 매장의 주소는 있음. 
- 이 사용자가 모든 쿠폰을 수도권으로 교환했으면 메트로 폴리스 유저로 정의 / 수도권 이외의 지역이면 교외지역 유저로 정의 / 수도권+비수도권 에도 교환하면 트래블링 유저 / 아예 교환 안했으면 non-redemp 유저로 정의
  - 위와 같은 변수를 categorical 변수로 만들어서 컨트롤 

> app user 

- 앱 사용 행동이 Endogenious 할 수 있다는 지적이 있었음
- app usage behavor
  - 사용자가 쿠폰을 받아서 redemption 을 했다면, 이 앱을 사용하니까 쿠폰을 주네 ? 더 사용하면 더 주려나 ? 와 같은 기대가 생기게 됨. 그럼에 따라 앱의 사용량이 늘어날 수 있습니다. 
  - 이를 확인하기 위해서 추가적인 분석을 시행함 
- 이때 그냥 OLS 와 같은 경우 two stage least square 와 같은 방법론은 사용할 수 없었음 . 
  - outcome 이 binary 라 two stage 와 같은 방법은 할 수 없엇음
- 그래서 ols 를 사용해 indegenous 와 같은 변수를 분석함 (분석 결과는 같다고 함 )

# [Arguments](#link){: .btn .btn--primary}{: .align-center}

> ## 메커니즘 1 : 겪는 Event 관점 

- 이러한 논문에서 중요한점중에 하나는 , 이러한 결과가 나오게 된 메커니즘을 밝히는것도 중요함

![jpg](/assets/images/Stat/147_24.jpg)

- commuter 가 non-commuter 대비 스트레스가 높아서 쿠폰의 사용량이 높았음
- non-commuter 와 commuter 가 쿠폰을 받고 나서, 이를 교환하기까지 겪는 Event 가 다름
  - 이러한 이벤트들이 누적되어 쿠폰의 redemption에 영향을 미친다고 볼 수 있습니다. 

> 검증

- 위와 같은 시나리오를 검증하기 위해서는 Redemption Period 사이가 길수록 다른 차이가 남을 검증하면 됩니다.
  - 즉 redemption Period 가 긴 사람일수록 Redemption Rate 가 클 것을 보이면 됩니다. 

![jpg](/assets/images/Stat/147_25.jpg)

- 하지만 위의 결과 (Rdp = Redempion period) 를 보면 기간이 늘수록 점점 효과가 줄어드는것을 볼 수 있습니다. 
- 즉 메커니즘 1에서 제시한 시나리오를 리젝트 하게 됩니다. 

> ## 메커니즘 2 : 겪는 스트레스 점

- 우리가 주장했던것처럼, commuter 의 스트레스가 커서 교환율이 크다고 볼 수 있었습니다. 
  - 이를 검증하기 위해서는 스트레스가 클수록 교환율이 커짐을 보이면 될 것입니다.

![jpg](/assets/images/Stat/147_26.jpg)

- 위처럼 Commuting Stress 가 발생하는 아침 / 저녁 (또는 러시아워) 구간에서만 Treatment Effect 가 Sifnificant 한 것을 볼 수 있습니다.
  - 즉 메커니즘 2를 Support 하는 증거입니다. 

> ## Note : 같은 유저에 대한 분석

![jpg](/assets/images/Stat/147_27.jpg)

- 위 그림의 상단처럼 우리가 했던 분석은 Commuter 과 Non-Commuter 를 독립적으로 바라보고 분석하였습니다.
  - 이는 , 우리가 이전에 Commuter 과 Non-Commuter 둘다 쿠폰을 받은 경우는 배제한것을 알 수 있습니다.
- 위 그림의 하단처럼 "같은 유저" 의 경우 Commuting Route 에서 받은 쿠폰과. Non- Commuter Route 에서 받은 쿠폰의 Redemption Rate 를 비교해 보았습니다.
  - 그 결과는 역시나 Commuter 인 쿠폰의 Redemption Rate 가 높은것을 볼 수 있습니다.

> ## Implications 

- Contextual Targeting 의 효과를 볼 수 있었던 논문 

![jpg](/assets/images/Stat/147_28.jpg)

- 위처럼 쿠폰 추천의 방향을 정할 수 있음

---

**Reference**



