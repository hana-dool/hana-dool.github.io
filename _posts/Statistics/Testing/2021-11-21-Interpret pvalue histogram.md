---
title:  "Interpret a p-value histogram"
excerpt: "p value histogram 해석하기"
categories:
  - Stat_Testing
last_modified_at: 2021-11-14

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 부트스트랩을 이용한 가설검정 절차
{: .notice--warning}

# [p-value histogram](#link){: .btn .btn--primary}{: .align-center}

> ## p-value histogram

- 우리는 다중검정을 통해서 테스트를 매우 많이 실시해야 되는 경우가 있습니다.
  - 각각 유전자에 대한 발현 여부 테스트라던지
  - 수백개의 나라에 대한 Multiple Testing 등...
- 하지만 위와 같은 다중 가설검정의 경우 위험성이 생기고 이를 Correction 하기 위해서 다양한 방법을 실시합니다. 
- 하지만 이런 Correlation 작업을 하기 전에, '우리 실험들이 과연 어떠한 상태일까? ' '완전히 의미없는 테스트들을 수행하고 있는것 아닐까?' 등의 의문이 들 수 있습니다. 
  - 이런 경우에 어떻게 하면 , 실험들의 Truthworthy 를 알 수 있을까요? 
- 이런 사전 진단용으로 사용될 수 있는게 바로 p-value histogram 입니다.
  - p-value histogram 이란, 많은 실험들에 대해서 각각의 p-value 를 히스토그램 형태로 나타낸 것입니다. 

![png](/assets/images/Stat/108_1.png)

- 위처럼 다양한 p-value histogram 을 통해서, '현재 실험이 어떤 상태' 인지 알 수 있습니다. 

> ## 시나리오 A : Anti Conservative

> Figure

![png](/assets/images/Stat/108_2.png)

- 위와 같은 p - value 를 얻었다면 우리는 정상적인 실험을 잘 실험한 것입니다.

![png](/assets/images/Stat/108_3.png)

- 그 이유는 위와 같습니다. 일반적으로 모든 실험이 귀무가설만을 지지할 경우에 (즉 효과가 없는것이죠..) 는 위와 같이 빨간색의 그래프 추이가 나오게 됩니다.
  - 그 이유는 P-value 의 설계 자체가 uniform 한 분포가 나오게 하기 때문이죠.
- 하지만 대립가설을 지지하는 실험이 많을 경우에는 위의 파란색 분포처럼 Exponential 과 같은 분포를 띠게 됩니다.
  - '대립가설쪽' 으로 증거가 있는 실험이 많으므로, 실험도 많이 기각하게 되는 것이죠.

> Summary

- 즉 정리하면 실험의 p  - value 추이가 오른쪽으로 skewed 된 추이를 보인다면, 실험들이 귀무가설을 많이 기각하는 , 좋은 실험을 만든 것입니다 .

![png](/assets/images/Stat/108_4.png)

- 위처럼 많은 실험이 귀무가설이 틀릴 경우에 점점 우측하단처럼 skewed 가 심해질 것입니다.

> ## 시나리오 B : 균일한 p값

> Figure

![png](/assets/images/Stat/108_5.png)

- 위와 같이 Uniform 한 분포를 가질때입니다.
  - 이는 우리의 실험이 너무 효과가 없어서, 대부분의 비교가 귀무가설만을 지지 (즉 효과가 없음) 하고 있는 상태입니다. 

- 위와 같은 경우 기껏해야 소수의 가설만이 Null 이 아닐것입니다.
  - Benjamini-Hochberg와 같은 FDR 수정 방법을 사용하면 이를 식별할 수 있을 것입니다. 
- 위와 같은 경우 0.05 보다 작으니 받아들여야지~ 와 같은 행동은 하면 안될것입니다! 

> Summary

- 대부분 효과없는 실험일때 uniform 하게 나타남

> ## 시나리오 C : Bimodal p-values

> Figure

![png](/assets/images/Stat/108_6.png)

- 위와 같이 0쪽과 1쪽에 Figure 가 높게 나오는 경우입니다. 

- 위와 같은 경우  false discovery rate control 을 하려고 하면 안됩니다.
  - 왜냐하면 FDR 을 조절하는 방식은 애초에 p-valur near 1 이 uniform 하다는 가정에서 시작하니까요 
- 그러므로 우선 Correction 을 마우생각없이 하려고 하지 말고, 왜 위와 같은 모양이 나오게 되었는지 조사해 봐야 합니다. 

> 1.혹시 One Tail Test 를 하고 있나요? 

- 즉 약물이 몸무게를 '줄여준다' 만 대립가설로 보고있는것 아닌가요? 
  - 어떠한 약물이 '몸무게를 늘이는 경우' 가 많다면 위와 같은 p-value histogram 이 나오게 됩니다. 
- 즉 One tail 을 사용하는데 , 대상들의 효과가 양쪽으로 다양하게 나오게 되면 위와 같은 추이를 얻게 됩니다. 
- 이런 경우, 좀 더 다양한 정보를 얻기 위해 Two Tail 을 쓸 수 있을것입니다.
  - 즉 위와 같은 상황은 반대쪽에 대한 정보도 많은 상황이니까 이걸 놓치는거는 아깝잖아요.

> Summary 

- 이상한 상황! Correction 을 적용하지는 말고 원인을 찾는게 중요.

> ## 시나리오 D : Conservative p-values

> Figure

![png](/assets/images/Stat/108_7.png)

- 위와 같이 1에 p 값이 몰려있는 (즉 우상향) 의 그래프입니다.
- 이러한 상황은 단순히 '가설이 효과가 없는거같아요' 가 아닙니다.
  - 효과가 없었으면 , 모두 귀무가설을 지지하므로 Uniform 한 모양을 띠었겠죠..

- 위와 같은 상황은 테스트에 문제가 있는것을 나타냅니다.
  - 데이터가 불연속인데 연속으로 가정하고 테스트 한 경우
  - 데이터가 심각하게 Assumption 과 다르게 비정상적인 경우

> Summary

- 실험 세팅이 잘못된 경우입니다. Assumption 을 체크해보세요

> ## 시나리오 E : Sparse p-values

> Figure

![png](/assets/images/Stat/108_8.png)

- 위와 같이 Sparse 한 p 값을 나타내는 경우는 어떻게 할까요? 
- Spare 한 p value 도 역시나 정상적인 경우가 아닙니다. 다음과 같은 경우가 이런 현상의 원인이 될 수 있습니다.
  - Bootstrap / Permutation 을 실시했는데 , iteration 을 너무 조금 하지 않았나요? 이러한 경우 많이 실시 (최소 1000) 해야 정확한 실험 결과를 얻을 수 있습니다.
  - Nonparameteric test 를 하는데 (wilcoxon rank sum 등) 샘플사이즈가 너무 작지 않았나요? 
  - 실험 데이터가 특정한 값만이 많이 나오는 데이터였나요?
- 이러한 경우에도 False Discovery Rate Control 을 하지 마세요. 이러한 수정은 p-value 가 uniform conti 하다는 가정을 하니까요

> Summary

- 데이터를 살펴보거나, 비모수 테스트를 실시하지는 않았는지 알아보세요.

> ## 시나리오 F : Something even weirder

> Figure

![png](/assets/images/Stat/108_9.png)

- 한마디로 말하면 '겁 나 이 상 한 경우' 입니다. 
- 이런 경우에는 어떠한 Correlation 을 하려고 하지 말고 Assumption 체크를 하던지, 데이터를 보던지.. 해야 합니다. 

> Summary

- 통계학자를 찾아가세요..

---

  **Reference**

- <http://varianceexplained.org/statistics/interpreting-pvalue-histogram/>





