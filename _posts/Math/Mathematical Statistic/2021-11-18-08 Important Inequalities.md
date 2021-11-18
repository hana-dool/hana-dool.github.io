---
title:  "Important Inequalites"
excerpt: "중요한 부등식들"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-18

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
---

 이 섹션에서는 Expectation 과 관련된 다양한 inequality 들에 대해서 알아보도록 하겠습니다.
{: .notice--warning}

# [Important Inequalites](#link){: .btn .btn--primary}{: .align-center}

> ## Theorem 

> Theorem

Let $X$ be a random variable and let $m$ be a positive integer. Suppose $E\left[X^{m}\right]$ exists. If $k$ is a positive integer and $k \leq m$, then $E\left[X^{k}\right]$ exists.

> Proof

We prove it for the continuous case; but the proof is similar for the discrete case if we replace integrals by sums. Let $f(x)$ be the pdf of $X .$ Then

$$\begin{aligned}
\int_{-\infty}^{\infty}|x|^{k} f(x) d x &=\int_{|x| \leq 1}|x|^{k} f(x) d x+\int_{|x|>1}|x|^{k} f(x) d x \\
& \leq \int_{|x| \leq 1} f(x) d x+\int_{|x|>1}|x|^{m} f(x) d x \\
& \leq \int_{-\infty}^{\infty} f(x) d x+\int_{-\infty}^{\infty}|x|^{m} f(x) d x \\
& \leq 1+E\left[|X|^{m}\right]<\infty
\end{aligned}$$

> Remark

- 즉 위처럼 m'th moment 의 평균이 존재하면 그보다 작은 값의 평균이 존재한다는것을 알 수 있습니다.
- 즉 '분산' 이 존재하면 '평균' 이 존재한다는것을 알 수 있습니다!

> ## Theorem : Markov's Inequality

> Theorem

Let $u(X)$ be a nonnegative function of the random variable $X .$ If $E[u(X)]$ exists, then for every positive constant $c$,

$$P[u(X) \geq c] \leq \frac{E[u(X)]}{c}$$

> Proof

The proof is given when the random variable $X$ is of the continuous type; but the proof can be adapted to the discrete case 

if we replace integrals by sums. Let $A=\{x: u(x) \geq c\}$ and let $f(x)$ denote the pdf of $X$. Then

$$E[u(X)]=\int_{-\infty}^{\infty} u(x) f(x) d x=\int_{A} u(x) f(x) d x+\int_{A^{c}} u(x) f(x) d x$$

Since each of the integrals in the extreme right-hand member of the preceding equation is nonnegative, the left-hand member is greater than or equal to either of them. In particular,

$$E[u(X)] \geq \int_{A} u(x) f(x) d x$$

However, if $x \in A$, then $u(x) \geq c$; accordingly, the right-hand member of the preceding inequality is not increased if we replace $u(x)$ by $c$. Thus

$$E[u(X)] \geq c \int_{A} f(x) d x$$

Since

$$\int_{A} f(x) d x=P(X \in A)=P[u(X) \geq c]$$

it follows that

$$E[u(X)] \geq c P[u(X) \geq c]$$

which is the desired result.

> ## Theorem : Chebyshev's Inequality

> Theorem

Let the random variable $X$ have a distribution of probability about which we assume only that there is a finite variance $\sigma^{2}$ [by Theorem 1.10.1, this implies the mean $\mu=E(X)$ exists]. Then for every $k>0$

![png](/assets/images/Stat/106_1.png)

$$P(|X-\mu| \geq k \sigma) \leq \frac{1}{k^{2}}$$

or, equivalently,

$$P(|X-\mu|<k \sigma) \geq 1-\frac{1}{k^{2}}$$

> Proof

Proof. In Theorem $1.10 .2$ take $u(X)=(X-\mu)^{2}$ and $c=k^{2} \sigma^{2} .$ Then we have

$$P\left[(X-\mu)^{2} \geq k^{2} \sigma^{2}\right] \leq \frac{E\left[(X-\mu)^{2}\right]}{k^{2} \sigma^{2}}$$

Since the numerator of the right-hand member of the preceding inequality is $\sigma^{2}$, the inequality may be written

$$P(|X-\mu| \geq k \sigma) \leq \frac{1}{k^{2}}$$

which is the desired result. Naturally, we would take the positive number $k$ to be greater than 1 to have an inequality of interest.

> ## Theorem : Jensen’s Inequality

> Theorem

![png](/assets/images/Stat/106_2.png)

If $\phi$ is convex on an open interval $I$ and $X$ is a random variable whose support is contained in $I$ and has finite expectation, then

$$\phi[E(X)] \leq E[\phi(X)]$$

If $\phi$ is strictly convex, then the inequality is strict unless $X$ is a constant random variable.

> Proof

Proof: For our proof we assume that $\phi$ has a second derivative, but in general only convexity is required. Expand $\phi(x)$ into a Taylor series about $\mu=E[X]$ of order 2 :

$$\phi(x)=\phi(\mu)+\phi^{\prime}(\mu)(x-\mu)+\frac{\phi^{\prime \prime}(\zeta)(x-\mu)^{2}}{2}$$

where $\zeta$ is between $x$ and $\mu$. Because the last term on the right side of the above equation is nonnegative, we have

$$\phi(x) \geq \phi(\mu)+\phi^{\prime}(\mu)(x-\mu)$$

Taking expectations of both sides leads to the result. The inequality is strict if $\phi^{\prime \prime}(x)>0$, for all $x \in(a, b)$, provided $X$ is not a constant.

> Example

Let $X$ be a nondegenerate random variable with mean $\mu$ and a finite second moment. Then $\mu^{2}<E\left(X^{2}\right)$. This is obtained by Jensen's inequality using the strictly convex function $\phi(t)=t^{2}$.

---

**Reference**

- Hoggs Introduction to Mathematical Statistics 7ed



