---
title:  "Extension to Several Random Variables"
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

 여러 변수들에 대한 확장
{: .notice--warning}

# [Extension to Several Random Variables](#link){: .btn .btn--primary}{: .align-center}

> ## Random Vector and Space

> Definition : Random Vector

Consider a random experiment with the sample space $\mathcal{C}$. Let the random variable $X_{i}$ assign to each element $c \in \mathcal{C}$ one and only one real number $X_{i}(c)=x_{i}, i=1,2, \ldots, n$. We say that $\left(X_{1}, \ldots, X_{n}\right)$ is an $n$-dimensional random vector.

> Definition : Space

The space of this random vector is the set of ordered $n$-tuples $\mathcal{D}=\left\{\left(x_{1}, x_{2}, \ldots, x_{n}\right): x_{1}=X_{1}(c), \ldots, x_{n}=X_{n}(c), c \in \mathcal{C}\right\}$

>  Definition : Probability. 

Furthermore, let $A$ be a subset of the space $\mathcal{D}$. Then $P\left[\left(X_{1}, \ldots, X_{n}\right) \in A\right]=P(C)$, where $C=\{c: c \in$ $\mathcal{C}$ and $\left.\left(X_{1}(c), X_{2}(c), \ldots, X_{n}(c)\right) \in A\right\} .$

> ## Joint CDF and pdf

> definition : Joint cdf

The joint cdf is defined to be

$$F_{\mathbf{X}}(\mathbf{x})=P\left[X_{1} \leq x_{1}, \ldots, X_{n} \leq x_{n}\right]$$

- Discrete Type

$$F_{\mathbf{X}}(\mathbf{x})=\sum_{w_{1} \leq x_{1}, \ldots, w_{n} \leq x_{n}} \sum p\left(w_{1}, \ldots, w_{n}\right)$$

- Continuous Type

$$F_{\mathbf{X}}(\mathbf{x})=\int_{-\infty}^{x_{1}} \int_{-\infty}^{x_{2}} \cdots \int_{-\infty}^{x_{n}} f\left(w_{1}, \ldots, w_{n}\right) d w_{n} \cdots d w_{1}$$

> Definition : joint Pdf

Discrete Case 의 경우는 pmf 가 쉽게 정의되므로 pdf 만 보도록 합시다.

$$\frac{\partial^{n}}{\partial x_{1} \cdots \partial x_{n}} F_{\mathbf{X}}(\mathbf{x})=f(\mathbf{x})$$

> ## Expectation

Let $\left(X_{1}, X_{2}, \ldots, X_{n}\right)$ be a random vector and let $Y=u\left(X_{1}, X_{2}, \ldots, X_{n}\right)$ for some function $u$. As in the bivariate case, the expected value of the random variable exists if the $n$-fold integral

> Definition : Continuous Case

if the $n$-fold integral exist

$$\int_{-\infty}^{\infty} \cdots \int_{-\infty}^{\infty}\left|u\left(x_{1}, x_{2}, \ldots, x_{n}\right)\right| f\left(x_{1}, x_{2}, \ldots, x_{n}\right) d x_{1} d x_{2} \cdots d x_{n}$$

then its expectation is given by 

$$E(Y)=\int_{-\infty}^{\infty} \cdots \int_{-\infty}^{\infty} u\left(x_{1}, x_{2}, \ldots, x_{n}\right) f\left(x_{1}, x_{2}, \ldots, x_{n}\right) d x_{1} d x_{2} \cdots d x_{n}$$

> Definition : Discrete Case

if the $n$-fold sum exist 

$$\sum_{x_{n}} \cdots \sum_{x_{1}}\left|u\left(x_{1}, x_{2}, \ldots, x_{n}\right)\right| p\left(x_{1}, x_{2}, \ldots, x_{n}\right)$$

then its expectation is given by

$$E(Y)=\sum_{x_{n}} \cdots \sum_{x_{1}} u\left(x_{1}, x_{2}, \ldots, x_{n}\right) p\left(x_{1}, x_{2}, \ldots, x_{n}\right)$$

> ## Propoerty : Linearlity of Expetation

> Propoerty

for the $n$-dimensional case also. In particular, $E$ is a linear operator. That is, if $Y_{j}=u_{j}\left(X_{1}, \ldots, X_{n}\right)$ for $j=1, \ldots, m$ and each $E\left(Y_{i}\right)$ exists, then

$$E\left[\sum_{j=1}^{m} k_{j} Y_{j}\right]=\sum_{j=1}^{m} k_{j} E\left[Y_{j}\right]$$

> ## marginal pdf

> Definition : Marginal Pdf of one variable

By an argument similar to the two-variable case, we have for every $b$

$$F_{X_{1}}(b)=P\left(X_{1} \leq b\right)=\int_{-\infty}^{b} f_{1}\left(x_{1}\right) d x_{1}$$

where $f_{1}\left(x_{1}\right)$ is defined by the $(n-1)$-fold integral

$$f_{1}\left(x_{1}\right)=\int_{-\infty}^{\infty} \cdots \int_{-\infty}^{\infty} f\left(x_{1}, x_{2}, \ldots, x_{n}\right) d x_{2} \cdots d x_{n}$$

> Definition : Marginal Pdf of k - variable

marginal pdf of this particular group of $k$ variables. Let take $n=6, k=3$, and let us select the group $X_{2}, X_{4}, X_{5} .$ Then the marginal pdf of $X_{2}, X_{4}, X_{5}$ is the joint pdf of this particular group of three variables, namely,

$$\int_{-\infty}^{\infty} \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} f\left(x_{1}, x_{2}, x_{3}, x_{4}, x_{5}, x_{6}\right) d x_{1} d x_{3} d x_{6}$$

> ## Conditional 

> joint conditional pdf

extend the definition of a conditional pdf. Suppose $f_{1}\left(x_{1}\right)>0$. Then we define the symbol $f_{2, \ldots, n \mid 1}\left(x_{2}, \ldots, x_{n} \mid x_{1}\right)$ by the relation

$$f_{2, \ldots, n \mid 1}\left(x_{2}, \ldots, x_{n} \mid x_{1}\right)=\frac{f\left(x_{1}, x_{2}, \ldots, x_{n}\right)}{f_{1}\left(x_{1}\right)}$$

and $f_{2, \ldots, n \mid 1}\left(x_{2}, \ldots, x_{n} \mid x_{1}\right)$ is called the joint conditional pdf of $X_{2}, \ldots, X_{n}$ given $X_{1}=x_{1}$ 

> Joint conditional pdf k-variable

이 경우, k-variable 이면, 아래와 같이 정의됩니다.

$$f_{k+1, \ldots, n \mid 1..k}\left(x_{k+1}, \ldots, x_{n} \mid x_{1}...x_{k}\right)=\frac{f\left( x_{k+1}, \ldots, x_{n}\right)}{f_{1}\left(x_{1}...x_{k}\right)}$$

> Expectation

Expectation 은 pdf 에 conditional 이 붙어서 구현됩니다. 

$$E\left[u\left(X_{2}, \ldots, X_{n}\right) \mid x_{1}\right]=\int_{-\infty}^{\infty} \cdots \int_{-\infty}^{\infty} u\left(x_{2}, \ldots, x_{n}\right) f_{2, \ldots, n \mid 1}\left(x_{2}, \ldots, x_{n} \mid x_{1}\right) d x_{2} \cdots d x_{n}$$

> ## Mutually independent

> Definition

Let the random variables $X_{1}, X_{2}, \ldots, X_{n}$ have the joint pdf $f\left(x_{1}, x_{2}, \ldots, x_{n}\right)$ and the marginal probability density functions $f_{1}\left(x_{1}\right), f_{2}\left(x_{2}\right), \ldots, f_{n}\left(x_{n}\right)$, respectively. The random variables $X_{1}, X_{2}, \ldots, X_{n}$ are said to be mutually independent if and only if

 the continuous case

$$f\left(x_{1}, x_{2}, \ldots, x_{n}\right) \equiv f_{1}\left(x_{1}\right) f_{2}\left(x_{2}\right) \cdots f_{n}\left(x_{n}\right)$$

In the discrete case

$$p\left(x_{1}, x_{2}, \ldots, x_{n}\right) \equiv p_{1}\left(x_{1}\right) p_{2}\left(x_{2}\right) \cdots p_{n}\left(x_{n}\right)$$

> Proporty : Probability

Suppose $X_{1}, X_{2}, \ldots, X_{n}$ are mutually independent. Then

$$\begin{aligned}
&P\left(a_{1}<X_{1}<b_{1}, a_{2}<X_{2}<b_{2}, \ldots, a_{n}<X_{n}<b_{n}\right) \\
&\quad=P\left(a_{1}<X_{1}<b_{1}\right) P\left(a_{2}<X_{2}<b_{2}\right) \cdots P\left(a_{n}<X_{n}<b_{n}\right) \\
&\quad=\prod_{i=1}^{n} P\left(a_{i}<X_{i}<b_{i}\right)
\end{aligned}$$

> Property : Expectation

for mutually independent random variables $X_{1}, X_{2}, \ldots, X_{n}$

$$E\left[\prod_{i=1}^{n} u_{i}\left(X_{i}\right)\right]=\prod_{i=1}^{n} E\left[u_{i}\left(X_{i}\right)\right]$$

> Property : MGF

Suppose $X_{1}, X_{2}, \ldots, X_{n}$ are $n$ mutually independent random variables. Suppose, for all $i=1,2, \ldots, n, X_{i}$ has mgf $M_{i}(t)$, for $-h_{i}<t<h_{i}$, where $h_{i}>0 .$ Let $T=\sum_{i=1}^{n} k_{i} X_{i}$, where $k_{1}, k_{2}, \ldots, k_{n}$ are constants. Then $T$ has the mgf given by

$$M_{T}(t)=\prod_{i=1}^{n} M_{i}\left(k_{i} t\right), \quad-\min _{i}\left\{h_{i}\right\}<t<\min _{i}\left\{h_{i}\right\}$$

> ## Note : Pairwise independent and Mutually independent

> Problem

$X$ 와 $Y$ 가 공정한 동전을 두번 던졌 을때에 1 , 뒷면은 0 으로 설정합니다. 세 번째 확률 변수 $Z$ 는 동전 던지기 중 정확히 하나만 "앞면"이 나온 경우 1 이고 그렇지 않은 경우 0 이라고 합시다. 그러면 3-triple 확률변수 $(X,$, $Y, Z)$ 은 다음과 같은 확률 분포를 갖습니다.

$$(X, Y, Z)= \begin{cases}(0,0,0) & \text { with probability } 1 / 4 \\ (0,1,1) & \text { with probability } 1 / 4 \\ (1,0,1) & \text { with probability } 1 / 4 \\ (1,1,0) & \text { with probability } 1 / 4\end{cases}$$

위의 분포로부터 우리는 아래의 확률표를 이끌어낼 수 있습니다.

$$\begin{aligned}
&f_{X}(0)=f_{Y}(0)=f_{Z}(0)=1 / 2 \\
&f_{X}(1)=f_{Y}(1)=f_{Z}(1)=1 / 2 \\
&f_{X, Y}=f_{X, Z}=f_{Y, Z} \\
&f_{X, Y}(0,0)=f_{X, Y}(0,1)=f_{X, Y}(1,0)=f_{X, Y}(1,1)=1 / 4
\end{aligned}$$

위와 같이, 각각의 X,Y,Z 는 Pairwise 하게 독립하다는것을 알 수 있죠!

- $X$ 와 $Y$ 는 독립
- $X$ 와 $Z$ 는 독립
- $Y$ 와 $Z$ 는 독립

그러나 이게 Mutually indepent 한지를 살펴봅시다. 위의 경우 X,Y,Z = (0,0,0) 인 경우에 각각의 확률은 다릅니다.  

$$\begin{aligned}
&f_{X, Y, Z}(0,0,0)=1 / 4 \\
&f_{X}(0) f_{Y}(0) f_{Z}(0)=1 / 8 \\
&f_{X, Y, Z}(x, y, z) \neq f_{X}(x) f_{Y}(y) f_{Z}(z)
\end{aligned}$$

- 즉 위와 같이 Mutually 독립이지 않습니다.

> Note

- 즉 위와 같이 Mutually independent 와 Pairwise independent 는 다른 개념입니다. 
  - 즉 Mutually $\to$ Pairwise 이지만 Pairwaise $\not \to $ Mutually 인 것이죠
- 우리는 통상 independence 를 말할때에는 Mutually independent 를 말하게 됩니다. 

> ## Definition : R.V. matrix

우리는 이전에 여러개의 random variable 들을 같이 바라볼때에는 Random vector 를 생성하여 고려하였습니다. 이때에 우리는 기댓값 , 분산 등을 어떻게 고려할까요? 

> Definition : Expectation of random vector

Let $\mathbf{X}=$ $\left(X_{1}, \ldots, X_{n}\right)^{\prime}$ be an $n$-dimensional random vector. Recall that we defined $E(\mathbf{X})=$ $\left(E\left(X_{1}\right), \ldots, E\left(X_{n}\right)\right)^{\prime}$, that is, the expectation of a random vector is just the vector

> Definition : Expectation of random vector

suppose $\mathbf{W}$ is an $m \times n$ matrix of random variables, say, $\mathbf{W}=\left[W_{i j}\right]$ for the random variables $W_{i j}, 1 \leq i \leq m$ and $1 \leq j \leq n$. 

Note that we can always string out the matrix into an $m n \times 1$ random vector. Hence, we define the expectation of a random matrix

$$E[\mathbf{W}]=\left[E\left(W_{i j}\right)\right]$$

> ## Theorem : $m \times n$ R.V.

> Theorem

Let $\mathbf{W}_{1}$ and $\mathbf{W}_{2}$ be $m \times n$ matrices of random variables, let $\mathbf{A}_{1}$ and $\mathbf{A}_{2}$ be $k \times m$ matrices of constants, and let $\mathbf{B}$ be an $n \times l$ matrix of constants. Then

$$\begin{aligned}
E\left[\mathbf{A}_{1} \mathbf{W}_{1}+\mathbf{A}_{2} \mathbf{W}_{2}\right] &=\mathbf{A}_{1} E\left[\mathbf{W}_{1}\right]+\mathbf{A}_{2} E\left[\mathbf{W}_{2}\right] \\
E\left[\mathbf{A}_{1} \mathbf{W}_{1} \mathbf{B}\right] &=\mathbf{A}_{1} E\left[\mathbf{W}_{1}\right] \mathbf{B}
\end{aligned}$$

> Proof

각각의 element 에 대해서 위의 등식이 성립함은 보이면 됩니다. 우선 첫번째 식에 대하여 성립함을 보이면 아래와 같습니다.

$$E\left[\sum_{s=1}^{m} a_{1 i s} W_{1 s j}+\sum_{s=1}^{m} a_{2 i s} W_{2 s j}\right]=\sum_{s=1}^{m} a_{1 i s} E\left[W_{1 s j}\right]+\sum_{s=1}^{m} a_{2 i s} E\left[W_{2 s j}\right]$$

두번째 식에 대해서는 자명하므로 증명은 생략하겠습니다

> ## Definition : Variance-Covariance matrix

> Definition

Let $\mathbf{X}=\left(X_{1}, \ldots, X_{n}\right)^{\prime}$ be an $n$-dimensional random vector, such that $\sigma_{i}^{2}=$ $\operatorname{Var}\left(X_{i}\right)<\infty$. The mean of $\mathbf{X}$ is $\boldsymbol{\mu}=E[\mathbf{X}]$ and we define its variance-covariance matrix to be,

$$\operatorname{Cov}(\mathbf{X})=E\left[(\mathbf{X}-\boldsymbol{\mu})(\mathbf{X}-\boldsymbol{\mu})^{\prime}\right]=\left[\sigma_{i j}\right]$$

where $\sigma_{i i}$ denotes $\sigma_{i}^{2}$ the $i$ th diagonal entry of $\operatorname{Cov}(\mathbf{X})$ is $\sigma_{i}^{2}=\operatorname{Var}\left(X_{i}\right)$ and the $(i, j)$ th off diagonal entry is $\operatorname{Cov}\left(X_{i}, X_{j}\right)$.

> Note

- 위와 같이 Diagnal 은 Variance 고, i,j element 는 covariance 입니다. 
- 즉 우리가 Variance-Covariance Matrix 라는 표현에 딱! 맞는거죠

> ## Theorem : cov and expectation

> Theorem

Let $\mathbf{X}=\left(X_{1}, \ldots, X_{n}\right)^{\prime}$ be an $n$-dimensional random vector, such that $\sigma_{i}^{2}=\sigma_{i i}=\operatorname{Var}\left(X_{i}\right)<\infty .$ Let $\mathbf{A}$ be an $m \times n$ matrix of constants. Then

$$\begin{aligned}
\operatorname{Cov}(\mathbf{X}) &=E\left[\mathbf{X} \mathbf{X}^{\prime}\right]-\boldsymbol{\mu} \mu^{\prime} \\
\operatorname{Cov}(\mathbf{A} \mathbf{X}) &=\mathbf{A} \operatorname{Cov}(\mathbf{X}) \mathbf{A}^{\prime}
\end{aligned}$$

> Proof

$$\begin{aligned}
\operatorname{Cov}(\mathbf{X}) &=E\left[(\mathbf{X}-\boldsymbol{\mu})(\mathbf{X}-\boldsymbol{\mu})^{\prime}\right] \\
&=E\left[\mathbf{X} \mathbf{X}^{\prime}-\boldsymbol{\mu} \mathbf{X}^{\prime}-\mathbf{X} \boldsymbol{\mu}^{\prime}+\boldsymbol{\mu} \boldsymbol{\mu}^{\prime}\right] \\
&=E\left[\mathbf{X X}^{\prime}\right]-\boldsymbol{\mu} E\left[\mathbf{X}^{\prime}\right]-E[\mathbf{X}] \boldsymbol{\mu}^{\prime}+\boldsymbol{\mu} \boldsymbol{\mu}^{\prime}
\end{aligned}$$

> ## note : Positive semi definite

> Theorem

All variance-covariance matrices are positive semi-definite matrices; that is, $\mathbf{a}^{\prime} \operatorname{Cov}(\mathbf{X}) \mathbf{a} \geq 0$, for all vectors $\mathbf{a} \in R^{n} .$ To see this let $\mathbf{X}$ be a random vector and let a be any $n \times 1$ vector of constants. Then $Y=\mathbf{a}^{\prime} \mathbf{X}$ is a random variable and, hence, has nonnegative variance; i.e.,

$$0 \leq \operatorname{Var}(Y)=\operatorname{Var}\left(\mathbf{a}^{\prime} \mathbf{X}\right)=\mathbf{a}^{\prime} \operatorname{Cov}(\mathbf{X}) \mathbf{a}$$

hence, $\operatorname{Cov}(\mathbf{X})$ is positive semi-definite.

> Note 

- 즉 모든 Covariance matrix 는 Semi-definite 임을 알 수 있습니다.
- 이는 중요한 정리이므로 잘 알아두세요

---

**Reference**

- Hoggs Introduction to Mathematical Statistics 7ed
- <https://people.math.gatech.edu/~ecroot/3225/rho_notes.pdf>





