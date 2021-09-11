---
title:  "Exponential family"
excerpt: "지수 분포족"
categories:
  - Stat
tags:
  - 1
last_modified_at: 2021-03-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true

---

# <center><font size="20"> Exponential Family </font></center>

exponential family over x 은 다음과 같은 일반화된 형식을 가져야 한다.

$$p({\bf x}\mid{\bf \eta})=h({\bf x})g({\bf \eta})\exp\{ {\bf \eta}^T{\bf u}({\bf x})\}$$

- $\eta$ 는 모수
- $u(\bf x)$ 는 $\bf x$ 에 대한 함수

위와 같은 형식을 가지는 분포는 아래와 같이 매우 많다.

![png](/assets/images/{Statistic}/0_1.PNG)

## 베르누이 분포

$p(x\mid\mu) = Bern(x\mid\mu)=\mu^x(1-\mu)^{1-x}$ 이다. 이를 Exponential 분포의 형식으로 바꾸게 되면

$$p(x\mid\mu) = \exp \{x\ln\mu + (1-x)\ln(1-\mu)\}\\\\=(1-\mu)\exp\left\{\ln\left(\dfrac{\mu}{1-\mu}\right)x\right\}$$



## 정규 분포

$$ p(x\mid\mu,\sigma^2)=\dfrac{1}{(2\pi\sigma^2)^{1/2}}\exp\left\{-\frac{1}{2\sigma^2}(x-\mu)^2\right\}\\ = \dfrac{1}{(2\pi\sigma^2)^{1/2}}\exp\left\{-\frac{1}{2\sigma^2}x^2+\frac{\mu}{\sigma^2}x-\frac{1}{2\sigma^2}\mu^2\right\}$$

위에서 exp 형식에 따른 각 값은

${\bf \eta} = \dbinom{\mu/\sigma^2}{-1/2\sigma^2}$

${\bf u}(x) = \dbinom{x}{x^2}$

$h(x)=(2\pi)^{-1/2}$

$g({\bf \eta})=(-2\eta_2)^{1/2}\exp\left(\frac{\eta_1^2}{4\eta_2}\right)$

가 된다. 즉 정규분포도 exp family 임을 알 수 있다.