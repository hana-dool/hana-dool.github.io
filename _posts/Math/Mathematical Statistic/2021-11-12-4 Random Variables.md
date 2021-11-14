---
title:  "Random Variable"
excerpt: "확률 변수에 대해서 알아보기"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-12
toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 제일 기초가 되는 기댓값 , 분산 등에 대한 정리를 알아봅시다. 
{: .notice--warning}

# [Random Variable](#link){: .btn .btn--primary}{: .align-center}

> ## Definition

> Definition

Consider a random experiment with a sample space $\mathcal{C}$. A function $X$, which assigns to each element $c \in \mathcal{C}$ one and only one number $X(c)=x$, is called $a$ random variable. The space or range of $X$ is the set of real numbers $\mathcal{D}=\{x: x=X(c), c \in \mathcal{C}\}$

> Note

- 위에서 $D$ 의 수에 따라서 Continuous 와 Discrete 이 달라집니다.
  - $D$ 가 Uncountable (Real 등) 이라면 Continuous R.V.
  - $D$ 가 Countable 이라면 Discrete Random Variables
-  $D$ 는 우리가 sample 에 대해서 관심있어 하는 부분입니다. (앞면의 수 라던지 ..) 
  - 이렇게 $D$ 를 정하고 나면, $X$ 에 대해서 Probability 를 정의할 수 있습니다. 이를 우리는 Distribution 이라고 합니다.

# [Discrete Random Variable](#link){: .btn .btn--primary}{: .align-center}

> ## Definition

> Definition

Suppose $X$ is a discrete random variable with a finite space $\mathcal{D}=\left\{d_{1}, \ldots, d_{m}\right\} .$ Define the function $p_{X}\left(d_{i}\right)$ on $\mathcal{D}$ by

$$p_{X}\left(d_{i}\right)=P\left(\left\{c: X(c)=d_{i}, c \in \Omega\right\}\right)$$

for $i=1, \ldots, m$, where $p_{X}\left(d_{i}\right)$ is called the probability mass function (pmf) of $X .$ In short, the pmf of $X$ is typically given by

$$p_{X}\left(d_{i}\right)=P\left(X=d_{i}\right)$$

> Note

- 즉 위처럼 Fitinite 한 space 인 $D$ 에 대하여 Probability 를 정의하게 되면 pdf 가 됩니다.

> ##  CDF

> Definition

Definition. Let $X$ be a random variable. Then its cumulative distribution function (cdf) is defined by

$$F_{X}(x)=p_{X}((-\infty, x])=P(X \leq x)$$

which is formally written as

$$P(X \leq x)=P(\{c: X(c) \leq x, c \in \Omega\})$$

> ## Properties

> Properties

Let $X$ be a random variable with cdf $F_{X}(x)$. Then,

- (a) If $a<b$, then $F_{X}(a) \leq F_{X}(b) .$ That is, $F_{X}(x)$ is a nondecreasing function.
- (b) $\lim _{x \rightarrow-\infty} F_{X}(x)=0 .$ That is, the lower limit of $F_{X}(x)$ is 0 .
- (c) $\lim _{x \rightarrow \infty} F_{X}(x)=1$. That is, the upper limit of $F_{X}(x)$ is 1 .
- (d) $\lim _{x \rightarrow x_{0}+} F_{X}(x)=F_{X}\left(x_{0}\right)$. That is, $F_{X}(x)$ is right continuous.
- (e) If $a<b$, then

$$P(a<X \leq b)=F_{X}(b)-F_{X}(a)$$

- (f) For all $x \in \Re$, we have

$$P(X=x)=F_{X}(x)-F_{X}(x-)$$

where $F_{X}(x-)=\lim _{z \rightarrow x-} F_{X}(z)$

# [Continuous Random Variable](#link){: .btn .btn--primary}{: .align-center}

> ## Definition

> Definitions

A random variable is said to be a continuous random variable if its cumulative distribution function $F_{X}(x)$ is a continuous function for all $x \in \Re$.

> Note

- 즉, 이전에 Discrete R.V. 를 정의할떄에는 $D$ 의 Cardinality 로 정의했지만, 이 경우에는 CDF 가 Conti 인지 아닌지로 정의하게 됩니다.

> ## Properties : pdf and cdf

> Property 

For a continuous random variable $X$, there are no points of discrete mass, i.e.,

$$P(X=x)=0 \text { for all } x \in \Re$$

Thus, the cdf of $X$ is expressed as

$$F_{X}(x)=\int_{-\infty}^{x} f_{X}(z) d z$$

where $f_{X}(z)$ is called a probability density function (pdf) of $X .$ Then the Fundamental Theorem of Calculus implies that

$$\frac{d}{d x} F_{X}(x)=f_{X}(x)$$

> Note 

- 이때, Contnuous Variable 은 각 point 에 대해서 mass 가 존재하지 않습니다. 
  - 그러므로 우리는 CDF 를 통하여 확률을 정의합니다.

> ## Properties : probability and pdf

> Property

The probabilities of a continuous random variable $X$ can be obtained by

$$P(a<X \leq b)=F_{X}(b)-F_{X}(a)=\int_{a}^{b} f_{X}(z) d z$$

and we have $f_{X}(x)>0$ and $\int_{-\infty}^{\infty} f_{X}(x) d x=1$.

> Note

- 그리고 위처럼 특정 구간의 값을 cdf 를 이용하여 구할 수 있습니다. 
- Conti 의 경우 확률은 특정 구간의 적분을 통해서 계산됩니다.

---

**Reference**

- Hogg introdusction to Mathematical Statistics 7ed



