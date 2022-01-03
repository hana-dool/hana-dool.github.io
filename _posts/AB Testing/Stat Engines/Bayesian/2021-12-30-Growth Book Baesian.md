---
title: "Growth Book Bayesian Statistics Engine"
excerpt: "CLT 를 활용한 Bayesian Framework"
tags :
  - AB_Stat
last_modified_at: 2021-12-30

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Growth Book 에서 사용하고 있는 Bayesian AB Testing
{: .notice--warning}

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## Abstract

- A/B 테스트 분석에 접근하는 방법은 여러 가지가 있습니다. 
- Growth BOok 에서는 사람들이 A/B 테스트 결과를 볼 때 가장 흔히 갖는 세 가지 질문, 즉 "어느 버전이 더 나은가?", "얼마나 더 나은가?", "이제 결론을 내릴만큼 충분한 데이터가 있는가" 에 대한 질문에 명쾌하게 답하기 위해서 베이지안 방법론을 도입했습니다.
- 또한 이러한 질문에 답함과 동시에 AB Testing 에서 흔히 발생할 수 있는 Pitfall 인 SRM 이라던지, Fixed Horizon Peeking Problem 등의 문제를 해결하는데에도 도움을 주었습니다.

> ## The Problem

- A/B 검정 분석은 종종 카이 제곱 또는 Student T 검정과 같은 빈도주의자 가설 검정 방법을 사용합니다. 
- 이러한 접근법에는 두 가지 심각한 문제가 있습니다. 

> First Problem

- 먼저 실험을 실행하기 전에 표본 크기를 미리 결정해야 합니다. 이를 고정 지평선이라고 합니다. 
  - p - value 등의 통계적 유효성을 유지하기 위해서는 어떤 이유로든 실험을 조기에 중단할 수 없습니다.
- 하지만 이때 조기 중단을 결정할 수 있는 버튼이 없다면, 승패가 분명한 실험도 전체 기간동안 계속 실행되게 됩니다. (즉 샘플의 낭비라도고 할 수 있죠.)
- 그렇다고 조기종료를 남발하자니, Peeking Problem 이라고 하는 Pitfall 이 발생하게 됩니다. (유의수준에 도달하게 되면 바로 중지해버리는 이슈)
  - 이렇게 하면 False - Positive 의 확률이 엄청나게 늘어납니다.
- Note : Microsoft 에서는 조기종료를 주어진 기간 stamp (1일에 한번 등) 으로 제한하면 이러한 False Positive Inflation 을 크게 줄일 수 있다고 합니다. 

> Second Problem

- 빈도주의 방법의 경우 의사 결정자가 올바르게 해석하기 매우 어렵습니다.
  - P- value 가 0.05 이면 Treatment 가 Control 보다 좋을 확률이 95% 라고 잘못 가정하게 되는 경우가 많습니다.
  - 이 경우 맞는 해석은 효과가 없는 실험이 여러번 반복되었을때 이와 같은 검정통계량 값을 가지게 될 비율이 5% 라고 해석하는게 맞는 해석입니다. 
- 마찬가지로 95% 신뢰 구간에 실제 값이 포함될 확률이 95%라고 잘못 가정하게 됩니다.
  - 이는 '신뢰 구간이' 실제 모수를 포함할 확률이 95% 라는것이지, '모수' 가 신뢰 구간에 포함된다는것이 아닙니다.
  - 즉 맞는 해석은 실험이 여러번 반복되었을때, 계산된 신뢰 구간 95% 가 모수를 Cover 할 확률이 95% 라는 것입니다.

# [Bayesian Stat](#link){: .btn .btn--primary}{: .align-center}

> ## Bayesian Statsitics

- 베이지안 접근법에 의하면, 고정된 Horizon 이 없습니다.
  - 결과를 보고싶을떄마다 봐도, 추론이 정확할 수 있습니다. (이건 솔직히 통계적 관점의 차이일뿐이지 중간에 보고싶을때마다 보는게 용납되는지는 잘 모르겠음.. )
- 또한 베이즈 통계는 불확실성을 결과에 포함하기 떄문에 사람들이 해석하기가 매우 쉽습니다.
  - 즉 사람들이 생각하는 방식인 '새로운 버튼이 더 나을 확률은 95% 이다' 와 같은 해석이 가능하다는 것입니다.

> ## Posterior and Prior

- 베이지안 가설 검정은 실험을 시작하기 전에 모집단에 대해 알고 있는 것을 나타내는 사전 분포로 시작합니다. 
- Growth Book에서는 Uninformative Prior 를 사용합니다. 
  - 물론 Informative Prior 를 사용하면 실험 시간을 단축할 수 있고, 데이의 정규화에 좀 더 도움을 줍니다. 현재는 이러한 Informative Prior 를 지원하지 않지만, 나중에 추가하여 우리의 통계 엔진을 더 강력하게 만들려고 합니다.
- 실험이 실행되고 데이터가 수집되면, 사전분포가 사후분포로 업데이트 되게 됩니다.

> Binomial Metric

- Binomial Metric 의 경우 매개변수 $\alpha$ 와 $\beta$ 를 가진 메트릭을 사용하게 됩니다.
  - 물론 이때 둘다 Unif(0,1) 로 설정된 균등분포를 사용하게 됩니다.

$$P_{A} \mid X_{A} \sim \operatorname{Beta}\left(\alpha+x_{A}, \beta+n_{A}-x_{A}\right)$$

- 그 업데이트는 위와 같이 일어나게 됩니다.
  - count of converted users $x_{A}$ 
  - the total number of users $n_{A}$

> Gaussian Metrics

- Count , Duration, Revenue 와 같은 메트릭의 경우 우리는 Gaussian prior parameter $\mu_{0}, n_{0},\sigma^2_0$ 을 사용합니다. 
- 그리고 Prior 는 $\mu_{0}=0, \sigma_{0}^{2}=1, n_{0}=0$ 를 사용하게 됩니다
  - 즉 평균에 대해서 $N(0,1)$ 을 가정합니다.
- 이때 주어진 Sample Average $$\bar{X}_{A}$$ 와 Sample standard deviation $$s_{A}$$, 에 대해서 우리는 아래와 같이 Posterior Distribution 을 얻을 수 있습니다.
  - 이떄 각각의 평균은 각각의 Inverse Variance 로 Weighted Mean 이 들어가게 됩니다.

$$\mu_{A} \mid X_{A} \sim N\left(\left(\frac{n_{A}}{s^{2}{ }_{A}}+\frac{n_{0}}{\sigma_{0}^{2}}\right)^{-1}\left(\frac{n_{A}}{s_{A}^{2}} \cdot \bar{X}_{A}+\frac{n_{0}}{\sigma^{2}{ }_{0}} \cdot \mu_{0}\right),\left(\frac{n_{A}}{s_{A}^{2}}+\frac{n_{0}}{\sigma^{2}{ }_{0}}\right)^{-1}\right)$$

- 이때 위의 Update Rule 은 사실 잘 생각해보면 Normal with Known variance 일떄의 Conjugate 추정과 같다는것을 기억하세요

> ## Continuous Posterior 를 이끌어내기

- 당연히, Binomial 과 같은 경우에는 Beta Prior 가 적용되는게 너무 간단하고 명확하므로 , 여기에서는 생략하도록 하겠습니다. 
- 그러므로 Continuous Posetior 를 어떤 과정을 거쳐서 위와 같은  Form 으로 끌어내게 되었는지를 살펴봅시다!

> Fixed variance $\left(\sigma^{2}\right)$, random mean $(\mu)$ Normal Conjugates

- Assume $x_i \mid \mu \sim \mathcal{N}\left(\mu, \sigma^{2}\right)$ and $\mu \sim \mathcal{N}\left(\mu_{0}, \sigma_{0}^{2}\right) .$ Then:

$$\mu \mid x_1,x_2...x_n \sim \mathcal{N}\left(\frac{1}{\frac{1}{\sigma_{0}^{2}}+\frac{n}{\sigma^{2}}}\left(\frac{\mu_{0}}{\sigma_{0}^{2}}+\frac{\sum_{i=1}^{n} x_{i}}{\sigma^{2}}\right),\left(\frac{1}{\sigma_{0}^{2}}+\frac{n}{\sigma^{2}}\right)^{-1}\right)$$

- 즉 위와 같이, 하나의 데이터가 업데이트될떄는 위의 형태를 따릅니다. 
  - 이때, 데이터의 '평균' 을 하나의 데이터라고 가정합시다. 그러면 다음과 같습니다.

> Assume mean X has Normal Distribution (Likelihood Assumption)

- Assume $\bar{X} \mid \mu \sim \mathcal{N}\left(\mu, \sigma^{2}/n\right)$ and $\mu \sim \mathcal{N}\left(\mu_{0}, \sigma_{0}^{2}\right) .$ 

$$\mu \mid \bar{X} \sim \mathcal{N}\left(\frac{1}{\frac{1}{\sigma_{0}^{2}}+\frac{1}{\sigma^{2}/n}}\left(\frac{\mu_{0}}{\sigma_{0}^{2}}+\frac{\sum_{i=1}^{n} x_{i}}{\sigma^{2}/n}\right),\left(\frac{1}{\sigma_{0}^{2}}+\frac{1}{\sigma^{2}/n}\right)^{-1}\right)$$

- 즉 , 위의 경우, 정리하면 아래와 같습니다.
- Assume $\bar{X_A} \mid \mu \sim \mathcal{N}\left(\mu, \sigma^{2}/n_A\right)$ and $\mu \sim \mathcal{N}\left(\mu_{0}, \sigma_{0}^{2}\right) .$

$$\mu \mid \bar{X_A} \sim \mathcal{N}\left(\left(\frac{1}{\sigma_{0}^{2}}+\frac{n_A}{\sigma^{2}}\right)^{-1}\left(\frac{\mu_{0}}{\sigma_{0}^{2}}+\frac{n_A}{\sigma^{2}}\bar{X_A}\right),\left(\frac{1}{\sigma_{0}^{2}}+\frac{n_A}{\sigma^{2}}\right)^{-1}\right)$$

- 위에서, data $X_A$ 가 따르는 Variance 인 경우 Fixed Variance , 즉 우리가 가정하는 값이므로 $s_a$ 로 추정하게 하고, 고치면 아래와 같습니다.

- Assume $\bar{X_A} \mid \mu \sim \mathcal{N}\left(\mu, s_A^{2}/n_A\right)$ and $\mu \sim \mathcal{N}\left(\mu_{0}, \sigma_{0}^{2}\right) .$

$$\mu \mid \bar{X_A} \sim \mathcal{N}\left(\left(\frac{1}{\sigma_{0}^{2}}+\frac{n_A}{s_A^{2}}\right)^{-1}\left(\frac{\mu_{0}}{\sigma_{0}^{2}}+\frac{n_A}{s_A^{2}}\bar{X_A}\right),\left(\frac{1}{\sigma_{0}^{2}}+\frac{n_A}{s_A^{2}}\right)^{-1}\right)$$

> what is $n_0$

- 이 경우, Growth Book 에서는 $n_0$ 을 설정하는데요, 이 값은 어떤것을 의미할까요? 
  - 이 값은 바로 prior 의 강도를 나타냅니다. 

- Assume $\bar{X_A} \mid \mu \sim \mathcal{N}\left(\mu, s_A^{2}/n_A\right)$ and $\mu \sim \mathcal{N}\left(\mu_{0}, \sigma_{0}^{2}/n_0\right)$ 

$$\mu \mid \bar{X_A} \sim \mathcal{N}\left(\left(\frac{n_0}{\sigma_{0}^{2}}+\frac{n_A}{s_A^{2}}\right)^{-1}\left(\frac{n_0}{\sigma_{0}^{2}}\mu_{0}+\frac{n_A}{s_A^{2}}\bar{X_A}\right),\left(\frac{n_0}{\sigma_{0}^{2}}+\frac{n_A}{s_A^{2}}\right)^{-1}\right)$$

- 즉 위와 같이 Growth Book 에서 설명하고 있는 Prior 와 완전히 같은 Prior 를 이끌어 내었습니다. 
- prior 는 쉽게 말해서 데이터의 갯수가 $n_0$ 개일때에 Sample mean 에 대한 prior 를 나타내게 됩니다. 

> ## Comparison with Freq 

- 위의 분포를 잘 살펴봅시다. 

$$\mu \mid \bar{X_A} \sim \mathcal{N}\left(\left(\frac{n_0}{\sigma_{0}^{2}}+\frac{n_A}{s_A^{2}}\right)^{-1}\left(\frac{n_0}{\sigma_{0}^{2}}\mu_{0}+\frac{n_A}{s_A^{2}}\bar{X_A}\right),\left(\frac{n_0}{\sigma_{0}^{2}}+\frac{n_A}{s_A^{2}}\right)^{-1}\right)$$

- 위에서 Prior 는 $\mu_{0}=0, \sigma_{0}^{2}=1, n_{0}=0$ 를 사용한다는것을 명심합시다. (사실 어느정도 작은 분포를 사용하게 되더라도, Large sample 에서는 데이터가 Dominant 하게 되므로 무시할 수 있습니다.)

$$\mu \mid \bar{X_A} \sim \mathcal{N}\left(\left(\frac{n_A}{s_A^{2}}\right)^{-1}\left(\frac{n_A}{s_A^{2}}\bar{X_A}\right),\left(\frac{n_A}{s_A^{2}}\right)^{-1}\right)$$

- 즉 정리하면 아래와 같습니다.

$$\mu \mid \bar{X_A} \sim \mathcal{N}\left(\bar{X_A},\frac{s_A^{2}}{n_A}\right)$$

- 앗..? 이는 바로 CLT와 똑같아 보이지 않나요? 

> Central Limmit Theorem

$$\sqrt{n}\left(\left(\frac{1}{n} \sum_{i=1}^{n} X_{i}\right)-\mu\right) \stackrel{d}{\rightarrow} \mathcal{N}\left(0, \sigma^{2}\right)$$

- 위의 분포의 경우 , 정리하면 (물론 위이 정리가 Approximation 을 의미하므로 n 을 오른쪽으로 옮기는것은 안되지만, 충분히 큰 n 에 대해서 Normal 을 따르고 있다고 가정한 뒤에 옮겨볼게요)

$$\bar{X} \sim \mathcal{N}(\mu,\frac{\sigma^2}{n})$$

- 즉, 우리가 T-test 를 수행할떄에는 위의 $\sigma$ 를 표본표준편차 $s$ 라고 가정하게 되므로 정리하면 아래와 같습니다.

$$\bar{X_A} \sim \mathcal{N}(\mu,\frac{s_A^2}{n_A})$$

- 그렇습니다! 위와 같은 방법을 사용한다고는 하지만, 결국에 CLT 와 같은 방법론을 사용하는것과 비슷하죠.
  - 이는 Bayesian 의 Born-mises thm 과도 연결됩니다. (Bayesian CLT 에 대해서는 나중에 더 알아보도록 해요..)

> ## Justification

- 아마 특정한 메트릭 (수익, 체류시간 등) 은 Gaussian Distribution 을 따르지 않기 때문에, 일반적으로 Likelihood 를 명시해야 하는 Bayesian 방법론의 경우 잘 계산되지 않습니다.
- 하지만 다행히 중심극한정리 (CLT) 의 경우는 데이터 자체가 아니라 표본 평균의 분포를 다루기 떄문에 , 메트릭의 생김새와는 상관없이 대부분 표본평균의 likelihood 는 Normal 임이 성립하게 됩니다.
- 그러므로 위와 같이 평균 메트릭에 대해서 Likelihood 를 Normal 로 정의하고 그 Conjugate 를 이끌어낼 수 있습니다.

> Note

- 이때 극도로 치우처진 분포의 경우, (Exponential 등) 사이트의 트래픽을 사용하더라도 CLT 가 작동하지 않을 수 있습니다.
  - 이 경우 metric 에 대해서 capping 을 지원합니다. 
- 즉 일반적으로 주문값이 5달러이지만, 10만 달러와 같은 주문의 경우에는 Filtering 한 이후에 분석할 수 있습니다. 
  - 이러한 Capping 과 같이 Continuous 지표를 사용하게 되면, 모든 연속분포 메트릭에 대해서 CLT 를 성립하게 할 수 있습니다.

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

- AB Test 의 결과를 살펴볼때에는, 늘 다음과 같은 3개의 궁금증이 떠오르게 됩니다.

1. 어떤 버젼이 더 좋을까?
2. 얼마나 더 좋을까?
3. 내가 지금 테스트를 하기에 충분한 데이터가 있을까?

> ## Which version is better? : Binomial

- 이길 확률을 계산하기 위해서 제일 쉬운 방법은 역시나 Montecarlo Simulation 일 것입니다.
  - 하지만! Wix.com 에서는 수백가지의 A/B 테스트를 진행하고 각각의 A/B Testing 은 수천개의 KPI  가 있습니다. 그러므로 모든것을 계산해내기가 Computational COst 가 엄청 큰것이죠.
- 이럴때에 수행할 수 있는 방법은 바로 아래 두가지 방법을 쓸 수 있을것입니다.
  - [Gaussian Quadratures](https://en.wikipedia.org/wiki/Gaussian_quadrature) 
  - [Central Limit Theorem](https://en.wikipedia.org/wiki/Central_limit_theorem) (이 방법을 이용해 beta 분포에 대해서 Approximation 을 진행)
- Beta 분포의 경우, 샘플 수가 커지면 Normal 로 Approximation 한다는것이 증명되어 있습니다. 그러므로 이를 이용해서 검정을 할 수 있습니다.
- 이, 질문에 답하기 위해서, 우리는 다음과 같이 2개의 분포를 생각합니다.
  -  Distribution $D_1$ 을 두개 Variant 의 차이로 정의합시다. 즉 $\left(P_{B}-P_{A}\right)$ 로 정의합니다. 이 경우에는 상대적인 Difference 를 비교할떄 쓰입니다.
  - Distribution $D_2$ 를 두개 Variant 의 log 비율로 정의합니다. 즉 log $P_B/P_A$ 이 경우는 상대적인 Relative Uplift 를 비교할때에 쓰입니다.
- 이때, 각각이 따르는 분포는 아래와 같습니다. 

> Eq. 4: CLT approximation of the difference and ratio between two Beta random variables

$$
D_{1}=P_{B}-P_{A} \mid X \sim \mathcal{N}\left(E\left[P_{B} \mid X_{B}\right]-E\left[P_{A} \mid X_{A}\right], \operatorname{Var}\left(P_{A} \mid X_{A}\right)+\operatorname{Var}\left(P_{B} \mid X_{B}\right)\right)
$$

$$
D_{2}=\ln \frac{P_{B}}{P_{A}} \mid X \dot{\mathcal{N}}\left(E\left[\ln P_{B} \mid X_{B}\right]-E\left[\ln P_{A} \mid X_{A}\right], \operatorname{Var}\left(\ln P_{A} \mid X_{A}\right)+\operatorname{Var}\left(\ln P_{B} \mid X_{B}\right)\right)
$$

- To complete the formulas above, we denote the [digamma function](https://en.wikipedia.org/wiki/Digamma_function) and the first [polygamma function](https://en.wikipedia.org/wiki/Polygamma_function) with *ψ* and *ψ*₁ respectively. You don’t really need to know what they do, just where to find them in SciPy! The equations below are simply copied from Wikipedia:

> Eq. 5: Moments of a Beta variable and it’s logarithm, taken from Wikipedia

$$
\begin{aligned}
\alpha_{A} &=\alpha+x_{A} \\
\beta_{A} &=\beta+n_{A}-x_{A} \\
E\left[P_{A} \mid X_{A}\right] &=\frac{\alpha_{A}}{\alpha_{A}+\beta_{A}} \\
\operatorname{Var}\left(P_{A} \mid X_{A}\right) & \approx \frac{\alpha_{A} \beta_{A}}{\left(\alpha_{A}+\beta_{A}\right)^{3}} \\
E\left[\ln P_{A} \mid X_{A}\right] &=\psi\left(\alpha_{A}\right)-\psi\left(\alpha_{A}+\beta_{A}\right) \\
\operatorname{Var}\left(\ln P_{A} \mid X_{A}\right) &=\psi_{1}\left(\alpha_{A}\right)-\psi_{1}\left(\alpha_{A}+\beta_{A}\right)
\end{aligned}
$$

- Using these formulas, we can easily calculate the probability B is better with *P(D₁ > 0)*, and the Credibility Interval with the quantiles of *D₁* or *D₂:*

```python
from scipy.stats import norm, beta
from scipy.special import digamma, polygamma

log_beta_mean = lambda a, b: digamma(a) - digamma(a + b)
var_beta_mean = lambda a, b: polygamma(1, a) - polygamma(1, a + b)


d1_beta = norm(loc=beta.mean(alpha_b, beta_b) - beta.mean(alpha_a, beta_a),
               scale=np.sqrt(beta.var(alpha_a, beta_a) + beta.var(alpha_b, beta_b)))
d2_beta = norm(loc=log_beta_mean(alpha_b, beta_b) - log_beta_mean(alpha_a, beta_a),
               scale=np.sqrt(var_beta_mean(alpha_a, beta_a) + var_beta_mean(alpha_b, beta_b)))


print(f'The probability the conversion in B is higher is {d1_beta.sf(0)}')
# >>> The probability the conversion in B is higher is 0.9040503042127781

print(f'The 95% crediblity interval of (p_b/p_a-1) is {np.exp(d2_beta.ppf((.025, .975))) - 1}')
# >>> The 95% crediblity interval of (p_b/p_a-1) is [-0.0489547   0.28350359]
```

> ## Which version is better? : Normal

- For the Normal-Normal case, *D₁* is pretty [straightforward](https://en.wikipedia.org/wiki/Normal_distribution#Operations_on_two_independent_normal_variables). But what if we want to use the relative difference instead? We’ve decided to use the [Delta method](https://en.wikipedia.org/wiki/Delta_method) to find the approximate distribution of *ln μᴀ*. Now you might be thinking — how the heck can I take the logarithm of a Gaussian random variable? And (again) you’ll be completely right — the Gaussian distribution’ support includes negative numbers and its logarithm isn’t properly defined. But (again) with a sample size of tens of thousands, it’s a “good enough” approximation as *μᴀ*’s distribution is “pretty far away” from 0.

> Eq. 6: Distribution of the difference between two Gaussian variables, and the approximate distribution of their ratio found with the Delta method.

$$
D_{1}=\mu_{B}-\mu_{A} \mid X  \sim \dot{\mathcal{N}}\left(E\left[\mu_{B} \mid X_{B}\right]-E\left[\mu_{A} \mid X_{A}\right], \operatorname{Var}\left(\mu_{A} \mid X_{A}\right)+\operatorname{Var}\left(\mu_{B} \mid X_{B}\right)\right)
$$

$$
D_{2}=\ln \frac{\mu_{B}}{\mu_{A}} \mid X \dot \sim N\left(\ln E\left[\mu_{B} \mid X_{B}\right]-\ln E\left[\mu_{A} \mid X_{A}\right], \frac{\operatorname{Var}\left(\mu_{A} \mid X_{A}\right)}{E^{2}\left[\mu_{A} \mid X_{A}\right]}+\frac{\operatorname{Var}\left(\mu_{B} \mid X_{B}\right)}{E^{2}\left[\mu_{B} \mid X_{B}\right]}\right)
$$

```python
d1_norm = norm(loc=mu_b - mu_a,
               scale=np.sqrt(sd_a ** 2 + sd_b ** 2))
d2_norm = norm(loc=np.log(mu_b) - np.log(mu_a),
               scale=np.sqrt((sd_a / mu_a)**2 + (sd_b / mu_b)**2))


print(f'The probability the average income in B is 2% lower (or worse) is {d2_norm.cdf(np.log(.98))}')
# >>> The probability the average income in B is 2% lower (or worse) is 0.00011622384023304196

print(f'The 95% crediblity interval of (m_b - m_a) is {d1_norm.ppf((.025, .975))}')
# >>> The 95% crediblity interval of (m_b - m_a) is [-0.04834271  1.94494332]
```

> ## Calculating Risk

- Now we have finally arrived to the important part: The Risk measure is the most important measure in Bayesian A/B testing. It replaces the P-value as a [decision rule](https://en.wikipedia.org/wiki/Decision_rule), but also serves as a [stopping rule](https://en.wikipedia.org/wiki/Stopping_time) — since the Bayesian A/B test has a dynamic sample size.
- It is interpreted as “When B is worse than A, If I choose B, how many conversions am I expected to lose?”, and formally, it is defined as

> Eq. 7: Formal definition of the Risk in a Bayesian A/B test

$$
\begin{aligned}
\mathcal{R}_{B} &=E\left[\max \left\{P_{A}-P_{B}, 0\right\} \mid X\right] \\
&=E\left[\left(P_{A}-P_{B}\right) \cdot 1_{\left\{P_{A}>P_{B}\right\}} \mid X\right] \\
&=\int_{0}^{1} \int_{0}^{p_{A}}\left(p_{A}-p_{B}\right) f\left(P_{A}=p_{A}, P_{B}=p_{B} \mid X\right) d p_{B} d p_{A}
\end{aligned}
$$

- with **1** as an indicator function. Notice the integral on the third line — I really hate that integral! It doesn’t have an analytical solution, and **we can’t approximate it with the CLT**. But as I previously mentioned, Monte-Carlo simulations are NOT an option for us. So what did we do?

> Gaussian Quadratures

- [Gaussian quadratures](https://en.wikipedia.org/wiki/Gaussian_quadrature) (GQ) are a cool way of approximating integrals with a weighted sum of a small number of nodes. The nodes and weights are calculated by the GQ algorithm. Formally, we find *n* nodes (*x*) and weights (*w*) that best approximate the integral of *g* with a summation:

> Eq. 8: A Gaussian quadrature approximates an integral with a weighted sum of selected nodes. *-∞ ≤ a < b ≤ +*∞

$$
\int_{a}^{b} g(x) d x \approx \sum_{i=1}^{n} g\left(x_{i}\right) w_{i}
$$

- As we saw earlier, the Risk metric is an integral — so we can try to approximate it with a GQ. First, let’s simplify it’s expression:

$$
\begin{aligned}
E\left[\left(P_{A}-P_{B}\right) \cdot 1_{\left\{P_{A}>P_{B}\right\}} \mid X\right] &=E\left[P_{A} \cdot \mathbf{1}_{\left\{P_{A}>P_{B}\right\}} \mid X\right]-E\left[P_{B} \cdot\left(1-\mathbf{1}_{\left\{P_{B}>P_{A}\right\}}\right) \mid X\right] \\
&=E\left[P_{A} \cdot \mathbf{1}_{\left\{P_{B}<P_{A}\right\}} \mid X\right]+E\left[P_{B} \cdot \mathbf{1}_{\left\{P_{A}<P_{B}\right\}} \mid X\right]-E\left[P_{B} \mid X\right]
\end{aligned}
$$

$$
\begin{aligned}
E\left[P_{A} \cdot \mathbf{1}_{\left\{P_{B}<P_{A}\right\}} \mid X\right] &=E\left[E\left[P_{A} \cdot \mathbf{1}_{\left\{P_{B}<P_{A}\right\}} \mid P_{A}\right] \mid X\right] \\
&=E\left[P_{A} \cdot P\left(P_{B}<P_{A}\right) \mid X\right] \\
&=\int_{0}^{1} u \cdot P\left(P_{B}<u \mid X\right) \cdot f\left(P_{A}=u \mid X\right) d u \\
&=: \xi_{A}
\end{aligned}
$$

- Now $\xi_{A}$ is an integral we can approximate with a Gaussian quadrature! We can accurately calculate the Risk with about 20 nodes, instead of thousands in a Monte-Carlo simulation:

$$
\mathcal{R}_{B}=\xi_{A}+\xi_{B}-E\left[P_{B}\right]
$$

- We implemented this approximation using [scipy.special.roots_hermitnorm](https://docs.scipy.org/doc/scipy/reference/generated/scipy.special.roots_hermitenorm.html) and a work-around over [scipy.special.roots_sh_jacobi](https://docs.scipy.org/doc/scipy/reference/generated/scipy.special.roots_sh_jacobi.html) (more on the work-around in my notes). This isn’t *very* fast, but it’s the fastest way we found.

```python
from scipy.special import roots_hermitenorm  # , roots_sh_jacobi
from orthogonal import roots_sh_jacobi


# The following throws an integer overflow error 
# if using scipy when a + b are too large
# Use the log trick instead (see my PR at scipy / walk around in repo)
def beta_gq(n, a, b):
    x, w, m = roots_sh_jacobi(n, a + b - 1, a, True)
    w /= m
    return x, w


nodes_a, weights_a = beta_gq(24, alpha_a, beta_a)
nodes_b, weights_b = beta_gq(24, alpha_b, beta_b)

gq = sum(nodes_a * beta.cdf(nodes_a, alpha_b, beta_b) * weights_a) + \
     sum(nodes_b * beta.cdf(nodes_b, alpha_a, beta_a) * weights_b)
risk_beta = gq - beta.mean((alpha_a, alpha_b), (beta_a, beta_b))

print(f'The risk of choosing A is losing {risk_beta[0]} conversions per user.\n'
      f'The risk of choosing B is losing {risk_beta[1]} conversions per user.')
# >>> The risk of choosing A is losing 0.021472801833822552 conversions per user.
# >>> The risk of choosing B is losing 0.0007175909729974506 conversions per user.


def norm_gq(n, loc, scale):
    x, w, m = roots_hermitenorm(n, True)
    x = scale * x + loc
    w /= m
    return x, w


nodes_a, weights_a = norm_gq(24, mu_a, sd_a)
nodes_b, weights_b = norm_gq(24, mu_b, sd_b)

gq = sum(nodes_a * norm.cdf(nodes_a, mu_b, sd_b) * weights_a) + \
     sum(nodes_b * norm.cdf(nodes_b, mu_a, sd_a) * weights_b)
risk_norm = gq - norm.mean((mu_a, mu_b))

print(f'The risk of choosing A is losing {risk_norm[0]}$ per user.\n'
      f'The risk of choosing B is losing {risk_norm[1]}$ per user.')
# >>> The risk of choosing A is losing 0.9544550905343314$ per user.
# >>> The risk of choosing B is losing 0.006154785995697409$ per user.
```

# Summary

The mathematics and programming in Bayesian A/B testing are a bit more challenging than in the Frequentist framework. However, as I argued in [my previous post](https://towardsdatascience.com/why-you-should-switch-to-bayesian-a-b-testing-364557e0af1a), I think it is worth it. Although it is more computationally expensive, the added clarity and interpretability of the A/B test gives an enormous value for anyone who uses them.

In this post, I reviewed the basics of the Beta-Binomial and Normal-Normal models for Bayesian A/B testing, and presented some of the approximations we implemented at Wix.com. While these approximations may not be 100% accurate, they are “good enough” when experiments have thousands of users, and they allowed us to support Bayesian A/B testing on a large scale.

This post focused on how to calculate Bayesian metric of an A/B test, and not on how to analyze it or when to stop it. If you want to read more on those issues, the posts in my references give an excellent overview.
