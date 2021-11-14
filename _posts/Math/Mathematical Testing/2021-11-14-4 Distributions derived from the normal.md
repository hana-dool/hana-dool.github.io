---
title:  "Distributions derived from the normal"
excerpt: "Normal 로 부터 유도되는 다양한 분산들"
categories:
  - Mathematical_Testing
last_modified_at: 2021-11-14

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Normal 부터 시작되는 분포들에 대해서 알아봅시다
{: .notice--warning}

# [Distributions derived from the normal](#link){: .btn .btn--primary}{: .align-center}

> ## Definition 7 :  ChiSquare Distributioin

> Definition

If $Z \sim N(0,1)$, then $Z^{2}$ has a chi-square distribution with 1 degree of freedom, denoted $\chi_{1}^{2}$.

> ## Definition 8 : n -degree Chisquare

> Definition

Definition 8. If $V_{1}, V_{2}, \ldots, V_{n}$ are independent random variables each with a chi-square distribution with 1 degree of freedom, then $\sum_{i=1}^{n} V_{i}$ has a chi-square distribution with $n$ degrees of freedom, denoted $\chi_{n}^{2}$.

> Fact 1 : pdf of chisquare

FAC 1 . The $p d f$ of a chi-square random variable with $k$ degrees of freedom is

$$\frac{1}{2^{k / 2} \Gamma(k / 2)} x^{k / 2-1} e^{-x / 2} \cdot I_{[0, \infty)}(x)$$



> ## Definition 9 : t Distribution

> Definition

DEFINITION $9 .$ If $Z$ and $U$ are independent random variables with $Z \sim N(0,1)$ and $U \sim \chi_{n}^{2}$, then

$$\frac{Z}{\sqrt{\frac{U}{n}}}$$

has a tdistribution with $n$ degrees of freedom, denoted $t_{n}$.

> ## Definition 10 : F Distribution

> Definition

DEFINITION $10 .$ If $U$ and $V$ are independent random variables, $U \sim \chi_{n}^{2}$ and $V=\chi_{m}^{2}$, then

$$\frac{U / n}{V / m}$$

has a F distribution with $n$ and $m$ degrees of freedom, denoted $F_{n, m}$.

> ## Fact 2 : Gamma pdf

> Definition

FACT 2. A random variable with a gamma distribution with parameters $\alpha$ and $\lambda$ has $p d f$

$$f(x)=\frac{\lambda^{\alpha} x^{\alpha-1} e^{-\lambda x}}{\Gamma(\alpha)}$$

for $x \geq 0, \alpha>0$ and $\lambda>0$

> ## Lemma 1 : MGF of chi square 

> Definition

LEMMA 1 . The moment generating function of a chi-square random variable with $k$ degrees of freedom is $(1-2 t)^{-k / 2}$ for $t<1 / 2$.

> Proof

The pdf of a chi-square random variable with $k$ degrees of freedom is

$$\frac{1}{2^{k / 2} \Gamma(k / 2)} x^{k / 2-1} e^{-x / 2} \cdot I_{[0, \infty)}(x)$$

So by Definition 4 , the moment generating function is

$$\begin{aligned}
M(t) &=\int_{0}^{\infty} e^{t x} \cdot \frac{1}{2^{k / 2} \Gamma(k / 2)} x^{k / 2-1} e^{-x / 2} d x \\
&=\int_{0}^{\infty} \frac{1}{2^{k / 2} \Gamma(k / 2)} x^{k / 2-1} e^{t x-x / 2} d x \\
&=\frac{2^{k / 2}(1-2 t)^{-k / 2}}{2^{k / 2}} \int_{0}^{\infty} \frac{\left(\frac{1-2 t}{2}\right) k / 2}{\Gamma(k / 2)} x^{k / 2-1} e^{-x \frac{(1-2 t)}{2}} d x \\
&=(1-2 t)^{-k / 2}
\end{aligned}$$

because

$$\frac{\left(\frac{1-2 t}{2}\right)^{k / 2}}{\Gamma(k / 2)} x^{k / 2-1} e^{-x \frac{(1-2 t)}{2}}$$

is the pdf of a gamma distribution with $\alpha=k / 2$ and $\lambda=\frac{(1-2 t)}{2}$ and probability density functions integrate to one. By the definition of the pdf of a gamma distribution, $\lambda>0$ or $\frac{(1-2 t)}{2}>0$. Therefore the moment generating function for a chi-square random variable is only defined if $t<1 / 2$.

> ## Lemma 2 : chi Square and E,Var

> Lemma

LEMMA 2. If $X \sim \chi_{k}^{2}$, then

$$\begin{gathered}
E(X)=k \\
\operatorname{Var}(X)=2 k
\end{gathered}$$

> Proof

PROOF. By Theorem 7 ,

$$M^{(r)}(0)=E\left(X^{r}\right)$$

so

$$\begin{aligned}
E(X) &=\left.\frac{d}{d t}(1-2 t)^{-k / 2}\right|_{t=0} \\
&=-\frac{k}{2}(1-2 t)^{-k / 2-1} \cdot-\left.2\right|_{t=0} \\
&=-\frac{k}{2}(1-2 \cdot 0)^{-k / 2-1} \cdot-2 \\
&=k
\end{aligned}$$

and

$$\begin{aligned}
E\left(X^{2}\right) &=\left.\frac{d^{2}}{d t^{2}}(1-2 t)^{-k / 2}\right|_{t=0} \\
&=k\left(-\frac{k}{2}-1\right)(1-2 t)^{-k / 2-2} \cdot-\left.2\right|_{t=0} \\
&=k(k+2)
\end{aligned}$$

Therefore

$$\begin{aligned}
\operatorname{Var}(X) &=E\left(X^{2}\right)-(E(X))^{2} \\
&=k(k+2)-k^{2} \\
&=k^{2}+2 k-k^{2} \\
&=2 k
\end{aligned}$$

>

---

**Reference**

- <https://digitalcommons.usu.edu/cgi/viewcontent.cgi?article=1014&context=gradreports>

