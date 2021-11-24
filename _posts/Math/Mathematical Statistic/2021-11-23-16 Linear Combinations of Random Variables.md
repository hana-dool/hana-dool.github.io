---
title:  "Linear Combinations of Random Variables"
excerpt: "Linear 변환에 대해 알아보기"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-23

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
---

 여러 변수들에 대한 Linearlity 성질
{: .notice--warning}

# [Linear Combinations of Random Variables](#link){: .btn .btn--primary}{: .align-center}

> ## Expectation Linear Combinations

> Theorem

Let $T=\sum_{i=1}^{n} a_{i} X_{i} .$ Provided $$E\left[\mid X_{i}\mid \right]<\infty$$, for $i=1, \ldots, n$ Then

$$E(T)=\sum_{i=1}^{n} a_{i} E\left(X_{i}\right)$$

> ## Covariance Linear Combinations

> Theorem

Let $T=\sum_{i=1}^{n} a_{i} X_{i}$ and let $W=\sum_{i=1}^{m} b_{i} Y_{i} .$ If $E\left[X_{i}^{2}\right]<\infty$, and $E\left[Y_{j}^{2}\right]<\infty$ for $i=1, \ldots, n$ and $j=1, \ldots, m$, then

$$\operatorname{Cov}(T, W)=\sum_{i=1}^{n} \sum_{j=1}^{m} a_{i} b_{j} \operatorname{Cov}\left(X_{i}, Y_{j}\right)$$

> Proof

$$\begin{aligned}
\operatorname{Cov}(T, W) &=E\left[\sum_{i=1}^{n} \sum_{j=1}^{m}\left(a_{i} X_{i}-a_{i} E\left(X_{i}\right)\right)\left(b_{j} Y_{j}-b_{j} E\left(Y_{j}\right)\right)\right] \\
&=\sum_{i=1}^{n} \sum_{j=1}^{m} a_{i} b_{j} E\left[\left(X_{i}-E\left(X_{i}\right)\right)\left(Y_{j}-E\left(Y_{j}\right)\right)\right]
\end{aligned}$$

> Corollary

Let $T=\sum_{i=1}^{n} a_{i} X_{i}$. Provided $E\left[X_{i}^{2}\right]<\infty$, for $i=1, \ldots, n$,

$$\operatorname{Var}(T)=\operatorname{Cov}(T, T)=\sum_{i=1}^{n} a_{i}^{2} \operatorname{Var}\left(X_{i}\right)+2 \sum_{i<j} a_{i} a_{j} \operatorname{Cov}\left(X_{i}, X_{j}\right)$$

> Corollary

If $X_{1}, \ldots, X_{n}$ are independent random variables with finite variances, then

$$\operatorname{Var}(T)=\sum_{i=1}^{n} a_{i}^{2} \operatorname{Var}\left(X_{i}\right)$$

Note that we need only $X_{i}$ and $X_{j}$ to be uncorrelated for all $i \neq j$ to obtain this result; for example, $\operatorname{Cov}\left(X_{i}, X_{j}\right)=0, i \neq j$, which is true when $X_{1}, \ldots, X_{n}$ are independent.

---

**reference**

- Hoggs Introduction to Mathematical Statistics 7ed
- <https://people.math.gatech.edu/~ecroot/3225/rho_notes.pdf>





