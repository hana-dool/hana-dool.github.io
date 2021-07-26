---
title:  "Goodness Of Fit Test"
excerpt: "내 데이터가 어떤 분포를 따를까?"
categories:
  - Stat
tags:
  - 1
last_modified_at: 2021-07-27

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# 1. Chi-Square Test

> The chi-square test ([Snedecor and Cochran, 1989](https://www.itl.nist.gov/div898/handbook/eda/section4/eda43.htm#Snedecor)) is used to test if a sample of data came from a population with a specific distribution.

- 이 테스트 방법이 좋은점은 Descrete Distribution 에서도 쓸 수 있다는 점입니다. 

![png](/assets/images/Stat/17_1.png)

- 위와 같이, 두 분포가 동일한지에 대해서 검사할 수 있습니다.
- 이는 "Empirical Distribution" 과. 알려진 Distribution 을 비교할 수 있다는 뜻입니다.

![png](/assets/images/Stat/17_2.png)

- Continuous Distribution 의 경우 위와 같이, 각 Binning 으로 나눈 후 검정을 할 수 있습니다.
  - 이는 Conti 한 분포를 Discrete 하게 바꾼 후 진행한것이라 보시면 됩니다.

- 이경우 . 각 binning 에 대해서 기대되는 빈도 수는 5 이상이여야 합니다.
  - 이는 확률적으로 너무 낮은 구간을 없애기 위함입니다. 

<br>

# 2. Kolmogorov–Smirnov test

- KS Test 란, Continuous Distribution 에 대해서 두 분포가 동일한지 검사합니다.
- 이 경우 통계량은 , 두 분포의 CDF(데이터의 경우 ECDF) 거리의 최대값이 됩니다. 

![png](/assets/images/Stat/17_3.png)

![png](/assets/images/Stat/17_4.png)

- 위와 같이, "서로 다른 2개의 Distribution" 에 대해서도 검정이 가능합니다. 
- 위는 '통계량' 이라는말에 걸맞게, Sample 수가 많다면 Brownian 분포로 분포수렴함이 알려져 있습니다. 
  - 자세한것은 검색..
- 하지만, 'CDF 차이의 최대' 인 지점은 통상 분포의 중간쯤에서 나타나기 때문에, 분포의 처음 지점이나 마지막 지점에서 분포가 다른것은 과소평가 하는 경향이 있습니다.



