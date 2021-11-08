---
title: "Mutivariate testing at Optimizely(2017)"
excerpt: "Optimizely 에서 다변수 테스트를 실행하는 방법"
categories:
  - AB_Testing
last_modified_at: 2021-11-08

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Optimizely 에서 어떻게 다변수 테스트를 수행하고 있는지에 대해서 알아봅시다. 
{: .notice--warning}

# [Multivariate Test](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

- Multivariate Testing 은 여러개의 Variants 를 한번에 실험하는 방법론입니다. 
  - 하지만 많은 variants 는 높은 False positive 의 수가 증가하게 됩니다.
  - 이러한 문제는 multiple comparisons or multiple hypothesis testing problem 으로 알려져 있습니다. 
- 이러한 문제를 다루기 위하여 두가지 대표적인 방법을 소개하자면 다음과 같습니다.
  - FWER 을 제어하는 Bonferroni 방법
  - FDR 을 제어하는 Benjamin Hochberg 방법 
- 이떄 Bonferrnoi 방법에서 $\alpha = 0.05$ 로 Control 하겠다고 정하게 되면 우리는 FWER 을 5% 로 제어하게 됩니다. (Bonferroni q-values 이용)
  - 이떄 Bonferroni q-values 란,  FWER 를 Control 하기 위하여, 조절된 adjusted p-value 라고 이해하시면 됩니다.
- Benjamin Hochberg 방법에서 $\alpha = 0.05$ 로 Control 하겠다고 정하게되면 우리는 FDR 을 5% level 로 제어하게 됩니다. (BH q-values 이용)

> ## Dashboard 

- Optimizely 에서는 대시보드에 이러한 q - 값을 표시한다고합니다. 
- 즉 사용자는 3개의 P value 에 대해서 각각 얻을 수 있는 정보가 있습니다.
  - 여기서 딜레마는 FWER Control 은 가장 안전한 추론을 제공하지만, Power 가 너무 낮다는 것입니다. 
- 우리는 사용자 연구를 통하여 Optimizely 의 고객이 의사결정을 할 떄에 FDR 이 가장 직관을 잘 반영한다는것을 알았습니다. 
  - 즉 고객은 그들이 얻은 '유효하다고 얻은 결론' 들이 얼마나 정확한지 에 대해서 관심이 많았다는 것입니다. 
  - '실험에서 내리는 모든 결정이 맞을 확률' 에 대해서는 그다지 관심이 없었습니다. 

> ## Appendex : Calculation

![png](/assets/images/Stat/97_1.png)

---

**reference**

- <http://library.usc.edu.ph/ACM/KKD%202017/pdfs/p1517.pdf>

