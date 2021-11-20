---
title:  "Interval Estimation"
excerpt: "신뢰 구간에 대해서 알아보기"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-19

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
---

 Confidence interval 에 대해서 알아보기
{: .notice--warning}

# [Interval Estimation ans Hypothesis Testing](#link){: .btn .btn--primary}{: .align-center}

> ## Definition : Confidence interval

> Definition

Let $X_{1}, \ldots, X_{n}$ be a sample on a random variable $X$, where $X$ has $f(x ; \theta)$, $\theta \in \Theta .$ Let $0<\alpha<1$ be specified. Let $L=L\left(X_{1}, \ldots, X_{n}\right)$ and $U=U\left(X_{1}, \ldots, X_{n}\right)$ be two statistics. We say that the interval $(L, U)$ is a $(1-\alpha) \times 100 \%$ confidence interval for $\theta$ if

$$1-\alpha=P_{\theta}\{\theta \in(L, U)\}$$

That is, the probability that the interval includes $\theta$ is $1-\alpha$, which is called the confidence coefficient of the interval. Here, $L$ and $U$ are called as lower and upper confidence limits, respectively.

> Note

- 우선, 여기에서 설명하는것들은 모두 Frequantist View 이므로 신뢰구간도 Freq View 로 설명하겠습니다.
- 위의 Confidence interval 은 'interval' 이 $\theta$ 를 포함할 확률이 $1-\alpha$ 라는 의미입니다. 
  - 이는 '모수' 는 고정되어있고, 신뢰구간의 Upper 과 Lower 는 R.V. 인 데이터로 이루어진 함수라는것을 기억합시다.

![png](/assets/images/Stat/107_1.png)

- 즉 위 그림처럼 Confidence interval 은 데이터에 따라 바뀌며, 무수한 CI 중에서 $\theta$ 를 포함할 확률이 95% 라는것을 의미합니다! 

> ## Definition : Pivotal Quantity

> Definition : Pivotal Quantity

Let $X_{1}, \ldots, X_{n}$ be a random sample from the density $f(x ; \theta) .$ Let $Q=q\left(X_{1}, \ldots, X_{n} ; \theta\right)$ be a function of $X_{1}, \ldots, X_{n}$ and $\theta$. If $Q$ has a distribution that does not depend on $\theta$, then we call $Q$ as a pivotal quantity.

> Note

- 즉 Q 라는 통계량이 따르는 분포가 $\theta$ 에 영향을 받지 않을때, Q 를 pivoval Quantity 라고 부르게 됩니다.

$$\begin{aligned}
&X_{1}, \ldots, X_{n} \stackrel{i i d}{\sim} N\left(\mu, \sigma^{2}\right) . \\
&T=(\bar{X}-\mu) /(S / \sqrt{n}) \text { has a t(n-1)-distribution. }
\end{aligned}$$

- 위와 같이 통계량 $T$ 는 $t_{n-1}$ 의 분포를 따르고 있습니다.
  - 이때 분포 $t_{n-1}$ 은 $\mu$ 와는 상관 없다는것을 잘 보세요! 즉 Pivotal Quantity 가 될 수 있습니다.

> ## Method : Pivotal Quantity Method

> Method

Pivotal Quantity method For any fixed $\alpha \in(0,1)$, there will exist $q_{1}$ and $q_{2}$ depending on $\alpha$ such that

$$P\left(q_{1}<Q<q_{2}\right)=1-\alpha$$

- (i) $q_{1}$ and $q_{2}$ are independent of $\theta$.
- (ii) the interval $\left(q_{1}, q_{2}\right)$ can be 'inverted' or 'pivoted' around our target parameter $\theta$.
- (iii) For any fixed $\alpha$, there exists many pairs of $\left(q_{1}, q_{2}\right)$ and then they produce the different confidence limits.

> Note

- 즉 Confidence Interval 이라는게 Upper , Lower 를 어느정도 잘 설정해서, 모수를 커버할 확률이 $1-\alpha$ 으로만 만들면 됩니다.
- 즉 '무수히 많은' Confidence interval 을 생성할 수 있다는 것이죠. 
- 이때에 자연스럽게 드는 의문 하나가 있을텐데요, 이렇게 무수히 많은 Confidence interval 들 중에서 어떤것을 골라야 좋은 CI 가 될까요? 

> ## confidence interval for $\mu$ under normality

> Example : confidence interval for $\mu$ under normality

Confidence interval for $\mu$ under normality.

- $X_{1}, \ldots, X_{n} \stackrel{i i d}{\sim} N\left(\mu, \sigma^{2}\right)$
- $T=(\bar{X}-\mu) /(S / \sqrt{n})$ has a t-distribution.

- $(1-\alpha) \times 100 \%$ confidence interval for $\mu$

$$\left(\bar{x}-t_{1-\alpha / 2, n-1} s / \sqrt{n}, \bar{x}+t_{1-\alpha / 2, n-1} s / \sqrt{n}\right)$$

> Note : 왜 Pivotal Quantity 사용시에 $(\bar{X}-\mu) /(\sigma / \sqrt{n})$ 는 사용하지 않는지?

- Population variance $\sigma^{2}$ 를 알아야 하기 때문입니다. 
- 지금 우리가 보려고 하는 모수는 $\mu$ 이니까요..

> Note : 왜 위와 같은 interval 을 사용하였는지? 

- 일반적으로 A general expression of confidence intervals 은

$$\left(\bar{X}-q_{2}(S / \sqrt{n}), \bar{X}-q_{1}(S / \sqrt{n})\right)$$

- 이때 위의 CI 길이는 $L=\left(q_{2}-q_{1}\right) \times(S / \sqrt{n})$ 가 됩니다.
- 우리는 길이를 최소화 하고 싶습니다. 
  - $L$ subject to $\int_{q_{1}}^{q_{2}} f(t) d t=1-\alpha$, where $f(t)$ follows $t$-distribution with $n-1$ degrees of freedom.
- Will obtain $q_{1}=-q_{2}$ as the solution of the above optimization problem.
  - 이때 Optimization 은 $L$ 이 최소값을 가지게 미분했을때 0, 두번 미분했을때는 양수가 나오도록 식을 짜서 식을 풀어보면 위와 같습니다. 

# [Optimal Confidence interval](#link){: .btn .btn--primary}{: .align-center}

> ## Confidence interval for the variance $\sigma^{2}$.

> Example

- $X_{1}, \ldots, X_{n} \stackrel{i i d}{\sim} N\left(\mu, \sigma^{2}\right)$$
- $$T=(n-1) S^{2} / \sigma^{2}$$ has a chi-square distribution with $n-1$ degrees of freedom

- $(1-\alpha) \times 100 \%$ confidence interval for $\sigma^{2}$

$$\left(\frac{(n-1) S^{2}}{\chi_{1-\alpha / 2}^{2}}, \frac{(n-1) S^{2}}{\chi_{\alpha / 2}^{2}}\right)$$

> Note : 추정은 $\sigma$ 인데 이때 $\mu$ 는 어떻게 해야될까요?

- 이때 $\mu$ 는 모르는 값이여도 됩니다. 
  - 왜냐하면 애초에 Statistic 자체에 $\mu$ 가 없어도 되니까요 

> Note : Confidence interval 은 optimal 할까?

- Optimal confidence interval? first consider a general expression

$$\left(\frac{(n-1) S^{2}}{q_{2}}, \frac{(n-1) S^{2}}{q_{1}}\right)$$

- Length of confidence intervals: $L=\left(1 / q_{1}-1 / q_{2}\right)(n-1) S^{2}$.
- Want to minimize the length $L$ subject to $\int_{q_{1}}^{q_{2}} f(t) d t=1-\alpha$, where $f(t)$ follows chi-square distribution with $n-1$ degrees of freedom.
- Will obtain $q_{1}^{2} f\left(q_{1}\right)=q_{2}^{2} f\left(q_{2}\right)$ as the solution of the above optimization problem.
- 하지만 위의 Optimization 은 Closed Form 이 없습니다.
  - 그래서 그냥 편의상 Equal Tail 을 사용합니다.

# [Confidence interval](#link){: .btn .btn--primary}{: .align-center}

> ## difference in means (equal var)

> Example : Confidence intervals for difference in means

- (i) $X_{1}, \ldots, X_{n_{1}} \stackrel{i i d}{\sim}\left(\mu_{1}, \sigma_{1}^{2}\right)$ and $Y_{1}, \ldots, Y_{n_{2}} \stackrel{i i d}{\sim}\left(\mu_{2}, \sigma_{2}^{2}\right)$.

- (ii) Normal assumption on $X$ and $Y$ with equal variance $\sigma_{1}^{2}=\sigma_{2}^{2}$ :

$$T=\frac{\bar{X}-\bar{Y}-\left(\mu_{1}-\mu_{2}\right)}{S_{p} \sqrt{\frac{1}{n_{1}}+\frac{1}{n_{2}}}} \stackrel{d}{\sim} t(n-2)$$

where

$$S_{p}^{2}=\frac{\left(n_{1}-1\right) S_{1}^{2}+\left(n_{2}-1\right) S_{2}^{2}}{n_{1}+n_{2}-2}$$

> Confidence interval 

$(1-\alpha) \times 100 \%$ confidence interval for $\mu_{1}-\mu_{2}$

$$\left((\bar{x}-\bar{y})-t_{1-\alpha / 2, n-2} s_{p} \sqrt{\frac{1}{n_{1}}+\frac{1}{n_{2}}},(\bar{x}-\bar{y})+t_{1-\alpha / 2, n-2} s_{p} \sqrt{\frac{1}{n_{1}}+\frac{1}{n_{2}}}\right)$$

> ## Difference in means (not equal var)

> Example : Confidence intervals for difference in means

- (i) $X_{1}, \ldots, X_{n_{1}} \stackrel{i i d}{\sim}\left(\mu_{1}, \sigma_{1}^{2}\right)$ and $Y_{1}, \ldots, Y_{n_{2}} \stackrel{i i d}{\sim}\left(\mu_{2}, \sigma_{2}^{2}\right)$.
- (ii) Normal assumption on $X$ and $Y$ but $\sigma_{1}^{2} \neq \sigma_{2}^{2}$ :

$$T=\frac{\bar{X}-\bar{Y}-\left(\mu_{1}-\mu_{2}\right)}{\sqrt{\frac{S_{1}^{2}}{n_{1}}+\frac{S_{2}^{2}}{n_{2}}}} \stackrel{d}{\sim} t(v)$$

> Confidence Interval

where

$$v=\frac{\left(\frac{S_{1}^{2}}{n_{1}}+\frac{S_{2}^{2}}{n_{2}}\right)^{2}}{\frac{S_{1}^{4}}{n_{1}^{2}\left(n_{1}-1\right)}+\frac{S_{2}^{4}}{n_{2}^{2}\left(n_{2}-1\right)}}$$

and $S_{1}^{2}=\left(n_{1}-1\right)^{-1} \sum_{i=1}^{n_{i}}\left(X_{i}-\bar{X}\right)^{2}$ and $S_{2}^{2}=\left(n_{1}-1\right)^{-1} \sum_{i=1}^{n_{i}}\left(Y_{i}-\bar{Y}\right)^{2} .$
Then, $(1-\alpha) \times 100 \%$ confidence interval for $\mu_{1}-\mu_{2}$

$$\left((\bar{x}-\bar{y})-t_{1-\alpha / 2, v} \sqrt{\frac{s_{1}^{2}}{n_{1}}+\frac{s_{2}^{2}}{n_{2}}},(\bar{x}-\bar{y})+t_{1-\alpha / 2, v} \sqrt{\frac{s_{1}^{2}}{n_{1}}+\frac{s_{2}^{2}}{n_{2}}}\right)$$

> ## Confidence for bibrate normal

> Example 

- $\left(X_{1}, Y_{1}\right), \ldots,\left(X_{n}, Y_{n}\right)$ is a random sample generated from a bivariate normal distribution with a correlation $\rho,-1<\rho<1$.
- Define $D_{i}=X_{i}-Y_{i} .$ Then $D_{i} \stackrel{i i d}{\sim} N\left(\mu_{1}-\mu_{2}, \sigma_{1}^{2}+\sigma_{2}^{2}-2 \rho \sigma_{1} \sigma_{2}\right) .$
> Confidence interval

- $(1-\alpha) \times 100 \%$ confidence interval for $\mu_{1}-\mu_{2}$

$$\left(\bar{d}-t_{1-\alpha / 2, n-1} \sqrt{\frac{s_{D}^{2}}{n}}, \bar{d}+t_{1-\alpha / 2, n-1} \sqrt{\frac{s_{D}^{2}}{n}}\right)$$

where $\bar{D}=n^{-1} \sum_{i=1}^{n} D_{i}$ and $S_{D}^{2}$ is the sample variance of $d_{1}, \ldots, d_{n}$

# [Confidence interval for Large sample](#link){: .btn .btn--primary}{: .align-center}

> ## Confidence interval for large sample

> Large sample + $\mu$

Large sample confidence interval for $\mu$ without normality. 

- $X_{1}, \ldots, X_{n} \stackrel{i i d}{\sim}\left(\mu, \sigma^{2}\right)$
- $T=(\bar{X}-\mu) /(S / \sqrt{n})$ has a normal distribution

> Confidence interval

$(1-\alpha) \times 100 \%$ confidence interval for $\mu$

$$\left(\bar{x}-z_{1-\alpha / 2} s / \sqrt{n}, \bar{x}+z_{1-\alpha / 2} s / \sqrt{n}\right)$$

> ## Confidence interval for proportion p

> Large sample + $p$

Large sample confidence interval for proportion $p$ 

- $X_{1}, \ldots, X_{n} \stackrel{i i d}{\sim} \operatorname{Bernoulli}(p)$

> Confidence interval

- $(1-\alpha) \times 100 \%$ confidence interval for $p$

$$\left(\hat{p}-z_{1-\alpha / 2} \sqrt{\hat{p}(1-\hat{p}) / n}, \hat{p}+z_{1-\alpha / 2} \sqrt{\hat{p}(1-\hat{p}) / n}\right)$$

> ## Confidence intervals for differene in means

> difference in means

- $X_{1}, \ldots, X_{n_{1}} \stackrel{i i d}{\sim}\left(\mu_{1}, \sigma_{1}^{2}\right)$ and $Y_{1}, \ldots, Y_{n_{2}} \stackrel{i i d}{\sim}\left(\mu_{2}, \sigma_{2}^{2}\right)$

$$Z=\frac{\bar{X}-\bar{Y}-\left(\mu_{1}-\mu_{2}\right)}{\sqrt{\frac{S_{1}^{2}}{n_{1}}+\frac{S_{2}^{2}}{n_{2}}}} \stackrel{d}{\rightarrow} N(0,1)$$

- $(1-\alpha) \times 100 \%$ confidence interval for $\mu_{1}-\mu_{2}$

$$\left((\bar{x}-\bar{y})-z_{1-\alpha / 2} \sqrt{\frac{s_{1}^{2}}{n_{1}}+\frac{s_{2}^{2}}{n_{2}}},(\bar{x}-\bar{y})+z_{1-\alpha / 2} \sqrt{\frac{s_{1}^{2}}{n_{1}}+\frac{s_{2}^{2}}{n_{2}}}\right)$$

> ## Confidence intervals for difference in proportions

> Difference in proportions

- $X_{1}, \ldots, X_{n} \stackrel{i i d}{\sim} \operatorname{Bernoulli}\left(p_{1}\right)$ and $Y_{1}, \ldots, Y_{n} \stackrel{i i d}{\sim} \operatorname{Bernoulli}\left(p_{2}\right)$

> Confidence intervals

- $(1-\alpha) \times 100 \%$ confidence interval for $p_{1}-p_{2}$

$$\hat{p}_{1}-\hat{p}_{2} \pm z_{\alpha / 2} \sqrt{\hat{p}_{1}\left(1-\hat{p}_{1}\right) / n_{1}+\hat{p}_{2}\left(1-\hat{p}_{2}\right) / n_{2}}$$

---

**Reference**

- Hoggs Introduction to Mathematical Statistics 7ed
- yonsei university Mathematical Statistics (2) lecture notes



