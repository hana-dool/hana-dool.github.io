---
title:  "Practical Significance"
excerpt: "통계적 유의성과 실제적 유의성"
categories:
  - Stat_Testing
last_modified_at: 2021-09-22

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 Practical significace 현실에 의미있는 차이를 다룹니다. 이에 대해서 알아봅시다.
{: .notice--warning}

# [Practical Significance](#link){: .btn .btn--primary}{: .align-center}

- Practical significance는 실제 세상에 의미가 있을만한 차이를 나타냅니다
  - 예를 들어서, 신약개발의 경우 기존 약이 80% 의 치유율을 보인다고 합시다. 이 회사는  80.01%의 치유률을 가지는 신약을 개발하였습니다.
  - 신약에 대한 AB Test 결과 p - value 가 0.0004 으로 두 차이는 통계적으로 유의한 수준임이 밝혀졌다고 합시다. (Statistical Significant)
  - 이 떄에 회사는 통계적으로 유의하므로 신약을 출시해야 할까요? 
- 이 경우, 신약 출시는 매우 큰 비용이 들어갑니다. 그러므로, 0.01% 의 차이떄문에 신약을 내면 안될것입니다. 

> ## Sample Size Relations

- 우리는 Test 를 시행하기 전에 Sample size 를 정하곤 합니다. 
  - 적은 차이를 통계적으로 유의한 수준까지 검정하기 위해서는 매우 큰 Sample size 가 필요합니다. 
  - 그에 비해 큰 차이를 검정할떄에는 Sample size 가 별로 필요 없습니다.
- 그러므로 Sample size 를 결정할때에는, 어느 차이까지 Detect 할 수준으로 Sample size 를 정해야 할까요? 
  - 이 떄에 필요한것이 바로 Practical Significance 입니다. 
  - 신약 개발의 경우 , 기존 신약보다 최소 치유율이 10% 향상되야 의미가 있다고 합시다.(Practical Significant)
  - 그렇다면 Baseline 의 치유율이 50% 인 경우, Alternative 의 치유율이 55% 라 가정한 상태에서 유의한 결과를 얻기 위한 최소의 Sample size 를 계산할 수 있을것입니다. 
    - 물론 이 경우 type1 error , type2 error 를 정하여 Test 를 Construct 하기 떄문에 각 error 를 정하는것은 사용자의 판단입니다.

- Practical significant 는 Effect size 로도 불립니다.

> ## Example

- 라면 회사에서 신제품을 낼지 말지가 궁금하여 현재 우리 지역의 인당 1년 라면 소비량이 궁금하다고 합시다.

$H_0 : \mu = 500$

$H_a : \mu > 500$

- 별 생각 없이 많은 샘플을 모아야 좋다는 생각으로 1200명의 샘플을 모았고, 그에 따라 결과는 $\bar{X} = 506$ 의 결과를 얻었습니다. 
- Mean Test 에서 결과는 p-value 0.0188 이 나왔습니다. 
- 하지만 이러한 차이는 겨우 년당 6개의 차이밖에 나지 않습니다. 라면회사는 최소 인당 소비량이 520개 정도는 되어야 진출할 수 있다고 합니다.
  - 즉 Statistical Significant 는 유효하지만 Practical Significant 는 유효하지 않습니다.

---

**Reference**

- <https://online.stat.psu.edu/stat200/lesson/6/6.4>

 사실 Practical significant 는 Statistical Significant 와는 달리 매우 주관적이고, 현실적인 문제입니다. 그래서 통계'학' 에서 다루기에는 약간 학문과 거리가 먼 주제지만 알아두면 좋은 주제라 선정하게 되었습니다. 
{: .notice--success}

