---
title:  "Two sample F test for population variances"
excerpt: "등분산 F 테스트"
categories:
  - Mathematical_Testing
last_modified_at: 2021-11-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 등분산 검정
{: .notice--warning}

# [Two sample F test for population variances](#link){: .btn .btn--primary}{: .align-center}

> ## Theorem 25 

> Theorem

Under the null hypothesis that $\sigma_{X}^{2}=\sigma_{Y}^{2}=\sigma^{2}$, the test statistic

$$F=\frac{S_{X}^{2}}{S_{Y}^{2}}$$

has a $F$ distribution with $n-1$ and $m-1$ degrees of freedom.

> Proof

$$\begin{aligned} F &=\frac{S_{X}^{2}}{S_{Y}^{2}} \\ &=\frac{S_{X}^{2}}{S_{Y}^{2}} \cdot \frac{1}{\frac{\sigma^{2}}{1}} \cdot \frac{(n-1)}{(n-1)} \frac{(m-1)}{(m-1)} \\ &=\frac{\left(\frac{(n-1) S_{X}^{2}}{\sigma^{2}}\right) \div(n-1)}{\left(\frac{(m-1) S_{Y}^{2}}{\sigma^{2}}\right) \div(m-1)} \\ &=\frac{U /(n-1)}{V /(m-1)} \end{aligned}$$

where $U=\frac{(n-1) S_{X}^{2}}{\sigma^{2}} \sim \chi_{n-1}^{2}$ and $V=\frac{(m-1) S_{Y}^{2}}{\sigma^{2}} \sim \chi_{m-1}^{2}$ by Theorem 19. Then by Definition 10, $F \sim F_{n-1, m-1}$

> ## Remark : Statistics 

Therefore, the F distribution with $n-1$ and $m-1$ degrees of freedom can be used to find the p-values for the two sample $\mathrm{F}$ test for population variances.

---

**reference**

- <https://digitalcommons.usu.edu/cgi/viewcontent.cgi?article=1014&context=gradreports>

