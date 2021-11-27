---
title:  "Confidence interval for Discrete"
excerpt: "이산확률 분포에 대한 CI 구하기"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-25

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
---

 Confidence interval 에 대해서 알아보기 ( for Discrete Distribution )
{: .notice--warning}

# [Interval Estimation ans Hypothesis Testing](#link){: .btn .btn--primary}{: .align-center}

> ## Definition : Confidence interval

- 이 섹션에서 우리는 Discrete Random Variable 에 대하여 Exact Confidence interval 을 알아보도록 하겠습니다. 
- Let $X_{1}, X_{2}, \ldots, X_{n}$ be a random sample on a discrete random variable $X$ with $\operatorname{pmf} p(x ; \theta), \theta \in \Omega$, where $\Omega$ is an interval of real numbers. 
- Let $T=T\left(X_{1}, X_{2}, \ldots, X_{n}\right)$ be an estimator of $\theta$ with $\operatorname{cdf} F_{T}(t ; \theta)$. Assume that $F_{T}(t ; \theta)$ is a nonincreasing and continuous function of $\theta$ for every $t$ in the support of $T$. 
  - 즉 $\theta$ 의 변화에 따라서 cdf 는 increasing 이 아니라는 것입니다.
- Let $\alpha_{1}>0$ and $\alpha_{2}>0$ be given such that $\alpha=\alpha_{1}+\alpha_{2}<0.50$. Let $\underline{\theta}$ and $\bar{\theta}$ be the solutions of the equations

$$F_{T}(T-; \underline{\theta})=1-\alpha_{2} \text { and } F_{T}(T ; \bar{\theta})=\alpha_{1}$$

where $T-$ is the statistic whose support lags by one value of $T$ 's support. For instance, if $t_{i}<t_{i+1}$ are consecutive support values of $T$, then $T=t_{i+1}$ if and only if $T-=t_{i}$. 

- 이때 위처럼 정의한 $\underline{\theta}$ 와 $\bar{\theta}$ 는 Confidence interval 이 될 수 있습니다. (증명은 아래에서 하겠습니다.)

> Proof

A brief sketch of the theory behind this confidence interval follows. Consider the general setup in the first paragraph of this section, where $T$ is an estimator of the unknown parameter $\theta$ and $F_{T}(t ; \theta)$ is the cdf of $T$. Define
$$
\begin{aligned}
\bar{\theta} &=\sup \left\{\theta: F_{T}(T ; \theta) \geq \alpha_{1}\right\} \\
\underline{\theta} &=\inf \left\{\theta: F_{T}(T-; \theta) \leq 1-\alpha_{2}\right\}
\end{aligned}
$$
Hence, we have
$$
\begin{aligned}
\theta>\bar{\theta} & \Rightarrow F_{T}(T ; \theta) \leq \alpha_{1} \\
\theta<\underline{\theta} & \Rightarrow F_{T}(T-; \theta) \geq 1-\alpha_{2}
\end{aligned}
$$
These implications lead to
$$
\begin{aligned}
P[\underline{\theta}<\theta<\bar{\theta}] &=1-P[\{\theta<\underline{\theta}\} \cup\{\theta>\bar{\theta}\}] \\
&=1-P[\theta<\underline{\theta}]-P[\theta>\bar{\theta}] \\
& \geq 1-P\left[F_{T}(T-; \theta) \geq 1-\alpha_{2}\right]-P\left[F_{T}(T ; \theta) \leq \alpha_{1}\right] \\
& \geq 1-\alpha_{1}-\alpha_{2},
\end{aligned}
$$
where the last inequality is evident from equations (4.3.9) and (4.3.10). A rigorous proof can be based on Exercise $4.8 .13 ;$ see page 425 of Shao (1998) for details.

> ## Bisect Algorithm 

> Algorithm

Suppose we want to solve the equation $g(x)=d$, where $g(x)$ is strictly decreasing. Assume on a given step of the algorithm that $a<b$ bracket the solution; i.e., $g(a)>d$ and $g(b)<d .$ Let $c=(a+b) / 2 .$ Then on the next step of the algorithm, the new bracket values $a$ and $b$ are determined by

$$\begin{array}{lll}
\operatorname{if}(g(c)>d) & \text { then } & \{a \leftarrow c \text { and } b \leftarrow b\} \\
\operatorname{if}(g(c)<d) & \text { then } & \{a \leftarrow a \text { and } b \leftarrow c\}
\end{array}$$

The algorithm continues until $a-b<\epsilon$, where $\epsilon>0$ is a specified tolerance.

> ## Example

> Example

Let $X$ have a Bernoulli distribution with $\theta$ as the probability of success. Let $\Omega=(0,1) .$ Suppose $X_{1}, X_{2}, \ldots, X_{n}$ is a random sample on $X$. As our point estimator of $\theta$, we consider $\bar{X}$, which is the sample proportion of successes. 

> CDF 를 구한뒤에, Decreasing 임을 증명하기

The cdf of $n \bar{X}$ is binomial $(n . \theta)$. Thus

$$\begin{aligned}
F_{\bar{X}}(\bar{x} ; \theta) &=P(n \bar{X} \leq n \bar{x}) \\
&=\sum_{j=0}^{n \bar{x}}\left(\begin{array}{c}
n \\
j
\end{array}\right) \theta^{j}(1-\theta)^{n-j} \\
&=1-\sum_{j=n \bar{x}+1}^{n}\left(\begin{array}{c}
n \\
j
\end{array}\right) \theta^{j}(1-\theta)^{n-j} \\
&=1-\int_{0}^{\theta} \frac{n !}{(n \bar{x}) ![n-(n \bar{x}+1] ! !} z^{n \bar{x}}(1-z)^{n-(n \bar{x}+1)} d z ....(1)
\end{aligned}$$

마지막 equality 으로 변하는 이유는 여기서 증명하지는 않겠습니다. 이떄 우리는 Fundamental Theorem of Calculus 로 인하여 위 식 (1) 을 미분하면 아래와 같습니다. 
$$
\frac{d}{d \theta} F_{\bar{X}}(\bar{x} ; \theta)=-\frac{n !}{(n \bar{x}) ![n-(n \bar{x}+1] !} \theta^{n \bar{x}}(1-\theta)^{n-(n \bar{x}+1)}<0
$$
hence, $F_{\bar{X}}(\bar{x} ; \theta)$ is a strictly decreasing function of $\theta$, for each $\bar{x}$. 

> $\alpha_1 , \alpha_2$ 을 정하여 Confidence interval 을 만들어내기

Next, let $\alpha_{1}, \alpha_{2}>0$ be specified constants such that $\alpha_{1}+\alpha_{2}<1 / 2$ and let $\underline{\theta}$ and $\bar{\theta}$ solve the equations

$$F_{\bar{X}}(\bar{X}-; \underline{\theta})=1-\alpha_{2} \text { and } F_{\bar{X}}(\bar{X} ; \bar{\theta})=\alpha_{1}$$

Then $(\underline{\theta}, \bar{\theta})$ is a confidence interval for $\theta$ with confidence coefficient at least $1-\alpha$, where $\alpha=\alpha_{1}+\alpha_{2}$. These equations can be solved iteratively, as discussed in the following numerical illustration.

> ## Example : Numerical Calculation

- 위에서, 어떻게 구하면 된다! 까지는 알았으므로, 이제 실제로 예시를 통하여 어떻게 하면 Confidence interval 을 계산할 수 있을지에 대해서 알아봅시다.

> Example

Suppose $n=30, \bar{x}=0.60$​, and $\alpha_{1}=\alpha_{2}=0.05$​ Because the support of the binomial consists of integers and $n \bar{x}=18$​, we can write the equation in $$F_{\bar{X}}(\bar{X}-; \underline{\theta})=1-\alpha_{2} $$ As 

$$\sum_{j=0}^{17}\left(\begin{array}{l}
n \\
j
\end{array}\right) \underline{\theta}^{j}(1-\underline{\theta})^{n-j}=0.95$$

Let $\operatorname{bin}(n, p)$ denote a random variable with binomial distribution with parameters $n$ and $p$. Because $P(\operatorname{bin}(30,0.4) \leq 17)=0.9787$ and $P(\operatorname{bin}(30,0.45) \leq 17)=$ $0.9286$, the values $0.4$ and $0.45$ bracket the solution to the first equation. We used the $\mathrm{R}$ command pbinom to do these computations. Using these bracket values as input to the R function binomci.r (see Appendix B) the solution to the first equation is $\underline{\theta}=0.434$. In the same way, because $P(\operatorname{bin}(30,0.7) \leq 18)=0.1593$ and $P(\operatorname{bin}(30,0.8) \leq 18)=0.0094$, the values $0.7$ and $0.8$ bracket the solution to the second equation. This leads to the solution $\bar{\theta}=0.750$. Thus the confidence interval is $(0.434,0.750)$, with a confidence of at least $90 \%$. For comparison, the asymptotic $90 \%$ confidence interval of $$
\left(\widehat{p}-z_{\alpha / 2} \sqrt{\widehat{p}(1-\widehat{p}) / n}, \widehat{p}+z_{\alpha / 2} \sqrt{\widehat{p}(1-\widehat{p}) / n}\right)$$ is $(0.453,0.747)$ 

---

**Reference**

- Hoggs Introduction to Mathematical Statistics 7ed



