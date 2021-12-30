---
title:  "Uniform"
excerpt: ""
categories:
  - Mathematical_Distribution
last_modified_at: 2021-11-24

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true

---

 Binomial Distribution
{: .notice--warning}

# [Uniform Distribution](#link){: .btn .btn--primary}{: .align-center}

> ## Definition

> Definition

주어진 범위 $a \leq x \leq b$ 에 대하여, 연속적인 랜덤 변수 $X$ 가 다음의 pdf를 가질 때 이를 uniform $(a, b)$ Distribution 이라고 한다.

$$f_{X}(x)=\left\{\begin{array}{cl}
\frac{1}{b-a} & \text { if } a \leq x \leq b \\
0 & \text { otherwise }
\end{array}\right.$$

랜덤 변수 $X$ 가 uniform $(a, b)$ distribution을 따른다는 것을 줄여서 다음과 같이 표현합니다.

$$X \sim \operatorname{unif}(a, b)$$

# [Elementary Properties](#link){: .btn .btn--primary}{: .align-center}

> ## Tables

$$\begin{array}{|l|l|}
\hline \text { Parameters } & -\infty<a<b<\infty \\
\hline \text { Support } & x \in[a, b] \\
\hline \text { PDF } & \begin{cases}\frac{1}{b-a} & \text { for } x \in[a, b] \\
0 & \text { otherwise }\end{cases} \\
\hline \text { CDF } & \begin{cases}0 & \text { for } x<a \\
\frac{x-a}{b-a} & \text { for } x \in[a, b] \\
1 & \text { for } x>b\end{cases} \\
\hline \text { Mean } & \frac{1}{2}(a+b) \\
\hline \text { Median } & \frac{1}{2}(a+b) \\
\hline \text { Mode } & \text { any value in }(a, b) \\
\hline \text { Variance } & \frac{1}{12}(b-a)^{2} \\
\hline
\hline \text { Skewness } & 0 \\
\hline \text { Ex, kurtosis } & -\frac{6}{5} \\
\hline \text { Entropy } & \ln (b-a) \\
\hline \text { MGF } & \begin{cases}\frac{\mathrm{e}^{t b}-\mathrm{e}^{t a}}{t(b-a)} & \text { for } t \neq 0 \\
1 & \text { for } t=0\end{cases} \\
\hline \text { CF } & \begin{cases}\frac{\mathrm{e}^{i t b}-\mathrm{e}^{i t a}}{i t(b-a)} & \text { for } t \neq 0 \\
1 & \text { for } t=0\end{cases} \\
\hline
\end{array}$$

> ## Proof : E(X) = $\frac{1}{2}(a+b)$

> Proof

$$\begin{aligned}
\mathrm{E}(X) &=\int_{-\infty}^{a} 0 x \mathrm{~d} x+\int_{a}^{b} \frac{x}{b-a} \mathrm{~d} x+\int_{b}^{\infty} 0 x \mathrm{~d} x \\
&=\left[\frac{x^{2}}{2(b-a)}\right]_{a}^{b} \\
&=\frac{b^{2}-a^{2}}{2(b-a)} \\
&=\frac{(b-a)(b+a)}{2(b-a)} \\
&=\frac{a+b}{2}
\end{aligned}$$

> ## Proof : V(X)

> Proof

From Variance as Expectation of Square minus Square of Expectation:

$$\operatorname{var}(X)=\int_{-\infty}^{\infty} x^{2} f_{X}(x) \mathrm{d} x-(\mathrm{E}(X))^{2}$$

So

$$\begin{aligned}
\operatorname{var}(X) &=\int_{-\infty}^{a} 0 x^{2} \mathrm{~d} x+\int_{a}^{b} \frac{x^{2}}{b-a} \mathrm{~d} x+\int_{b}^{\infty} 0 x^{2} \mathrm{~d} x-\frac{(a+b)^{2}}{4} \\
&=\left[\frac{x^{3}}{3(b-a)}\right]_{a}^{b}-\frac{(a+b)^{2}}{4} \\
&=\frac{b^{3}-a^{3}}{3(b-a)}-\frac{(a+b)^{2}}{4} \\
&=\frac{4(b-a)\left(a^{2}+a b+b^{2}\right)}{12(b-a)}-\frac{3(a+b)^{2}}{12} \\
&=\frac{4 a^{2}+4 a b+4 b^{2}-3 a^{2}-6 a b-3 b^{2}}{12} \\
&=\frac{b^{2}-2 a b+a^{2}}{12} \\
&=\frac{(b-a)^{2}}{12}
\end{aligned}$$



---

**reference**

- Hoggs Introduction to Mathematical Statistics 7ed
- <http://cknudson.com/StudentWork/NegBin.pdf>







