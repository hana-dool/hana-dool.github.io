---
title:  "Special Expectation"
excerpt: "통계학적인 기댓값"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-13

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

---

**Reference**

- 호그의 Introduction to Mathematical Statistics 7ed



