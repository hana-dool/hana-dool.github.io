---
title:  "Kolmogorov-Smirnov test"
excerpt: "두 분포가 같은지 테스트 하는 방법"
categories:
  - Stat_Testing
last_modified_at: 2021-11-10

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Kolmogorov-Smirnov test 는 두 분포가 같은지 테스트 하는 방법입니다. 이를 어떻게 알 수 있는지 한번 알아보도록 합시다.
{: .notice--warning}

# [Kolmogorov-Smirnov test](#link){: .btn .btn--primary}{: .align-center}

> ## Kolmogorov-Smirnov test

- 우리는 $\mathbb{P}$ 로부터 추출한 iid 한 샘플 $X_1 ... X_n $ 을 가지고 있다고 합시다. 
- 그리고 우리는 이 분포가 특정한 분포인 $\mathbb{P_0}$ 에서 나왔는지를 알고 싶습니다. 
  - 즉 다음과 같은 분포를 테스팅 하고 싶다고 합시다.

$$H_{0}: \mathbb{P}=\mathbb{P}_{0}, \quad H_{1}: \mathbb{P} \neq \mathbb{P}_{0}$$

- 위를 테스트 하는 방법중에는 Chi - squared 방법론이 있습니다. 
  - 이 방법론은 약간 



---

   **Reference**

- <https://myweb.uiowa.edu/pbreheny/uk/teaching/621/notes/10-11.pdf>

 위와 같은 방법론은 비교하기가 편리해서 많은사람이 잘못 판단하는 부분이라 주의가 필요합니다. Schenker와 Gentleman (2001)은 의학 분 야 학술지에서 이러한 오류를 범한 논문을 60개 넘게 발견했다고 보고했다고 합니다..
{: .notice--success}

