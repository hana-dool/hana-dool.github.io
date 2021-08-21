---
title:  "[Test] Robust Two Sample Test"
excerpt: "Robust 한 비모수 Test"
categories:
  - Stat_Non_Parametric
tags:
  - 1
last_modified_at: 2021-08-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

- http://faculty.washington.edu/yenchic/18W_425/Lec1_TwoSample.pdf

# Introduction

- 실제 많은 상황에서 우리는 Two Sample Test 를 주로 하게됩니다.
- 예를 들어서 다음과 같은 상황을 가정하고 , 서술을 이어가봅시다.
- 어떤 연구소에서 질병을 치료하기위해서 신약을 개발했다고 합니다.
- 그러면 이 연구소에서는 이 신약을 테스트하기 위해서 임상 실험을 하려 할 것입니다. 
- 연구소는 임상실험에서 환자들을 모집한뒤 , 대조군 / 치료군 2가지로 나눠서 실험을 하려 할 것입니다.
- 두 그룹의 반응을 비교하여서 다른지 아닌지에 검사하고, 이게 정말 다른지 아닌지 검사하게 됩니다. 
- 우리는 위의 상황을 아래와 같이 단순화 할 수 있습니다. 

![png](/assets/images/Stat/42_1.png)

- 위에서 $P_X, P_Y$ 는 Population 을 의미합니다. (cdf , pdf 를 의미한다고 해도 됩니다.)
- 만약 약이 아무 효과가 없다면, 두 모집단의 분포는 같을것입니다.
  - 즉 $H_0 : P_X = P_Y$ 로 두고 테스트를 하게 됩니다.
- 하지만 위의 테스트를 진행하는것은 쉽지 않습니다. $P_X,P_Y$ 는 cdf 이기 떄문입니다.
  - 이러한 분포가 같다는것을 테스트하는것은 매우 힘듭니다.
- 그러므로 우리는 주로 Two Sample Mean Test (Z-Test 또는 T-Test) 를 진행하곤 합니다. 
  - $H_0 : \mu_X = \mu_Y$
- 그러나 이러한 Mean 은 Outler 가 있는경우 그 신뢰성이 달라집니다. 

![png](/assets/images/Stat/42_2.png)

- 두 집단의 Sample Avergae 는 모두 0 입니다. 하지만 대부분의 값들은 $S_Y$ 가 더 큽니다.
- 이러한 경우 대부분의 Mean Test 는 테스트에 실패하게 됩니다. 
- 이러한 Outlier 에 대해 Robust 한 테스트들을 알아보도록 하겠습니다.
- 각기 양이 좀 되서, 다른 문서에서 알아보도록 하겠습니다.
  - Sign Test
  - Sined- Rank Test
  - Rank-sum Test
  - Median Test
- 4 가지에 대해서 알아보겠습니다.
