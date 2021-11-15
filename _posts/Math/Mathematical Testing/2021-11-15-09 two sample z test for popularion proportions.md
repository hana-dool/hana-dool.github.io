---
title:  "Two sample z-test for the population proportion"
excerpt: "이표본 비율검정"
categories:
  - Mathematical_Testing
last_modified_at: 2021-11-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 비율에 대한 검정
{: .notice--warning}

# [Two sample z-test for the population proportion](#link){: .btn .btn--primary}{: .align-center}

> ## Theorem 18

> Theorem

If $X \sim \operatorname{Bin}\left(p_{X}, n\right)$ and $Y \sim \operatorname{Bin}\left(p_{Y}, m\right)$, then $\hat{p}_{X}=\frac{X}{n}$ is approximately distributed

$$N\left(p_{X}, \frac{p_{X}\left(1-p_{X}\right)}{n}\right)$$

and $\hat{p}_{Y}=\frac{Y}{m}$ is approximately distributed

$$N\left(p_{Y}, \frac{p_{Y}\left(1-p_{Y}\right)}{m}\right)$$

by Theorem 17. Then $\hat{p}_{X}-\hat{p}_{Y}$ is approximately distributed

$$N\left(p_{X}-p_{Y}, \frac{p_{X}\left(1-p_{X}\right)}{n}+\frac{p_{Y}\left(1-p_{Y}\right)}{m}\right)$$

by Theorems 10 and 12. Therefore

$$\frac{\left(\hat{p}_{X}-\hat{p}_{Y}\right)-\left(p_{X}-p_{Y}\right)}{\sqrt{\frac{p_{X}\left(1-p_{X}\right)}{n}+\frac{p_{Y}\left(1-p_{Y}\right)}{m}}}$$

has an approximate standard normal distribution.

> Proof

PROOF. See theorem 13 with $E\left(\hat{p}_{X}-\hat{p}_{Y}\right)=p_{X}-p_{Y}$ and

$$\operatorname{Var}\left(\hat{p}_{X}-\hat{p}_{Y}\right)=\frac{p_{X}\left(1-p_{X}\right)}{n}+\frac{p_{Y}\left(1-p_{Y}\right)}{n}$$

> ## Corollary 7

> Corollary

Under the null hypothesis that $p_{X}=p_{Y}=p$,

$$\frac{\left(\hat{p}_{X}-\hat{p}_{Y}\right)}{\sqrt{p(1-p)\left(\frac{1}{n}+\frac{1}{m}\right)}}$$

Has an approximate standard normal distribution 

> Proof

$$\begin{aligned}
\frac{\left(\hat{p}_{X}-\hat{p}_{Y}\right)-\left(p_{X}-p_{Y}\right)}{\sqrt{\frac{p_{X}\left(1-p_{X}\right)}{n}+\frac{p_{Y}\left(1-p_{Y}\right)}{m}}} &=\frac{\left(\hat{p}_{X}-\hat{p}_{Y}\right)-(p-p)}{\sqrt{\frac{p(1-p)}{n}+\frac{p(1-p)}{m}}} \\
&=\frac{\left(\hat{p}_{X}-\hat{p}_{Y}\right)}{\sqrt{p(1-p)\left(\frac{1}{n}+\frac{1}{m}\right)}}
\end{aligned}$$

> Remark

- two sample z- test for population proportions  을 할 때, 우리는 다음과 같은 Null hypothesis 를 가정하게 됩니다.

$$p_X = p_Y = p$$

- p 는 미지의 값이므로 우리는 $$\hat{p}=\frac{X+Y}{n+m}$$ 값을 overall proportion 으로서 , $p$ 를 추정하게 됩니다. 

> ## Remark 10 : Test statistics

> Remark

As a result of Corollary 7 , the test statistic

$$Z=\frac{\left(\hat{p}_{X}-\hat{p}_{Y}\right)}{\sqrt{\hat{p}(1-\hat{p})\left(\frac{1}{n}+\frac{1}{m}\right)}}$$

has an approximate normal distribution. 

> Note

- 그러므로, Standard normal distribution 을 이용하여 two sample z test for population proportion 에 이용할 수 있을 것입니다.

# [Test Procedure](#link){: .btn .btn--primary}{: .align-center}

> ## When can this test be used?

- The data comes from a binomial experiment.
- Both sample sizes are large. (A rule of thumb is that the sample sizes are large enough the number of success and the number of failures is at least 5 for both samples)

> ## Notation

$$\begin{array}{|c|c|c|c|c|}
\hline \text { Population } & \text { Count of Successes } & \text { Sample Size } & \text { Population Proportion } & \text { Sample Proportion } \\
\hline \hline 1 & X & n & p_{x} & \hat{p}_{x}=\frac{X}{n} \\
\hline 2 & Y & m & p_{y} & \hat{p}_{y}=\frac{Y}{m} \\
\hline
\end{array}$$

> ## How this test used?

> (1) State the hypotheses:

$$\begin{aligned}
&H_{0}: p_{x}=p_{y} \\
&H_{A}: p_x \neq p_{y} \text { or } H_{A}: p_x>p_{y} \text { or } H_{A}: p_x<p_{y}
\end{aligned}$$

> (2) Pick a significance level, $\alpha$.

> (3) Compute the test statistic:

$$z=\frac{\hat{p}_{x}-\hat{p}_{y}}{\sqrt{\hat{p}(1-\hat{p})\left(\frac{1}{n}+\frac{1}{m}\right)}}$$

where $\hat{p}=\frac{X+Y}{n+m}$ is the overall proportion of successes.

> (4) Find the p-value

The p-value depends on which alternative hypothesis is being used. The p-value is the probability or the area in the tail(s) of the standard normal curve.

$\text { If } H_{A}: p_{x}>p_{y}, \text { p-value }=P(Z \geq z)$

![png](/assets/images/Stat/104_1.png)

$\text { If } H_{A}: p_{x}<p_{y}, \mathrm{p} \text {-value }=P(Z \leq z)$

![png](/assets/images/Stat/104_2.png)

$\text { If } H_{A}: p_{x} \neq p_{y}, \text { p-value }=P(Z \leq-|z| \text { or } Z \geq|z|) \text { or } 2 P(Z \geq|z|)$

![png](/assets/images/Stat/104_3.png)

> (5) State the conclusion

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

