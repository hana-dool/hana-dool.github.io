---
title:  "Special Expectation"
excerpt: "통계학적인 기댓값"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-16

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
---

 제일 기초가 되는 기댓값 , 분산 등에 대한 정리를 알아봅시다. 
{: .notice--warning}

# [Expectation](#link){: .btn .btn--primary}{: .align-center}

> ## Mean

> Definition

Let $X$ be a random variable whose expectation exists. The mean value $\mu$ of $X$ is defined to be $\mu=E(X)$.

> Remark

- 평균에 대한 정의를 Expectation 이라고 하겠다는 것입니다.
- 사실 역사적으로는 '평균' 이 '기댓값' 보다 훨씬 일찍 나온 개념이라, 위와 같은 관계는 지극히 자연스러운 것이죠

> ## Variance

> Definition

Let $X$ be a random variable with finite mean $\mu$ and such that $E\left[(X-\mu)^{2}\right]$ is finite. Then the variance of $X$ is defined to be $E\left[(X-\mu)^{2}\right]$. It is usually denoted by $\sigma^{2}$ or by $\operatorname{Var}(X)$.

> Proposition

$$\begin{aligned}
\sigma^{2} &=E\left(X^{2}\right)-2 \mu E(X)+\mu^{2} \\
&=E\left(X^{2}\right)-2 \mu^{2}+\mu^{2} \\
&=E\left(X^{2}\right)-\mu^{2}
\end{aligned}$$

> ## Example 1

> Example

Let $X$ have the pdf

$$f(x)= \begin{cases}\frac{1}{2}(x+1) & -1<x<1 \\ 0 & \text { elsewhere }\end{cases}$$

> Answer

Then the mean value of $X$ is

$$\mu=\int_{-\infty}^{\infty} x f(x) d x=\int_{-1}^{1} x \frac{x+1}{2} d x=\frac{1}{3}$$

while the variance of $X$ is

$$\sigma^{2}=\int_{-\infty}^{\infty} x^{2} f(x) d x-\mu^{2}=\int_{-1}^{1} x^{2} \frac{x+1}{2} d x-\left(\frac{1}{3}\right)^{2}=\frac{2}{9}$$

> ## Example 2 : Not Exist Case

> Example

If $X$ has the $\mathrm{pdf}$

$$f(x)= \begin{cases}\frac{1}{x^{2}} & 1<x<\infty \\ 0 & \text { elsewhere }\end{cases}$$

> Answer

then the mean value of $X$ does not exist, because

$$\begin{aligned}
\int_{1}^{\infty}|x| \frac{1}{x^{2}} d x &=\lim _{b \rightarrow \infty} \int_{1}^{b} \frac{1}{x} d x \\
&=\lim _{b \rightarrow \infty}(\log b-\log 1)
\end{aligned}$$

> ## Definition : MGF

> Definition : Moment Generating Function

Let $X$ be a random variable such that for some $h>0$, the expectation of $e^{t X}$ exists for $-h<t<h$. The moment generating function of $X$ is defined to be the function $M(t)=E\left(e^{t X}\right)$, for $-h<t<h .$ We use the abbreviation mgf to denote the moment generating function of a random variable.

> Remark

- mgf 는 open interval 에서 정의되어야 한다는것을 잘 기억해주세요! 
  - 그러므로 0 에서 존재한다고 해서, mgf 가 존재하는것이 아닙니다.

> Example 

다음과 같은 pdf 를 가지는 확률변수 x 에 대하여 MGF 를 구하세요

$$p(x)=\frac{1}{3}\left(\frac{2}{3}\right)^{x-1}, \quad x=1,2,3, \ldots$$

> Answer

$$\begin{aligned} M(t)=E\left(e^{t X}\right) &=\sum_{x=1}^{\infty} e^{t x} \frac{1}{3}\left(\frac{2}{3}\right)^{x-1} \\ &=\frac{1}{3} e^{t} \sum_{x=1}^{\infty}\left(e^{t} \frac{2}{3}\right)^{x-1} \\ &=\frac{1}{3} e^{t}\left(1-e^{t} \frac{2}{3}\right)^{-1} \end{aligned}$$

provided that $e^{t}(2 / 3)<1$; i.e., $t<\log (3 / 2)$. This last interval is an open interval of $0 ;$ hence, the mgf of $X$ exists and is given in the final line of the above derivation.

> ## Theorem : MGF and Pdf

> Theorem

Let $X$ and $Y$ be random variables with moment generating functions $M_{X}$ and $M_{Y}$, respectively, existing in open intervals about $0 .$ Then $F_{X}(z)=$ $F_{Y}(z)$ for all $z \in R$ if and only if $M_{X}(t)=M_{Y}(t)$ for all $t \in(-h, h)$ for some $h>0$

> Remark

- 사실 $\to$ 방향은 매우 명확합니다. 애초에 MGF 가 pdf 를 가지고 계산하는것이니까요.
- 그런데 $\leftarrow$ 방향은 약간 보이기가 어렵습니다. 이는 따로 새로운 포스트에서 따로 증명을 하도록 할게요

> ## definition m'th Moment

> Intuition

- MGF 와 pdf 가 연결되어있으므로, mgf 를 이용하여 pdf 의 성질을 이끌어 낼 수 있다는점은 놀라운것이 아닐 것입니다. 
- 우리는 existence of $M(t)$ for $-h<t<h$ 을 보였으므로, derivatives of $M(t)$ of all orders exist at $t=0$. 일 것입니다. 
- 그러므로 다음과 같은 propoerties 들을 볼 수 있을것입니다.

> Propertis : $\mu$

That is, if $X$ is continuous,

$$M^{\prime}(t)=\frac{d M(t)}{d t}=\frac{d}{d t} \int_{-\infty}^{\infty} e^{t x} f(x) d x=\int_{-\infty}^{\infty} \frac{d}{d t} e^{t x} f(x) d x=\int_{-\infty}^{\infty} x e^{t x} f(x) d x$$

Likewise, if $X$ is a discrete random variable,

$$M^{\prime}(t)=\frac{d M(t)}{d t}=\sum_{x} x e^{t x} p(x)$$

Upon setting $t=0$, we have in either case

$$M^{\prime}(0)=E(X)=\mu$$

> Properties : $\sigma$

The second derivative of $M(t)$ is

$$M^{\prime \prime}(t)=\int_{-\infty}^{\infty} x^{2} e^{t x} f(x) d x \quad \text { or } \quad \sum_{x} x^{2} e^{t x} p(x)$$

so that $M^{\prime \prime}(0)=E\left(X^{2}\right)$. Accordingly, $\operatorname{Var}(X)$ equals

$$\sigma^{2}=E\left(X^{2}\right)-\mu^{2}=M^{\prime \prime}(0)-\left[M^{\prime}(0)\right]^{2}$$

> Propoerties : m'th moment

In general, if $m$ is a positive integer and if $M^{(m)}(t)$ means the $m$ th derivative of $M(t)$, we have, by repeated differentiation with respect to $t$,

$$M^{(m)}(0)=E\left(X^{m}\right)$$

Now

$$E\left(X^{m}\right)=\int_{-\infty}^{\infty} x^{m} f(x) d x \quad \text { or } \quad \sum_{x} x^{m} p(x)$$

and the integrals (or sums) of this sort are, in mechanics, called moments. Since $M(t)$ generates the values of $E\left(X^{m}\right), m=1,2,3, \ldots$, it is called the momentgenerating function (mgf). In fact, we sometimes call $E\left(X^{m}\right)$ the mth moment of the distribution, or the $m$ th moment of $X$.

---

**Reference**

- Hoggs Introduction to Mathematical Statistics 7ed



