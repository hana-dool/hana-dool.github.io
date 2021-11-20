---
title:  "Bessel's Correlation"
excerpt: "왜 표본분산은 n-1 로 나누는가?"
categories:
  - Stat
last_modified_at: 2021-11-19

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 표본분산은 왜 Unbiased 가 되기 위해서는 n-1 로 나누어야 할까요? 이에 대해서 알아보도록 합시다.
{: .notice--warning}

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

> # Bessel's correction

> definition

- In statistics, Bessel's correction is the use of n − 1 instead of n in the formula for the sample variance and sample standard deviation,

> Note

- 즉 원래는 분산은 n 을 나누어서 계산하는데, 표본 분산을 계산시 n 으로 나누지 않고 n-1 로 나누어 분산을 추정하는것입니다. 
  - 이러한 Correlation (수정) 작업이 있어야 분산이 제대로 추정된다고 합니다.

> ## Cautions

- 이러한 Bessel correlation 을 사용하려면 몇가지 경고사항이 있습니다. 

> 1.It does not yield an unbiased estimator of standard *deviation*.

- 즉 '표본 분산' 에 대해서는 Unbiased extimator 를 만들어내지만, '표준 편차' 에 대해서는 Biased estimator 를 만들어낸다는 의미입니다!
- 이는 다음과 같이 직관적으로 알 수 있습니다. 
  - $$E(g(x)) \not= g(E(x))$$ 입니다. 즉, s 를 표본분산 계산시에 n-1 로 나눈(즉 Correlation 을 적용 ) 분산이라고 가정할때에 $$E(s) = \sigma$$ 가 되지 않는다는 이야기죠 
- 그러므로 우리는 늘 '분산에 대해서' 만 이야기 하고 있다는 것입니다.

> 2.the unbiased estimator does not minimize mean squared error (MSE), 

- 즉 Unbiased 가 항상 좋은 메져는 아닐 수 있다는 이야기입니다.
- 이는 추정량의 성질이 Biased 도 있지만 Variance 도 잘 챙겨야 한다는 직관에서, 이해할 수 있을것입니다.

> 3.correction is only necessary when the population mean is unknown

- 즉, '평균이 알려져 있지 않을때' 에만 유효한 방법이라는 것입니다.
- 평균이 알려진 경우, 관측치의 편차는 n 을 가지게 됩니다. 

> ## intuition

- 이러한 현상에 대해서 직관적으로 알아보아야겠죠? 다음과 같은 상황을 고려해봅시다. 
  - 여기서 논하는 표본 분산은 correlation 이 들어가있지 않다고 합시다. 즉 n 으로 나누어서 추정하게 됩니다. 

> Examples

- 모평균이 1000 이라고 가정하정합시다. 우리는 지금 모평균을 모르므로 아래의 5개 샘플을 얻었다고 하겠습니다.

$$\begin{aligned}
&1001, \quad 1003, \quad 1005, \quad 1000, \quad 1001 \\
&(\text { mean })=\frac{1}{5}(1001+1003+1005+1000+1001)=1002
\end{aligned}$$

- 이는 평균에 대한 '추정치'이므로 이를 이용하여 모분산을 추정하는데에 있어서 오류가 발생합니다. 

> 정확한 모분산

- 만약 정확한 모평균 값을 알고 있다면 모분산은 다음과 같이 추정할 수 있습니다.

$$\begin{aligned}
& \frac{1}{5}\left[(1001-1000)^{2}+(1003-1000)^{2}+(1005-1000)^{2}+(1000-1000)^{2}+(1001-1000)^{2}\right] \\
=& \frac{36}{5}=7.2
\end{aligned}$$

> 표본분산으로 모분산 추정

- 그러나 우리는 정확한 모평균을 알 수 없으며, 따라서 표본평균인 1002 를 사용할 수밖에 없습니다.

$$\begin{aligned}
& \frac{1}{5}\left[(1001-1002)^{2}+(1003-1002)^{2}+(1005-1002)^{2}+(1000-1002)^{2}+(1001-1002)^{2}\right] \\
=& \frac{16}{5}=3.2
\end{aligned}$$

- 이는 전자의 모분산 추정치보다 훨씬 작은 값이며, 실제로 이러한 방식으로 취득한 모분산은 모평균과 같지 않을 때 실제보다 항상 작습니다.
  - 이는 대수적으로도 증명이 가능합니다.

> Mathematical Proof

Show that $\Sigma(\mathrm{X}-\mathrm{c})^{2}$ is a minimuum when $\mathrm{c}=\bar{X}$.

$$\begin{aligned}
&\sum(X-c)^{2} \\
&\sum\left(X^{2}-2 c X+c^{2}\right) \\
&\sum X^{2}-\sum 2 c X+\sum c^{2} \\
&\sum X^{2}-2 c \sum X+n c^{2}
\end{aligned}$$

Differentiate with respect to $\mathrm{c}$.

$$-2 \sum X+2 n c$$

Set derivative to zero and solve for $\mathrm{c}$.

$$\begin{aligned}
&-2 \sum X+2 n c=0 \\
&2 n c=2 \sum X \\
&c=\frac{2 \sum X}{2 n} \\
&c=\frac{\sum X}{n}=\bar{X}
\end{aligned}$$

> Conclusion

- 즉 항상 표본분산은 correlation 이 들어가지 않는다면 작을수밖에 없습니다! 
- 이를 보정하기 위해서, 표본분산을 조금 키워줘야 될 필요성이 생기고, 그에 따라서 n-1 로 나누게 되는 것이죠

# [Bessel's correction](#link){: .btn .btn--primary}{: .align-center}

> ## correlation

- 표본 평균은 다음과 같이 계산됩니다.

$$\bar{x}=\frac{1}{n} \sum_{i=1}^{n} x_{i}$$

- 이때 편향된(즉 correlated 되지 않은) 표본 분산은 다음과 같이 계산됩니다.

$$s_{n}^{2}=\frac{1}{n} \sum_{i=1}^{n}\left(x_{i}-\bar{x}\right)^{2}=\frac{\sum_{i=1}^{n} x_{i}^{2}}{n}-\frac{\left(\sum_{i=1}^{n} x_{i}\right)^{2}}{n^{2}}$$

- 편향되지 않은 표본 분산은 다음과 같이 작성됩니다.

$$s^{2}=\frac{1}{n-1} \sum_{i=1}^{n}\left(x_{i}-\bar{x}\right)^{2}=\frac{\sum_{i=1}^{n} x_{i}^{2}}{n-1}-\frac{\left(\sum_{i=1}^{n} x_{i}\right)^{2}}{(n-1) n}=\left(\frac{n}{n-1}\right) s_{n}^{2}$$

> ## Proof Unbased

> Proof

The expected discrepancy between the biased estimator and the true variance is

$$\begin{aligned}
\mathrm{E}\left[\sigma^{2}-s_{n}^{2}\right] &=\mathrm{E}\left[\frac{1}{n} \sum_{i=1}^{n}\left(x_{i}-\mu\right)^{2}-\frac{1}{n} \sum_{i=1}^{n}\left(x_{i}-\bar{x}\right)^{2}\right] \\
&=\mathrm{E}\left[\frac{1}{n} \sum_{i=1}^{n}\left(\left(x_{i}^{2}-2 x_{i} \mu+\mu^{2}\right)-\left(x_{i}^{2}-2 x_{i} \bar{x}+\bar{x}^{2}\right)\right)\right] \\
&=\mathrm{E}\left[\frac{1}{n} \sum_{i=1}^{n}\left(\mu^{2}-\bar{x}^{2}+2 x_{i}(\bar{x}-\mu)\right)\right] \\
&=\mathrm{E}\left[\mu^{2}-\bar{x}^{2}+\frac{1}{n} \sum_{i=1}^{n} 2 x_{i}(\bar{x}-\mu)\right] \\
&=\mathrm{E}\left[\mu^{2}-\bar{x}^{2}+2(\bar{x}-\mu) \bar{x}\right] \\
&=\mathrm{E}\left[\mu^{2}-2 \bar{x} \mu+\bar{x}^{2}\right] \\
&=\mathrm{E}\left[(\bar{x}-\mu)^{2}\right] \\
&=\mathrm{Var}(\bar{x}) \\
&=\frac{\sigma^{2}}{n}
\end{aligned}$$

So, the expected value of the biased estimator will be

$$\mathrm{E}\left[s_{n}^{2}\right]=\sigma^{2}-\frac{\sigma^{2}}{n}=\frac{n-1}{n} \sigma^{2}$$

So, an unbiased estimator should be given by

$$s^{2}=\frac{n}{n-1} s_{n}^{2}$$

---

**Reference**

- <http://www.philender.com/courses/intro/meanproof.html>
- <https://ko.wikipedia.org/wiki/%EB%B2%A0%EC%85%80_%EB%B3%B4%EC%A0%95>
- <https://en.wikipedia.org/wiki/Bessel%27s_correction>



