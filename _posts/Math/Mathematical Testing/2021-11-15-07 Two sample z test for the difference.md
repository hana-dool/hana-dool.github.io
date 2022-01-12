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

# [Test Procedure](#link){: .btn .btn--primary}{: .align-center}

> ## When can this test be used?

- There are two samples from two populations. (The samples can be different sizes.)
- The two samples are independent.
- Both populations are normally distributed or both sample sizes are large enough that the means are normally distributed. (A rule of thumb is each sample size is $n \geq 30$.)
- Both population standard deviations, $\sigma_{x}$ and $\sigma_{y}$, are known.

> ## Notation

$$
\begin{array}{|c|c|c|c|c|c|}
\hline \text { Population } & \text { Data } & \text { Mean } & \text { Standard Deviation } & \text { Sample Size } & \text { Sample Mean } \\
\hline \hline 1 & x_{i} & \mu_{x} & \sigma_{x} & n & \bar{x} \\
\hline 2 & y_{i} & \mu_{y} & \sigma_{y} & m & \bar{y} \\
\hline
\end{array}
$$

> ## Test Used

> State the hypotheses

- 검증하고자 하는 두 샘플 평균의 차이를 $D$ 라고 합시다. 그럼 가설은 아래와 같습니다.
- Hypothesis
  - $H_{0}: \mu_{x}-\mu_{y}=D$
  - $H_{A}: \mu_{x}-\mu_{y} \neq D$ or $H_{A}: \mu_{x}-\mu_{y}>D$ or $H_{A}: \mu_{x}-\mu_{y}<D$

- 위 Hypotheis 의 예시를 알아보자.
  - 차 회사 A와 차 회사 B의 평균 주행 거리보다 최소 20000마일 이상 더 길다고 생각한다면 D = 20000 으로 설정할 수 있습니다. 이떄 A 회사와 B 회사가 임의로 선택한 차가 독립적이라 합시다. 그러면 가설은 $H_{0}: \mu_{x}-\mu_{y}=20,000$ $H_{A}: \mu_{x}-\mu_{y}>20,000$ 가 될 것입니다. 
- 많은 경우에는 $D=0$ 을 설정하게 됩니다. 즉, 아래와 같이 설정되게 됩니다.  
  - $H_{0}: \mu_{x}=\mu_{y}$
  - $H_{A}: \mu_{x} \neq \mu_{y}$ or $H_{A}: \mu_{x}>\mu_{y}$ or $H_{A}: \mu_{x}<\mu_{y}$

> (2) Pick a significance level, $\alpha$.

- 유의수준을 설정합니다. 

> (3) Compute the test statistic

$$z=\frac{(\bar{x}-\bar{y})-D}{\sqrt{\frac{\sigma_{x}^{2}}{n}+\frac{\sigma_{y}^{2}}{m}}}=\frac{\text { difference in sample means }-\text { hypothesized difference in population means }}{\sqrt{\frac{\text { population } 1 \text { variance }}{\text { sample } 1 \text { size }}+\frac{\text { population } 2 \text { variance }}{\text { sample } 2 \text { size }}}}$$

> (4) Find the $\mathrm{p}$-value

- The p-value depends on which alternative hypothesis is being used. The p-value is the probability or the area in the tail(s) of the standard normal curve.
- If $H_{A}: \mu_{x}-\mu_{y}>D$, p-value $=P(Z \geq z)$
- If $H_{A}: \mu_{x}-\mu_{y}<D$, p-value $=P(Z \leq z)$
- If $H_{A}: \mu_{x}-\mu_{y} \neq D$, p-value $=P(Z \leq-|z|$ or $Z \geq|z|)$ or $2 P(Z \geq|z|)$

> (5) State the conclusion

- Once the p-value is known, compare it to $\alpha$, the significance level.
- If the $\mathrm{p}$-value is smaller than $\alpha$, the observed outcome wasn't very likely given that the null hypothesis is true. So reject the null hypothesis in favor of the alternative hypothesis.
- If the p-value is greater than $\alpha$ then the observed outcome was likely enough that it is reasonable to assume that the null hypothesis is true so fail to reject the null hypothesis.

$$
\begin{array}{|c|c|}
\hline p-\text { value }<\alpha & \text { reject } H_{0} \\
\hline p-\text { value }>\alpha & \text { fail to reject } H_{0} \\
\hline
\end{array}
$$



---

**Reference**

- <https://digitalcommons.usu.edu/cgi/viewcontent.cgi?article=1014&context=gradreports>

