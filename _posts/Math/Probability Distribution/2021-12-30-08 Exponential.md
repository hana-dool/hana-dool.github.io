---
title:  "Exponential"
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

# [Exponential DIstribution](#link){: .btn .btn--primary}{: .align-center}

> ## Definition

> pdf

$$f(x ; \lambda)= \begin{cases}\lambda e^{-\lambda x} & x \geq 0 \\ 0 & x<0\end{cases}$$

- 이때 위의 $\lambda$ 는 rate parameter 라고 합니다. 만일 scale parameter 를 쓰게된다면 아래와 같습니다.

$$f(x ; \beta)= \begin{cases}\frac{1}{\beta} e^{-x / \beta} & x \geq 0 \\ 0 & x<0\end{cases}$$

- 위의 scale parameter 는 다음과 같은 관계를 가집니다. $$\beta=1 / \lambda$$

# [Elementary Properties](#link){: .btn .btn--primary}{: .align-center}

$$\begin{array}{|l|l|}
\hline \text { Parameters } & \lambda>0, \text { rate, or inverse scale } \\
\hline \text { Support } & x \in[0, \infty) \\
\hline \text { PDF } & \lambda e^{-\lambda x} \\
\hline \text { CDF } & 1-e^{-\lambda x} \\
\hline \text { Quantile } & -\frac{\ln (1-p)}{\lambda} \\
\hline \text { Mean } & \frac{1}{\lambda} \\
\hline \text { Median } & \frac{\ln 2}{\lambda} \\
\hline \text { Mode } & 0 \\
\hline \text { Variance } & \frac{1}{\lambda^{2}} \\
\hline \text { Skewness } & 2 \\
\hline \text { Ex. kurtosis } & 6 \\
\hline \text { Entropy } & 1-\ln \lambda \\
\hline \text { MGF } & \frac{\lambda}{\lambda-t}, \text { for } t<\lambda \\
\hline
\end{array}$$

> ## $E[X] = 1/\lambda$

$$\begin{aligned}
\mathrm{E}[X] &=\int_{0}^{\infty} x f_{X}(x) d x \\
&=\int_{0}^{\infty} x \lambda \exp (-\lambda x) d x \\
&=[-x \exp (-\lambda x)]_{0}^{\infty}+\int_{0}^{\infty} \exp (-\lambda x) d x \\
&=(0-0)+\left[-\frac{1}{\lambda} \exp (-\lambda x)\right]_{0}^{\infty} \\
&=0+\left(0+\frac{1}{\lambda}\right) \\
&=\frac{1}{\lambda}
\end{aligned}$$

> ## $Var[X] = 1/\lambda^2$

$$\begin{aligned}
\mathrm{E}\left[X^{2}\right] &=\int_{0}^{\infty} x^{2} \lambda \exp (-\lambda x) d x \\
&=\left[-x^{2} \exp (-\lambda x)\right]_{0}^{\infty}+\int_{0}^{\infty} 2 x \exp (-\lambda x) d x \quad \text { (integrating by parts) } \\
&=(0-0)+\left[-\frac{2}{\lambda} x \exp (-\lambda x)\right]_{0}^{\infty}+\frac{2}{\lambda} \int_{0}^{\infty} \exp (-\lambda x) d x \quad \text { (integrating by parts again) } \\
&=(0-0)+\frac{2}{\lambda}\left[-\frac{1}{\lambda} \exp (-\lambda x)\right]_{0}^{\infty} \\
&=\frac{2}{\lambda^{2}} \\
\mathrm{E}[X]^{2} &=\left(\frac{1}{\lambda}\right)^{2}=\frac{1}{\lambda^{2}} \\
\operatorname{Var}[X] &=\mathrm{E}\left[X^{2}\right]-\mathrm{E}[X]^{2}=\frac{2}{\lambda^{2}}-\frac{1}{\lambda^{2}}=\frac{1}{\lambda^{2}}
\end{aligned}$$



---

**reference**

- Hoggs Introduction to Mathematical Statistics 7ed
- <https://elementary-physics.tistory.com/139>
- <https://mast.queensu.ca/~stat455/lecturenotes/set4.pdf>









