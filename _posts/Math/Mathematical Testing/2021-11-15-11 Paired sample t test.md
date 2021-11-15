---
title:  "Paired sample t-test for the population mean"
excerpt: "쌍체 T 검정"
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

# [Paired sample t-test for the population mean](#link){: .btn .btn--primary}{: .align-center}

> ## Theorem 21

> Theorem

If $X_{1}, X_{2}, \ldots, X_{n}$ and $Y_{1}, Y_{2}, \ldots, Y_{m}$ are normally distributed random variables, $X_{i}$ and $Y_{i}$ are independent, then

$$Z=\frac{\bar{D}-\delta}{\frac{S_{D}}{\sqrt{n}}} \sim N(0,1)$$

where $D_{i}=X_{i}-Y_{i}$ is a pairwise difference, $\bar{D}=\frac{\sum_{i=1}^{n} D_{i}}{n}, \delta$ is the mean of the pairwise differences under the null hypothesis, and $S_{D}$ is the sample standard deviation of the pairwise differences.

> Proof

Proof. Note that $X_{i}$ and $Y_{i}$ are normal random variables, so $D_{i}=X_{i}-Y_{i}$ is also a normal random variable by Theorem 12. Then $D_{1}, D_{2}, \ldots, D_{n}$ can be thought of as the sequence of random variables $$\left\{X_{i}\right\}_{i=1}^{n}$$described in Theorem 20. Therefore $$t \sim t_{n-1}$$

> ## Remark : Statistics

- 즉 위에서 t distribution 을 이용하여 우리는 Test statistics 가 따르는 분포를 알 수 있을것입니다.





---

**Reference**

- <https://digitalcommons.usu.edu/cgi/viewcontent.cgi?article=1014&context=gradreports>

