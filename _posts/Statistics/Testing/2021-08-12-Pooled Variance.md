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

<br>

# Pooled Variance

- Pooled Variance 란 각 집단의 Variance 가 같다는 가정 하에서 Variance 를 추정하는 방법입니다. 
- Population 의 Variance 가 같다는 Assumption 하에서는  Pooled Sample Variance 는 모든 정보를 합쳐서 계산하므로, Individual Sample Variance 보다는 훨씬 높은 정확성을 가집니다.
- 이러한 높은 정확성은 Test 의 Power 를 높혀줍니다 
  - '등분산' 이라는 정보를 사용해서 더 테스트를 좋게 만들었다고 생각하시면 좋습니다.

![png](/assets/images/Stat/33_2.png)

- 위와 같이 추정됩니다.

<br>

# Pooled, Unpooled T-test

![png](/assets/images/Stat/33_3.png)

- 위와 같이 왼쪽은 Unpooled T test / 오른쪽은 Pooled T test 가 됩니다.
- 이 경우 왼쪽은 등분산 가정이 없는 상태 / 오른쪽은 등분산 가정이 있는 상태입니다. 
  - Note ) 원래 General 한 버젼에서 자유도는 더 복잡한 식을 따릅니다만 위와 같이 Conservative 하게 고르는것도 가능합니다. 

<br>

# Pooled Proportion Test

![png](/assets/images/Stat/33_4.png)

- 일반적으로, 위와 같이 비율에 대한 Test 는 무조건 Pooled 를 사용합니다.
- 이는 귀무가설 (평균이 같다) 이 맞으면, 자연적으로 분산도 같아지기 떄문입니다.
  - 이는 data 가 0,1 인 Bernoulli 이기 떄문에 가능한 습성입니다.
- 그러므로 더 정확성이 좋아지는 Pooled Variance 를 사용하지 않을 이유가 없지요.
  - 귀무가설 입장에서 바라보는게 테스팅이고, 귀무가설 입장에서는 분산추정을 더 정확히 하고싶은건 당연하니까요.

# Refer

- https://online.stat.psu.edu/stat500/lesson/7/7.3/7.3.1/7.3.1.1
- https://ncss-wpengine.netdna-ssl.com/wp-content/themes/ncss/pdf/Procedures/PASS/Tests_for_Two_Proportions.pdf
- https://slidetodoc.com/chapter-8-hypothesis-testing-with-two-samples-larsonfarber/
