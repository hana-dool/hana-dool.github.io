---
title:  "Rao Cramer Lower bound"
excerpt: "제일 좋은 추정량"
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

<br>

# Rao Cramer Lower Bound

- 우선 아래와 같이 Regularity 를 먼저 정의해야 합니다.

![png](/assets/images/Stat/23_1.png)

![png](/assets/images/Stat/23_2.png)

- 위와 같은 Regularity 를 만족할때 아래와 같은 Rao - Cramer lower bound 가 성립합니다.

![png](/assets/images/Stat/23_3.png)

- 위의 의미는, 어떤 추정량에 대해서, 제일 좋은 추정량의 분산의 하한은 정해져 있다는 것입니다.
- Unbiased 인 경우에는, Variance가 $1/nI(\theta)$ 로 bounded 됩니다.
  - 이때에   $1/nI(\theta)$ 은 데이터 X 가 없는 Constant 입니다.
  - 즉 우리는 완벽한 추정을 할 수 없다는.. 슬픈 사실.. 

