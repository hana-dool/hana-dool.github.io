---
title:  "Shapley Additive explanations"
excerpt: "게임 이론에 근거한 해석"
categories:
  - Interpretable_ML
tags:
  - 1
last_modified_at: 2021-09-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# [Lime 리뷰](#link){: .btn .btn--primary} 

![jpg](/assets/images/ML/1_35.jpg)

- 대리 함수 g(x) 를 이용해 대신 해석하려 함 (Linear model)
- 무시무시한 고차원을 바로 Linear 에 적합시킬 수는 없으므로, x' 로 변환하는 작업이 필요 (이미지의 경우)
- g 함수가, f 의 예측값을 어느정도 잘 근사하게 (비슷하게) 학습시키고자 함.

# [Additive?](#link){: .btn .btn--primary} 

- 왜 Additive 라는 말이 붙었을까? Additive 는 Additive Feature Attribute Merhods 에서 나온 말입니다.

![jpg](/assets/images/ML/1_36.jpg)

- Lime 의 Surrogate는 Linear 함수로 정의된다. 이 Linear 모델은 Additive Feature Attribute Method 가 됩니다.
  - Feature 는 슈퍼 픽셀이 됩니다.
  - Attribute 는 $\phi$ 가 됩니다.

# [Why Shap is Better?](#link){: .btn .btn--primary} 

![jpg](/assets/images/ML/2_6.png)

- 농구 게임을 한다고 생각해 봅시다.
- 팀의 점수 / 플레이어 ($z_i$) 가 있느냐 없느냐 / 각각 개인의 점수 에 대해서 다음과 같은 성질을 만족해야 할 것이다.
  - 각 팀원의 점수를 합치면 전체 점수가 된다. 
  - 매번 같은 방식으로 플레이하면 같은 점수를 가진다. 
  - 팀 플레이에 참가하지 않으면 점수가 0점이다. 

- Lime 에서는 협업 이론 게임 관점에서, 2가지나 불공평한것이다.

![jpg](/assets/images/ML/1_38.jpg)

- 즉 바라는 특징 3가지(Additive / Consistency / Missingness) 를 가지는 기여도 $\phi$ 를 계산하고자 함. 
- 이런 특성을 갖춘 기여도는 '유일하게 Shapley Value' 임
  - 이러한 Shapley value 를 사용하는 Additive Feature Arribute method 를 사용하면 특성들을 만족하는 공평한 방법이 된다!

# [어떻게 계산될까?](#link){: .btn .btn--primary} 

![jpg](/assets/images/ML/2_7.png)

1. 직관적으로 보자면, 어떠한 사람 i 의 중요도는 i가 있을떄의 스코어 - i가 없을떄의 스코어 가 된다. 
2. 좀더 Formal 하게 정의를 살펴보면, '어떠한 사람 i' 가 있고 / 없고는 어떤 집합에 들어가느냐에 따라서 기여도 차이가 달라짐.
   - 즉 모든 집합에 대해서 i 가 있고 / 없고를 모두 구한 뒤 평균한 값을 취하게 됩니다. 
   - 즉 특정한 Subset 에 국한된 Marginal Contribution 이 아니라 모든 경우에 대해 구한, 공정한 Contribution 이 됩니다.
3. 수식을 그대로 살펴보자면, $\phi_i$ 는 모든 수열에 대해서 구한 값을 평균 낸 것이 됩니다. 
   - 이때에, $\mid S \mid ! (n - \mid S\mid-1)!$ 가 의미하는것은 , i 를 제외하였을떄에 $S$ 를 Permutation * 나머지 permutation 의 가짓수입니다.

![jpg](/assets/images/ML/1_40.jpg)

<BR>

# [Example](#link){: .btn .btn--primary} 

![jpg](/assets/images/ML/2_8.png)

- 예측에 어떤 변수가 제일 큰 기여를 했는지 알고싶다. 

![jpg](/assets/images/ML/2_9.png)

- 위를 볼때에, X2, X3를 사용하지 않았을떄에, X1 의 유무에 따라 그 차이는 4가 됩니다. 

![jpg](/assets/images/ML/2_10.png)

- 위를 볼때에 X2 는 사용하고 , X3은 사용하지 않았을떄에 X1 의 유무에 따라서 그 차이는1이 됩니다. 

![jpg](/assets/images/ML/2_11.png)

- 계속 계산해보면 위와 같이 X2,X3 의 조합의 수만큼 X1 의 영향을 계산할 수 있습니다.
- 그리고 각각의 경우에 대해서 가중치가 다릅니다.  

![jpg](/assets/images/ML/2_12.png)

![jpg](/assets/images/ML/2_13.png)

![jpg](/assets/images/ML/2_14.png)

![jpg](/assets/images/ML/2_15.png)

![jpg](/assets/images/ML/2_16.png)

- 위처럼 모든것을 포함할떄의 예측값 - 아무것도 사용하지 않을떄 예측값 = 모든 Shapley value 의 합 이 됩니다.

  - 즉 예측들을 각 변수들이 사이좋게 나누어먹은것입니다.


# [Advantage](#link){: .btn .btn--primary} 

- 모델 전체를 완전히 설명할 수 있다. 
- **대조 설명(contrastive explanations)이 가능하다.** 즉, 전체와 하나의 관측치를 비교하여 영향도를 구할 수 있고 전체 데이터의 일부분 또는 다른 하나의 인스턴스와 비교해서도 영향도를 구할 수 있다
- **이론적인 배경이 탄탄하다.** Efficiency, symmetric, dummy 그리고 addictivity와 같은 공리들이 설명성에 합리적인 기반을 제공한다

# [Disadvantage](#link){: .btn .btn--primary} 

- Shapley value는 연산량이 너무 많다. 현실의 문제들 중 99.9%에서는 추정방법만이 사용가능하다. 특성들의 가능한 조합(2^k)과 특성의 “결측(absence)”은 아무 관측치로 대체하는 것(이로인해 Shapley value 추청값의 분산이 증가한다.)까지 모두 고려하기 때문에 연산 비용이 너무 크다
  - 연합의 지수적 크기는 샘플링과 반복횟수 M을 제한해서 대처할 수 있다. M을 줄이는 것만으로도 연산 시간을 줄일 수 있지만 Shapley value의 분산을 키울 수 있다.
  -  M에 대한 최적의 수가 따로 정해진건 없다. M은 Shapley value를 정확히 추정하기위해 크면 클 수록 좋다. 그러니 적당한 시간에 계산을 할 수 있는 정도로 정하면된다
- Shapley value는 잘못 해석될 수 있다. 앞서 말한 주의사항처럼 단순히 기여도를 알고싶은 특성을 모델에서 제외했을때 생기는 차이로 Shapley value라고 생각될 수 있다. 그러나 다시 말하자면 Shapley value는 로 다른 특성들의 조합으로 얻은 예측값에 대한 해당 특성(기여도를 알고싶은 특성)의 기여도를 평균하여 계산한 값이다.
- Shapley value는 LIME과 다르게 설명가능한 모델이 아닌 단순히 특성별 기여도를 나타내는 값이다. 즉 입력값의 변화에 따른 예측값의 변화를 설명하기 힘들다. 예를 들면 “내가 1년에 300 유로를 더 번다면 내 신용점수는 5 포인트만큼 오를거야”와 같은 설명이 불가능하다.

# [Refer](#link){: .btn .btn--primary} 

- https://www.youtube.com/watch?v=NF6kk8QkiHE
- https://www.youtube.com/watch?v=f2XqxOny3NA
- https://datanetworkanalysis.github.io/2019/12/23/shap1

