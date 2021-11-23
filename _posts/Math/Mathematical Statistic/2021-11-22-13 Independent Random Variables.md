---
title:  "Independent Random Variable"
excerpt: "통계적 독립"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-22

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
---

 독립독립
{: .notice--warning}

# [Independent Random Variable](#link){: .btn .btn--primary}{: .align-center}

> ## Independent Random Variables

> Intuition

- $X_1$ 과 $X_2$ 가 Random Variable 을 나타낸다고 합시다. 
  - 그러면 우리는 두 관계가 '독립' 이라는것을 어떻게 나타낼 수 있을까요? 

$$f_{2}\left(x_{2}\right)=f_{2 \mid 1}\left(x_{2} \mid x_{1}\right) \quad and \quad f\left(x_{1}, x_{2}\right)=f_{1}\left(x_{1}\right) f_{2}\left(x_{2}\right)$$

- 위처럼 각각의 variable 들이 서로가에게 어떤 값을 가지던지 간에 같은 값을 가진다면 독립이라고 할 수 있을것입니다. 
  - 위를 다시 표현한다면 아래와 같습니다.

 $$f\left(x_{1}, x_{2}\right)= f_{1}\left(x_{1}\right) f_{2}\left(x_{2}\right)$$

> Definition 

(Independence). Let the random variables $X_{1}$ and $X_{2}$ have the joint pdf $f\left(x_{1}, x_{2}\right)$ [joint pmf $\left.p\left(x_{1}, x_{2}\right)\right]$ and the marginal pdfs [pmfs] $f_{1}\left(x_{1}\right)\left[p_{1}\left(x_{1}\right)\right]$ and $f_{2}\left(x_{2}\right)\left[p_{2}\left(x_{2}\right)\right]$, respectively. The random variables $X_{1}$ and $X_{2}$ are said to be independent if, and only if, $f\left(x_{1}, x_{2}\right) \equiv f_{1}\left(x_{1}\right) f_{2}\left(x_{2}\right)\left[p\left(x_{1}, x_{2}\right) \equiv p_{1}\left(x_{1}\right) p_{2}\left(x_{2}\right)\right]$. Random variables that are not independent are said to be dependent.

> ## Example

Let the joint pdf of $X_{1}$ and $X_{2}$ be

$$f\left(x_{1}, x_{2}\right)= \begin{cases}x_{1}+x_{2} & 0<x_{1}<1, \quad 0<x_{2}<1 \\ 0 & \text { elsewhere }\end{cases}$$

show that $X_{1}$ and $X_{2}$ are dependent. 

> Answer

Here the marginal probability density functions are

$$f_{1}\left(x_{1}\right)= \begin{cases}\int_{-\infty}^{\infty} f\left(x_{1}, x_{2}\right) d x_{2}=\int_{0}^{1}\left(x_{1}+x_{2}\right) d x_{2}=x_{1}+\frac{1}{2} & 0<x_{1}<1 \\ 0 & \text { elsewhere }\end{cases}$$

and

$$f_{2}\left(x_{2}\right)= \begin{cases}\int_{-\infty}^{\infty} f\left(x_{1}, x_{2}\right) d x_{1}=\int_{0}^{1}\left(x_{1}+x_{2}\right) d x_{1}=\frac{1}{2}+x_{2} & 0<x_{2}<1 \\ 0 & \text { elsewhere }\end{cases}$$

Since $f\left(x_{1}, x_{2}\right) \not \equiv f_{1}\left(x_{1}\right) f_{2}\left(x_{2}\right)$, the random variables $X_{1}$ and $X_{2}$ are dependent.

> ## $$f\left(x_{1}, x_{2}\right) \equiv g\left(x_{1}\right) h\left(x_{2}\right)$$ $\leftrightarrow$ $\bot$

Let the random variables $X_{1}$ and $X_{2}$ have supports $\mathcal{S}_{1}$ and $\mathcal{S}_{2}$, respectively, and have the joint pdf $f\left(x_{1}, x_{2}\right) .$ Then $X_{1}$ and $X_{2}$ are independent if and only if $f\left(x_{1}, x_{2}\right)$ can be written as a product of a nonnegative function of $x_{1}$ and a nonnegative function of $x_{2}$. That is,

$$f\left(x_{1}, x_{2}\right) \equiv g\left(x_{1}\right) h\left(x_{2}\right)$$

where $g\left(x_{1}\right)>0, x_{1} \in \mathcal{S}_{1}$, zero elsewhere, and $h\left(x_{2}\right)>0, x_{2} \in \mathcal{S}_{2}$, zero elsewhere.

> Proof $$f\left(x_{1}, x_{2}\right) \equiv g\left(x_{1}\right) h\left(x_{2}\right)$$ $\leftarrow$ $\bot$

If $X_{1}$ and $X_{2}$ are independent, then $f\left(x_{1}, x_{2}\right) \equiv f_{1}\left(x_{1}\right) f_{2}\left(x_{2}\right)$, where $f_{1}\left(x_{1}\right)$ and $f_{2}\left(x_{2}\right)$ are the marginal probability density functions of $X_{1}$ and $X_{2}$, respectively. Thus the condition $f\left(x_{1}, x_{2}\right) \equiv g\left(x_{1}\right) h\left(x_{2}\right)$ is fulfilled.

> Proof $$f\left(x_{1}, x_{2}\right) \equiv g\left(x_{1}\right) h\left(x_{2}\right)$$ $\to$ $\bot$

if $f\left(x_{1}, x_{2}\right) \equiv g\left(x_{1}\right) h\left(x_{2}\right)$, then, for random variables of the continuous type, we have

$$f_{1}\left(x_{1}\right)=\int_{-\infty}^{\infty} g\left(x_{1}\right) h\left(x_{2}\right) d x_{2}=g\left(x_{1}\right) \int_{-\infty}^{\infty} h\left(x_{2}\right) d x_{2}=c_{1} g\left(x_{1}\right)$$

and

$$f_{2}\left(x_{2}\right)=\int_{-\infty}^{\infty} g\left(x_{1}\right) h\left(x_{2}\right) d x_{1}=h\left(x_{2}\right) \int_{-\infty}^{\infty} g\left(x_{1}\right) d x_{1}=c_{2} h\left(x_{2}\right)$$

where $c_{1}$ and $c_{2}$ are constants, not functions of $x_{1}$ or $x_{2} .$ Moreover, $c_{1} c_{2}=1$ because

$$1=\int_{-\infty}^{\infty} \int_{-\infty}^{\infty} g\left(x_{1}\right) h\left(x_{2}\right) d x_{1} d x_{2}=\left[\int_{-\infty}^{\infty} g\left(x_{1}\right) d x_{1}\right]\left[\int_{-\infty}^{\infty} h\left(x_{2}\right) d x_{2}\right]=c_{2} c_{1}$$

These results imply that

$$f\left(x_{1}, x_{2}\right) \equiv g\left(x_{1}\right) h\left(x_{2}\right) \equiv c_{1} g\left(x_{1}\right) c_{2} h\left(x_{2}\right) \equiv f_{1}\left(x_{1}\right) f_{2}\left(x_{2}\right)$$

Accordingly, $X_{1}$ and $X_{2}$ are independent.

> ## $F\left(x_{1}, x_{2}\right)=F_{1}\left(x_{1}\right) F_{2}\left(x_{2}\right)$ $\leftrightarrow$ $\bot$

Let $\left(X_{1}, X_{2}\right)$ have the joint cdf $F\left(x_{1}, x_{2}\right)$ and let $X_{1}$ and $X_{2}$ have the marginal cdfs $F_{1}\left(x_{1}\right)$ and $F_{2}\left(x_{2}\right)$, respectively. Then $X_{1}$ and $X_{2}$ are independent if and only if

$$F\left(x_{1}, x_{2}\right)=F_{1}\left(x_{1}\right) F_{2}\left(x_{2}\right) \quad \text { for all }\left(x_{1}, x_{2}\right) \in R^{2}$$

> Proof $F\left(x_{1}, x_{2}\right)=F_{1}\left(x_{1}\right) F_{2}\left(x_{2}\right)$ $\to$ $\bot$

the mixed second partial is (by Definition)

$$\frac{\partial^{2}}{\partial x_{1} \partial x_{2}} F\left(x_{1}, x_{2}\right)=f_{1}\left(x_{1}\right) f_{2}\left(x_{2}\right)$$

> Proof $F\left(x_{1}, x_{2}\right)=F_{1}\left(x_{1}\right) F_{2}\left(x_{2}\right)$ $\leftarrow$ $\bot$

suppose $X_{1}$ and $X_{2}$ are independent. Then by the definition of the joint cdf,

$$\begin{aligned}
F\left(x_{1}, x_{2}\right) &=\int_{-\infty}^{x_{1}} \int_{-\infty}^{x_{2}} f_{1}\left(w_{1}\right) f_{2}\left(w_{2}\right) d w_{2} d w_{1} \\
&=\int_{-\infty}^{x_{1}} f_{1}\left(w_{1}\right) d w_{1} \cdot \int_{-\infty}^{x_{2}} f_{2}\left(w_{2}\right) d w_{2}=F_{1}\left(x_{1}\right) F_{2}\left(x_{2}\right)
\end{aligned}$$

> ## Theorem

> Theorem

The random variables $X_{1}$ and $X_{2}$ are independent random variables if and only if the following condition holds,

$$P\left(a<X_{1} \leq b, c<X_{2} \leq d\right)=P\left(a<X_{1} \leq b\right) P\left(c<X_{2} \leq d\right)$$

for every $a<b$ and $c<d$, where $a, b, c$, and $d$ are constants.

> Proof $\to$

If $X_{1}$ and $X_{2}$ are independent, then

$$\begin{aligned}
P\left(a<X_{1} \leq b, c<X_{2} \leq d\right)=& F(b, d)-F(a, d)-F(b, c)+F(a, c) \\
=& F_{1}(b) F_{2}(d)-F_{1}(a) F_{2}(d)-F_{1}(b) F_{2}(c) \\
&+F_{1}(a) F_{2}(c) \\
=&\left[F_{1}(b)-F_{1}(a)\right]\left[F_{2}(d)-F_{2}(c)\right]
\end{aligned}$$

which is the right side of expression

> Proof $\leftarrow$

condition implies that the joint cdf of $\left(X_{1}, X_{2}\right)$ factors into a product of the marginal cdfs, which in turn by Previous Thm and this implies that $X_{1}$ and $X_{2}$ are independent.

> ## Theorem : indpendent and Expectation

> Theorem

Suppose $X_{1}$ and $X_{2}$ are independent and that $E\left(u\left(X_{1}\right)\right)$ and $E\left(v\left(X_{2}\right)\right)$ exist. Then

$$E\left[u\left(X_{1}\right) v\left(X_{2}\right)\right]=E\left[u\left(X_{1}\right)\right] E\left[v\left(X_{2}\right)\right]$$

> Proof

We give the proof in the continuous case. The independence of $X_{1}$ and $X_{2}$ implies that the joint pdf of $X_{1}$ and $X_{2}$ is $f_{1}\left(x_{1}\right) f_{2}\left(x_{2}\right)$. Thus we have, by definition of expectation,

$$\begin{aligned}
E\left[u\left(X_{1}\right) v\left(X_{2}\right)\right] &=\int_{-\infty}^{\infty} \int_{-\infty}^{\infty} u\left(x_{1}\right) v\left(x_{2}\right) f_{1}\left(x_{1}\right) f_{2}\left(x_{2}\right) d x_{1} d x_{2} \\
&=\left[\int_{-\infty}^{\infty} u\left(x_{1}\right) f_{1}\left(x_{1}\right) d x_{1}\right]\left[\int_{-\infty}^{\infty} v\left(x_{2}\right) f_{2}\left(x_{2}\right) d x_{2}\right] \\
&=E\left[u\left(X_{1}\right)\right] E\left[v\left(X_{2}\right)\right]
\end{aligned}$$

> Note 

- 만일 위의 $u(\cdot)$ and $v(\cdot)$ 가 identity function 이라고 한다면, 이는 위의 정리에 의하여 다음과 같은 equality 가 성립합니다.

$$E\left(X_{1} X_{2}\right)=E\left(X_{1}\right) E\left(X_{2}\right)$$

> ## Example

> Problem

Let $X$ and $Y$ be two independent random variables with means $\mu_{1}$ and $\mu_{2}$ and positive variances $\sigma_{1}^{2}$ and $\sigma_{2}^{2}$, respectively. 

show that the independence of $X$ and $Y$ implies that the correlation coefficient of $X$ and $Y$ is zero. 

> Proof

This is true because the covariance of $X$ and $Y$ is equal to

$$E\left[\left(X-\mu_{1}\right)\left(Y-\mu_{2}\right)\right]=E\left(X-\mu_{1}\right) E\left(Y-\mu_{2}\right)=0$$

---

**Reference**

- Hoggs Introduction to Mathematical Statistics 7ed
- <https://people.math.gatech.edu/~ecroot/3225/rho_notes.pdf>





