---
title:  "One sample z-test for the population proportion"
excerpt: "일표본 비율 검정"
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

# [One sample z-test for the population proportion](#link){: .btn .btn--primary}{: .align-center}

> ## proposition 2 : Lindeberg-Levy Central Limit Theorem

> proposition

If $$\left\{X_{n}\right\}_{i=1}^{\infty}$$ is a sequence of random variables that are independent and identically distributed, each with mean $E\left(X_{i}\right)=\mu$ and positive finite variance $\operatorname{Var}\left(X_{i}\right)=\sigma^{2}$, with $$\bar{X}_{n}=\frac{1}{n} \sum_{i=1}^{n} X_{i}$$, then

$$\frac{\sqrt{n}\left(\bar{X}_{n}-\mu\right)}{\sigma} \stackrel{d}{\rightarrow} Z$$

where $\boldsymbol{Z} \sim N(0,1)$

> Remark

- 위의 정리를 증명하려면, 꽤나 힘이 드는 부분이라 여기에서는 넘기겠습니다

> ## Theorem 17

> Theorem 

Therefore, if $X \sim \operatorname{Bin}(n, p)$, and $\hat{p}=\frac{X}{n}$, then for large $n$ $\hat{p}$ is approximately distributed $N\left(p, \frac{p(1-p)}{n}\right)$

> Proof

If $X \sim B i n(n, p)$, then $X=\sum_{i=1}^{n} X_{i}$ where each $X_{i}$ is a Bernoulli random variable with probability of success $p$. Therefore $\hat{p}=\frac{X}{n}=\frac{\sum_{i=1}^{n} X_{i}}{n}=\bar{X} . E\left(X_{i}\right)=p$ and $\operatorname{Var}\left(X_{i}\right)=p(1-p)<\infty$ $\forall i$. Then it holds for $$\hat{p}_{n}=\bar{X}_{n}$$ that

$$\frac{\hat{p}_{n}-p}{\sqrt{\frac{p(1-p)}{n}}} \stackrel{d}{\rightarrow} Z$$

where $Z \sim N(0,1)$ by the Lindeberg-Levy Central Limit Theorem.

> ## Corollary : Test statistics 

> Corollary

The test statistic

$$Z=\frac{\hat{p}-p_{0}}{\sqrt{\frac{p_{0}\left(1-p_{0}\right)}{n}}}$$

is approximately normally distributed under the null hypothesis of $p=p_{0}$ for large $n$

> Proof

Since $\hat{p}$ is approximately normally distributed with mean $p_{0}$ and variance $\frac{p_{0}\left(1-p_{0}\right)}{n}$, by Theorem $13, Z$ is approximately normally distributed.

> Remark

- 위를 보다시피, 우리는 standard normal distribution 을 이용하여, p-value 를 계산할 수 있을 것입니다.
  - population proportion 은 CLT 가 성립하기 때문!



---

**Reference**

- <https://digitalcommons.usu.edu/cgi/viewcontent.cgi?article=1014&context=gradreports>

