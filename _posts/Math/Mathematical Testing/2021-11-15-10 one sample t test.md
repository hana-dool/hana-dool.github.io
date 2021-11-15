---
title:  "One sample t-test for the population mean"
excerpt: "일표본 T test"
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

# [One sample t test](#link){: .btn .btn--primary}{: .align-center}

> ## Lemma 5 

> lemma

$\sum_{i=1}^{n}\left(X_{i}-\bar{X}\right)=0$

> Proof

$$\begin{aligned}
\sum_{i=1}^{n}\left(X_{i}-\bar{X}\right) &=\sum_{i=1}^{n} X_{i}-\sum_{i=1}^{n} \bar{X} \\
&=\sum_{i=1}^{n} X_{i}-n \bar{X} \\
&=\sum_{i=1}^{n} X_{i}-n \frac{\sum_{i=1}^{n} X_{i}}{n} \\
&=\sum_{i=1}^{n} X_{i}-\sum_{i=1}^{n} X_{i} \\
&=0
\end{aligned}$$

> ## Theorem 19 : $(n-1) S^{2}/{\sigma^{2}} \sim \chi_{n-1}$ 

> Theorem

$\frac{(n-1) S^{2}}{\sigma^{2}}$ has a chi-square distribution with $n-1$ degrees of freedom.

> Proof

$$S^{2}=\frac{\sum_{i=1}^{n}\left(X_{i}-\bar{X}\right)^{2}}{n-1}$$

so

$$\frac{(n-1) S^{2}}{\sigma^{2}}=\frac{(n-1)}{\sigma^{2}} \frac{\sum_{i=1}^{n}\left(X_{i}-\bar{X}\right)^{2}}{n-1}=\frac{1}{\sigma^{2}} \sum_{i=1}^{n}\left(X_{i}-\bar{X}\right)^{2}$$

Now

$$\begin{aligned}
\frac{1}{\sigma^{2}} \sum_{i=1}^{n}\left(X_{i}-\mu\right)^{2} &=\sum_{i=1}^{n}\left(\frac{X_{i}-\mu}{\sigma}\right)^{2} \\
&=\sum_{i=1}^{n}\left(Z_{i}\right)^{2} \\
&=\sum_{i=1}^{n} V_{i}
\end{aligned}$$

where $Z_{i} \sim N(0,1)$ by Theorem 13 and $V_{i} \sim \chi_{1}^{2}$ by Definition 7 . Then by Definition 8 ,

$$\frac{1}{\sigma^{2}} \sum_{i=1}^{n}\left(X_{i}-\mu\right)^{2} \sim \chi_{n}^{2}$$

We also have

$$\begin{aligned}
\frac{1}{\sigma^{2}} \sum_{i=1}^{n}\left(X_{i}-\mu\right)^{2} &=\frac{1}{\sigma^{2}} \sum_{i=1}^{n}\left(\left[X_{i}-\bar{X}\right]+[\bar{X}-\mu]\right)^{2} \\
&=\frac{1}{\sigma^{2}} \sum_{i=1}^{n}\left[\left(X_{i}-\bar{X}\right)^{2}+2\left(X_{i}-\bar{X}\right)(\bar{X}-\mu)+(\bar{X}-\mu)^{2}\right] \\
&=\frac{1}{\sigma^{2}} \sum_{i=1}^{n}\left(X_{i}-\bar{X}\right)^{2}+\frac{2}{\sigma^{2}}(\bar{X}-\mu) \sum_{i=1}^{n}\left(X_{i}-\bar{X}\right)+\frac{1}{\sigma^{2}} \sum_{i=1}^{n}(\bar{X}-\mu)^{2}
\end{aligned}$$

Note that $\sum_{i=1}^{n}\left(X_{i}-\bar{X}\right)=0$ by Lemma 5 and $(\bar{X}-\mu)^{2}$ is a constant. Therefore

$$\begin{aligned}
\frac{1}{\sigma^{2}} \sum_{i=1}^{n}\left(X_{i}-\mu\right)^{2} &=\frac{1}{\sigma^{2}} \sum_{i=1}^{n}\left(X_{i}-\bar{X}\right)^{2}+0+\frac{n}{\sigma^{2}}(\bar{X}-\mu)^{2} \\
&=\frac{(n-1) S^{2}}{\sigma^{2}}+\left(\frac{\bar{X}-\mu}{\frac{\sigma}{\sqrt{n}}}\right)^{2}
\end{aligned}$$

Let $W=\frac{1}{\sigma^{2}} \sum_{i=1}^{n}\left(X_{i}-\mu\right)^{2}, U=\frac{(n-1) S^{2}}{\sigma^{2}}$, and $V=\left(\frac{\bar{X}-\mu}{\frac{\sigma}{\sqrt{n}}}\right)^{2} .$ Then $W=U+V$
We know $W \sim \chi_{n}^{2}$ and

$$\frac{\bar{X}-\mu}{\frac{\sigma}{\sqrt{n}}} \sim N(0,1)$$

by Theorem 14 , so $V \sim \chi_{1}^{2}$. The moment generating function of a random variable with $n$ degrees of freedom is $M(t)=(1-2 t)^{-n / 2}$ by Lemma 10. By Theorem $9, M_{W}(t)=M_{U}(t) M_{V}(t)$. Then

$$\begin{aligned}
M_{U}(t) &=\frac{M_{W}(t)}{M_{V}(t)} \\
&=\frac{(1-2 t)^{-n / 2}}{(1-2 t)^{-1 / 2}} \\
&=(1-2 t)^{-(n-1) / 2}
\end{aligned}$$

which is the mgf of random variable with a chi-square distribution with $n-1$ degrees of freedom. By uniqueness of moment generating functions, Proposition $1, U \sim \chi_{n-1}^{2}$

> ## Theorem 20 : $(\bar{X}-\mu)/(S/\sqrt{n}) \sim t_{n-1}$

$$\begin{aligned} \frac{\bar{X}-\mu}{S / \sqrt{n}} &=\frac{1}{S} \cdot \frac{\bar{X}-\mu}{1 / \sqrt{n}} \cdot \sqrt{\frac{\sigma^{2}}{\sigma^{2}}} \\ &=\sqrt{\frac{\sigma^{2}}{S^{2}} \cdot \frac{\bar{X}-\mu}{\sqrt{\sigma^{2} / n}}} \\ &=\sqrt{\frac{(n-1) \sigma^{2}}{(n-1) S^{2}}} \cdot \frac{\bar{X}-\mu}{\sqrt{\sigma^{2} / n}} \\ &=\frac{\frac{\bar{X}-\mu}{\sqrt{\sigma^{2} / n}}}{\sqrt{\frac{\left(\frac{(n-1) S^{2}}{\sigma^{2}}\right)}{(n-1)}}} \\ &=\frac{Z}{\sqrt{\frac{U}{n-1}}} \end{aligned}$$

where $Z=\frac{\bar{X}-\mu}{\sqrt{\sigma^{2} / n}} \sim N(0,1)$ by Theorem 14 and $U=\frac{(n-1) S^{2}}{\sigma^{2}} \sim \chi_{n-1}^{2}$ by Theorem 19. Then by Definition $9, \frac{\bar{X}-\mu}{S / \sqrt{n}} \sim t_{n-1}$

> ## Corollary 8

> Corollary

The test statistic $t=\frac{\bar{X}-\mu_{0}}{S / \sqrt{n}}$ has a t distribution with $n-1$ degrees of freedom under the null hypothesis.

> Proof

This corollary is a direct result of Theorem 20 .

> ## Remark 12 : Statistics 

- 위의 정리들에 의해서, 우리는 t statistics 를 이용하여 one sample t test 를 수행할 수 있을 것입니다! 



---

**Reference**

- <https://digitalcommons.usu.edu/cgi/viewcontent.cgi?article=1014&context=gradreports>

