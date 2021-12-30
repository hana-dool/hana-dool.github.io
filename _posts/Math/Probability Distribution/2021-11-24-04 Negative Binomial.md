---
title:  "Negative Bimonial"
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

 음이항분포
{: .notice--warning}

# [Geometric Distribution](#link){: .btn .btn--primary}{: .align-center}

> ## Definition

> Definition

- 성공 확률이 $p$ 인 실험 (즉 $\operatorname{Bernoulli}(p)$ trials) 을 계속 수행하는데, $r$ 번의 성공을 얻기 위하여 실행한 실험 횟수의 분포입니다.

$$P(X=x \mid r, p)=\left(\begin{array}{l}
x-1 \\
r-1
\end{array}\right) p^{r}(1-p)^{x-r}, \quad x=r, r+1, \ldots$$

- 위와 같을때 we say that $X$ has a negative $\operatorname{binomial}(r, p)$ distribution.

> Note

- r 번의 성공을 얻기 위해서 얼마나 실험을 수행하느냐? 도 X 가 될 수 있지만 r 번의 성공을 얻기 위하여 얼마나 실패하느냐? 를 Y 변수로 두고 이를 Negative Binomial 이라고도 합니다.

$$P(Y=y \mid r,p)=\left(\begin{array}{c}
y+r-1 \\
y
\end{array}\right) p^{r}(1-p)^{y}, \ \ y= 0,1..$$

> ## Pmf

> Pmf of Negative binomial Distribuition

$$P(X=x \mid r, p)=\left(\begin{array}{l}
x-1 \\
r-1
\end{array}\right) p^{r}(1-p)^{x-r}, \quad x=r, r+1, \ldots$$

> Proof

$$\begin{aligned} P(X=k) &=P\left(r^{\text {th }} \text { on } k^{\text {th }} \text { trial }\right) \\ &=P\left(r-1^{\text {th }} \text { on } \mathrm{k}-1 \text { trials }\right) \cdot P\left(\text { success on } k^{\text {th }} \text { trial }\right) \\ &=\left(\begin{array}{l}k-1 \\ r-1\end{array}\right) p^{r-1}(1-p)^{k-1-(r-1)} \cdot p \\ &=\left(\begin{array}{l}k-1 \\ r-1\end{array}\right) p^{r-1}(1-p)^{k-r} \cdot p \\ &=\left(\begin{array}{l}k-1 \\ r-1\end{array}\right) p^{r}(1-p)^{k-r} \end{aligned}$$

# [Elementary Properties](#link){: .btn .btn--primary}{: .align-center}

> ## Relationship with Geometric

- We can also interpret $X \sim N B(r, p)$ as the sum of $r$ independent geometric distributions.

$X=X_{1}+X_{2}+\cdots+X_{r}$

$P(X)=P\left(X_{1}+X_{2}+\cdots+X_{r}\right)=P\left(X_{1}\right) \cdot P\left(X_{2}\right) \cdots P\left(X_{r}\right)$

---

**reference**

- Hoggs Introduction to Mathematical Statistics 7ed
- <http://cknudson.com/StudentWork/NegBin.pdf>
- <http://www.math.ntu.edu.tw/~hchen/teaching/StatInference/notes/lecture16.pdf>









