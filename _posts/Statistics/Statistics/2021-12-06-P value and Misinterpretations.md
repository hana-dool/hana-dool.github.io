---
title:  "Statistical tests, P values, confidence intervals, and power"
excerpt: "misinterpretations 에 대한 가이드라인 논문" 
categories:
  - Statㄴ
last_modified_at: 2021-12-05

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Likelihood Principle 에 대해서 알아보도록 합시다.
{: .notice--warning}

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## Abstract

- 통계 테스트, 신로구간, 검정력의 잘못된 해석은 지난 수십년동안 이슈가 되었지만 여전히 만연합니다. 
- 이렇게 된 이유는 이러한 개념들이 어려워서, 간단하고 직관적이며 절대적인 해석이 없다는것에 있습니다.
  - 그래서 이러한 개념을 간단하게 소개하기 위해서 간단하게 풀어쓴 정의들이 많지만 많은 정의는 사실 틀린 정의입니다. 
- 우리는 여기에서 25가지의 잘못된 해석에 대한 설명 목록을 제공하고, 통계적 해석을 올바르게 하는 법을 소개하고자 합니다.

> ## Introductino

> 잘못된 해석들

- Statistical Test 의 잘못된 해석, 남용은 수십년동안 골머리입니다. 
  - 어떤 Scientific journal 은 statistical significance 의 사용을 아예 금지하려고도 합니다. 
- 어떠한 저널은 모든 통계 테스트, 신뢰 구간과 같은 통계적 방법론을 금지하기까지 하고 있습니다.
  - 이러한 금지에 대한 장점에 대해서는 상당한 논쟁 부분입니다.



# [misinterpretations of single P values](#link){: .btn .btn--primary}{: .align-center}

> ## p 값은 테스트가 참일 확률이다.

검정에서 p-value 는 0.01 이 나왔다면, 귀무가설이 참일 확률은 1% 일거야 !
{: .notice}

> 바로잡기 1 : pvalue 의 정의

- P 값은 '귀무가설이 참일 확률' 을 말하지 않습니다. P value 는 귀무가설이 맞을때에 내 데이터가 대립가설 쪽으로 얼마나 이상한지 를 말하는 값입니다.
  - P value 는 단순히 Null Hypothesis (귀무가설) 과 얼마나 가까운지 만을 나타날 뿐입니다.
- p-value : 0.01 : 데이터가 Null Hypothesis 와 매우 멀다는것을 의미 (Not 1%!)

> 바로잡기 2 : Freq 의 Framework

- 귀무가설은 다음과 같이 모수에 대한 정의로 시작된다는것을 기억하세요! 

$$H_0 : \theta = 0$$

- 즉 귀무가설이 맞다는것은 애초에 parameter $\theta$ 를 모수 취급하겠다는 것인데, 이러한 접근은 Bayes 의 접근법입니다. Freq 에서 모수는 Constant 에요! 그니까 확률도 없는것입니다.

> ## p 값은 내 데이터값을 얻을 확률이다.

검정에서 p 값이 0.01 이 나왔다면, 우연히 내 데이터를 얻을 확률은 1% 일꺼야! 
{: .notice}

>  바로잡기 

- 확률을 논할떄 $P(D \mid H_0)$ 을 p-value 로 정의한다는 것을 기억합시다. 
- 즉 위의 논의는 $P(D)$ 를 나타내는것이고,  이 값은 모수에 대한 가정이 없으므로 일반적으로 구할 수 있는 값이 아닙니다.

> ## p 값이 0.05 미만이면 Test Hypothesis 가 틀리다.

> 바로잡기

- 귀무가설이 맞더라도 단순히 우연으로 데이터가 대립가설쪽으로 쏠려서 0.05 보다 작은 p-value 를 가질 수 있습니다.
- 또는 무작위 오차(Error) 가 커서 p-value 가 작게 나왔을 수 있습니다. 
- 데이터 계산에 사용된 가정사항이 위반되어ㅓ 작아질 수 있습니다.

> ## P 값이 0.05 이상이면 이는  Test hypothesis 가 맞다.

> 바로잡기

- 이 역시 위와 같은 이유다. 높은 p-value 는 대립가설이 맞더라도 충분히 높게 나올 수 있다.
- 다만 대립가설의

---

**Reference**

- <https://link.springer.com/article/10.1007%2Fs10654-016-0149-3>









