---
title:  "[Test] (Wilcoxon) Sign Ranked Test"
excerpt: "Rank 를 이용해 Paried Sample 테스트"
categories:
  - Stat_Non_Parametric
tags:
  - 1
last_modified_at: 2021-08-22

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# (Wilcoxon) Sign - Rank Test

- 먼저 본격적으로 테스트 이야기를 하기 전에 , Setting 이 어떻게 되는지 살펴봅시다.

![png](/assets/images/Stat/46_4.png)

![png](/assets/images/Stat/46_3.png)

- 위처럼 , $X,Y$ 가 같은지 아닌지를 검정하고자 하는게 목적이고 위처럼 그 차이를 Z 라고 정의합니다.
  - 이때 Sample 이 Paired Test 임을 기억합시다.

![png](/assets/images/Stat/46_1.png)

- Sign Test 는 오로지 + , - 두가지만 고려했었습니다.
- 하지만 Sign -Rank Test 는 Rank 도 고려하게 됩니다.

![png](/assets/images/Stat/46_2.png)

- Z 의 절댓값에 대한 Rank와 음수인지 아닌지의 정보인Sign 을 이용해 통계량 W 를 만듭니다.  
- W 는 CLT 에 의해서 위와 같이 Limiting Distribution 을 알아낼 수 있고, 이를 통해서 위처럼 검정을 할 수 있습니다.
- 이 때에, 가설은 다음과 같습니다.

![png](/assets/images/Stat/46_8.png)

- 이떄에 위처럼 Symmetric 을 가정하면 Median 와 Mean 이 같아짐을 기억합시다. 

<br>

# Proof

![png](/assets/images/Stat/46_6.png)

![png](/assets/images/Stat/46_7.png)

- Symmetric 이므로 Sign 은 Bernouli(1/2) 를 따른다고 할 수 있습니다.
- 또한 CLT 에 의해 Normal 을 따른다고 볼 수 있으므로 검정을 할 수 있을것입니다.

<br>

# Example

![png](/assets/images/Stat/46_9.png)

- 위와 같이 위의 예제에서 두 Pairwise Difference 의 Median 은 0 이라고 볼 수 있습니다.

<br>

# Refer

- http://faculty.washington.edu/yenchic/18W_425/Lec1_TwoSample.pdf
- https://en.wikipedia.org/wiki/Wilcoxon_signed-rank_test
- https://web.stanford.edu/class/archive/stats/stats200/stats200.1172/Lecture08.pdf



