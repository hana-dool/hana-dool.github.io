---
title:  "Limiting 분포"
excerpt: "Large N 일떄의 극한분포"
categories:
  - Stat
tags:
  - 1
last_modified_at: 2021-07-08

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [Limiting Distribution](#link){: .btn .btn--primary}{: .align-center}

> ## Binomial -> Normal

아래와 같이 CLT 로 인해서 Binomial 과 Normal 의 관계가 성립하게 된다. (n 이 충분히 크기만 하면 된다!)

![png](/assets/images/Stat/15_1.png)

> ## Binomial -> Poisson

$B(n,p) \to Pois(np)$ when $ n \to \inf , p \to 0 $ (가이드는 없지만 $ 100 \le n , p \le 0.01$ 이라고 한다..)

아래 식에서 since , and 부분의 식을 볼때에 n->inf / p->0 의 식이 필요함을 볼 수 있다.

![png](/assets/images/Stat/15_2.png)

아래와 같이 poisson 분포는 lambda 가 커질수록 Normal 에 가까워진다는것을 볼 수 있다.

![png](/assets/images/Stat/15_3.png)

> ## Poisson -> Normal

$\lambda$ 가 충분히 크다면 $pois(\lambda) \sim N(\lambda , \lambda)$  가 성립한다. 이 이유는 아래와 같다.

![png](/assets/images/Stat/15_4.png)

> ## hypergeometric -> Normal

![png](/assets/images/Stat/15_5.png)

> ## beta -> Normal

![png](/assets/images/Stat/15_6.png)

Let $\mathrm{B}_{r 1, r_{2}}=\frac{V_{1}}{V_{1}+V_{2}}$ where $V_{1} \sim \chi^{2}\left(2 r_{1}\right)=\operatorname{Gamma}\left(r_{1}, 2\right)$ and $V_{2} \sim \chi^{2}\left(2 r_{2}\right)=\operatorname{Gamma}\left(r_{2}, 2\right)$ and $V_{1}, V_{2}$ are independent.
Now we know that $\frac{V_{1}-2 r_{1}}{\sqrt{4 r_{1}}} \rightarrow \mathrm{N}(0,1)$ as $r_{1} \rightarrow \infty$ and $\frac{V_{2}-2 r_{2}}{\sqrt{4 r_{2}}} \rightarrow \mathrm{N}(0,1)$ as $r_{2} \rightarrow \infty$. Therefore, $\sqrt{r_{1}+r_{2}}\left(\frac{V_{1}-2 r_{1}}{\sqrt{4 r_{1}\left(r_{1}+r_{2}\right)}}, \frac{V_{2}-2 r_{2}}{\sqrt{4 r_{2}\left(r_{1}+r_{2}\right)}}\right)^{t} \rightarrow \mathrm{N}_{2}(0, I)$ where $I$ is the identity matrix.
Also, $\sqrt{r_{1}+r_{2}}\left(\frac{V_{1}-2 r_{1}}{\sqrt{4 r_{1}\left(r_{1}+r_{2}\right)}}, \frac{V_{2}-2 r_{2}}{\sqrt{4 r_{2}\left(r_{1}+r_{2}\right)}}\right)^{t}$ $\quad \sim \sqrt{n}\left(\frac{V_{1}}{\sqrt{4 \gamma} n}-\sqrt{\gamma}, \frac{V_{2}}{\sqrt{4(1-\gamma)} n}-\sqrt{1-\gamma}\right)^{t}$
Where $r_{1}+r_{2}=n, r_{1} \sim \gamma n, r_{2} \sim(1-\gamma) n$.
$$
\begin{aligned}
&\text { Now let } g(x, y)=\frac{\sqrt{\gamma} x}{\sqrt{\gamma} x+\sqrt{1-\gamma} y} \text {, then } \\
&g^{\prime}(x, y)=\left(\frac{\sqrt{\gamma(1-\gamma)} y}{(\sqrt{\gamma} x+\sqrt{1-\gamma} y)^{2}},-\frac{\sqrt{\gamma(1-\gamma)} x}{(\sqrt{\gamma} x+\sqrt{1-\gamma} y)^{2}}\right)^{t}
\end{aligned}
$$
Therefore,
$$
\begin{aligned}
&\sqrt{n}\left(g\left(\frac{V_{1}}{\sqrt{4 \gamma} n}, \frac{V_{2}}{\sqrt{4(1-\gamma)} n}\right)-g(\sqrt{\gamma}, \sqrt{1-\gamma})\right) \\
&=\sqrt{n}\left(\mathrm{~B}_{r_{1}, r_{2}}-\gamma\right) \rightarrow g^{\prime}(\sqrt{\gamma}, \sqrt{1-\gamma})^{t} \mathrm{~N}(0, I)=\mathrm{N}(0, \gamma(1-\gamma))
\end{aligned}
$$

- https://math.stackexchange.com/questions/2362780/prove-the-normal-approximation-of-beta-distribution

> ## ChiSquared -> Normal

![png](/assets/images/Stat/15_7.png)

> ## Gamma -> Normal

- $X_1 \sim \Gamma(a_1,b)$ , $X_2 \sim \Gamma(a_2,b)$  에 대해서,  두 r.v. 가 서로 독립이면 $X_1 + X_2 \sim \Gamma(a_1 + a_2 , b)$ 입니다. 
- 즉 CLT 에 의해서 a 가 크면 ( Shape ) Normal 에 가까워진다고 할 수 있습니다. 

![png](/assets/images/Stat/15_8.png)

> Q. 아니 그러면 모든 Gamma 는 Normal 아닌가요? 왜냐하면 Gamma(1,1) 도 결국에는 $\Gamma(0.01,1)+\Gamma(0.01,1) .....$ 아닌가요?

- 아닙이다. 위와 같은 로직이라면 모든 Additive 성질이 있는 Distribution 은 Normal 이겠죠.
- 물론 $\Gamma(0.01,1)$ 을 무한에 가깝게 더하게되면, $X = \sum X_i$ 는 Normal Approximation 이됩니다.
- 하지만 위 예시는 100개뿐이죠. 게다가 각각의 $\Gamma(0.01,1)$ 은 분산이 매우 크다는 점에서 Normal 로 근사하기까지는 매우 큰 표본이 필요합니다. 

![png](/assets/images/Stat/15_10.png)

- 위와 같은 그래프가 Normal 이 되려면 Sample 수가 적어도 10000개는 필요할 것입니다. 
  - 즉 쪼개놓은 각각의 그래프는 Normal 근사가 쉽지 않아서 CLT 가 성립하지 않는것입니다.

> More General Proof

Theorem The limiting distribution of the gamma $(\alpha, \beta)$ distribution is the $N\left(\mu, \sigma^{2}\right)$ distribution where $\mu=\alpha \beta$ and $\sigma^{2}=\alpha^{2} \beta$.

Proof Let the random variable $X$ have the gamma $(\alpha, \beta)$ distribution with probability density function
$$
f_{X}(x)=\frac{x^{\beta-1} \mathrm{e}^{-x / \alpha}}{\alpha^{\beta} \Gamma(\beta)} \quad x>0 .
$$
The moment generating function of $X$ is
$$
M_{X}(t)=(1-\alpha t)^{-\beta} \quad t<\frac{1}{\alpha} .
$$
The mean of $X$ is $E[X]=\alpha \beta$ and the variance of $X$ is $V[X]=\alpha^{2} \beta$. Subtract the mean and divide by the standard deviation before taking the limit. The transformation
$$
Y=g(X)=(X-\alpha \beta) /(\alpha \sqrt{\beta})=X /(\alpha \sqrt{\beta})-\sqrt{\beta}
$$
is a 1-1 transformation from $\mathcal{X}=\{x \mid x>0\}$ to $\mathcal{Y}=\{y \mid y>-\sqrt{\beta}\}$. The moment generating function of $Y$ is
$$
\begin{aligned}
M_{Y}(t) &=E\left[e^{t Y}\right] \\
&=E\left[e^{t(x /(\alpha \sqrt{\beta})-\sqrt{\beta})}\right] \\
&=e^{-t \sqrt{\beta}} E\left[e^{t(x /(\alpha \sqrt{\beta}))}\right] \\
&=e^{-t \sqrt{\beta}} M_{X}(t /(\alpha \sqrt{\beta})) \\
&=e^{-t \sqrt{\beta}}(1-(t / \sqrt{\beta}))^{-\beta} \\
&=E \sqrt{\beta}
\end{aligned}
$$
The limiting moment generating function of $Y$ is
$$
\lim _{\beta \rightarrow \infty} M_{Y}(t)=\lim _{\beta \rightarrow \infty} e^{-t \sqrt{\beta}}(1-(t / \sqrt{\beta}))^{-\beta}=e^{t^{2} / 2} \quad-\infty<t<\infty
$$

> ## T distribution -> Normal

![png](/assets/images/Stat/15_9.png)

##Ref

- https://modelassist.epixanalytics.com/display/EA/Normal+approximation+to+the+Gamma+distribution

