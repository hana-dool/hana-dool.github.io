---
title: "Two sample z-test  for the difference of population means"
excerpt: "이표본 평균 Z Test"
categories:
  - Mathematical_Testing
last_modified_at: 2021-11-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 두개 모집단에 대한 평균 차이검정.
{: .notice--warning}

# [Two Sample z test](#link){: .btn .btn--primary}{: .align-center}

> ## Lemma 4

> Lemma

If $X_{1}, X_{2}, \ldots, X_{n}$ and $Y_{1}, Y_{2}, \ldots, Y_{m}$ are independent with $X_{i} \sim N\left(\mu_{X}, \sigma_{X}^{2}\right)$ and $Y_{i} \sim N\left(\mu_{Y}, \sigma_{Y}^{2}\right)$ then

$$\bar{X}-\bar{Y} \sim N\left(\mu_{X}-\mu_{Y}, \frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}\right)$$

> Proof

By Lemma $3, \bar{X} \sim N\left(\mu_{X}, \frac{\sigma_{X}^{2}}{n}\right)$ and $\bar{Y} \sim N\left(\mu_{Y}, \frac{\sigma_{Y}^{2}}{m}\right) .$ Then by Theorems 10 and 12,

$$\begin{aligned}
\bar{X}-\bar{Y} &=\bar{X}+(-1) \bar{Y} \\
& \sim N\left(\mu_{X}-\mu_{Y}, \frac{\sigma_{X}^{2}}{n}+(-1)^{2} \frac{\sigma_{Y}^{2}}{m}\right)
\end{aligned}$$

> ## Theorem 16

> Theorem

If $X_{1}, X_{2}, \ldots, X_{n}$ and $Y_{1}, Y_{2}, \ldots, Y_{m}$ are independent with $X_{i} \sim N\left(\mu_{X}, \sigma_{X}^{2}\right)$ and $Y_{i} \sim N\left(\mu_{Y}, \sigma_{Y}^{2}\right)$ then

$$Z=\frac{(\bar{X}-\bar{Y})-\left(\mu_{X}-\mu_{Y}\right)}{\sqrt{\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}}} \sim N(0,1)$$

> Proof

PROOF. By Lemma $4, \bar{X}-\bar{Y} \sim N\left(\mu_{X}-\mu_{Y}, \frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}\right)$, so the mean of $\bar{X}-\bar{Y}$ is $\mu_{X}-\mu_{Y}$ and the variance is $\sqrt{\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}}$. Then $\bar{X}-\bar{Y}$ can be standardized using Theorem 13, giving

$$\frac{(\bar{X}-\bar{Y})-\left(\mu_{X}-\mu_{Y}\right)}{\sqrt{\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}}} \sim N(0,1)$$

> Remark 

- 즉 위의 정리를 이용하면 우리는 two sample z test for difference of population of meas 를 계산할 수 잇을것입니다.

---

**Reference**

- <https://digitalcommons.usu.edu/cgi/viewcontent.cgi?article=1014&context=gradreports>

