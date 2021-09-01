---
title:  "Assumtion and OLS estimator"
excerpt: "어느정도까지 가정을 세워야 할까?"
categories:
  - Regression
tags:
  - 1
last_modified_at: 2021-06-26

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# Intro

- OLS estimator 에 대해서, 어디까지 가정을 해야, 우리 OLS 모델의 Estimator 가 좋은 성질을 가질 수 있을까요?
- 즉 만약 $V[\epsilon_i] \not= \sigma ^2$ 라면? (즉 등분산 침해)
- 또는 Error 가 Normal Error 가 아니라면? 
- 이러한 상황에서 우리의 추정 OLS Estimator 는 어떻게 변하는지 알아봅시다. 



# 기본모델

![png](/assets/images/Stat/2_1.png)

<br>

# Unbiased

![png](/assets/images/Stat/2_2.png)

- 이 경우에 Unbiasd 를 위한 가정은 오로지 $E[\epsilon_i]=0$  만 필요한것에 집중합시다.

<br>

# Consistency

![png](/assets/images/Stat/2_3.png)

- 이때에 X 가 점점 커질수록 OLS 추정량의 Variance 가 낮아지므로 Consistency 하다고 볼 수 있습니다. 
- 이경우 가정은 Normal 을 제외한 다른 가정들입니다. 

<br>

# Blue

- Blue 란 Best Linear Unbiased Estimator 로서, linear 로 이루어진 Unbiased 추정량중에서 제일 Variance 가 낮다는 것입니다. 

![png](/assets/images/Stat/2_4.png)

- 위에서 보듯이, Normal 을 제외한 다른 가정이 성립할떄에 Blue 가 됩니다.

<br>

# Normal

- 위와 같이 Blue 가 되기까지도 Normal 가정은 필요없었습니다. 
- 그러면 왜 Normal 가정을 사용하는것일까요? 
  - 어쩃든 '모든 Exact inference 를 위해서는 분포가정이 필요합니다.'
  - 에러에 대해서 어떠한 분포가정을 해야 '통계정 추정' 이 가능해진다는 의미입니다. 
  - 이떄에 error 가 경험적으로 Normal 을 따르는 경우가 많았고 또한 Normality 가정을 하게된다면 OLS Estimator 와 MLE Estimator 가 같아지는 이점이 있습니다. 
  - mle 를 구하기도 쉬워지며 + mle 의 좋은 성질을 이용할 수 있게됩니다.
- MLE 의 좋은 성질이란..? 
  - 바로! Assymptotic Normal ! 그러므로 추정시 사용 가능합니다.
  - 하지만 MLE 와 LSE 추정이 달라진다면..?
    - LSE 추정의 분포를 다시 구해야하고, 이는.. 매우 어렵습니다. 
    - 또한 LSE 추정이 과연 Consistency 와 같은 좋은 MLE 성질이 있을까요? 

<Br>

# Summary

![png](/assets/images/Stat/2_5.png)

<br>

# Reference

- https://towardsdatascience.com/ols-linear-regression-gauss-markov-blue-and-understanding-the-math-453d7cc630a5

- https://en.wikipedia.org/wiki/Ordinary_least_squares
