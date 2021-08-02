---
title:  "Multiple Comparison"
excerpt: "다중비교"
categories:
  - Stat_Testing
tags:
  - 1
last_modified_at: 2021-08-02

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# Multiple Comparison

- Multiple Comparison 이란, 여러개의 가설을 한꺼번에 검정하는 것 입니다. 
- 하지만 이렇게 설정할 경우, 유의수준의 설정에 에러가 생기고 마는데요. 아래의 계산 결과를 보면 알 수 있습니다.

![png](/assets/images/Stat/25_1.png)

- 위의 경우에는, 통계적 가설을 20개 한번에 비교하는 상황이고, 각각의 가설은 유의수준이 0.05 인 상태입니다.
- 하지만 0.05 로 유의수준을 하게되면, 다중비교를 할 때에, 적어도 하나 이상 틀릴 확률이 64% 나 되게 됩니다. 
- 통계적 가설의 수립 / 검정 과정에서는 유의수준을 먼저 고정하고 테스팅 한다는것을 기억합시다. 위와 같은 64% 의 수준은 용납할 수 없기떄문에 번페로니 방법으로 유의수준을 조절하기도 합니다.

![png](/assets/images/Stat/25_3.png)

- 위와 같이, 가설이 N 개라면 유의수준을 a/N 으로 맞추는 형식입니다.
- '정확하게' N 개의 가설에 대해서 a 로 유의수준을 맞추지는 못하지만 , 그 이하로 맞출 수 있는 방법입니다. 
- 하지만.. 이렇게 각 가설에 대해서 유의수준을 위와 같이 맞추면, 필연적으로 Sensitivity (Power) 가 줄어들게 됩니다. 
- 즉.. 애초에 다중비교하는것은 잘 추천하지 않는 방법입니다. 

<br>

# Problem

![png](/assets/images/Stat/25_2.png)

- 그리고 위와 같이 아이러니한 상황이 나오기도 합니다. 
- 즉,  $\mu_1 \not= \mu_2$   $\mu_2 = \mu_3$ 인데,  위와 같이 $\mu_1 = \mu_3$ 의 결론이 나오고 있습니다.
- 하지만, 이떄에 위 결과는 "사실" 이 아니라 '데이터가 얼마나 대립가설쪽으로 치우쳐있는지' 를 가지고 결론내린것이기 때문에, 위와 같은 결론이 가능한것입니다.
- 하지만, 이런 결과를 실무에 이용하기에는 무리가 있습니다.. 
- 제가 알기로는 Multiple Comparison 은 잘 하지 않는것으로 알고있습니다.

<br>

# Refer

- <https://www.stat.berkeley.edu/~mgoldman/Section0402.pdf>

