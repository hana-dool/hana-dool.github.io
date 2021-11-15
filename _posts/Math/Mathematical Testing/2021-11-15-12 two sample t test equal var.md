---
title:  "Two sample t-test for population means (equal variances)"
excerpt: "두표본 평균 t test(등분산)"
categories:
  - Mathematical_Testing
last_modified_at: 2021-11-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 평균에 대한검정
{: .notice--warning}

# [Two sample t-test](#link){: .btn .btn--primary}{: .align-center}

> ## Lemma 6 

> Lemma

If $X_{1}, X_{2}, \ldots, X_{n}$ and $Y_{1}, Y_{2}, \ldots, Y_{m}$ are independent with $X_{i} \sim N\left(\mu_{X}, \sigma^{2}\right)$ and $Y_{i} \sim N\left(\mu_{Y}, \sigma^{2}\right)$ then

$$\bar{X}-\bar{Y} \sim N\left(\mu_{X}-\mu_{Y}, \sigma^{2}\left(\frac{1}{n}+\frac{1}{m}\right)\right)$$

> Proof

Proof. By Lemma $3, \bar{X} \sim N\left(\mu_{X}, \frac{\sigma^{2}}{n}\right)$ and $\bar{Y} \sim N\left(\mu_{Y}, \frac{\sigma^{2}}{m}\right)$. Then by Theorems 10 and 12,

$$\begin{aligned}
\bar{X}-\bar{Y} &=\bar{X}+(-1) \bar{Y} \\
& \sim N\left(\mu_{X}-\mu_{Y}, \frac{\sigma^{2}}{n}+(-1)^{2} \frac{\sigma^{2}}{m}\right)
\end{aligned}$$

> ## Lemma 7

> Lemma

 If $X_{1}, X_{2}, \ldots, X_{n}$ and $Y_{1}, Y_{2}, \ldots, Y_{m}$ are independent with $X_{i} \sim N\left(\mu_{X}, \sigma^{2}\right)$ and $Y_{i} \sim N\left(\mu_{Y}, \sigma^{2}\right)$, then

$$\frac{(\bar{X}-\bar{Y})-\left(\mu_{X}-\mu_{Y}\right)}{\sigma \sqrt{\frac{1}{n}+\frac{1}{m}}} \sim N(0,1)$$

> Proof

By Lemma $6, \bar{X}-\bar{Y} \sim N\left(\mu_{X}-\mu_{Y}, \sigma^{2}\left(\frac{1}{n}+\frac{1}{m}\right)\right)$, so the mean $\bar{X}-\bar{Y}$ is $\mu_{X}-\mu_{Y}$ and the variance is $\sigma \sqrt{\frac{1}{n}+\frac{1}{m}}$.

$\bar{X}-\bar{Y}$ can be standardized by Theorem 13 , giving

$$\frac{(\bar{X}-\bar{Y})-\left(\mu_{X}-\mu_{Y}\right)}{\sigma \sqrt{\frac{1}{n}+\frac{1}{m}}} \sim N(0,1)$$

> ## Theorem 22

> Theorem

If $X_{1}, X_{2}, \ldots, X_{n}$ and $Y_{1}, Y_{2}, \ldots, Y_{m}$ are independent with $X_{i} \sim N\left(\mu_{X}, \sigma_{X}^{2}\right)$ and $Y_{i} \sim N\left(\mu_{Y}, \sigma_{Y}^{2}\right)$, then the statistic

$$T=\frac{(\bar{X}-\bar{Y})-\left(\mu_{X}-\mu_{Y}\right)}{S_{p} \sqrt{\frac{1}{n}+\frac{1}{m}}}$$

where

$$S_{p}=\sqrt{\frac{(n-1) S_{X}^{2}+(m-1) S_{Y}^{2}}{n+m-2}}$$

has a t distribution with $n+m-2$ degrees of freedom.

> Proof

$$\begin{aligned}
T &=\frac{(\bar{X}-\bar{Y})-\left(\mu_{X}-\mu_{Y}\right)}{\sqrt{\frac{(n-1) S_{X}^{2}+(m-1) S_{Y}^{2}}{n+m-2}} \sqrt{\frac{1}{n}+\frac{1}{m}} \cdot \frac{\sigma}{\sigma}} \\
&=\frac{(\bar{X}-\bar{Y})-\left(\mu_{X}-\mu_{Y}\right)}{\sigma \sqrt{\frac{1}{n}+\frac{1}{m}}} \div \sqrt{\left[\frac{(n-1) S_{X}^{2}}{\sigma^{2}}+\frac{(m-1) S_{Y}^{2}}{\sigma^{2}}\right] \cdot \frac{1}{n+m-2}}
\end{aligned}$$



Let $Z=\frac{(\bar{X}-\bar{Y})-\left(\mu_{X}-\mu_{Y}\right)}{\sigma \sqrt{\frac{1}{n}+\frac{1}{m}}} .$ By Lemma $7, Z \sim N(0,1)$
Let $U=\left[\frac{(n-1) S_{X}^{2}}{\sigma^{2}}+\frac{(m-1) S_{Y}^{2}}{\sigma^{2}}\right] .$ Then $U \sim \chi_{n+m-2}^{2}$ by Definition 8 because $\frac{(n-1) S_{X}^{2}}{\sigma^{2}} \sim \chi_{n-1}^{2}$ and $\frac{(m-1) S_{Y}^{2}}{\sigma^{2}} \sim \chi_{m-1}^{2}$ by Theorem 19. Therefore,

$$T=\frac{Z}{\sqrt{\frac{U}{n+m-2}}}$$

which has a t distribution with $n+m-2$ degrees of freedom by Definition 9 .

> ## Remark : Test Statistic

- 그러므로 우리는 Test statistic 이 따르는 분포를 알 수 있고, 이를 이용하여 difference of population mean 을 테스트 할 수 있게 됩니다.

---

**reference**

- <https://digitalcommons.usu.edu/cgi/viewcontent.cgi?article=1014&context=gradreports>

