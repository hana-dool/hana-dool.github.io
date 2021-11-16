---
title:  "Chi-square test for population variance"
excerpt: "카이제곱 분산 테스트"
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

# [Chi-square test for population variance](#link){: .btn .btn--primary}{: .align-center}

> ## Corollary 

> Corollary

Under the null hypothesis that $\sigma^{2}=\sigma_{0}^{2}$, the test statistic

$$\chi^{2}=\frac{(n-1) S^{2}}{\sigma_{0}^{2}}$$

has a chi-square distribution with $n-1$ degrees of freedom. 

> Proof

- 이는 Thm 19 에 의해 directly 하게 풀립니다. thm19 에 대해서 remind 하자면

THEOREM 19. $\frac{(n-1) S^{2}}{\sigma^{2}}$ has a chi-square distribution with $n-1$ degrees of freedom

> ## Remark

- 위와 같이 분산에 대한 Testing 을 할 때에 Chi Square 을 쓸 수 있음을 알 수 있습니다.

# [Test Procedure](#link){: .btn .btn--primary}{: .align-center}

> ## When can this test be used?

- The population is normally distributed.
- The population variance, $\sigma^{2}$ is unknown

> ## How is this Test used? 

> (1) Pick a significance level, $\alpha$

> (2) State the hypotheses;

$$\begin{aligned}
&H_{0}: \sigma^{2}=\sigma_{0}^{2} \\
&H_{A}: \sigma^{2} \neq \sigma_{0}^{2} \text { or } H_{A}: \sigma^{2}>\sigma_{0}^{2} \text { or } H_{A}: \sigma^{2}<\sigma_{0}^{2}
\end{aligned}$$

> (3) Compute the test statistic:

$$X^{2}=\frac{(n-1) s^{2}}{\sigma_{0}^{2}}=\frac{(\text { sample size }-1)(\text { the sample variance })}{\text { the hypothesized population variance }}$$

> (4) Find your degrees of freedom.

$$d f=n-1$$

The degrees of freedom is the sample size minus $1 .$

> (5) Find the p-value:

The p-value depends on which alternative hypothesis is being used. The p-value is found by the probability or the area in the tail(s) of the $\chi^{2}$ distribution with $n-1$ degrees of freedom.

Warning! The $\chi^{2}$ distribution is not symmetric. The probability of each tail must be calculated separately.

If $H_{A}: \sigma^{2}>\sigma_{0}^{2}, \mathrm{p}$-value $=P\left(\chi^{2} \geq X^{2}\right)$

![png](/assets/images/Stat/105_1.png)

If $H_{A}: \sigma^{2}<\sigma_{0}^{2}, \mathrm{p}$-value $=P\left(\chi^{2} \leq X^{2}\right)$

![png](/assets/images/Stat/105_2.png)

If $H_{A}: \sigma^{2} \neq \sigma_{0}^{2}, \mathrm{p}$-value $=2\left(\chi^{2} \leq X^{2}\right)$ if the test statistic $X^{2}$ is less than the median or $2 P\left(\chi^{2} \geq X^{2}\right)$ if $X^{2}$ is greater than the median.

![png](/assets/images/Stat/105_3.png)

> (6) State the Conclusion 

- Once the $\mathrm{p}$-value is known, compare it to $\alpha$, the significance level.

- If the p-value is smaller than $\alpha$, the observed outcome wasn't very likely given that the null hypothesis is true. So reject the null hypothesis in favor of the alternative hypothesis.

- If the p-value is greater than $\alpha$ then the observed outcome was likely enough that it is reasonable to assume that the null hypothesis is true so fail to reject the null hypothesis.

$$\begin{array}{|c|c|}
\hline p-\text { value }<\alpha & \text { reject } H_{0} \\
\hline p-\text { value }>\alpha & \text { fail to reject } H_{0} \\
\hline
\end{array}$$



---

**reference**

- <https://digitalcommons.usu.edu/cgi/viewcontent.cgi?article=1014&context=gradreports>

