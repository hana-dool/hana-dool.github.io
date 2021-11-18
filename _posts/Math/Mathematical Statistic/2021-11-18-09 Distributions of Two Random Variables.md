---
title:  "Distributions of Two Random Variables"
excerpt: "2개 변수에 대한 R.V."
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-18

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
---

 두개의 R.V. 에 대해서 Distribution 을 알아보도록 하겠습니다.
{: .notice--warning}

# [Probability](#link){: .btn .btn--primary}{: .align-center}

> ## Definition : Radom Vector (2 element)

> Definition

Given a random experiment with a sample space $\mathcal{C}$, consider two random variables $X_{1}$ and $X_{2}$, which assign to each element $c$ of $\mathcal{C}$ one and only one ordered pair of numbers $X_{1}(c)=x_{1}, X_{2}(c)=x_{2}$. Then we say that $\left(X_{1}, X_{2}\right)$ is a random vector. The space of $\left(X_{1}, X_{2}\right)$ is the set of ordered pairs $$\mathcal{D}=\left\{\left(x_{1}, x_{2}\right): x_{1}=X_{1}(c), x_{2}=X_{2}(c), c \in \mathcal{C}\right\}$$

> Remark

- 이전과는 다르게 벡터에 대해서 논해야되므로, 먼저 다양한 Notation 에 대해 언급해보고자 합니다.
- $\mathbf{X}=\left(X_{1}, X_{2}\right)^{\prime}$ :  $\left(X_{1}, X_{2}\right)$ 를 Transpose 한 Column Vector
-  $\mathcal{D}$ 를 $\left(X_{1}, X_{2}\right)$ 랜덤 벡터의 공간이라고 하고, $A$ 를 $\mathcal{D}$ 의 Subset 이라 합시다. 이때 Event $A$ 에 대한 확률은 $P_{X_{1}, X_{2}}[A]$ 로 표기합니다.

> ## Definition : joint probability

> Definition : joint cdf 

cumulative distribution function (cdf), which is given by

$$F_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right)=P\left[\left\{X_{1} \leq x_{1}\right\} \cap\left\{X_{2} \leq x_{2}\right\}\right]$$

for all $\left(x_{1}, x_{2}\right) \in R^{2}$.

> Definition : joint Probability mass function 

$$p_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right)=P\left[X_{1}=x_{1}, X_{2}=x_{2}\right]$$

for all $\left(x_{1}, x_{2}\right) \in \mathcal{D}$. As with random variables, the pmf uniquely defines the cdf.

For an event $B \in \mathcal{D}$, we have

$$P\left[\left(X_{1}, X_{2}\right) \in B\right]=\sum \sum_{B} p_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right)$$

> Definition : Joint Probability density function 

We say a random vector $\left(X_{1}, X_{2}\right)$ with space $\mathcal{D}$ is of the continuous type if its cdf $F_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right)$ is continuous. For the most part, the continuous random vectors in this book have cdfs which can be represented as integrals of nonnegative functions. That is, $F_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right)$ can be expressed as

$$F_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right)=\int_{-\infty}^{x_{1}} \int_{-\infty}^{x_{2}} f_{X_{1}, X_{2}}\left(w_{1}, w_{2}\right) d w_{1} d w_{2}$$

for all $\left(x_{1}, x_{2}\right) \in R^{2} .$ We call the integrand the joint probability density function (pdf) of $\left(X_{1}, X_{2}\right)$. Then

$$\frac{\partial^{2} F_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right)}{\partial x_{1} \partial x_{2}}=f_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right)$$

For an event $A \in \mathcal{D}$, we have

$$P\left[\left(X_{1}, X_{2}\right) \in A\right]=\iint_{A} f_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right) d x_{1} d x_{2}$$

> ## Eample : Probability

> Example

$$f\left(x_{1}, x_{2}\right)= \begin{cases}6 x_{1}^{2} x_{2} & 0<x_{1}<1,0<x_{2}<1 \\ 0 & \text { elsewhere }\end{cases}$$

be the pdf of two random variables $X_{1}$ and $X_{2}$ of the continuous type. We have, for instance,

$$\begin{aligned}
P\left(0<X_{1}<\frac{3}{4}, \frac{1}{3}<X_{2}<2\right) &=\int_{1 / 3}^{2} \int_{0}^{3 / 4} f\left(x_{1}, x_{2}\right) d x_{1} d x_{2} \\
&=\int_{1 / 3}^{1} \int_{0}^{3 / 4} 6 x_{1}^{2} x_{2} d x_{1} d x_{2}+\int_{1}^{2} \int_{0}^{3 / 4} 0 d x_{1} d x_{2} \\
&=\frac{3}{8}+0=\frac{3}{8}
\end{aligned}$$

> ## Definition : marginal 

> Definition : marginal 

Let $\left(X_{1}, X_{2}\right)$ be a random vector. Then both $X_{1}$ and $X_{2}$ are random variables. We can obtain their distributions in terms of the joint distribution of $\left(X_{1}, X_{2}\right)$ as follows. Recall that the event which defined the cdf of $X_{1}$ at $x_{1}$ is $$\left\{X_{1} \leq x_{1}\right\}$$. However,

$$\left\{X_{1} \leq x_{1}\right\}=\left\{X_{1} \leq x_{1}\right\} \cap\left\{-\infty<X_{2}<\infty\right\}=\left\{X_{1} \leq x_{1},-\infty<X_{2}<\infty\right\}$$

Taking probabilities, we have

$$F_{X_{1}}\left(x_{1}\right)=P\left[X_{1} \leq x_{1},-\infty<X_{2}<\infty\right]$$

for all $x_{1} \in R$. By Theorem 1.3.6 we can write this equation as $F_{X_{1}}\left(x_{1}\right)=$ $$\lim _{x_{2} \uparrow \infty} F\left(x_{1}, x_{2}\right)$$ Thus we have a relationship between the cdfs, which we can extend to either the pmf or pdf depending on whether $\left(X_{1}, X_{2}\right)$ is discrete or continuous.

> Definition : Discrete marginal pmf

By the uniqueness of cdfs, the quantity in braces must be the pmf of $X_{1}$ evaluated at $w_{1}$; that is,

$$p_{X_{1}}\left(x_{1}\right)=\sum_{x_{2}<\infty} p_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right)$$

for all $$x_{1} \in \mathcal{D}_{X_{1}}$$

> Definition : Continuous marginal pdf

First consider the discrete case. Let $$\mathcal{D}_{X_{1}}$$ be the support of $X_{1}$. For $x_{1} \in \mathcal{D}_{X_{1}}$, Equation (2.1.7) is equivalent to

$$F_{X_{1}}\left(x_{1}\right)=\sum_{w_{1} \leq x_{1},-\infty<x_{2}<\infty} p_{X_{1}, X_{2}}\left(w_{1}, x_{2}\right)=\sum_{w_{1} \leq x_{1}}\left\{\sum_{x_{2}<\infty} p_{X_{1}, X_{2}}\left(w_{1}, x_{2}\right)\right\}$$

We next consider the continuous case. Let $$\mathcal{D}_{X_{1}}$$ be the support of $X_{1}$. For $x_{1} \in \mathcal{D}_{X_{1}}$, Equation (2.1.7) is equivalent to

$$F_{X_{1}}\left(x_{1}\right)=\int_{-\infty}^{x_{1}} \int_{-\infty}^{\infty} f_{X_{1}, X_{2}}\left(w_{1}, x_{2}\right) d x_{2} d w_{1}=\int_{-\infty}^{x_{1}}\left\{\int_{-\infty}^{\infty} f_{X_{1}, X_{2}}\left(w_{1}, x_{2}\right) d x_{2}\right\} d w_{1}$$

By the uniqueness of cdfs, the quantity in braces must be the pdf of $X_{1}$, evaluated at $w_{1}$; that is,

$$f_{X_{1}}\left(x_{1}\right)=\int_{-\infty}^{\infty} f_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right) d x_{2}$$

for all $$x_{1} \in \mathcal{D}_{X_{1}}$$. Hence, in the continuous case the marginal pdf of $X_{1}$ is found by integrating out $x_{2}$. Similarly, the marginal pdf of $X_{2}$ is found by integrating out $x_{1} .$

> ## Example : marginal probability

> Example

Let $X_{1}$ and $X_{2}$ have the joint pdf

$$f\left(x_{1}, x_{2}\right)= \begin{cases}x_{1}+x_{2} & 0<x_{1}<1, \quad 0<x_{2}<1 \\ 0 & \text { elsewhere }\end{cases}$$

> The marginal pdf of $X_{1}$ 

$$f_{1}\left(x_{1}\right)=\int_{0}^{1}\left(x_{1}+x_{2}\right) d x_{2}=x_{1}+\frac{1}{2}, \quad 0<x_{1}<1$$

zero elsewhere

> marginal pdf of $X_{2}$ 

$$f_{2}\left(x_{2}\right)=\int_{0}^{1}\left(x_{1}+x_{2}\right) d x_{1}=\frac{1}{2}+x_{2}, \quad 0<x_{2}<1$$

zero elsewhere. 

> A probability $P\left(X_{1} \leq \frac{1}{2}\right)$ 

can be computed from either $f_{1}\left(x_{1}\right)$ or $f\left(x_{1}, x_{2}\right)$ because

$$\int_{0}^{1 / 2} \int_{0}^{1} f\left(x_{1}, x_{2}\right) d x_{2} d x_{1}=\int_{0}^{1 / 2} f_{1}\left(x_{1}\right) d x_{1}=\frac{3}{8}$$

> probability $P\left(X_{1}+X_{2} \leq 1\right)$, 

$$\begin{aligned}
\int_{0}^{1} \int_{0}^{1-x_{1}}\left(x_{1}+x_{2}\right) d x_{2} d x_{1} &=\int_{0}^{1}\left[x_{1}\left(1-x_{1}\right)+\frac{\left(1-x_{1}\right)^{2}}{2}\right] d x_{1} \\
&=\int_{0}^{1}\left(\frac{1}{2}-\frac{1}{2} x_{1}^{2}\right) d x_{1}=\frac{1}{3}
\end{aligned}$$

# [Expectation](#link){: .btn .btn--primary}{: .align-center}

> ## Definition : Expectation

> Definition : Continuous Expectation

Suppose $\left(X_{1}, X_{2}\right)$ is of the continuous type. Then $E(Y)$ exists if

$$\int_{-\infty}^{\infty} \int_{-\infty}^{\infty}\left|g\left(x_{1}, x_{2}\right)\right| f_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right) d x_{1} d x_{2}<\infty$$

Then

$$E(Y)=\int_{-\infty}^{\infty} \int_{-\infty}^{\infty} g\left(x_{1}, x_{2}\right) f_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right) d x_{1} d x_{2}$$

> Definition : Discrete Expectation

Likewise if $\left(X_{1}, X_{2}\right)$ is discrete, then $E(Y)$ exists if

$$\sum_{x_{1}} \sum_{x_{2}}\left|g\left(x_{1}, x_{2}\right)\right| p_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right)<\infty$$

Then

$$E(Y)=\sum_{x_{1}} \sum_{x_{2}} g\left(x_{1}, x_{2}\right) p_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right)$$

> ## Theorem : Linear property

> Theorem

Let $\left(X_{1}, X_{2}\right)$ be a random vector. Let $Y_{1}=g_{1}\left(X_{1}, X_{2}\right)$ and $Y_{2}=g_{2}\left(X_{1}, X_{2}\right)$ be random variables whose expectations exist. Then for all real numbers $k_{1}$ and $k_{2}$,

$$E\left(k_{1} Y_{1}+k_{2} Y_{2}\right)=k_{1} E\left(Y_{1}\right)+k_{2} E\left(Y_{2}\right)$$

> Proof : Existence

We prove it for the continuous case. The existence of the expected value of $k_{1} Y_{1}+k_{2} Y_{2}$ follows directly from the triangle inequality and linearity of integrals; i.e.,

$$\begin{aligned}
&\int_{-\infty}^{\infty} \int_{-\infty}^{\infty}\left|k_{1} g_{1}\left(x_{1}, x_{2}\right)+k_{2} g_{1}\left(x_{1}, x_{2}\right)\right| f_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right) d x_{1} d x_{2} \\
&\leq\left|k_{1}\right| \int_{-\infty}^{\infty} \int_{-\infty}^{\infty}\left|g_{1}\left(x_{1}, x_{2}\right)\right| f_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right) d x_{1} d x_{2} \\
&\quad+\left|k_{2}\right| \int_{-\infty}^{\infty} \int_{-\infty}^{\infty}\left|g_{2}\left(x_{1}, x_{2}\right)\right| f_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right) d x_{1} d x_{2}<\infty
\end{aligned}$$

> Proof : Linearity

$$\begin{aligned} E\left(k_{1} Y_{1}+k_{2} Y_{2}\right)=& \int_{-\infty}^{\infty} \int_{-\infty}^{\infty}\left[k_{1} g_{1}\left(x_{1}, x_{2}\right)+k_{2} g_{2}\left(x_{1}, x_{2}\right)\right] f_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right) d x_{1} d x_{2} \\=& k_{1} \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} g_{1}\left(x_{1}, x_{2}\right) f_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right) d x_{1} d x_{2} \\ &+k_{2} \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} g_{2}\left(x_{1}, x_{2}\right) f_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right) d x_{1} d x_{2} \\=& k_{1} E\left(Y_{1}\right)+k_{2} E\left(Y_{2}\right) \end{aligned}$$

> Corollary

We also note that the expected value of any function $g\left(X_{2}\right)$ of $X_{2}$ can be found in two ways:

$$E\left(g\left(X_{2}\right)\right)=\int_{-\infty}^{\infty} \int_{-\infty}^{\infty} g\left(x_{2}\right) f\left(x_{1}, x_{2}\right) d x_{1} d x_{2}=\int_{-\infty}^{\infty} g\left(x_{2}\right) f_{X_{2}}\left(x_{2}\right) d x_{2}$$

the latter single integral being obtained from the double integral by integrating on $x_{1}$ first. 

> ## Example 

> Example

Example 2.1.5. Let $X_{1}$ and $X_{2}$ have the pdf
$$
f\left(x_{1}, x_{2}\right)= \begin{cases}8 x_{1} x_{2} & 0<x_{1}<x_{2}<1 \\ 0 & \text { elsewhere }\end{cases}
$$
Then
$$
\begin{aligned}
E\left(X_{1} X_{2}^{2}\right) &=\int_{-\infty}^{\infty} \int_{-\infty}^{\infty} x_{1} x_{2}^{2} f\left(x_{1}, x_{2}\right) d x_{1} d x_{2} \\
&=\int_{0}^{1} \int_{0}^{x_{2}} 8 x_{1}^{2} x_{2}^{3} d x_{1} d x_{2} \\
&=\int_{0}^{1} \frac{8}{3} x_{2}^{6} d x_{2}=\frac{8}{21}
\end{aligned}
$$
In addition,
$$
E\left(X_{2}\right)=\int_{0}^{1} \int_{0}^{x_{2}} x_{2}\left(8 x_{1} x_{2}\right) d x_{1} d x_{2}=\frac{4}{5}
$$
Since $X_{2}$ has the $\operatorname{pdf} f_{2}\left(x_{2}\right)=4 x_{2}^{3}, 0<x_{2}<1$, zero elsewhere, the latter expectation can be found by
$$
E\left(X_{2}\right)=\int_{0}^{1} x_{2}\left(4 x_{2}^{3}\right) d x_{2}=\frac{4}{5}
$$
Thus
$$
\begin{aligned}
E\left(7 X_{1} X_{2}^{2}+5 X_{2}\right) &=7 E\left(X_{1} X_{2}^{2}\right)+5 E\left(X_{2}\right) \\
&=(7)\left(\frac{8}{21}\right)+(5)\left(\frac{4}{5}\right)=\frac{20}{3}
\end{aligned}
$$
suppose the random variable $Y$ is defined by $Y=X_{1} / X_{2} .$ We determine $E(Y)$ in two ways. The first way is by definition; i.e., find the distribution of $Y$ and then determine its expectation. The cdf of $Y$, for $0<y \leq 1$, is
$$
\begin{aligned}
F_{Y}(y) &=P(Y \leq y)=P\left(X_{1} \leq y X_{2}\right)=\int_{0}^{1} \int_{0}^{y x_{2}} 8 x_{1} x_{2} d x_{1} d x_{2} \\
&=\int_{0}^{1} 4 y^{2} x_{2}^{3} d x_{2}=y^{2}
\end{aligned}
$$
Hence, the pdf of $Y$ is
$$
f_{Y}(y)=F_{Y}^{\prime}(y)= \begin{cases}2 y & 0<y<1 \\ 0 & \text { elsewhere }\end{cases}
$$
which leads to
$$
E(Y)=\int_{0}^{1} y(2 y) d y=\frac{2}{3}
$$
For the second way, we make use of expression $(2.1 .10)$ and find $E(Y)$ directly by
$$
\begin{aligned}
E(Y) &=E\left(\frac{X_{1}}{X_{2}}\right)=\int_{0}^{1}\left\{\int_{0}^{x_{2}}\left(\frac{x_{1}}{x_{2}}\right) 8 x_{1} x_{2} d x_{1}\right\} d x_{2} \\
&=\int_{0}^{1} \frac{8}{3} x_{2}^{3} d x_{2}=\frac{2}{3}
\end{aligned}
$$
We next define the moment generating function of a random vector.

---

**Reference**

- Hoggs Introduction to Mathematical Statistics 7ed



