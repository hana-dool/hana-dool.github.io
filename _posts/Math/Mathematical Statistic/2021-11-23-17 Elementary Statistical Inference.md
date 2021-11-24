---
title:  "Sampling and Statistics"
excerpt: "Sampling Distribution 에 대해서 알아보기"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-23

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
---

 여러 변수들에 대한 Linearlity 성질
{: .notice--warning}

# [Sampling and Statistics](#link){: .btn .btn--primary}{: .align-center}

> ## Sampling and Statistics

> inference of $f(x)$

- Typical Statistical Problem 에서 우리는 $f(x)$ 를 모르는 상태에서 추론이 진행됩니다.
- 이때에 우리는 이러한 미지의 $f(x)$ 에 대해서 다음과 같이 2개의 방식으로 접근하게 됩니다. 

1. $f(x)$ or $p(x)$ is completely unknown.
1. The form of $f(x)$ or $p(x)$ is known down to a parameter $\theta$, where $\theta$ may be a vector.

- 첫번쨰 경우는 어떤 분포를 따르는지도 모르는 경우입니다. (Normal 인지 Gamma 인지....)
- 두번쨰 경우는 어떤 분포를 따르는지는 알지만 parameter 를 모르는 경우 (즉 Normal 을 따른다는것은 가정하나, $\mu , \sigma$ 는 미지의 값

> Note

- 여기에서 우리는 두번째 경우에 대해서만 고려하려고 합니다. (나머지 경우는 Advanced 한 경우라 나중에 알아볼게요)
- 두번째 경우에 우리는 다음과 같이 문제를 정의합니다.  random variable $X$ has a density or mass function of the form $f(x ; \theta)$ or $p(x ; \theta)$, where $\theta \in \Omega$ for a specified set $\Omega$. 
- 즉 예시로 parameter space $\Omega=\{\theta \mid \theta>0\}$.로 정의한다면 우리는 데이터(X) 로부터, 분포의 parameter 값 $\theta$ 를 추정하고 싶다는 것을 의미합니다.

> ## Random Samples

> Definition 

If the random variables $X_{1}, X_{2}, \ldots, X_{n}$ are independent and identically distributed (iid), then these random variables constitute a random sample of size $n$ from the common distribution.

> ## Statistic (통계량)

> Definition

Let $X_{1}, X_{2}, \ldots, X_{n}$ denote a sample on a random variable $X$. Let $T=T\left(X_{1}, X_{2}, \ldots, X_{n}\right)$ be a function of the sample. Then $T$ is called a statistic.

> Note

- 사실 어렵게 받아들일 필요는 없고, Random Variable 로 이루어진 함수를 모두 Statistic 이라고 한다고 이해하면 됩니다. 
  - $X_1 + X_2$ 도 통계량입니다.

> ## Estimator (추정량)

- 우리가 구하고자 하는 대상을 표본을 이용하여 추정하려면 어떻게 해야할까요?
  -  데이터 ($X_1,X_2...$) 들을 이용하여 함수를 만든뒤 , 이를 대상 ($\theta$) 을 추정하기 위한 추정량 으로 사용할 수  있니다. 이를 $\hat{\theta} $ 라 합니다.
- 이렇게 특정한것 (주로 모수) 을 추정하기 위해 사용되는 통계량을 추정량이라고 합니다.

> ## Unbiased

> Definition 

Let $X_{1}, X_{2}, \ldots, X_{n}$ denote a sample on a random variable $X$ with pdf $f(x ; \theta), \theta \in \Omega$. Let $T=T\left(X_{1}, X_{2}, \ldots, X_{n}\right)$ be a statistic. We say that $T$ is an unbiased estimator of $\theta$ if $E(T)=\theta$.

> ## Maximum Likelihood Estimator

> Definition

First proposed by the German mathematician Gauss (1821) and rediscovered and first investigated by the English statistician R.A.Fisher (1922).

$$\begin{aligned}
L(\theta ; \mathbf{x}) &=f(\mathbf{x} ; \theta) \quad \theta \in \Omega \\
&=\prod_{i=1}^{n} f\left(x_{i} ; \theta\right) \quad \text { (under iid or random sample) }
\end{aligned}$$

where $\Omega$ is parameter space.

> How to?

- Finding a value $\hat{\theta}$ that is "most likely" to have produced the data.

$$\hat{\theta}_{\text {mle }}=\max _{\theta}(\theta)=\max _{\theta} \prod_{i=1}^{n} f\left(x_{i} ; \theta\right) .$$

![png](/assets/images/Stat/111_1.png)

- 위와 같이 Likelihood 에 대해서 최댓값을 가지는 모수 $\theta$ 를 찾자는게 중심 아이디어입니다. 
- Log를 취해도 Maximize 하는것은 똑같으므로 아래와 같이 정의하기도 합니다.
  - 또한 Log 가 되면 Product 가 Summation 이 되어 여러모로 유리한점도 많습니다. (계산편리)

$$\hat{\theta}_{m l e}=\max _{\theta} \log L(\theta)=\max _{\theta} \sum_{i=1}^{n} \log f\left(x_{i} ; \theta\right) .$$

> Method

- The maximum lilkelihood estimator (mle) can be obtained by solving the (estimating) equation,

$$\frac{\partial l(\theta)}{\partial \theta}=0$$

where $l(\theta)=\log L(\theta)$.
- Ans, we also need to check $$\frac{\partial^{2} l(\theta)}{\partial \theta^{2}}\mid_{\theta=\hat{\theta}}<0$$.

> Note

- 즉 위와 같이 두가지 Rule 을 이용하여 최댓값을 구할 수 있습니다.

---

**reference**

- Hoggs Introduction to Mathematical Statistics 7ed
- <https://people.math.gatech.edu/~ecroot/3225/rho_notes.pdf>





