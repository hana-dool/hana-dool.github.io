---
title:  "Bayesian Regression(~ing)"
excerpt: "베이즈 선형회귀"
categories:
  - Bayes
tags:
  - 1
last_modified_at: 2021-08-22

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

- 연세대 통계학회 ESC 2021-Spring 의 내용을 정리한 것입니다.

# 다중선형 회귀분석

![png](/assets/images/Stat/45_1.jpg)

- 다중선형회귀는 위와 같은 Logic 을 따릅니다.
- 추가적으로 위를 보시면 , y-xb 를 최소화하는것은 결국에 MLE 를 최대화하는것과 같다는것을 알 수 있습니다.

![png](/assets/images/Stat/45_2.jpg)

- 맨 왼쪽 증명에서 Y 가 Normal 을 따르므로 ,  $\hat \beta$ 가 Normal 을 따르는것은 $\hat\beta = (X^TX)^{-1} X^T Y$ 에서 쉽게 알 수 있습니다.
- 이제 평균과 분산만 알면 되므로 중간 증명에서 평균과 분산을 알 수 있습니다. 이 단계에서 우리는 추정량이 Unbiased 임을 알 수 있으며, 추정량의 Exact 한 분포를 알 수 있습니다.
- 그리고 $\sigma^2$ 을 어떻게 추정해야하는지도 맨 오른쪽에서 알 수 있습니다.

<br>

# 베이지안 회귀분석

![png](/assets/images/Stat/45_3.jpg)

- Prior 를 따로따로 Independent 하게 준것은 Semi Conjugate Prior 입니다.
- sigma 와 beta 가 dependent 한 경우는 Full Conjugate 라고 합니다.
