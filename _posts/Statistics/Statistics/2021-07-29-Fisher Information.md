---
title:  "Fisher Information"
excerpt: "피셔 정보량이 의미하는것이 뭘까?"
categories:
  - Stat
tags:
  - 1
last_modified_at: 2021-07-30

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

#  Fisher Information

- 피셔 정보량은 Random Variable X 가 $\theta$ 파라미터에 대해서 얼마나 정보량을 가지고 있는지에 대해서 나타냅니다.

![png](/assets/images/Stat/21_1.png)

- 위와 같이 먼저 Score Function 을 먼저 정의합니다.
  - Score function 이란, $log (f(x\mid \theta )))$ 가 고정된 $x$ 에 대해서 $\theta$가 변할때에 얼마나 변하는지를 재는 함수입니다.
  - 즉 pdf 가 특정한 x 에서 모수의 변화에 대해서 얼마나 Sensitivity 하게 변하는지를 Measure 한다고 생각하시면 됩니다. 
- Score function 은 위와 같이 x 에 대해서 평균을 취하게 된다면, 0 이 됩니다. 즉 loglikelihood 의 변화량을 모든 x 에 대해 평균을 취하게 된다는 것입니다.
  - 만약 0보다 크다면, 특정한 theta 를 변화시킬때에 평균적으로 pdf 가 상승한다는 의미이고, 이는 pdf 의 합이 늘 1이라는 말에 위배되는 것입니다. (rough 하게 이해하면..)
- Information Value는 이러한 Score function 의 variation 으로 정의됩니다. 
  - 즉, $\theta$ 에 대한 log likelihood 의 변화량의 분산을 Information Value 라고 합니다.

<br>

# What it Means?

- 피셔 정보량을 조금만 더 직관적으로 이해해 봅시다. 
- 피셔 정보량은 Random Variable X 가 $\theta$ 파라미터에 대해서 얼마나 정보량을 가지고 있는지에 대해서 나타낸다고 했었죠? 그런데 어떻게 대체 정보량을 가지고 있다는걸까요?
- 먼저 로그 가능도의 이계도함수 평균의 음수가 FIsher information 이므로 이, 로그가능도의 이계도 함수의 의미를 먼저 살펴보겠습니다.
- 만약 이 로그 가능도의 이계도 함수가 매우 크다 (0으로부터 멀다) 는 것은, 기울기가 급격하게 변한다는 것이므로 봉우리에서 급격하게 변하는것을 상상할 수 있습니다.
- 이 로그 가능도의 이계도 함수의 평균이 매우 작다 (0에 가깝다) 는 것은, 기울기가 매우 완만하다는것이므로, 이는 봉우리에서 매우 완만하다는것을 나타냅니다.
- 로그가능도 함수를 두번 미분한 값에 대해서 평균을 취하고 음수를 취한것이 바로 FIsher information 이였습니다. 
  - 즉, Fisher information 이 크다는것은, 봉우리 근처에서 뾰족하다는것을 나타냅니다.
  - Fisher information 이 작다는것은 봉우리 근처에서 작다는것을 나타냅니다.
- 즉 ! 모수 근처에서 뾰족하다는건 데이터가 모수에 대해서 확실한 추정을 하고 있다는것이므로 Fisher information 이 큰것입니다. 
- 피셔 정보량은 Random Variable X 가 $\theta$ 파라미터에 대해서 얼마나 정보량을 가지고 있는지에 대해서 나타낸다는것이 이해가 가겠죠?

<br>

# With Sample Size

- Sample Size 가 N 개라고 합시다. 그러면, 이 N 개에 대해서 Likelihood 함수는 N 제곱배가 됩니다.
- 이를 로그 취하면 N 배가 되겠죠 ? 그리고 그에 따라서 이계도함수를 구해보면 N 배가 됩니다.
- 즉 Fisher Information 은 Sample size 가 N 이라면 1개인것에 비해 N 배가 됩니다. 
- 이는 , Sample 수가 더 클수록 Likelihood 가 뾰족해지고 (N제곱배가 되므로 낮은값은 더더욱 낮아지고 큰 값은 덜 낮아짐) 이는, 모수에 대해서 더 많은 정보량을 얻을 수 있다는 직관과 일치합니다. 

<br>

# MLE?

- 위에서처럼, 피셔 정보량이 크다는것은 결국 로그 가능도 함수가 뾰족하다는것을 의미합니다. 
- 즉 이는 MLE 의 성질과 이어진다고 예측할 수 있는데.. 아니나 다를까 역시나 연관됩니다.
- MLE 부분을 봅시당..

<Br>

# Bayeisan?

- 베이즈 정리에서와도 연관되는데, 샘플 사이즈가 크면 Assymptotic 하게 Fisher information 과 관련된 Normal 분포로 근사한다는 정리ㅇ가 있습니다.
- 즉 Prior 과는 상관없이 늘 Normal 을 따른다고 볼 수 있죠.
- **Bernstein-von Mises theorem** 을 참고합시당...
