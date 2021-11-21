---
title:  "Conditional Distribution and Expectation"
excerpt: "조건부 분포와 기댓값"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
---

 두개의 변수로 늘어남에 따라 정의되는 조건부분포
{: .notice--warning}

# [Conditional Distribution](#link){: .btn .btn--primary}{: .align-center}

> ## Conditional Distribution

> Definition

for all $x_{2}$ in the support $\mathcal{S}_{X_{2}}$ of $X_{2}$

$$p_{X_{2} \mid X_{1}}\left(x_{2} \mid x_{1}\right)=\frac{p_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right)}{p_{X_{1}}\left(x_{1}\right)}, \quad x_{2} \in S_{X_{2}} .$$

For any fixed $x_{1}$ with $p_{X_{1}}\left(x_{1}\right)>0$ 

> Note : 

- pdf 를 정의할때에도 똑같이 정의합니다.

$$f_{X_{1} \mid X_{2}}\left(x_{1} \mid x_{2}\right)=\frac{f_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right)}{f_{X_{2}}\left(x_{2}\right)}, \quad f_{X_{2}}\left(x_{2}\right)>0$$

> ## Proporties

> pdf 

$$\begin{aligned}
\int_{-\infty}^{\infty} f_{X_{2} \mid X_{1}}\left(x_{2} \mid x_{1}\right) d x_{2} &=\int_{-\infty}^{\infty} \frac{f_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right)}{f_{X_{1}}\left(x_{1}\right)} d x_{2} \\
&=\frac{1}{f_{X_{1}}\left(x_{1}\right)} \int_{-\infty}^{\infty} f_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right) d x_{2} \\
&=\frac{1}{f_{X_{1}}\left(x_{1}\right)} f_{X_{1}}\left(x_{1}\right)=1
\end{aligned}$$

즉 위처럼 Conditional pdf 는 pdf 의 성질을 만족합니다.

> ## conditional probability

> Definition

the conditional probability that $a<X_{2}<b$, given that $X_{1}=x_{1}$  If there is no ambiguity, this may be written in the form $P\left(a<X_{2}<b \mid x_{1}\right)$. Similarly, the conditional probability that $c<X_{1}<d$, given $X_{2}=x_{2}$, is

$$P\left(c<X_{1}<d \mid X_{2}=x_{2}\right)=\int_{c}^{d} f_{1 \mid 2}\left(x_{1} \mid x_{2}\right) d x_{1}$$

> ## E(X) , V(X)

> $E\left[u\left(X_{2}\right) \mid x_{1}\right]$

If $u\left(X_{2}\right)$ is a function of $X_{2}$, the conditional expectation of $u\left(X_{2}\right)$, given that $X_{1}=$ $x_{1}$, if it exists, is given by

$$E\left[u\left(X_{2}\right) \mid x_{1}\right]=\int_{-\infty}^{\infty} u\left(x_{2}\right) f_{2 \mid 1}\left(x_{2} \mid x_{1}\right) d x_{2}$$

> $\operatorname{Var}\left(X_{2} \mid x_{1}\right)$

$$E\left\{\left[X_{2}-E\left(X_{2} \mid x_{1}\right)\right]^{2} \mid x_{1}\right\}$$ is the variance of the conditional distribution of $X_{2}$, given $X_{1}=x_{1}$, 

> Note

- 물론 위의 Variance 는 아래와 같이 계산될수도 있습니다.

$$\operatorname{Var}\left(X_{2} \mid x_{1}\right)=E\left(X_{2}^{2} \mid x_{1}\right)-\left[E\left(X_{2} \mid x_{1}\right)\right]^{2}$$

> ## Example

> Problem

Let $X_{1}$ and $X_{2}$ have the joint pdf
$$
f\left(x_{1}, x_{2}\right)= \begin{cases}6 x_{2} & 0<x_{2}<x_{1}<1 \\ 0 & \text { elsewhere }\end{cases}
$$
> $f_{1}\left(x_{1}\right)$ ( marginal pdf of $X_{1}$ )

$$f_{1}\left(x_{1}\right)=\int_{0}^{x_{1}} 6 x_{2} d x_{2}=3 x_{1}^{2}, \quad 0<x_{1}<1$$

zero elsewhere. The conditional pdf of $X_{2}$, given $X_{1}=x_{1}$, is

> $f_{2 \mid 1}\left(x_{2} \mid x_{1}\right)$

$$f_{2 \mid 1}\left(x_{2} \mid x_{1}\right)=\frac{6 x_{2}}{3 x_{1}^{2}}=\frac{2 x_{2}}{x_{1}^{2}}, \quad 0<x_{2}<x_{1}$$

zero elsewhere, where $0<x_{1}<1 .$ 

> $E\left(X_{2} \mid x_{1}\right)$

The conditional mean of $X_{2}$, given $X_{1}=x_{1}$, is

$$E\left(X_{2} \mid x_{1}\right)=\int_{0}^{x_{1}} x_{2}\left(\frac{2 x_{2}}{x_{1}^{2}}\right) d x_{2}=\frac{2}{3} x_{1}, \quad 0<x_{1}<1$$

> ## Theorem 

> Theorem

Let $\left(X_{1}, X_{2}\right)$ be a random vector such that the variance of $X_{2}$ is finite. Then,

(a) $E\left[E\left(X_{2} \mid X_{1}\right)\right]=E\left(X_{2}\right)$.

(b) $\operatorname{Var}\left[E\left(X_{2} \mid X_{1}\right)\right] \leq \operatorname{Var}\left(X_{2}\right)$.

> (a) Proof

$$\begin{aligned}
E\left(X_{2}\right) &=\int_{-\infty}^{\infty} \int_{-\infty}^{\infty} x_{2} f\left(x_{1}, x_{2}\right) d x_{2} d x_{1} \\
&=\int_{-\infty}^{\infty}\left[\int_{-\infty}^{\infty} x_{2} \frac{f\left(x_{1}, x_{2}\right)}{f_{1}\left(x_{1}\right)} d x_{2}\right] f_{1}\left(x_{1}\right) d x_{1} \\
&=\int_{-\infty}^{\infty} E\left(X_{2} \mid x_{1}\right) f_{1}\left(x_{1}\right) d x_{1} \\
&=E\left[E\left(X_{2} \mid X_{1}\right)\right]
\end{aligned}$$

> (b) Proof

Consider with $\mu_{2}=E\left(X_{2}\right)$

$$\begin{aligned}
\operatorname{Var}\left(X_{2}\right)=& E\left[\left(X_{2}-\mu_{2}\right)^{2}\right] \\
=& E\left\{\left[X_{2}-E\left(X_{2} \mid X_{1}\right)+E\left(X_{2} \mid X_{1}\right)-\mu_{2}\right]^{2}\right\} \\
=& E\left\{\left[X_{2}-E\left(X_{2} \mid X_{1}\right)\right]^{2}\right\}+E\left\{\left[E\left(X_{2} \mid X_{1}\right)-\mu_{2}\right]^{2}\right\} \\
&+2 E\left\{\left[X_{2}-E\left(X_{2} \mid X_{1}\right)\right]\left[E\left(X_{2} \mid X_{1}\right)-\mu_{2}\right]\right\}
\end{aligned}$$

We show that the last term of the right-hand member of the immediately preceding equation is zero. It is equal to

$$\begin{array}{r}
2 \int_{-\infty}^{\infty} \int_{-\infty}^{\infty}\left[x_{2}-E\left(X_{2} \mid x_{1}\right)\right]\left[E\left(X_{2} \mid x_{1}\right)-\mu_{2}\right] f\left(x_{1}, x_{2}\right) d x_{2} d x_{1} \\
=2 \int_{-\infty}^{\infty}\left[E\left(X_{2} \mid x_{1}\right)-\mu_{2}\right]\left\{\int_{-\infty}^{\infty}\left[x_{2}-E\left(X_{2} \mid x_{1}\right)\right] \frac{f\left(x_{1}, x_{2}\right)}{f_{1}\left(x_{1}\right)} d x_{2}\right\} f_{1}\left(x_{1}\right) d x_{1}
\end{array}$$

But $E\left(X_{2} \mid x_{1}\right)$ is the conditional mean of $X_{2}$, given $X_{1}=x_{1} .$ Since the expression in the inner braces is equal to

$$E\left(X_{2} \mid x_{1}\right)-E\left(X_{2} \mid x_{1}\right)=0$$

the double integral is equal to zero. Accordingly, we have

$$\operatorname{Var}\left(X_{2}\right)=E\left\{\left[X_{2}-E\left(X_{2} \mid X_{1}\right)\right]^{2}\right\}+E\left\{\left[E\left(X_{2} \mid X_{1}\right)-\mu_{2}\right]^{2}\right\}$$

The first term in the right-hand member of this equation is nonnegative because it is the expected value of a nonnegative function, namely $\left[X_{2}-E\left(X_{2} \mid X_{1}\right)\right]^{2}$. Since $E\left[E\left(X_{2} \mid X_{1}\right)\right]=\mu_{2}$, the second term is $\operatorname{Var}\left[E\left(X_{2} \mid X_{1}\right)\right]$. Hence we have

$$\operatorname{Var}\left(X_{2}\right) \geq \operatorname{Var}\left[E\left(X_{2} \mid X_{1}\right)\right]$$

which completes the proof.

> intuition

- $X_2$ 의 평균을 알고싶다고 합니다. 이때에 $X_2$ 와 $E(X_2 \mid X_1)$ 모두 평균이 $\mu_2$ 이므로 우리는 두개중 어떤것을 사용해도 Unbiased estimator 를 얻을 수 있을것입니다. 
- 그리고 $$\operatorname{Var}\left(X_{2}\right) \geq \operatorname{Var}\left[E\left(X_{2} \mid X_{1}\right)\right]$$ 에 의하여, 우리는 $$E\left(X_{2} \mid X_{1}\right)$$ 의 추정이 좀 더 안정적인 추정을 제공한다는것을 알 수 있습니다.
- 즉 정리하면 guess. R.V. $\left(X_{1}, X_{2}\right)$ 에 대하여 $\left(x_{1}, x_{2}\right)$ 을 관측한다고 할때 우리는  unknown $\mu_{2}$. 를 추정할때 $E\left(X_{2} \mid x_{1}\right)$ 를 더 선호한다는 것입니다.

---

**--Reference--**

- Hoggs Introduction to Mathematical Statistics 7ed



