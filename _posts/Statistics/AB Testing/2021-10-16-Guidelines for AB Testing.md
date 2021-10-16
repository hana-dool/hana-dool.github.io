---
title: "Guidelines for A/B Testing"
excerpt: "Etsy Company Data scientist의 12 Guidelines"
categories:
  - AB_Testing
last_modified_at: 2021-10-16

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Etsy 에서 A/B Testing 을 담당했던 A/B Test Datascientist 의 12가지 조언입니다. 
{: .notice--warning}

# [Guidelines for A/B Testing](#link){: .btn .btn--primary}{: .align-center}

> ## **Have one key metric for your experiment**.

- 실험을 위해서 하나의 Key metric 만을 준비해야한다는 것입니다. 
- 이때에 '수입(revenue)' 은 아마 잘못된 선택기준일 것입니다. 
  - 왜냐하면 이 메트릭은 매우 Skewed 된 메트릭이고, 이는 통계적으로 좋은 power 를 가지기가 매우 힘들기 때문입니다.
- 저는 일반적으로 비율(proportion) 메트릭을 추천합니다. 
  - 그 이유는 첫쨰로 우리는 일반적으로 '사람이 무엇을 하는지' 보다 '무엇을 하는 사람 수' 에 더 신경쓰기 떄문입니다.
  - 둘쨰는 이런 비율 메트릭을 사용할 경우에 특이치 (Outlier) 나 표준편차 등에 대한 걱정을 안해도 되기 떄문입니다.
- 왜 측정 기준이 하나여야 할까요? key 매트릭을 여러가지를 보기 시작하면 이는 False Positive 비율이 증가하기 떄문입니다. 
  - 보정방법 (bonferoni...) 을 통해 이를 상쇄할 수 있지만 이는 Test 의 Power 를 낮추고 테스트를 보수적으로 만듭니다. 
- 또한 하나의 Key metric 은 의사결정을 더 명확하게 합니다.
  - 3개의 '동일하게 중요한' 메트릭을 가지는 경우 두개의 메트릭은 증가하는 반면, 다른 하나는 감소할 경우 어떻게 해야할까요..? 
  - 극단적으로 10개를 key metric 으로 가질경우는 어떻게 할까요? 거짓된 차이를 가지는 메트릭이 분명히 존재할 것이며, 또한 결정을 혼란스럽게 만듭니다.

> ## Use key metric do a power calculation

- A/B Test 의 흔한 실수는 적은 Traffic 임에도 불구하고, 일주일동안 실험을 실시하는 경우입니다. 
  -  이러한 경우 만족스러운 수준으로 탐지해 낼 MDE 는 엄청나게 큰 수준일 것입니다.
- 그러므로 먼저 실험을 시작하기 전에 power analysis 를 통하여 x% (MDE) 를 탐지하기 위하여 필요한 시간을 체크합니다. 
  - 이를 통하여 key metric 의 결정에 참고할 수 있습니다. 예를 들어 우리가 보고자 했던 메트릭은 MDE 5% 까지 탐지하고자 했는데, Power analysis 결과 MDE 30%까지만 탐지 가능하다고 합시다. 
  - 이러한 경우, key metric 을 바꾸는것이 필요할 것입니다. (더 적은 Variance 를 가지는 metric 또는 Conversion)

> ## Run your experiment for the length you’ve planned on

-  웬만하면 처음에 결정한 시간만큼 실험을 결정합니다. 
  - p-value 가 5% 아래로 떨어지자마자 멈추지 마세요. 이러한 경우 p-hacking 문제가 발생할 수 있습니다.

> ## Pay more attention to confidence intervals than p-values

- 사실 p-value 보다 confidence interval 과 비슷하다고 생각할 수 있지만 CI 는 '이 실험의 시신뢰성' 도 같이 볼 수 있다는 점에서 p-value 보다 더 좋은 측도입니다.
  - 예를 들어서 , 실험자 수가 100명이던 , 10만명이던 p-value 는 0.04 로 같을 수 있습니다. 
  - 하지만 CI 의 경우 실험자 수가 10만명이면 그 길이가 '더 짧습니다.' 즉 CI 는 실험의 신뢰성까지 얻을 수 있습니다. 
    - 100명일떄의 CI 는 0을 포함하지는 않지만 그 길이가 길것입니다. (신뢰성 있는 결과)
    - 10만명일떄 CI 는 0을 포함하지 않고 그 길이가 짧을것입니다. (신뢰성 없는 결과)

> ## **Don’t run tons of variants**

- 6가지 variant 를 사용하게 될 경우 False Positive 일 확률이 높아집니다.
  - 이는 각 그룹의 인원이 줄어들어서 power 가 낮아집니다.
  -  Multiple Testing 이기 떄문에 또한 False Positive 일 확률도 높아집니다. 
- 그러므로 Control 포함 4개 정도만 실험을 진행하기를 권장드립니다. 

> ## **Don’t try to look for differences for every possible segment**

- 우리는 A/B Test 가 성공했다고 하더라도, Segment 별로 확인하는것이 중요합니다. 
  - 국가별로는 어떨까? 
  - 남/녀 별로 다른 결과가 나오지는 않았을까? 
- 하지만 이렇게 'Segment를 나누어 보는 경우' 에도 False Positive 에서 안전하지 못합니다. 
  - 그러므로 '너무 많은 Segment' 를 보는것은 많은 variant 를 볼떄와 비슷한 묹를 일으킵니다. (False positive)

> ## **Check that there’s not bucketing skew**

- 버켓 skew를 (SRM)  체크하는것은 중요합니다. 
- 이를 탐지하는것 자체는 그저 비율검정을 하면 되므로 어렵지는 않습니다.
- 하지만 이를 어떻게 디버깅할 수 있을까요? 
  - 한가지 방법으로는 웹 브라우저 / 국가 등으로 세그먼트를 나누어 비율을 확인하는 방법이 있습니다. 
  - 특정한 세그먼트에서 비율차이가 매우 큰 p-value 로 나타난다면 그 세그먼트에 대한 설정에서 오류가 났을 수 있습니다. (물론 False positive 를 늘 조심하면서...)

> ## **Don’t overcomplicate your methods**

- Multi arm bandit testing , Bayesian method 등 메트릭을 복잡한 방법론을 이용해 검정하려고 할 수 있습니다.
- 만일 A/B Testing 을 막 시작하는 단계라면 기본적인 구조를 올바르게 만드는것에 집중하는게 좋습니다. (Freq 방법론은 좋은 방법입니다.) 
- 몇년이 지난 지금에도, 실험 구조를 좋게 만드는데에 투자하는것이 , Fancy 한 통계에 방법론에 투자하는것 보다 훨씬 좋습니다.

> ## **Be careful of launching things because they “don’t hurt”**

- 실제로 감지하기에는 작지만, 장기적으로는 부정적인 영향을 미치는 변화가 있을 수 있습니다. 
- 이러한 경우에는 많은 다른 메트릭을 살펴보는게 좋습니다.( Guardrail metric)

> ## **Have a data scientist/analyst involved in the whole process**

- 여기는 생략! (너무나 당연한 소리)

> ## **Only include people in your analysis who could have been affected by the change**

- 즉 Sample 에, 실험에 영향을 받는 사람만 추가하라는 의미입니다.
  - 왜냐하면 Treatment 에 영향을 받지 않는 사람들은 오로지 Noise 로만 작용하기 때문입니다.
- 이는 저의 다른 게시글에서도 많이 다루었으므로 생략! 

**reference**

- <https://hookedondata.org/guidelines-for-ab-testing/>

 이 글 쓴사람도 믿음직 하고, 그 Advise 도 좋은거같아서 번역해 보았습니다. 근데 막상 번역하고 나니까 별 얘기는 없네요...?
{: .notice--success}

