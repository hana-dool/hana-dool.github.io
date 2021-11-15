---
title:  "Paired sample z-test for the population mean of paired difference"
excerpt: "쌍체 Z 검정"
categories:
  - Mathematical_Testing
last_modified_at: 2021-11-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 평균에 대한 쌍체 검정에 대해서 알아봅시다.
{: .notice--warning}

# [paired sample z test](#link){: .btn .btn--primary}{: .align-center}

> ## Theorem : Statistic

THEOREM 15. If $X_{1}, X_{2}, \ldots, X_{n}$ and $Y_{1}, Y_{2}, \ldots, Y_{m}$ are normally distributed random variables and $X_{i}$ and $Y_{i}$ are independent, then

$$Z=\frac{\bar{D}-\delta}{\frac{\sigma_{D}}{\sqrt{n}}} \sim N(0,1)$$

where $D_{i}=X_{i}-Y_{i}$ is a pairwise difference, $\bar{D}=\frac{\sum_{i=1}^{n} D_{i}}{n}, \delta$ is the mean of the pairwise differences under the null hypothesis, and $\sigma_{D}$ is the population standard deviation of the pairwise differences.

> proof

Proof. Note that $X_{i}$ and $Y_{i}$ are normal random variables, so $D_{i}=X_{i}-Y_{i}$ is also a normal random variable by Theorem 12. Then $D_{1}, D_{2}, \ldots, D_{n}$ can be thought of as the sequence of random variables $$\left\{X_{i}\right\}_{i=1}^{n}$$ described in Corollary 5 . Therefore, $Z \sim N(0,1)$.

> Remark

- 쌍체검정에서, 이전의 Two Sample Mean Comparison 과 같은 방법을 쓸 수 없는 이유는 , 샘플끼리 Correlated 가 되어있기 때문입니다.
- 그러므로 각각의 Pair 를 짝으로 묶어서 테스트를 하게 되는 것입니다. 
  - 각각의 짝은 independence 가 보장되기 때문이죠!
- 쌍으로 묶고나면 사실, one sample test 와 동일합니다.

# [paired sample z test Procedure](#link){: .btn .btn--primary}{: .align-center}

> ## When can this test be used?

> When to use?

- There are two samples that are the same size.
- The two samples are dependent. (This can be when the two similar subjects are matched or paired, or when subjects come from the same source, or when 2 observations are made on the same subject such as pre and post tests.)
- Both populations are normally distributed or both sample sizes are large enough that the means are normally distributed.
(A rule of thumb is that the sample size is large enough if $n \geq 30$.)
- The standard deviation of the population of pairwise differences is known.

> Remark

- 일반적으로 두개의 샘플이 paired 되어있을때에 사용합니다. ( independent 면 굳이 사용할 )

> ## Notation

$$\begin{array}{|c|c|c|}
\hline x_{i} & \text { Data from sample } 1 & \\
\hline y_{i} & \text { Data from sample } 2 & \\
\hline d_{i} & \text { The pairwise difference } & d_{i}=x_{i}-y_{i} \\
\hline \bar{d} & \begin{array}{c}
\text { The mean of the sample of pairwise } \\
\text { differences }
\end{array} & \bar{d}=\frac{\sum_{i=1}^{n} d_{i}}{n} \\
\hline \sigma_{d} & \begin{array}{c}
\text { The standard deviation of the population } \\
\text { of pair wise differences }
\end{array} & \\
\hline n & \text { The sample size } & \\
\hline \mu_{d} & \begin{array}{c}
\text { The true mean of the population of } \\
\text { pairwise differences }
\end{array} & \\
\hline D & \begin{array}{c}
\text { The hypothesized mean of the pairwise } \\
\text { differences }
\end{array} & \\
\hline
\end{array}$$

> ## Test Procedure

> (1) State the hypotheses:

$$\begin{aligned}
&H_{0}: \mu_{d}=D \\
&H_{A}: \mu_{d} \neq D \text { or } H_{A}: \mu_{d}>D \text { or } H_{A}: \mu_{d}<D
\end{aligned}$$

The hypothesized difference in the means is $D$.

For instance, if Tire Company A thinks that the mean distance of its tires is at least 20,000 miles more than the mean distance of Tire Company B's tires, then $D=20,000$. If both companies put one tire on each car, then the samples would be matched or dependent. The hypotheses could be:

$$\begin{aligned}
&H_{0}: \mu_{d}=20,000 \\
&H_{A}: \mu_{d}>20,000
\end{aligned}$$

Usually, the hypothesized difference is $D=0 .$ In this case the hypotheses simplify to

$$\begin{aligned}
&H_{0}: \mu_{d}=0 \\
&H_{A}: \mu_{d} \neq 0 \text { or } H_{A}: \mu_{d}>0 \text { or } H_{A}: \mu_{d}<0
\end{aligned}$$

> (2) Pick a significance level $\alpha$

> (3) Compute the thest statistic

$$z=\frac{\bar{d}-D}{\frac{\sigma_{d}}{\sqrt{n}}}=\frac{\text { sample mean of pairwise differences }-\text { hypothesized mean of pairwise differences }}{\text { standard deviation of population of pairwise differences } / \sqrt{\text { sample }} \text { size }}$$

> (4) Find th p-value

The p-value depends on which alternative hypothesis is being used. The p-value is the probability or the area in the tail(s) of the standard normal curve.

$\text { If } H_{A}: \mu_{d}>D, \mathrm{p} \text {-value }=P(Z \geq z)$

![png](/assets/images/Stat/104_1.png)

$\text { If } H_{A}: \mu_{d}<D, \mathrm{p} \text {-value }=P(Z \leq z)$

![png](/assets/images/Stat/104_2.png)

$\text { If } H_{A}: \mu_{d} \neq D, \mathrm{p} \text {-value }=P(Z \leq-\mid z\mid \text { or } Z \geq\mid z\mid) \text { or } 2 P(Z \geq\mid z\mid)$

![png](/assets/images/Stat/104_3.png)

> (5) State the Conclusion

- Once the p-value is known, compare it to $\alpha$, the significance level.
- If the p-value is smaller than $\alpha$, the observed outcome wasn't very likely given that the null hypothesis is true. So reject the null hypothesis in favor of the alternative hypothesis.
- If the p-value is greater than $\alpha$ then the observed outcome was likely enough that it is reasonable to assume that the null hypothesis is true so fail to reject the null hypothesis.

$$\begin{array}{|c|c|}
\hline p-\text { value }<\alpha & \text { reject } H_{0} \\
\hline p-\text { value }>\alpha & \text { fail to reject } H_{0} \\
\hline
\end{array}$$

---

**Reference**

- <https://digitalcommons.usu.edu/cgi/viewcontent.cgi?article=1014&context=gradreports>

