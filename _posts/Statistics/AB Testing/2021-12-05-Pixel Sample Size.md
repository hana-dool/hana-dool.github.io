---
title: "Pixel Federation A/B Test (2018)"
excerpt: "Freq 에서 베이지안 A/B 테스트로 바꾼 이유"
categories:
  - AB_Testing
last_modified_at: 2021-12-05

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

Pixel Federation 에서 A/B 테스트를 수행하는 방식을 Freq 에서 Bayesian 으로 바꾼 이유는 뭘까요?
{: .notice--warning}

# [Bayesian A/B](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

- 1년전(즉 2017) 에서는 NHST (freq 방법론) 을 이용하여 A/B 테스트를 진행했었습니다.
  - Conversion : Chi-squared Testing
  - Revenue : T - test
- 하지만 지금은 베이즈 통계를 이용하고 있습니다. 
  - 여기에서는 NSHT 에서 Bayes 방법론으로 바꾸게 되었는지를 설명해보려고 합니다. 

> ## Interpretability of results

> Frequentist Test 의 Interpretation

- 빈도주의적 관점에서, 미리 결정된 alpha 수준에 대하여 차이가 유의미한지 아닌지를  p-value 를 통해서 결정하게 됩니다.
- 하지만 이러한 p-value 에 대해서 실제로 이해하는 사람은 별로 없습니다. (심지어 통계학과 대학생들도 p value 에 대해서 완벽히 이해하는 사람은 드뭅니다.. ㅜㅜ)
  - 이러한 문제점으로 인하여 p-hacking 과 같은 여러 이슈가 발생할 수 있습니다.
- p-value 를 그나마 직관적으로 설명하기 위하여, A/A 테스트를 매우 많이 실시했을때 우리 데이터가 얼마나 이상한가? 라는 식으로 설명하기도 합니다.
  - 이는 그나마 가장 간단한 p-val 의 해석이지만 여전히 혼란스러운 정의입니다...
- 몇주동안의 테스트 결과가 결국  0.07 의 p-value 가 나왔다고 합시다. 이때  실험의 결과는 '의미 없음' 으로 끝나게 됩니다. (너무 허무...)
  - 즉, 몇주간의 실험치고 우리가 얻는 정보다 너무 적다는 것입니다...

> Interpretation of Bayesian tests

- 베이지안 접근 방식은 직관적이면서 다양한 정보를 제공합니다.
- 특히 Freq 에서처럼, 결과를 해석시에 귀무가설 가정을 동반하지 않으며 이는 좀 더 유연하고 직관적인 해석이 가능하게 해줍니다. 
- p-value 와는 다르게 베이지안 방법론은 다음 3가지 값을 제공할 수 있습니다.
  - P(B>A) – 버전 B가 A보다 나을 확률
  - $E(loss \mid B)$ – B가 실제로 더 나쁜 경우 버전 B에서 예상되는 손실
  - $E(uplift \mid B)$ – B가 실제로 더 나은 경우 버전 B의 예상되는 증가

> Bayesian A/B Results

![jpg](/assets/images/Stat/119_1.jpg)

- 위와 같이 실험의 결과가 나왔다고 합시다. 이 경우 우리는 B 를 선택할 것입니다. 이때에 두가지 가능성이 존재하게 됩니다. 
  - 실제로는 B 가 더 나쁘다면 (3.6%) 그로 인하여 0.026% 의 Conversion 손실을 입을것이라고 예상할 수 있습니다.
  - 실제로도 B 가 더 좋다면 (96.4%) 3.3% 의 Conversion 이익을 얻을 수 있습니다.

> Decision Rules

- 물론 우리는 승자를 결정하기 위해서 Decision Rule 을 결정해야 합니다. 
  - *P(B > A)를* 기반으로 결정할 수 있지만 *E(loss|B)* 기반으로 결정하는게 좀 더 정교한 방법일 것입니다.
  - 기준은 서비스 담당자와 데이터 분석가가 같이 논의하여 정해야 할 것입니다.
- 이러한 결정 규칙은 p-value 만큼 명확하지는 않지만 매우 좋을 것입니다. 
  - 애초에 p-value = 0.05 의 기준은 어떤 맥락에서 의미가 있을지 생각조차 하지 않고 적용하는 경우가 많습니다.

> ## Sample Size 

- 지금까지는 테스트 결과의 이점을 이야기했습니다. 이젭터는 샘플 크기와 관련해서 왜 베이지안 테스트를 사용하게 되었는지를 말하려고 합니다. 
- NSHT 의 단점중 하나는 테스트를 실행하기 전에 샘플 크기를 미리 fix 해야 한다는것입니다. 
- 하지만 베이지안 테스트의 경우 요구사항이 없습니다. 또한 일반적으로 작은 크기에서 더 잘 작동합니다! 

> Freq Sample Size 

- NSHT 에서 왜 샘플 크기를 고정해야할까요? 그 이유는 데이터를 수집하는 방법에 따라서  p-value 가 달라지기 때문입니다.
  - ex : 10000명의 데이터를 얻기 / 100개의 Conversion 이 관찰될때까지 데이터를 얻기 두개의 데이터 수집 룰에 따라서 p-value 는 다르게 계산됩니다. 
  - 이는 직관적이지 않고, 종종 무시됩니다.. (자세한 계산방식은 다른곳에서 설명하도록 하겠습니다.)
- 즉 데이터를 수집하기 전에 테스트에 포함될 Sample 수를 정하고, 미리 정의된 샘플 크기에 도달했을때에만 결과를 평가해야합니다.
  - 하지만 우리는 일반적으로 실험을 할때에 True Sample size 가 얼마나 들어오게 될지 알 수 없으므로 테스트를 효율적으로 Construct 하기가 어렵습니다.
- 그리고 A/B 테스트는 결비용이 많이들기 때문에 가능한 한 효율적으로 테스트 하려고 하고, 고정된 Sample size 에 도달하기 전에 Peeking 하여 조기종료하려고 합니다. 
  - 이는 p-hacking 으로 알려진 문제를 야기하며 이를 해결하기 위해서 베이즈 테스트 또는 순차 테스트 (Continuous test) 를 제안하곤 합니다.

> Bayesian Sample Size

- 베이지안 검정은 유효한 결과를 제공하기 위해 고정된 샘플 수가 없습니다. 결과를 반복적으로 평가할 수 있으며, 그 판단은 계속 유효합니다.
- 이때에 주의깊게 생각하셔야되는게, Bayesian A/B 가 Peeking 을 허용한다고 하는 맥락은 'Peeking 을 하더라도 1종 오류율이 유지된다!' 의 맥락이 아니라 '예상 손실을 유지한다' 입니다. (이에 대해서는 따로 깊히 알아보겠습니다.)
- 좀 더 자세히 말하자면 Peeking 을 하게되면 제 1종 오류율은 베이즈 테스트에서도 에러율은 높아집니다. 하지만 베이지안 테스트는 처음부터 제 1종 오류율을 제한하지 않고. 예상 손실' 을 Decision Rule 로 이용하게 되며, Peeking 을 하더라도 예산 손실을 Bounded 된다는 점에서 Peeking 을 해도 된다고 하는 것입니다. 

> Type 1 error

- 물론 Type 1 에러를 Decision Rule 로 잡지 않겠다는 말은 의학과 같은 과학 연구에서는 치명적입니다. 
- 하지만 우리와 같은 A/B 테스트에서는 상황이 다릅니다. 우리는 항상 A 또는 B 를 선택하며, 실제로 차이가 별로 없거나 매우 작다면 1종 오류를 범한것에 대해서 별로 신경을 쓰지 않습니다. (Optimization 의 관점에서 차이가 적은 에러는 별로 치명적이지 않음)
  - 즉 우리는 오류가 너무 큰 경우의 에러에만 관심이 있으며 이는 제 1종 오류율을 제한하는것보다는 예상손실 (Expected loss) 를 제한하는것이 훨씬 더 합리적이라는것을 의미합니다.

> Less Sample Size 

- 위처럼 'decision rule 의 기준이 되는 값' 이 Optimization 의 입장에서 훨씬 합리적이라는 이점 외에도, 일반적으로 NHST 와 비교하여 동일한 수준의 검정력을 달성하기 위해서 매우 작은 표본크기가 필요합니다.
  - 이는 우리가 좀 더 빨리 결정을 내릴 수 있도록 해줍니다. 

![jpg](/assets/images/Stat/119_2.jpg)

- 위 그림은 각 표본 크기에 대해 1,000개의 카이제곱 테스트와 1,000개의 베이지안 테스트를 시뮬레이션하고 B를 승자로 올바르게 선언한 테스트의 백분율을 계산했습니다.
  - (Note : chi-square test 의 유의수준은 5 % , Bayesian test 는 Expected loss 가 0.1% 보다 낮을때 승자 선언)
- 80% 의 검정력을 얻기 위하여 필요한 표본 크기가 Bayesian Test 에서 훨씬 낮은것을 볼 수있습니다. (절반 미만) 
- 이때 A 와 B 가 효과가 없는경우 (즉 A/A Testing) 를 시뮬레이션 했을때에는 Freq 방법론이 95% 정도의 수준으로 더 맞는 결론을 내었습니다. 

> ## Works in practice

- 위에서 논의한것들이 바로 NSHT 에서 Bayes A/B 테스트로 전환한 이유들입니다.
- 베이즈가 더 좋다는것을 알았으므로, 이제는 어떻게 Bayes A/B Testing 을 적용할 수 있는지에 대해서 알아봅시다. 

> Conversion 

- Conversion 의 경우 전환율에 대해서 Ber 분포를 가정합니다. 다음과 같은 소스에서의 공식을 사용합니다. (정리하면 ber + Beta Conjugate)
  - <https://www.evanmiller.org/bayesian-ab-testing.html>
  - <https://www.chrisstucchio.com/blog/2014/bayesian_ab_decision_rule.html>

> Continuous 

- 수익 데이터의 경우 전환 베르누이 분포로 전환율을 별도로 추정하고 지수 분포를 사용하여 지불 금액을 별도로 추정합니다. 이 문서를 기반으로 구현했습니다.
  - Chris Stucchio의 VWO [에서의 베이지안 A/B 테스트](https://cdn2.hubspot.net/hubfs/310840/VWO_SmartStats_technical_whitepaper.pdf)

> Code

- 이 소스를 사용하여 R에서 A/B 테스트 계산기를 구현했습니다. 여기에서 시도해 볼 수 있습니다.
  - [변환을 위한 베이지안 A/B 테스트](https://vidogreg.shinyapps.io/bayes-conversion-test/)
  - [ARPU에 대한 베이지안 A/B 테스트](https://vidogreg.shinyapps.io/bayes-arpu-test/)

> ## Summary

- 베이지안 A/B 테스트를 사용하여 이제 더 실행 가능한 결과로 더 빠르게 테스트를 수행할 수 있습니다. 장점을 요약하자면 다음과 같습니다.

| **빈도주의자**                                               | **베이지안**                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| P 값은 이해하기 어렵고 비즈니스 가치가 없습니다.             | 결과는 명확한 비즈니스 가치를 가지며 이해하기 쉽습니다.      |
| 우리는 차이가 없는 테스트에서 유익한 결론을 내릴 수 없습니다. | 우리는 항상 유효한 결과 (이길확률 등)를 얻고 최소한 정보에 입각한 결정을 내릴 수 있습니다. |
| 샘플 크기를 고정하지 않으면 테스트가 유효하지 않습니다.      | 샘플 크기를 고정할 필요는 없습니다.                          |
| 더 큰 샘플 크기가 필요합니다.                                | 더 작은 샘플 크기로 충분합니다.                              |

---

**reference**

- <https://mobiledevmemo.com/its-time-to-abandon-a-b-testing/>

