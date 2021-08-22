---
title:  "Two, One Tail Paradox"
excerpt: "가설에 따라 달라지는 판단(ing)"
categories:
  - Stat_Paradox
tags:
  - 1
last_modified_at: 2021-08-22

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

- NOte : 시간문제로 아직 완전히 이해하지는 못해서 계속 추가하겠습니다.

# 가설에 따라 달라지는 판단?

A 와 B 의 차이를 검정하고 싶다고 합시다. 그래서 $\bar{A} - \bar{B}$ 의 분포를 아래와 같이 얻었습니다.  (부트스트랩으로 데이터를 여러번 추출하여서 얻었다고 하자.)

![png](/assets/images/{Statistic}/2_1.png)

이제 위 분포에서 각기 다른 가설들을 검정해보자. 가설을 검정하기 위해 얻은 통계량 $\bar{A} - \bar{B}$  = 1.4 라고 하자. 

1. $H_0 : \mu_a - \mu_b \le 0$  vs $H_1 : \mu_a-\mu_b >0$

위 귀무가설을 검정하기 위해서는 아래의 빨간 선 왼쪽 확률을 계산하면 p-value 가 나올것이다. 이 값은 0.0294 가 나온다. 즉 A평균이 B평균보다 크다고 할 수 있다.

![png](/assets/images/{Statistic}/2_2.png)

2. $H_0 : \mu_a - \mu_b \ge 0$  vs $H_1 : \mu_a-\mu_b <0$

위 귀무가설을 검정하기 위해서는 아래의 빨간 선 왼쪽 확률을 계산하면 p-value 가 나올것이다. 이 값은 0.9716 가 나온다. 즉 A평균이 B평균보다 크다고 할 수 있다.

![png](/assets/images/{Statistic}/2_3.png)

3. $H_0 : \mu_a - \mu_b = 0$  vs $H_1 : \mu_a-\mu_b \not=0$

위 귀무가설을 검정하기 위해서는 양쪽 빨간선 바깥쪽 확률을 검정해야한다. 이 값은 0.0615이다. 즉 A 와 B 평균간 차이가 없다고 할 수 있다.

![png](/assets/images/{Statistic}/2_4.png)

위와 같이 다른 가설에 따라 p-value 가 달라지고, 그에 따라서 판단도 달라지는것을 확인할 수 있었다. 

# 잘못된 이해

- 위와 같은 결과를 어떻게 이해할 수 있을까요..? 
- 일반적으로 위의 결과를 보고 사람들은 '양측검정이 좀 더 엄격하고 보수적으로 검정한다.' 라고 생각하게 됩니다.
  - 그러므로, 단측검정이 더 많은 1종오류를 생성하고 또한 양측검정보다 안좋다고 이해합니다. 
- 하지만 위와 같은 말은 사실이 아닙니다. 위와 같은 에러를 어떻게 해결할 수 있을까요? 

# 해설

- 위의 에러는 우리가 가설을 기각하고 나서의 결론만 집중하고, 그 과정 ( 어떤 귀무가설을 기각했는가? ) 을 고려하지 않아서 나오는 에러입니다.

- 단측검정의 경우
  - $H_0 : \mu_a - \mu_b \le 0$  를 기각하고 $H_1 : \mu_a-\mu_b >0 $ 를 선택하게 됩니다.
- 양측검정의 경우 
  - $H_0 : \mu_a - \mu_b = 0$  를 기각하고 $H_1 : \mu_a-\mu_b \not=0$ 를 선택하게 됩니다.
- 위와 같이 '다른 귀무가설' 을 기각하고, 대립가설을 선택하게 되므로 실제 가설이 없었음을 알 수 있습니다.

# 적용

- 위와 같은 경우, 결국 어떤 상황에서 어떻게 적용해야 좋을까요? 

## AB Test 에서는..?

- A 가 기존의 Control 이고 B 가 Treatment 라는 AB 테스트의 상황을 가정합시다.
- two Sided Test 에서는 다음과 같은 결론이 있을것입니다.
  - 귀무가설 기각 + A<B  : Treatment 적용
  - 귀무가설 기각 + A>B  : Treatment 미적용
  - 귀무가설 기각불가 : Treatment 미적용
- 위와 같은 사례를 본다면 귀무가설을 '기각' 하더라도 Decision 이 A<B 또는 A>B 에 따라서 나뉩니다. 
- 즉 다시말하면, A=B 나 A>B 인 경우는 같은 행동을 취한다는 것입니다. 
- 이러한 경우, One SIded Test 가 더 좋습니다. 왜냐하면 어짜피 우리의 행동은 A<B  이냐 , 아니냐 2가지이며, 이에 대해서 Error 를 계산하고 실험계획을 세워야 하기 때문입니다. 
- , Two Sided Test 의 경우는 A != B , A=B 두가지만을 나타내며 각각의 가설은 우리의 행동에 적절하지 않기 떄문입니다.
  - 즉 위의 가설에 의해 설계된 테스트는 우리의 바램과는 잘 맞지 않습니다.
  - 단적으로, alpha = 0.05 로 설정한 경우, 우리의 바램은 Treatment 가 더 좋은데 실수할 확률을 0.05 로 Bounded 시키길 기대합니다만, Two Tail 에서는 0.025 로 Bounded 시키는것과 같은 효과를 불러일으킬 뿐입니다.

## 다른 경우..?

- 하지만 만일 A>B , A=B , A<B 모두의 상황이 의미있는 경우는 위와 다르게 Two Tail Test 를 해야할 것입니다.

# Reference

- https://www.onesided.org/articles/the-paradox-of-one-sided-v-two-sided-tests-of-significance.php
- https://rebeccaebarnes.github.io/2018/05/01/what-is-a-p-value
- https://blog.analytics-toolkit.com/2017/one-tailed-two-tailed-tests-significance-ab-testing/
