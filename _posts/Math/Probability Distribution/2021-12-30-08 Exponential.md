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

> ## Intuition

- 지수 분포는 특정한 사건이 일어나고, 그 다음에 같은 사건이 다시 일어날 때까지 걸리는 시간에 대한 분포입니다.
- 예를 들어 평균적으로 10분마다 도착하는 버스가 있을 때, 버스를 놓친 후 그 다음 버스가 올때까지 기다리는 시간은 지수 분포를 따른다고 할 수 있을 것입니다. 
- 그런데, 이렇게 다음 사건이 발생할 때까지 기다리는 시간을 구하려면, 어떤 시간 단위에서 그 사건이 평균적으로 몇 번 발생하는지는 알아야 하지 않을까요? 
  - 다시 말해서, 특정 단위 구간에서 그 사건의 발생 횟수에 대한 분포를 알아야 할 것 같은데요. 그런데 이 분포 어디서 많이 보지 않았나요?! 
  - 바로 [포아송 분포](https://soohee410.github.io/discrete_dist3)입니다! 어떤 사건의 **발생 횟수**가 `포아송 분포`를 따르면, 사건 사이의 **대기 시간**은 `지수 분포`를 따르게 됩니다.

> ## Shape

![jpg](/assets/images/Stat/151_2.jpg)

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

> ## Relationship with poisson

- 어떤 사건 A의 발생 횟수가 발생률(rate, 평균 발생 건수)이 λλ인 포아송 분포를 따를 때, A가 일어나고 그 다음에 또 일어날 때까지 걸리는 시간을 W라고 한다면, W는 음이 아닌 값을 가지는 연속형 확률변수가 될 것입니다. 
  - 이 때, W의 cdf는 다음과 같이 표현될 것입니다

$$\begin{aligned}
F_{W}(w) &=P(W \leq w), \quad(w \geq 0) \\
&=1-P(W>w) \\
&=1-P[\text { 구간 }[0, w] \text { 에서 } A \text { 가 일어나지 않음] }\\
&=1-P[X=0 \text { for time unit }=1,2, \cdots, w] \\
&=1-P[X=0 \text { for time }=1] \cdots P[X=0 \text { for time }=w] \\
&=1-\left[\frac{\lambda^{0} e^{-\lambda}}{0 !}\right]^{w} \\
&=1-e^{-\lambda w}, \quad(w \geq 0)
\end{aligned}$$

- 따라서 이를 미분하면 다음과 같이 대기 시간 W의 pdf를 구할 수 있습니다.

$$\begin{aligned}
f_{W}(w) &=\frac{w}{d w} F_{W}(w) \\
&=\frac{w}{d w}\left[1-e^{-\lambda w}\right] \\
&=\lambda e^{-\lambda w}, \quad w \geq 0
\end{aligned}$$

- 위와 같은 pdf는 모수 λ를 포아송 분포의 모수와 같은 것으로 둬서 표현한 것입니다
- 경우에 지수 분포의 모수를 포아송 분포의 모수의 **역수**(1/λ)로 두기도 합니다.

> ## memoryless Property

- 지수 분포 하면 빼 놓을 수 없는 성질이 바로 **무기억성**입니다. 다음의 식을 만족하면 무기억성 성질을 갖는다고 말합니다. 일단 식을 만족하는 것부터 확인해봅시다. 식의 증명은 정말 간단합니다!

$$\begin{aligned}
P(X>a+t \mid X>a)=P &(X>t),(a, t \geq 0) \\
\therefore P(X>a+t \mid X>a) &=\frac{P(X>a+t)}{P(X>a)} \\
&=\frac{e^{-\lambda(a+t)}}{e^{-\lambda a}}=e^{-\lambda t} \\
&=P(X>t)
\end{aligned}$$

- 그러면 이제 ‘무기억성을 갖는다’는 것의 의미를 알아봅시다. 어떤 시점 부터 소요되는 시간은 과거 시간에 영향을 받지 않는다는 것입니다. 
- 예를 들어, 지수 분포는 전구 수명과 관련하여 자주 언급되는데요. 어떤 전구를 한 달간 사용했을 때, 남은 전구 수명은 한 달 간 사용했던 것에 영향을 받지 않고, 그냥 새 전구의 남은 수명과 같다는 것입니다. 
- 또 다른 예로 핸드폰을 5년 썼는데 고장나기 까지 걸리는 시간은, 처음 산 뒤 고장나기까지 걸리는 시간과 같다는 것입니다. 
- 우리의 생활 상식으로 상당히 비합리적으로 보입니다. 실제로 지수 분포는 우리 실생활에서 인간 또는 제품의 수명을 모델링하기에는 너무 단순화된 분포입니다. 
- 그래서 이렇게 위험률(hazard rate)이 일정한 지수 분포보다는 와이블 분포(Weibull Distribution)가 생존 분석 및 수명 모델링에 훨씬 유연하게 사용된다고 합니다.

> ## Relationship with geometric distribution

- 한편, 지수 분포와 기하분포가 상당히 닮지 않았나요? 물론 지수 분포는 연속형 분포이고, 기하 분포는 이산형 분포입니다. 그런데 지수 분포는 ‘어떤 사건이 일어나기까지 걸리는 시간’이고, 기하 분포는 ‘어떤 사건이 발생할 때까지 걸리는 시행 횟수’입니다. 또 한, 두 분포 공통적으로 무기억성을 갖고 있습니다.
  -  즉, 지수 분포는 기하 분포의 연속형 버전이라고 할 수 있습니다!

---

**reference**

- Hoggs Introduction to Mathematical Statistics 7ed
- <https://elementary-physics.tistory.com/139>
- <https://mast.queensu.ca/~stat455/lecturenotes/set4.pdf>









