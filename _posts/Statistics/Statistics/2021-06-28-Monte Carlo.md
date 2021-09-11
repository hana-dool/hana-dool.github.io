---
title:  "Monte Carlo Approximation"
excerpt: "샘플 수로 찍어누르기"
categories:
  - Stat
tags:
  - 1
last_modified_at: 2021-06-28

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# <center><font size="10">1. Monte Carlo Approximation</font></center>

- 일반적으로, 확률 변수에 대한 분포를 계산하는것은 매우 어렵습니다. 그래서 정확하게 분포를 계산하기 보다는, 몬테카를로 근사법을 이용하는 방법이 실용적으로 많이 쓰입니다. 

- 어떤 분포로부터 $N$ 개의 Sample $x_1, ..., x_N$ 를 추출했다고 합시다. 이 Sample에 기반하여 Empirical Distribution 인 $[f(x_i)]_{i=1}^N$ 를 이용하여 우리는 $f(X)$ 라는 분포를 근사할 수 있습니다. 이를 이용한 방법이 바로 몬테카를로 근사법입니다. 

![png](/assets/images/Stat/5_1.png)

- 위와 같이 몬테카를로 근사법을 이용하면, 확률 변수의 어떠한 함수에 대해서도 기댓값을 구할 수 있습니다.

> $$ E[f(X)] = \int f(x) p(x) dx \approx \frac{1}{N} \Sigma_{i=1}^N f(x_i) $$

- f 함수를 변환시켜 다음과 같은 여러 특성도 얻을 수 있습니다.

> $$ \bar{x} = \frac {1}{X} \Sigma_{i=1}^N x_i \approx E[X] $$
>
> $$ \Sigma_{i=1}^N (x_i - \bar{x})^2 \approx var[X] $$
>
> $$ median (x_1, ..., x_N) \approx median(X) $$

<br>

# <center><font size="10">2. LLN and Monte Carlo</font></center>

- 위의 Montecarlo 방법이 가능한 이유는 Law of Large number 덕분입니다.

![png](/assets/images/Stat/5_3.png)

- 위와 같이 LLN 에서 , $X_i$ 를 $f(X_i)$ 라고 생각하면 됩니다.

![png](/assets/images/Stat/5_2.png)

<br>

# <center><font size="10">3. Example: estimating $\pi$</font></center>

- 반지름이 r인 원의 면적을 $I$ 라고 합시다. 
- Indicator Function을 사용하여 면적을 나타내면 아래와 같습니다.

> $$ I = \int_{-r}^{r} \int_{-r}^{r} \mathbb{I} (x^2 + y^2 \le r^2) dxdy $$

- Indicatior Funciton을 $f(x, y)$ 라고 하고, 원 밖에 점이 찍히면 0, 안에 찍히면 1의 값을 갖는 함수라고 하자. 
- $p(x), p(y)$ 는 $-r, r$ 구간 내에 존재하는 균일 분포 함수이다. 따라서 $p(x) = p(y) = \frac{1}{2r}$ 이다.

> $$ I = (2r)(2r) \int \int f(x, y) p(x) p(y) dx dy \approx 4r^2 \frac{1}{N} \Sigma_{i=1}^N f(x_i, y_i) $$

<br>

# <center><font size="7">4. Accuracy of Monte Carlo Approximation</font></center>

- 기본적으로 몬테카를로 근사법은 표본의 크기가 클수록 정확도가 높아집니다.

- 실제 평균을 $\mu = E[f(X)]$ 라고 합시다. 그리고 몬테카를로 근사법에 의한 근사 평균을 $\hat{\mu}$ 라고 합시다. ind sample 이라는 가정을 한다면 중심극한정리에 의해

> $$ \hat{\mu} - \mu \to \mathcal{N} (0, \frac{\sigma^2}{N}) $$
>
> $$ \sigma^2 = var[f(X)] $$ 

- 위. 물론 $\sigma^2$ 는 미지의 값입니다. 하지만 이 또한 몬테카를로 적분에 의해 근사될 수 있습니다.

> $$ \hat{\sigma}^2 = \frac{1}{N} \Sigma_{i=1}^N (f(x_i) - \hat{\mu})^2 $$
>
> $$ P(\mu - 1.96 \frac{\hat{\sigma}}{\sqrt{N}} \le \hat{\mu} \le \mu + 1.96 \frac{\hat{\sigma}}{\sqrt{N}}) \approx 0.95 $$

- 이 때 $\sqrt{ \frac{\hat{\sigma^2}} {N}}$ 는 Numerical(Empirical) Standard Error 라고 불리며, 이는 $\mu$ 의 추정량에 대한 불확실성에 대한 추정치 입니다.
- 만약 우리가 95%의 확률로 $\pm \epsilon$ 내부에 위치할 만큼 정확한 Report를 원한다면 우리는 $1.96 \sqrt{ \frac{\hat{\sigma}^2}{N}} \le \epsilon$ 을 만족시키는 N 개의 Sample이 필요합니다.

<br>

# Ref

- http://www.math.chalmers.se/Stat/Grundutb/CTH/tms150/1516/MC_20151008.pdf
- https://en.wikipedia.org/wiki/Law_of_large_numbers
- https://slideplayer.com/slide/7453543/
- https://greeksharifa.github.io/bayesian_statistics/2020/07/30/Monte-Carlo-Approximation/

