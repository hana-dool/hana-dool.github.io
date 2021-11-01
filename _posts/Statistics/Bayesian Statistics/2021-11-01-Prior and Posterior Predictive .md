---
title:  "Prior,Posterior Predictive Distributions"
excerpt: "Prior 과 Posterior 의 예측분포"
categories:
  - Bayes
last_modified_at: 2021-11-01

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 MLE 와 MAP 는 같은 Pointer estimator 를 돌려준다는 매우 닮았습니다. 이 둘의 차이는 뭔지에 대해서 알아봅시다.
{: .notice--warning}

# [Prior and Posterior Predictive](#link){: .btn .btn--primary}{: .align-center}

> ## Oberserved Case

- Prior distribution ($p(\theta)$) 는 데이터를 알기 전의 분포입니다.
- Posterior distribution ($p(\theta \mid y)$) 는 데이터를 알고 난 후의 분포입니다. 

> ## Unobserved Case

- Unobserved data ($\tilde{y}$) 에 대해서 예측하는 경우에 대해서 생각해 봅시다. 

> Prior Predictive Distribution

- Prior predictive 란, 우리가 사전에 가지고 있는 믿음에 근거하여 예측값을 생성하는 것입니다.

$$p(\tilde{y}) = \int p(\tilde{y}, \theta) d\theta = \int p( \tilde{y}| \theta) \times p(\theta) d\theta$$

> Posterior Predictive Distribution

- Posterior Predictive 란 업데이트 된 믿음에 근거하여 예측값을 생성하는 것입니다.

$$p(\tilde{y}| y) = \int p(\tilde{y}, \theta | y) d\theta = \int p( \tilde{y}| \theta, y) \times p(\theta| y) d\theta$$

- 일반적으로 $y$ 와 $\tilde{y}$ 는 iid (독립) 이라고 가정하기 때문에 이를 Bayes rule 로 전개하게 되면 다음과 같이 정의됩니다.

$$p(\tilde{y}| y) = \int p(\tilde{y}, \theta | y) d\theta = \int p( \tilde{y}| \theta) \times p(\theta| y) d\theta$$

> ## Example (prior predictive)

시행횟수가 10인 이항분포를 따르는 확률 변수 X가 있다. 이항분포의 모수가 균일분포을 따를 때, 확률 변수 X의 사전예측분포를 구하여라.

- Prior:

$$
f(\theta)=I_{\{0 \leq \theta \leq 1\}}
$$
- Liklihood:

$$
f(x \mid \theta)=\frac{10 !}{x !(10-x) !} \theta^{x}(1-\theta)^{10-x}
$$
- Prior predictive distribution:

$$\begin{aligned}
&f(x)=\int_{0}^{1} f(x \mid \theta) f(\theta) d \theta=\int_{0}^{1} \frac{10 !}{x !(10-x) !} \theta^{x}(1-\theta)^{10-x}(1) d \theta \\
&=\int_{0}^{1} \frac{\Gamma(11)}{\Gamma(x+1) \Gamma(11-x)} \theta^{x}(1-\theta)^{10-x} d \theta \\
&=\frac{\Gamma(11)}{\Gamma(12)} \int_{0}^{1} \frac{\Gamma(12)}{\Gamma(x+1) \Gamma(11-x)} \theta^{(x+1)-1}(1-\theta)^{(11-x)-1} d \theta \\
&=\frac{\Gamma(11)}{\Gamma(12)}(1)=\frac{1}{11}
\end{aligned}$$

> ## Example (Posterior Predictive)

동전을 던졌을 때, 앞면이 나올 확률이 균일분포를 따른다. 동전을 던졌더니 앞면이 나왔을 때, 이 결과를 이용하여 사후예측분포를 구하여라. 이때, 각 시행은 독립적이다.

- Prior:

$$
f(\theta)=I_{\{0 \leq \theta \leq 1\}}
$$
- Liklihood:

$$
f(x \mid \theta)=\theta^{x}(1-\theta)^{1-x}
$$
- Posterior predictive distribution:

$$
\begin{aligned}
&f\left(x \mid X_{1}=1\right)=\int_{0}^{1} f\left(x \mid X_{1}=1, \theta\right) f\left(\theta \mid X_{1}=1\right) d \theta \\
&=\int_{0}^{1} f(x \mid \theta) f\left(\theta \mid X_{1}=1\right) d \theta \\
&=\int_{0}^{1} f(x \mid \theta)(2 \theta) d \theta \\
&=\int_{0}^{1} \theta^{x}(1-\theta)^{1-x}(2 \theta) d \theta
\end{aligned}
$$
$$
\begin{aligned}
&f\left(X_{2}=1 \mid X_{1}=1\right)=\int_{0}^{1} 2 \theta^{2} d \theta=\frac{2}{3} \\
&f\left(X_{2}=0 \mid X_{1}=1\right)=\frac{1}{3}
\end{aligned}
$$

> ## difference with Freq

- Freq 방법론에서의 예측과 베이즈에서의 예측은 위의 식을 볼떄에 매우 다릅니다.

> Freq

- 일반적으로 Freq 방법론은 'MLE' 를 통해 모수를 고정한 다음 분포에서 예측값을 형성합니다.
- 즉 $\tilde{y} \sim f(y,\hat{\theta})$ 을 이용하여 $x_{new}$ 를 우리의 예측이라고 정하게 되죠. 

> Bayes

- 그에 반해 베이즈 방법론은 $$p(\tilde{y}| y) = \int p(\tilde{y}, \theta | y) d\theta = \int p( \tilde{y}| \theta, y) \times p(\theta| y) d\theta$$ 와 같이 추정합니다.
- 이는 '모든 가능도' 에 대해서 적분한 것으로, MLE 는 '최대한 그럴듯한 모수에 대한 단면의 예측' 인 반면에 베이즈는 '모수의 분포를 모~두 고려하여 예측' 한 것에서 차이가 있다고 볼 수 있을것입니다.

**reference**

- <https://donghwa-kim.github.io/Pred_-baye.html>
- <https://rooney-song.tistory.com/9>

위와  
{: .notice--success}

