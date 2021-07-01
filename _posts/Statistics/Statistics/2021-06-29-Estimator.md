---
title:  "Estimator"
excerpt: "좋은 추정량의 조건"
categories:
  - Stat
tags:
  - 1
last_modified_at: 2021-06-29

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# <center><font size="10">Estimator</font></center>

- Estimator 란 무엇일까? 
- 우선, 우리가 알고싶은 값들(평균, 분산,모수...)이 있을것이다. 
- 하지만 위 값들의 경우 True 값은 아무도 알 수 없다. 
- 그러므로 우리는 데이터를 통해서 위 값을 추정해야한다. 
- 즉, 추정량은 True 값을 알 수 없으니, 데이터로부터 이를 추정한것이 바로 추정량이다.
- 이제 좋은 추정량이란, 어떠한 성질을 가져야 하는지 알아보도록 하자.

<BR>

# <center><font size="10">1. Unbiased</font></center>

> $E[t_n] = \theta$
>
> 추정량은 편향되어있지 않다.

- 위를 만족하는 추정량 $t_n$ 을 Unbiased 라 부른다. 
- 이러한 성질을 가져야 좋은 Estimator 인것은 매우 당연해보인다.

<br>

# <center><font size="10">2. Consistency</font></center>

> $\lim_{n\to \infty} P(\mid t_n - \theta \mid < \epsilon ) = 1$
>
> Sample 수가 늘어날수록 정확해지는것을 담보한다.

- 사실 추정량은 위 성질, Consistency 가 '매우' 중요하다
- .위 Consistency 를 만족하지 못하는 추정량은 샘플수가 늘어나도, 정확해지 않을수도 있다는것이다.

![png](/assets/images/Stat/6_1.png)

- 위처럼 샘플수가 많아지면, 정확해지는것이 Consistency 이다. 
- inconsistency 하다면, 정확해지기 위하여 어떤 방법을 써야하는지가 매우 난해할 것이다..

<br>

# <center><font size="10">3. Efficiency</font></center>

>$Var(t_n)$ 이 작을수록 좋다.
>
>즉 추정시에, 흔들림이 없이 비슷한 값을 추정하는게 좋다는 의미

![png](/assets/images/Stat/6_2.png)

- 물론 Efficiency 를 따질때에는 Unbiased Estimator 끼리의 분산을 보고 비교하긴 하거나, RCLB 를 달성하는것으로 간주하긴 한다.
- 하지만, 다양한 분야에서 혼용해서 쓰이는 개념으로, 위처럼 추정시 분산이 작다는것으로 생각해도 된다.

<br>

# <center><font size="10">4. Robustness</font></center>

>가정의 침해에도, 추정량이 크게 영향받지 않을떄 Robust 하다.

- 매우 Skewed 된 데이터를 생각해보자. 
- 이러한 경우 Outlier 가 생길 수 있기떄문에, 평균을 추정할때에 Sample mean 은 좋지 못하다.
- 즉 위같은 상황을 피하기 위해서, Sample mean 을 사용하되, 상위 1% 와 하위 99% 의 데이터를 Trim 해서 사용하기도 한다. 

<br>

# <center><font size="10">5. Asymptotic normality</font></center>

> sample size 가 커질수록, 추정량이 Normal 극한분포를 따른다는 것
>
> $\sqrt{n} (\hat \theta - \theta) \to N(0,\sigma^2_\theta)$ 

- 사실 Assymptotic Normal 은 추정량의 정확도와는 크게 상관이 없습니다. 
- 하지만 '추정량의 분포' (Sample 의 분포이기 때문에 Sampling Distribution 이라고도 합니다.) 를 알 수 있으면, Confidence Interval 을 이용해, 추정량에 대해서 '구간 추정' 이 가능해집니다.
  - 이러한 구간추정은 구간의 길이를 통해 추정의 '정확성' 까지 표현할 수 있기때문에 점추정보다 훨씬 선호됩니다. 
- 그러므로 훨씬 더 많은것이 가능해집니다. 
- 물론 극한분포가 아니라 Exact 분포, 다른 극한분포일 수 있고 이러한 경우도 선호됩니다. 

# ref

- https://multithreaded.stitchfix.com/blog/2020/09/24/what-makes-a-good-estimator/

