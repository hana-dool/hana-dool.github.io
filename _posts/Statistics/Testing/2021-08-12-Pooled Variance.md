---
title:  "Pooled Variance Test"
excerpt: "더욱더 정확한 추정을 위한 분산 추정"
categories:
  - Stat_Testing
tags:
  - 1
last_modified_at: 2021-08-12

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [Pooled Variance](#link){: .btn .btn--primary}{: .align-center}

> ## Pooled Variance

- 합동 분산이라고도 하는  Pooled variance 는 각 모집단의 분산은 동일하다고 가정할때, 여러 다른 모집단의 분산을 추정하는 방법입니다. 
- 모집단 분산이 같다고 가정하면 통합 표본 분산은 개별 표본 분산보다 더 정확한 분산 추정치를 제공할 수 있습니다. 
  - 이런식으로 더 높은 정밀도는 t -test 와 같이 모집단을 비교하는 통계적 검정 에서 사용될 때 통계적 검정력 을 증가시킬 수 있습니다 . 
- Pooled variance 의 제곱근은 Pooled standard variance 라고도 합니다. 

> ## intuition

- Population 의 Variance 가 같다는 Assumption 하에서는  Pooled Sample Variance 는 모든 정보를 합쳐서 계산하므로, Individual Sample Variance 보다는 훨씬 높은 정확성을 가집니다.

- 이러한 높은 정확성은 Test 의 Power 를 높혀줍니다 '등분산' 이라는 정보를 사용해서 더 테스트를 좋게 만들었다고 생각하시면 좋습니다.

> ## Computation of Pooled variance 

- If the populations are indexed $i=1, \ldots, k$, then the pooled variance $s_{p}^{2}$ can be computed by the weighted average

$$s_{p}^{2}=\frac{\sum_{i=1}^{k}\left(n_{i}-1\right) s_{i}^{2}}{\sum_{i=1}^{k}\left(n_{i}-1\right)}=\frac{\left(n_{1}-1\right) s_{1}^{2}+\left(n_{2}-1\right) s_{2}^{2}+\cdots+\left(n_{k}-1\right) s_{k}^{2}}{n_{1}+n_{2}+\cdots+n_{k}-k}$$

- where $n_{i}$ is the sample size of population $i$ and the sample variances are

$$s_{i}^{2}=\frac{1}{n_{i}-1} \sum_{j=1}^{n_{i}}\left(y_{j}-\overline{y_{i}}\right)^{2}$$

- Use of $\left(n_{i}-1\right)$ weighting factors instead of $n_{i}$ comes from Bessel's correction.

> ## Pooled, Unpooled T-test

![png](/assets/images/Stat/33_3.png)

- 위와 같이 왼쪽은 Unpooled T test / 오른쪽은 Pooled T test 가 됩니다.
- 이 경우 왼쪽은 등분산 가정이 없는 상태 / 오른쪽은 등분산 가정이 있는 상태입니다. 
  - Note ) 원래 General 한 버젼에서 자유도는 더 복잡한 식을 따릅니다만 위와 같이 Conservative 하게 고르는것도 가능합니다.

> ## Pooled Proportion Test

![png](/assets/images/Stat/33_4.png)

- 일반적으로, 위와 같이 비율에 대한 Test 는 무조건 Pooled 를 사용합니다.
- 이는 귀무가설 (평균이 같다) 이 맞으면, 자연적으로 분산도 같아지기 떄문입니다.
  - 이는 data 가 0,1 인 Bernoulli 이기 떄문에 가능한 습성입니다.
- 그러므로 더 정확성이 좋아지는 Pooled Variance 를 사용하지 않을 이유가 없지요.
  - 귀무가설 입장에서 바라보는게 테스팅이고, 귀무가설 입장에서는 분산추정을 더 정확히 하고싶은건 당연하니까요.

---

**Refer**

- https://online.stat.psu.edu/stat500/lesson/7/7.3/7.3.1/7.3.1.1
- https://ncss-wpengine.netdna-ssl.com/wp-content/themes/ncss/pdf/Procedures/PASS/Tests_for_Two_Proportions.pdf
- https://slidetodoc.com/chapter-8-hypothesis-testing-with-two-samples-larsonfarber/
