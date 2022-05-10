---
title: "Calculate Sample Size"
excerpt: "샘플 사이즈를 계산하는 공식"
tags:
  - AB_Stat
last_modified_at: 2021-12-13

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../../hana-dool.github.io
---

A/B Testing 에서 샘플 사이즈를 계산하는 공식
{: .notice--warning}

# [One Sample mean Test  and Power](#link){: .btn .btn--primary}{: .align-center}

> ## Power Calculation $$H_{0}: \mu=\mu_{0} \quad vs \quad H_{1}: \mu<\mu_{0}$$

- Hypothesis 가 아래와 같이 정의한다고 합시다.

$$H_{0}: \mu=\mu_{0} \quad vs \quad H_{1}: \mu<\mu_{0}$$

- Power 의 이때 Power 의 계산은 , $H_1$ 이 맞을때, $H_0$ 을 기각할 확률입니다. 즉 이때 실제 $H_1 $ 이 맞아서 $\mu = \mu_1$ 이라고 합시다. 그러면 power 는 아래와 같이 계산됩니다.

$$\begin{aligned} \text { Power } 
&=\operatorname{Pr}\left(\text { reject } H_{0} \mid H_{0} \text { false }\right)\\
&=\operatorname{Pr}\left(Z<z_{\alpha} \mid \mu=\mu_{1}\right) \\ 
&=\operatorname{Pr}\left(\frac{\bar{X}-\mu_{0}}{\sigma / \sqrt{n}}<z_{\alpha} \mid \mu=\mu_{1}\right) \\ 
&=\operatorname{Pr}\left(\bar{X}<\mu_{0}+z_{\alpha} \sigma / \sqrt{n} \mid \mu=\mu_{1}\right) \end{aligned}$$

- under $H_{1}$ 하에서는 $ \bar{X} \sim N\left(\mu_{1}, \sigma^{2} / n\right)$ 라는것을 알고 있습니다. 그러므로 Power 의 계산은 아래와 같이 이루어집니다.

$$\begin{aligned}
\text { Power }
&=\operatorname{Pr}\left(\bar{X}<\mu_{0}+z_{\alpha} \sigma / \sqrt{n} \mid \mu=\mu_{1}\right)\\ &=\operatorname{Pr}\left((\bar{X}-\mu_1)/(\sigma/\sqrt{n})<(\mu_{0}+z_{\alpha} \sigma / \sqrt{n} -\mu_1)/(\sigma/\sqrt{n}) \mid \mu=\mu_{1}\right)\\ 
&=\operatorname{Pr}\left(Z<(\mu_{0}+z_{\alpha} \sigma / \sqrt{n} -\mu_1)/(\sigma/\sqrt{n}) \right)\\ 
&=\Phi\left[\left(\mu_{0}+z_{\alpha} \sigma / \sqrt{n}-\mu_{1}\right) /(\sigma / \sqrt{n})\right]\\
&=\Phi\left[z_{\alpha}+\frac{\left(\mu_{0}-\mu_{1}\right)}{\sigma} \sqrt{n}\right]
\end{aligned}$$

- 즉 One Sample Z Test 의 경우, one - sided Test 라면 위처럼 Power 가 계산되게 됩니다. 

> Note

![jpg](/assets/images/Stat/132_1.jpg) 

-  $\mu_{0}+z_{\alpha} \sigma / \sqrt{n}$ under the $H_{0}$ distribution 일때에, 오른쪽 면적은 Alpha (1종 오류) 가 됩니다.
-  $\mu_{0}+z_{\alpha} \sigma / \sqrt{n}$ under the $H_{1}$ distribution 일때 오른쪽 면적은  power $=1-\beta$. 가 됩니다.

> ## Power Calculation $$H_{0}: \mu=\mu_{0} \quad vs \quad H_{1}: \mu>\mu_{0}$$

- Hypothesis 가 아래와 같이 정의한다고 합시다.

$$H_{0}: \mu=\mu_{0} \quad vs \quad H_{1}: \mu>\mu_{0}$$

- Power 의 이때 Power 의 계산은 , $H_1$ 이 맞을때, $H_0$ 을 기각할 확률입니다. 즉 이때 실제 $H_1 $ 이 맞아서 $\mu = \mu_1$ 이라고 합시다. 그러면 power 는 아래와 같이 계산됩니다.

$$\begin{aligned} \text { Power } 
&=\operatorname{Pr}\left(\text { reject } H_{0} \mid H_{0} \text { false }\right)\\
&=\operatorname{Pr}\left(Z>z_{1-\alpha} \mid \mu=\mu_{1}\right) \\ 
&=\operatorname{Pr}\left(\frac{\bar{X}-\mu_{0}}{\sigma / \sqrt{n}}>z_{1-\alpha} \mid \mu=\mu_{1}\right) \\ 
&=\operatorname{Pr}\left(\bar{X}>\mu_{0}+z_{1-\alpha} \sigma / \sqrt{n} \mid \mu=\mu_{1}\right) \end{aligned}$$

- under $H_{1}$ 하에서는 $ \bar{X} \sim N\left(\mu_{1}, \sigma^{2} / n\right)$ 라는것을 알고 있습니다. 그러므로 Power 의 계산은 아래와 같이 이루어집니다.

$$\begin{aligned}
\text { Power }
&=\operatorname{Pr}\left(\bar{X}>\mu_{0}+z_{1-\alpha} \sigma / \sqrt{n} \mid \mu=\mu_{1}\right)\\ &=\operatorname{Pr}\left((\bar{X}-\mu_1)/(\sigma/\sqrt{n})>(\mu_{0}+z_{1-\alpha} \sigma / \sqrt{n} -\mu_1)/(\sigma/\sqrt{n}) \mid \mu=\mu_{1}\right)\\ 
&=\operatorname{Pr}\left(Z>(\mu_{0}+z_{1-\alpha} \sigma / \sqrt{n} -\mu_1)/(\sigma/\sqrt{n}) \right)\\ 
&=1-\Phi\left[\left(\mu_{0}+z_{1-\alpha} \sigma / \sqrt{n}-\mu_{1}\right) /(\sigma / \sqrt{n})\right]\\
&=1-\Phi\left[z_{1-\alpha}+\frac{\left(\mu_{0}-\mu_{1}\right)}{\sigma} \sqrt{n}\right]
\end{aligned}$$

- 이떄 $\Phi(-x)=1-\Phi(x)$ and $z_{\alpha}=-z_{1-\alpha}$ 의 조건을 이용한다면, if $\mu_{1}>\mu_{0}$ 일때

$$\begin{aligned}
\text { Power }
&=\Phi\left[-z_{1-\alpha}+\frac{\left(\mu_{1}-\mu_{0}\right) \sqrt{n}}{\sigma}\right]\\
&=\Phi\left[z_{\alpha}+\frac{\left(\mu_{1}-\mu_{0}\right) \sqrt{n}}{\sigma}\right]
\end{aligned}$$

> Note

![jpg](/assets/images/Stat/132_2.jpg) 

- 위처럼 계산됩니다.

> ## Power Calculation $$H_{0}: \mu=\mu_{0} \quad vs \quad H_{1}: \mu=\mu_{1}$$

- 이 증명은 , 위에서 2가지 방향으로 진행합니다. 

- The power of the test for the hypothesis

$$H_{0}: \mu=\mu_{0} \quad \text { vs. } \quad H_{1}: \mu=\mu_{1}$$

- where the underlying distribution is normal and the population variance $\left(\sigma^{2}\right)$ is assumed known is given by

$$\Phi\left(z_{\alpha}+\left|\mu_{0}-\mu_{1}\right| \sqrt{n} / \sigma\right)=\Phi\left(-z_{1-\alpha}+\left|\mu_{0}-\mu_{1}\right| \sqrt{n} / \sigma\right)$$

- 즉 우리는 위의 식에서 다음과 같이, Power 에 영향을 끼치는것들을 짐작할 수 있습이다.

> Factor Affecting the Power

- (1) If the significance level is made smaller ( $\alpha$ decreases), $z_{\alpha}$ increases and hence the power decreases.
- (2) If the alternative mean is shifted farther away from the null mean $\left(\mid \mu_{0}-\mu_{1}\mid \right.$ increases), then the power increases.
- (3) If the standard deviation of the distribution of individual observations increases ( $\sigma$ increases), then the power decreases.
- (4) If the sample size increases ( $n$ increases), then the power increases.

> ## Power Calculation $$H_{0}: \mu=\mu_{0} \quad vs \quad H_{1}: \mu\not=\mu_{1}$$

- The power of the two-sided test $H_{0}: \mu=\mu_{0}$ vs. $H_{1}: \mu \neq \mu_{0}$ for the specific alternative $\mu=\mu_{1}$, where the underlying distribution is normal and the population variance $\left(\sigma^{2}\right)$ is assumed known, is given exactly by

$$\Phi\left[-Z_{1-\alpha / 2}+\frac{\left(\mu_{0}-\mu_{1}\right) \sqrt{n}}{\sigma}\right]+\Phi\left[-Z_{1-\alpha / 2}+\frac{\left(\mu_{1}-\mu_{0}\right) \sqrt{n}}{\sigma}\right]$$

- and approximately by

$$\Phi\left[-z_{1-\alpha / 2}+\frac{\left|\mu_{0}-\mu_{1}\right| \sqrt{n}}{\sigma}\right]$$

> Proof

- 이때 Two Sided Test 이므로, 양측검정이 되어야 합니다. 즉 

$$z=\frac{\bar{x}-\mu_{0}}{\sigma / \sqrt{n}}<z_{\alpha / 2} \quad \text { or } \quad z=\frac{\bar{x}-\mu_{0}}{\sigma / \sqrt{n}}>z_{1-\alpha / 2}$$

- 이를 다시 정리하면 아래와 같습니다.

$$\bar{x}<\mu_{0}+z_{\alpha / 2} \sigma / \sqrt{n} \quad \text { or } \quad \bar{x}>\mu_{0}+z_{1-\alpha / 2} \sigma / \sqrt{n}$$

- 이를 이용해 Power Calculation 을 해보겠습니다

$$\begin{aligned}
\text { Power } &=\operatorname{Pr}\left(\bar{X}<\mu_{0}+z_{\alpha / 2} \sigma / \sqrt{n} \mid \mu=\mu_{1}\right)+\operatorname{Pr}\left(\bar{X}>\mu_{0}+z_{1-\alpha / 2} \sigma / \sqrt{n} \mid \mu=\mu_{1}\right) \\
&=\Phi\left(\frac{\mu_{0}+z_{\alpha / 2} \sigma / \sqrt{n}-\mu_{1}}{\sigma / \sqrt{n}}\right)+1-\Phi\left(\frac{\mu_{0}+z_{1-\alpha / 2} \sigma / \sqrt{n}-\mu_{1}}{\sigma / \sqrt{n}}\right) \\
&=\Phi\left[z_{\alpha / 2}+\frac{\left(\mu_{0}-\mu_{1}\right) \sqrt{n}}{\sigma}\right]+1-\Phi\left[z_{1-\alpha / 2}+\frac{\left(\mu_{0}-\mu_{1}\right) \sqrt{n}}{\sigma}\right]
\end{aligned}$$

- Using the relationship $1-\Phi(x)=\Phi(-x)$, the last two terms can be combined as follows:

$$\text { Power }=\Phi\left[z_{\alpha / 2}+\frac{\left(\mu_{0}-\mu_{1}\right) \sqrt{n}}{\sigma}\right]+\Phi\left[-z_{1-\alpha / 2}+\frac{\left(\mu_{1}-\mu_{0}\right) \sqrt{n}}{\sigma}\right]$$

- Finally, recalling the relationship $Z_{\alpha / 2}=-Z_{1-\alpha / 2}$, we have

$$\text { Power }=\Phi\left[-z_{1-\alpha / 2}+\frac{\left(\mu_{0}-\mu_{1}\right) \sqrt{n}}{\sigma}\right]+\Phi\left[-z_{1-\alpha / 2}+\frac{\left(\mu_{1}-\mu_{0}\right) \sqrt{n}}{\sigma}\right]$$

> Power Figure

![jpg](/assets/images/Stat/132_3.jpg)

- 위와 같이 $\mu_1 < \mu_0 $ 일때와, $\mu_1 > \mu_)$ 일때에 다르게 계산됩니다.

> Proof : Approximately

- 이때 위에 계산된 Power 를 보면, 2개의 CDF 가 같이 있기때문에, 쉽게 활용할 수가 없습니다.
- $\mu_{1}<\mu_{0}$ 라면, second term ($\Phi\left[-z_{1-\alpha / 2}+\frac{\left(\mu_{1}-\mu_{0}\right) \sqrt{n}}{\sigma}\right]$) 값의 경우, First Term 보다 cdf 안의 값이 더 작으므로, cdf 도 매우 작습니다. 그러므로 무시 가능합니다. 
-  $\mu_{1}>\mu_{0}$ 라면 First Term ($\Phi\left[-z_{1-\alpha / 2}+\frac{\left(\mu_{0}-\mu_{1}\right) \sqrt{n}}{\sigma}\right])$ 값의 경우, Second Term 보다 cdf 안의 값이 더 작으므로, cdf 도 매우 작습니다. 그러므로 무시 가능합니다. 
- 그러므로 Power 에 대한 Approximation 은 다음과 같이 계산됩니다.

$$\Phi\left[-z_{1-\alpha / 2}+\frac{\left|\mu_{0}-\mu_{1}\right| \sqrt{n}}{\sigma}\right]$$

# [One Sample proportion Test  and Power](#link){: .btn .btn--primary}{: .align-center}

> ## Power Calculation $$H_{0}: p=p_{0} \quad vs \quad H_{1}: p<p_{0}$$

- Hypothesis 가 아래와 같이 정의한다고 합시다.

$$H_{0}: p=p_{0} \quad vs \quad H_{1}: p<p_{0}$$

- Power 의 이때 Power 의 계산은 , $H_1$ 이 맞을때, $H_0$ 을 기각할 확률입니다. 즉 이때 실제 $H_1 $ 이 맞아서 $p = p_1$ 이라고 합시다. 그러면 power 는 아래와 같이 계산됩니다.

$$\begin{aligned} \text { Power } 
&=\operatorname{Pr}\left(\text { reject } H_{0} \mid H_{0} \text { false }\right)\\
&=\operatorname{Pr}\left(Z<z_{\alpha} \mid p=p_{1}\right) \\ 
&=\operatorname{Pr}\left(\frac{\bar{X}-p_0}{\sqrt{p_0q_0}/\sqrt{n}}<z_{\alpha} \mid p=p_{1}\right) \\ 
&=\operatorname{Pr}\left(\bar{X}<p_{0}+z_{\alpha} \sqrt{p_0q_0}/ \sqrt{n} \mid p=p_{1}\right) \end{aligned}$$

- under $H_{1}$ 하에서는 $ \bar{X} \sim N\left(p_{1}, p_1q_1 / n\right)$ 라는것을 알고 있습니다. 그러므로 Power 의 계산은 아래와 같이 이루어집니다.

$$\begin{aligned}
\text { Power }
&=\operatorname{Pr}\left(\bar{X}<p_{0}+z_{\alpha} \sqrt{p_0q_0} / \sqrt{n} \mid p=p_{1}\right)\\ 
&=\operatorname{Pr}\left((\bar{X}-p_1)/(\sqrt{p_1p_2}/\sqrt{n})<(p_{0}+z_{\alpha} \sqrt{p_0q_0}/ \sqrt{n} -p_1)/(\sqrt{p_1p_2}/\sqrt{n}) \mid p=p_{1}\right)\\ 
&=\operatorname{Pr}\left(Z<(p_{0}+z_{\alpha} \sqrt{p_0q_0}/ \sqrt{n} -p_1)/(\sqrt{p_1p_2}/\sqrt{n}) \mid p=p_{1}\right)\\ 
&=\Phi\left[(p_{0}+z_{\alpha} \sqrt{p_0q_0}/ \sqrt{n} -p_1)/(\sqrt{p_1p_2}/\sqrt{n})\right]\\
\end{aligned}$$

- 즉 위처럼 Power 가 계산되게 됩니다. 

> ## Power Calculation $$H_{0}: p=p_{0} \quad vs \quad H_{1}: p>p_{0}$$

- Hypothesis 가 아래와 같이 정의한다고 합시다.

$$H_{0}: p=p_{0} \quad vs \quad H_{1}: p>p_{0}$$

- Power 의 이때 Power 의 계산은 , $H_1$ 이 맞을때, $H_0$ 을 기각할 확률입니다. 즉 이때 실제 $H_1 $ 이 맞아서 $p = p_1$ 이라고 합시다. 그러면 power 는 아래와 같이 계산됩니다.

$$\begin{aligned} \text { Power } 
&=\operatorname{Pr}\left(\text { reject } H_{0} \mid H_{0} \text { false }\right)\\
&=\operatorname{Pr}\left(Z>z_{1-\alpha} \mid p=p_{1}\right) \\ 
&=\operatorname{Pr}\left(\frac{\bar{X}-p_0}{\sqrt{p_0q_0}/\sqrt{n}}>z_{1-\alpha} \mid p=p_{1}\right) \\ 
&=\operatorname{Pr}\left(\bar{X}>p_{0}+z_{1-\alpha} \sqrt{p_0q_0}/ \sqrt{n} \mid p=p_{1}\right) \end{aligned}$$

- under $H_{1}$ 하에서는 $ \bar{X} \sim N\left(p_{1}, p_1q_1 / n\right)$ 라는것을 알고 있습니다. 그러므로 Power 의 계산은 아래와 같이 이루어집니다.

$$\begin{aligned}
\text { Power }
&=\operatorname{Pr}\left(\bar{X}>p_{0}+z_{1-\alpha} \sqrt{p_0q_0} / \sqrt{n} \mid p=p_{1}\right)\\ 
&=\operatorname{Pr}\left((\bar{X}-p_1)/(\sqrt{p_1q_1}/\sqrt{n})>(p_{0}+z_{1-\alpha} \sqrt{p_0q_0}/ \sqrt{n} -p_1)/(\sqrt{p_1q_1}/\sqrt{n}) \mid p=p_{1}\right)\\ 
&=\operatorname{Pr}\left(Z>(p_{0}+z_{1-\alpha} \sqrt{p_0q_0}/ \sqrt{n} -p_1)/(\sqrt{p_1q_1}/\sqrt{n}) \mid p=p_{1}\right)\\ 
&=1-\Phi\left[(p_{0}+z_{1-\alpha} \sqrt{p_0q_0}/ \sqrt{n} -p_1)/(\sqrt{p_1q_1}/\sqrt{n})\right]\\
\end{aligned}$$

- 즉 위처럼 Power 가 계산되게 됩니다. 

> ## Power Calculation $$H_{0}: p=p_{0} \quad vs \quad H_{1}: p \not= p_{0}$$

- 2 SIded Test 이므로 Power Calculation 이 일어날때에는, Power 가 다음과 같이 계산됩니다.

$$\text{ Power }=\Phi\left[(p_{0}+z_{\alpha} \sqrt{p_0q_0}/ \sqrt{n} -p_1)/(\sqrt{p_1q_1}/\sqrt{n})\right] +1-\Phi\left[(p_{0}+z_{1-\alpha} \sqrt{p_0q_0}/ \sqrt{n} -p_1)/(\sqrt{p_1q_1}/\sqrt{n})\right] $$

- 이때 위 계산에서  $\Phi(-x)=1-\Phi(x)$ and $z_{\alpha}=-z_{1-\alpha}$ 를 이용한다면 

$$\text{ Power }=\Phi\left[\sqrt{n}(p_0-p_{1})/\sqrt{p_1q_1} +z_{\alpha}\sqrt{p_0q_0/p_1q_1}\right] +\Phi\left[\sqrt{n}(p_1-p_{0})\sqrt{p_1q_1}/ +z_{\alpha}\sqrt{p_0q_0/p_1q_1}\right] $$

> Approximation

- $p_0 > p_1$ 이면 두번쨰 term 이 더 작으므로 없앨 수 있습니다.
- $p_0 < p_1$  이면 첫번째 term 이 더 작으므로 없앨 수 있습니다.
- 즉 Approximation 은 다음과 같습니다.

$$\text{ Power }=\Phi\left[\sqrt{n} \mid p_0-p_{1}\mid/\sqrt{p_1q_1} +z_{\alpha}\sqrt{p_0q_0/p_1q_1}\right]$$

# [Two Sample Mean Test with Sample SIze](#link){: .btn .btn--primary}{: .align-center}

> ## Power Calculation $H_{0}: \mu_{1}=\mu_{2}$ vs. $H_{1}: \mu_{1}>\mu_{2}$

- $H_{0}: \mu_{1}=\mu_{2}$ vs. $H_{1}: \mu_{1} > \mu_{2}$ 를 테스트 한다고 합시다. 이때 실제 $H_1$ 는 $\mu_1 - \mu_2 = \Delta_1$ 이라고 합시다. 
- 가설은 $$\bar{X}_{1}-\bar{X}_{2} \sim N\left(\mu_{1}-\mu_{2}, \frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}\right)$$ 라고 합시다 그러면

$$\begin{aligned} \text { Power } 
&=\operatorname{Pr}\left(\text { reject } H_{0} \mid H_{0} \text { false }\right)\\
&=\operatorname{Pr}\left(Z>z_{1-\alpha} \mid \Delta=\Delta_{1}\right) \\ 
&=\operatorname{Pr}\left(\frac{\bar{X}-\bar{Y}-0}{\sqrt{\frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}}}>z_{1-\alpha} \mid \Delta=\Delta_{1}\right) \\ 
&=\operatorname{Pr}\left(\bar{X}-\bar{Y}>z_{1-\alpha} \sqrt{\frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}} \mid \Delta=\Delta_{1}\right) \end{aligned}$$

- 이제 이를 정리하면 아래와 같습니다.

$$\begin{aligned}
\text { Power }
&=\operatorname{Pr}\left(\bar{X}-\bar{Y}>z_{1-\alpha} \sqrt{\frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}} \mid \Delta=\Delta_{1}\right)\\
&=\operatorname{Pr}\left((\bar{X}-\bar{Y}-\Delta_1)/\sqrt{\frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}}> (z_{1-\alpha} \sqrt{\frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}}-\Delta_1)/\sqrt{\frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}} \mid \Delta=\Delta_{1}\right)\\
&=\operatorname{Pr}\left(Z>(z_{1-\alpha} -\Delta_1/\sqrt{\frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}} \right)\\ 
&=1-\Phi\left[(z_{1-\alpha} -\Delta_1/\sqrt{\frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}}\right]\\
&=1-\Phi\left[(z_{1-\alpha} -\left(\Delta_1/\sqrt{\sigma_1^2 + \sigma_2^2}) \right)\sqrt{n}\right]\\
\end{aligned}$$

> ## Power Calculation $H_{0}: \mu_{1}=\mu_{2}$ vs. $H_{1}: \mu_{1}<\mu_{2}$

- $H_{0}: \mu_{1}=\mu_{2}$ vs. $H_{1}: \mu_{1} > \mu_{2}$ 를 테스트 한다고 합시다. 이때 실제 $H_1$ 는 $\mu_1 - \mu_2 = \Delta_1$ 이라고 합시다. 
- 가설은 $$\bar{X}_{1}-\bar{X}_{2} \sim N\left(\mu_{1}-\mu_{2}, \frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}\right)$$ 라고 합시다 그러면

$$\begin{aligned} \text { Power } 
&=\operatorname{Pr}\left(\text { reject } H_{0} \mid H_{0} \text { false }\right)\\
&=\operatorname{Pr}\left(Z<z_{\alpha} \mid \Delta=\Delta_{1}\right) \\ 
&=\operatorname{Pr}\left(\frac{\bar{X}-\bar{Y}-0}{\sqrt{\frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}}}<z_{\alpha} \mid \Delta=\Delta_{1}\right) \\ 
&=\operatorname{Pr}\left(\bar{X}-\bar{Y}<z_{\alpha} \sqrt{\frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}} \mid \Delta=\Delta_{1}\right) \end{aligned}$$

- 이제 이를 정리하면 아래와 같습니다.

$$\begin{aligned}
\text { Power }
&=\operatorname{Pr}\left(\bar{X}-\bar{Y}<z_{\alpha} \sqrt{\frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}} \mid \Delta=\Delta_{1}\right)\\
&=\operatorname{Pr}\left((\bar{X}-\bar{Y}-\Delta_1)/\sqrt{\frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}}< (z_{\alpha} \sqrt{\frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}}-\Delta_1)/\sqrt{\frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}} \mid \Delta=\Delta_{1}\right)\\
&=\operatorname{Pr}\left(Z<(z_{\alpha} -\Delta_1/\sqrt{\frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}} \right)\\ 
&=\Phi\left[(z_{\alpha} -\Delta_1/\sqrt{\frac{\sigma_{1}^{2}}{n_{1}}+\frac{\sigma_{2}^{2}}{n_{2}}}\right]\\
&=\Phi\left[(z_{\alpha} -\left(\Delta_1/\sqrt{\sigma_1^2 + \sigma_2^2}) \right)\sqrt{n}\right]\\
\end{aligned}$$

> ## Power Calculation $H_{0}: \mu_{1}=\mu_{2}$ vs. $H_{1}: \mu_{1} \not = \mu_{2}$

- 양측검정일 경우, 위에서 살펴본 단측검정을 각각 $\alpha/2 $ 만큼 수행하는 것이므로, power 는 아래와 같습니다.

$$\text{power} = \Phi\left[(z_{\alpha/2} -\left(\Delta_1/\sqrt{\sigma_1^2 + \sigma_2^2}) \right)\sqrt{n}\right] + 1-\Phi\left[(z_{1-\alpha/2} -\left(\Delta_1/\sqrt{\sigma_1^2 + \sigma_2^2}) \right)\sqrt{n}\right]$$ 

- 이때 $1-\Phi(x)=\Phi(-x)$, 를 이용한다면 최종적으로 아래와 같이 계산됩니다.

$$\text{power} = \Phi\left[(z_{\alpha/2} -\left(\Delta_1/\sqrt{\sigma_1^2 + \sigma_2^2}) \right)\sqrt{n}\right] + \Phi\left[(z_{\alpha/2} +\left(\Delta_1/\sqrt{\sigma_1^2 + \sigma_2^2}) \right)\sqrt{n}\right]$$ 

> Approximation

- $\mu_1 > \mu_2$ 일때에는 $\mu_1 - \mu_2 = \Delta_1$ 이므로, $\Delta_1>0$ 입니다. 즉 first Term ($\Phi\left[(z_{\alpha/2} -\left(\Delta_1/\sqrt{\sigma_1^2 + \sigma_2^2}) \right)\sqrt{n}\right]$) 이 더 작으므로 생략할 수 있습니다. 
- $\mu_1 < \mu_2$ 일때에는 $\mu_1 - \mu_2 = \Delta_1$ 이므로, $\Delta_1<0$ 입니다. 즉 Second Term($\Phi\left[(z_{\alpha/2} +\left(\Delta_1/\sqrt{\sigma_1^2 + \sigma_2^2}) \right)\sqrt{n}\right]$) 이 더 작으므로 생략할 수 있습니다. 

$$\text{power} = \Phi\left[(z_{\alpha/2} +\left(\mid\Delta_1 \mid /\sqrt{\sigma_1^2 + \sigma_2^2}) \right)\sqrt{n}\right]$$ 

> ## Sample Calculation $H_{0}: \mu_{1}=\mu_{2}$ vs. $H_{1}: \mu_{1} \not = \mu_{2}$

- power 를 $1-\beta$ 라고 하겠습니다. 그러면 

$$\begin{aligned}
1-\beta
&= \Phi\left[(z_{\alpha/2} +\left(\mid\Delta_1 \mid /\sqrt{\sigma_1^2 + \sigma_2^2}) \right)\sqrt{n}\right] \\
\end{aligned}$$ 

- 양변에 역 cdf 를 곱해주고 정리하면 

> Theorem

$n=\frac{\left(\sigma_{1}^{2}+\sigma_{2}^{2}\right)\left(z_{1-\alpha / 2}+z_{1-\beta}\right)^{2}}{\Delta^{2}}=$ sample size for each group 

- where $$\Delta=\mid\mu_{2}-\mu_{1}\mid$$
- The means and variances of the two respective groups are $\left(\mu_{1}\right.$, $\left.\sigma_{1}^{2}\right)$ and $\left(\mu_{2}, \sigma_{2}^{2}\right)$

> ##  unequal Sample Size

> Theorem 

- Sample Size Needed for Comparing the Means of Two Normally Distributed Samples of Unequal Size Using a Two-Sided Test with Significance Level $\alpha$ and Power $1-\beta$

$$\begin{aligned}
&n_{1}=\frac{\left(\sigma_{1}^{2}+\sigma_{2}^{2} / k\right)\left(z_{1-\alpha / 2}+z_{1-\beta}\right)^{2}}{\Delta^{2}}=\text { sample size of first group } \\
&n_{2}=\frac{\left(k \sigma_{1}^{2}+\sigma_{2}^{2}\right)\left(z_{1-\alpha / 2}+z_{1-\beta}\right)^{2}}{\Delta^{2}}=\text { sample size of second group }
\end{aligned}$$

- where $$\Delta=\mid\mu_{2}-\mu_{1}\mid ;\left(\mu_{1}, \sigma_{1}^{2}\right),\left(\mu_{2}, \sigma_{2}^{2}\right)$$, are the means and variances of the two respective groups 
- and $k=n_{2} / n_{1}=$ the projected ratio of the two sample sizes.

> Note

- 위의 증명은 , 저희가 샘플 계산시에 $n_1=n_2=n$  로 가정하고 계산했는데요, 이 조건을 없애고, $n_1\not= n_2$ 라고 한 뒤에 계산하면 됩니다.

# [Two Sample Proportion Test with Sample SIze](#link){: .btn .btn--primary}{: .align-center}

> ## Power Caclulation  $H_{0}: p_1=p_2$ Vs $H_{1}: p_{1}>p_{2}$

- Assume $H_{0}: p_1=p_2$ vs. $H_{1}: p_{1}>p_{2}$ 라고 합시다.
  - 그리고 $p_1 - p_2 = \Delta$ 라고 합시다.

$$\begin{aligned} \text { Power } 
&=\operatorname{Pr}\left(\text { reject } H_{0} \mid H_{0} \text { false }\right)\\
&=\operatorname{Pr}\left(Z>z_{1-\alpha} \mid p_1-p_2= \Delta\right) \\ 
&=\operatorname{Pr}\left(\frac{\bar{X_1} - \bar{X_2}}{\sqrt{\bar{p}\bar{q}/n_1+\bar{p}\bar{q}/n_2}}>z_{1-\alpha} \mid p_{1}-p_2 = \Delta\right) \\ 
&=\operatorname{Pr}\left(\bar{X_1}-\bar{X_2}>z_{1-\alpha}\sqrt{\bar{p}\bar{q}/n+\bar{p}\bar{q}/n} \mid p_1-p_2=\Delta\right) \end{aligned}$$

- under $H_{1}$ 하에서는 $ \bar{X_1}-\bar{X_2} \sim N\left(\Delta, (p_1q_1+p_2q_2) / n\right)$ 라는것을 알고 있습니다. 그러므로 Power 의 계산은 아래와 같이 이루어집니다.

$$\begin{aligned}
\text { Power }
&=\operatorname{Pr}\left(\bar{X_1}-\bar{X_2}>z_{1-\alpha}\sqrt{\bar{p}\bar{q}/n+\bar{p}\bar{q}/n} \mid p_1-p_2=\Delta\right)\\
&=\operatorname{Pr}\left((\bar{X_1}-\bar{X_2}-\Delta)/(\sqrt{p_1q_1+p_2q_2}/\sqrt{n})>(z_{1-\alpha} \sqrt{2\bar{p}\bar{q}}/ \sqrt{n} -\Delta)/(\sqrt{p_1q_1+p_2q_2}/\sqrt{n}) \mid p_1-p_2 = \Delta\right)\\ 
&=\operatorname{Pr}\left(Z>(z_{1-\alpha} \sqrt{2\bar{p}\bar{q}}/ \sqrt{n} -\Delta)/(\sqrt{p_1q_1+p_2q_2})/\sqrt{n})\right)\\ 
&=1-\Phi[(z_{1-\alpha} \sqrt{2\bar{p}\bar{q}}/ \sqrt{n} -\Delta)/(\sqrt{p_1q_1+p_2q_2})/\sqrt{n})]\\
\end{aligned}$$

- 즉 위처럼 Power 가 계산되게 됩니다. 

> ## Power Caclulation  $H_{0}: p_1=p_2$ Vs $H_{1}: p_{1}<p_{2}$

- Assume $H_{0}: p_1=p_2$ vs. $H_{1}: p_{1}<p_{2}$ 라고 합시다.
  - 그리고 $p_1 - p_2 = \Delta$ 라고 합시다.

$$\begin{aligned} \text { Power } 
&=\operatorname{Pr}\left(\text { reject } H_{0} \mid H_{0} \text { false }\right)\\
&=\operatorname{Pr}\left(Z<z_{\alpha} \mid p_1-p_2= \Delta\right) \\ 
&=\operatorname{Pr}\left(\frac{\bar{X_1} - \bar{X_2}}{\sqrt{\bar{p}\bar{q}/n_1+\bar{p}\bar{q}/n_2}}<z_{\alpha} \mid p_{1}-p_2 = \Delta\right) \\ 
&=\operatorname{Pr}\left(\bar{X_1}-\bar{X_2}<z_{\alpha}\sqrt{\bar{p}\bar{q}/n+\bar{p}\bar{q}/n} \mid p_1-p_2=\Delta\right) \end{aligned}$$

- under $H_{1}$ 하에서는 $ \bar{X_1}-\bar{X_2} \sim N\left(\Delta, (p_1q_1+p_2q_2) / n\right)$ 라는것을 알고 있습니다. 그러므로 Power 의 계산은 아래와 같이 이루어집니다.

$$\begin{aligned}
\text { Power }
&=\operatorname{Pr}\left(\bar{X_1}-\bar{X_2}<z_{\alpha}\sqrt{\bar{p}\bar{q}/n+\bar{p}\bar{q}/n} \mid p_1-p_2=\Delta\right)\\
&=\operatorname{Pr}\left((\bar{X_1}-\bar{X_2}-\Delta)/(\sqrt{p_1q_1+p_2q_2}/\sqrt{n})<(z_{\alpha} \sqrt{2\bar{p}\bar{q}}/ \sqrt{n} -\Delta)/(\sqrt{p_1q_1+p_2q_2}/\sqrt{n}) \mid p_1-p_2 = \Delta\right)\\ 
&=\operatorname{Pr}\left(Z<(z_{\alpha} \sqrt{2\bar{p}\bar{q}}/ \sqrt{n} -\Delta)/(\sqrt{p_1q_1+p_2q_2})/\sqrt{n})\right)\\ 
&=\Phi[(z_{\alpha} \sqrt{2\bar{p}\bar{q}}/ \sqrt{n} -\Delta)/(\sqrt{p_1q_1+p_2q_2})/\sqrt{n})]\\
\end{aligned}$$

- 즉 위처럼 Power 가 계산되게 됩니다. 

> ## Power Calculation $H_{0}: p_1=p_2$ Vs $H_{1}: p_{1}\not =p_{2}$

> Calculation

- 양측검정에서는, 위의 계산이 양측검정으로 이루어지기 때문에, alpha 가 alpha/2 로 계산되게 됩니다.

$\text{Power} = \Phi[(z_{\alpha/2} \sqrt{2\bar{p}\bar{q}}/ \sqrt{n} -\Delta)/(\sqrt{p_1q_1+p_2q_2})/\sqrt{n})]+1-\Phi[(z_{1-\alpha/2} \sqrt{2\bar{p}\bar{q}}/ \sqrt{n} -\Delta)/(\sqrt{p_1q_1+p_2q_2})/\sqrt{n})]$

- 이떄 위의 값은 다음과 같이 변환됩니다.

$\text{Power} = \Phi[(z_{\alpha/2} \sqrt{2\bar{p}\bar{q}/(p_1q_1 + p_2q_2)} -\Delta \sqrt{n}/\sqrt{p_1q_1+p_2q_2}))]+\Phi[(z_{\alpha/2} \sqrt{2\bar{p}\bar{q}/(p_1q_1 + p_2q_2)} +\Delta \sqrt{n}/\sqrt{p_1q_1+p_2q_2}))]$

- 위에서, $p_1>p_2$ 이면 $\Delta < 0 $ 이므로 두번째 term 은 제거될 수 있습니다.
- 위에서 $p_2>p_1$ 이면 $\Delta>0$ 이므로 첫번째 term 은 제거될 수 있습니다.

> Approximation

$\text{Power} = \Phi[(z_{\alpha/2} \sqrt{2\bar{p}\bar{q}/(p_1q_1 + p_2q_2)} +\mid \Delta \mid  \sqrt{n}/\sqrt{p_1q_1+p_2q_2}))]$

> ## Sample Calculation $H_{0}: p_1=p_2$ Vs $H_{1}: p_{1}\not=p_{2}$

- 기본적으로 Sample Size Calculation 은 Two Sided Test 일때에 진행됩니다.

$1 - \beta = \Phi[(z_{\alpha/2} \sqrt{2\bar{p}\bar{q}/(p_1q_1 + p_2q_2)} +\mid \Delta \mid  \sqrt{n}/\sqrt{p_1q_1+p_2q_2}))]$ 

- 위에 대해서 역 cdf 를 양쪽에 적용하고, 정리하면 아래와 같은 식이 나옵니다.

$$\begin{aligned}
&n=\left[z_{1-\alpha / 2}\sqrt{2\bar{p} \bar{q}} +z_{1-\beta}\sqrt{p_{1} q_{1}+p_2q_2} \right]^{2} / \Delta^{2} \\
\end{aligned}$$

- where $p_{1}, p_{2}=$ projected true probabilities of success in the two groups

$$\begin{aligned}
q_{1}, q_{2} &=1-p_{1}, 1-p_{2} \\
\Delta &=\left|p_{2}-p_{1}\right| \\
\bar{p} &=\frac{p_{1}+p_{2}}{1+1} \\
\bar{q} &=1-\bar{p}
\end{aligned}$$

> ## unequal Sample Size

- Sample Size Needed to Compare Two Binomial Proportions Using a Two-Sided Test with Significance Level $\alpha$ and Power $1-\beta$, Where One Sample $\left(\boldsymbol{n}_{2}\right)$ Is $\boldsymbol{k}$ Times as Large as the Other Sample $\left(n_{1}\right)$ (Independent-Sample Case)
- To test the hypothesis $H_{0}: p_{1}=p_{2}$ vs. $H_{1}: p_{1} \neq p_{2}$ for the specific alternative $\mid p_{1}-p_{2}\mid=\Delta$, with a significance level $\alpha$ and power $1-\beta$, the following sample size is required

$$\begin{aligned}
&n_{1}=\left[\sqrt{\bar{p} \bar{q}\left(1+\frac{1}{k}\right)} z_{1-\alpha / 2}+\sqrt{p_{1} q_{1}+\frac{p_{2} q_{2}}{k}} z_{1-\beta}\right]^{2} / \Delta^{2} \\
&n_{2}=k n_{1}
\end{aligned}$$

- where $p_{1}, p_{2}=$ projected true probabilities of success in the two groups

$$\begin{aligned}
q_{1}, q_{2} &=1-p_{1}, 1-p_{2} \\
\Delta &=\left|p_{2}-p_{1}\right| \\
\bar{p} &=\frac{p_{1}+k p_{2}}{1+k} \\
\bar{q} &=1-\bar{p}
\end{aligned}$$

# Note : Sample size Calculator

- <https://www.stat.ubc.ca/~rollin/stats/ssize/>
- <https://bookingcom.github.io/powercalculator/>

---

**reference**

- Fundamentals of Biostatistics
- https://towardsdatascience.com/required-sample-size-for-a-b-testing-6f6608dd330a





