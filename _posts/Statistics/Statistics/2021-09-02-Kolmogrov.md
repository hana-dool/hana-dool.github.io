---
title:  "Kolmogorov Probability Axiom"
excerpt: "측도에 기반한 현대 확률론"
categories:
  - Stat
last_modified_at: 2021-09-01

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

현대 확률론에서는 확률의 정의를 '엄밀' 하게 함으로서 확률의 각종 모순(베르트랑 의 역설 등) 을 해결하고 기초를 탄탄히 했습니다. 이러한 Axiom 이 어떻게 정의되었는지 알아보기 위해 우선 아래의 사항을 살펴봅시다.
{: .notice--warning}

# [Intro](#link){: .btn .btn--primary}{: .align-center}

- 먼저 확률을 엄밀하게 정의하기 위해서 알아야 할 것들에 대해서 알아봅시다.

> ## 기초 용어 정의

![png](/assets/images/Stat/53_1.png)

- 위와 같이 확률을 정의하기 위해 표본공간 , Event 에 대해서 정의합니다.

> ## Sigma Algebra

![png](/assets/images/Stat/53_2.png)

![png](/assets/images/Stat/53_3.png)

![png](/assets/images/Stat/53_4.png)

# [Kolmogrov Probability Axiom](#link){: .btn .btn--primary}{: .align-center}

![png](/assets/images/Stat/53_5.png)

- 위와 같이 , 두리뭉술하게 '모든 경우에 대해서 확률을 측정하자~' 가 아니라, sigma algebra 를 정의함으로서 그 domain 을 명확히 합니다.
- 그럼에 따라서 위와 같이 엄밀한 domaim 을 시그마 Algebra 로 정의함으로서 베르트랑의 역설을 해결하고 확률론의 토대를 공고히 한 것입니다.

**Reference**

- <https://bayestour.github.io/blog/docs/previous/mpsl/0103>

위와 같이 엄밀한 확률의 정의를 통하여, 확률 공간이 무한할떄의 역설을 해결하였고, 학문으로서의 기초를 다졌습니다. 하지만 사실 위의 정의들도 찍먹한것에 불과하고 집합의 크기를 정의해하는 측도론에 대해서 더 깊은 정의들이 존재합니다. (르벡 적분 ...) 하지만 이것은 범위를 넘어서므로 다음에 다루도록 하겠습니다.
{: .notice--success}

