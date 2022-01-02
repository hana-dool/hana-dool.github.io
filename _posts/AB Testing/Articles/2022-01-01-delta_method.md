---
title: "Delta Method in AB test"
excerpt: "Delta 방법론"
categories:
  - AB_Article
last_modified_at: 2022-01-01

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

Outlier 와 A/B Testing
{: .notice--warning}

# [Randomization Unit](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

- A / B 테스트 분석에서, Treatment 과 Control 의 평균 차이가 잇는지 없는지를 검정합니다. 
- 이때 Continuous 변수인 경우 아래와 같이 Two Sample T test 를 수행할 수 있습니다.

$$T=\frac{\bar{X}_{B}-\bar{X}_{A}}{\sqrt{\operatorname{Var}\left(\bar{X}_{A}\right)+\operatorname{Var}\left(\bar{X}_{B}\right)}}$$

$$\operatorname{Var}(X)=\frac{1}{n-1} \sum_{i}^{n}\left(X_{i}-\bar{X}\right)^{2}$$

- 그러나 위에서 계산되는 평균 및 분산 공식은 iid(독립적이고 동일하게 분포된) 랜덤 변수에만 적용되며 실제 비즈니스 사례에서는 메트릭이 더 복잡합니다. 
  - 한 예로 클릭수/조회수로 정의되는 클릭률 또는 CTR과 같은 비율로 정의됩니다.
- 클릭수와 조회수는 무작위 변수이므로 단일 측정항목 CTR로 결합하면 Joint Distriburion 을 갖게 됩니다.
-  또한 무작위화가 user_id를 기반으로 하는 경우 한 사용자가 매트릭을 여러개 생성할수도 있기 떄문에, Independent 가 아닙니다.
- 따라서 위의 분산 추정 공식은 CTR 분산을 추정하는 데 사용할 수 없습니다.
  -  여기에서는 메트릭 비율의 분산을 근사하기 위해 델타 방법을 사용합니다.

> ## Note : Delta Method in one Sample

- 우선 Delta Method 를 Multi 분포에서 어떻게 쓰는지에 대해서 알아봅시다.
- By definition, a consistent estimator $B$ converges in probability to its true value $\beta$, and often a central limit theorem can be applied to obtain asymptotic normality:

$$\sqrt{n}(B-\beta) \stackrel{L}{\longrightarrow} N(0, \Sigma)$$

- where $n$ is the number of observations and $\sum$ is a (symmetric positive semi-definite) covariance matrix. Suppose we want to estimate the variance of a scalar-valued function $h$ of the estimator $B$. Keeping only the first two terms of the Taylor series, and using vector notation for the gradient, we can estimate $h$ (B) as

$$h(B) \approx h(\beta)+\nabla h(\beta)^{T} \cdot(B-\beta)$$

- which implies the variance of $h(B)$ is approximately

$$\begin{aligned}
\operatorname{Var}(h(B)) & \approx \operatorname{Var}\left(h(\beta)+\nabla h(\beta)^{T} \cdot(B-\beta)\right) \\
&=\operatorname{Var}\left(h(\beta)+\nabla h(\beta)^{T} \cdot B-\nabla h(\beta)^{T} \cdot \beta\right) \\
&=\operatorname{Var}\left(\nabla h(\beta)^{T} \cdot B\right) \\
&=\nabla h(\beta)^{T} \cdot \operatorname{Cov}(B) \cdot \nabla h(\beta) \\
&=\nabla h(\beta)^{T} \cdot(\Sigma) \cdot \nabla h(\beta)
\end{aligned}$$

- One can use the mean value theorem (for real-valued functions of many variables) to see that this does not rely on taking first order approximation.
  The delta method therefore implies that

$$\sqrt{n}(h(B)-h(\beta)) \stackrel{\nu}{\longrightarrow} N\left(0, \nabla h(\beta)^{T} \cdot \Sigma \cdot \nabla h(\beta)\right)$$

- or in univariate terms,

$$\sqrt{n}(h(B)-h(\beta)) \stackrel{\nu}{\longrightarrow} N\left(0, \sigma^{2} \cdot\left(h^{\prime}(\beta)\right)^{2}\right) .$$

> ## Ratio Delta Meth**reference**

- The multivariate delta method has a heuristic justification here: https://en.wikipedia.org/wiki/Delta_method#Multivariate_delta_method. For the multivariate delta method you have a specific function $f$ that takes a vector argument which is $p$ dimensional and maps this to a $k$ dimensional space. In the case of a ratio estimator $p=2$ and $k=1$. The function $f$ is

$$f\left(\left[\begin{array}{c}
\bar{y} \\
\bar{x}
\end{array}\right]\right)=\bar{y} / \bar{x}$$

- Now what are needed are a few more quantities, the first is:

$$f(\vec{\mu})=f\left(\left[\begin{array}{l}
\mu_{y} \\
\mu_{x}
\end{array}\right]\right)=\mu_{y} / \mu_{x}$$

- These are the $h(B)$ and $h(\beta)$ respectively in notation in the Wikipedia link. Next you need the vector of partial derivatives of $f(\vec{\mu})$, this is

$$\nabla f(\vec{\mu})=\left[\begin{array}{c}
\frac{1}{\mu_{x}} \\
\frac{-\mu_{y}}{\mu_{x}^{2}}
\end{array}\right]$$

- Also we need the variance covariance matrix of the vector

$$\left[\begin{array}{l}
\bar{y} \\
\bar{x}
\end{array}\right]$$

- which is

$$\left[\begin{array}{cc}
\sigma_{y}^{2} / n & \sigma_{y x}/n \\
\sigma_{y x}/n & \sigma_{x}^{2} / n
\end{array}\right] .$$

- Note this variance-covariance matrix is the $\Sigma / n$ in the Wikipedia notation. Now the only thing left is to calculate the quadratic form:

$$\nabla f(\vec{\mu})^{T}\left[\begin{array}{cc}
\sigma_{y}^{2} / n & \sigma_{y x}/n \\
\sigma_{y x}/n & \sigma_{x}^{2} / n
\end{array}\right] \nabla f(\vec{\mu})=\left[\begin{array}{c}
\frac{1}{\mu_{x}} \\
\frac{-\mu_{y}}{\mu_{x}^{2}}
\end{array}\right]^{T}\left[\begin{array}{cc}
\sigma_{y}^{2} / n & \sigma_{y x}/n \\
\sigma_{y x}/n & \sigma_{x}^{2} / n
\end{array}\right]\left[\begin{array}{c}
\frac{1}{\mu_{x}} \\
\frac{-\mu_{y}}{\mu_{x}^{2}}
\end{array}\right] .$$

- Which when I worked this out gives you the equation:

$$\sigma_{R}^{2}=\frac{\sigma_{y}^{2}}{n \mu_{x}^{2}}-2 \frac{\mu_{y} \sigma_{x y}}{n\mu_{x}^{3}}+\frac{\sigma_{x}^{2} \mu_{y}^{2}}{n \mu_{x}^{4}},$$

- where this quantity is the variance of the delta method normal distribution. Putting this altogether gives us that

$$\left(\frac{\bar{y}}{\bar{x}}-\frac{\mu_{y}}{\mu_{x}}\right) \sim N\left(0, \sigma_{R}^{2}\right)$$

- So you can estimate the ratio of the population means by the ratio of the sample means provided you can estimate variances and the covariance, or equivalently, the correlation $\rho=\frac{\sigma_{x y}}{\sigma_{x} \sigma_{y}}$, by substitution, $\sigma_{x} \sigma_{y} \rho=\sigma_{x y}$. This is how the delta method is most commonly used in the derivation of the ratio estimator distribution.

> CI

$$\underbrace{\frac{\bar{Y}}{\bar{X}}-1}_{\text {point estimate }} \pm \underbrace{\frac{z_{\alpha / 2}}{\sqrt{n} \bar{X}} \sqrt{s_{y}^{2}-2 \frac{\bar{Y}}{\bar{X}} s_{x y}+\frac{\bar{Y}^{2}}{\bar{X}^{2}} s_{x}^{2}}}_{\text {uncertainty quantification }}$$

> ## Two Variant

- Treatment 와 Control 이 있다고 합시다. 
  - 이때 우리의 측정항목은 CTR = 클릭수/조회수입니다. 
  - 먼저 각 Variant 에 대한 CTR 의 평균을 계산해봅시다.

$$\begin{aligned}
\overline{C T R}_{\text {treatment }} &=\frac{\text { Total Clicks }}{\text { Total Views }} \\
\overline{C T R}_{\text {control }} &=\frac{\text { Total Clicks }}{\text { Total Views }}
\end{aligned}$$

- 그런 다음 Y는 클릭이고 X는 조회수인 비율에 대한 분산 공식을 사용하여 CTR의 분산을 계산합니다.

$$\operatorname{Var}(C T R) \approx \frac{1}{n} \frac{\mu_{y}^{2}}{\mu_{x}^{2}}\left[\frac{\sigma_{y}^{2}}{\mu_{y}^{2}}-2 \frac{\operatorname{Cov}(X, Y)}{\mu_{x} \mu_{y}}+\frac{\sigma_{x}^{2}}{\mu_{x}^{2}}\right]$$

- 마지막으로 t-값을 계산할 수 있습니다. 절대 t-값이 임계값보다 크면 귀무 가설을 기각합니다. 반대로 절대 t-값이 임계값보다 작으면 귀무 가설을 기각하지 못합니다.

$$T=\frac{\overline{C T R}_{\text {treatment }}-\overline{C T R}_{\text {control }}}{\sqrt{\operatorname{Var}\left(\overline{C T R}_{\text {treatment }}\right)+\operatorname{Var}\left(\overline{C T R}_{\text {control }}\right)}}$$

> ## Code Example

- 마지막으로 더미 데이터를 이용한 계산 예를 들어 보겠습니다. 계산은 간단하고 간단합니다. 일반적으로 SQL을 사용하여 데이터베이스에서 데이터를 수집하고 처리하더라도 SQL에서 신뢰 구간을 직접 계산할 수 있습니다.

```python
import pandas as pd
import numpy as np
from random import randint
from scipy import stats 

#dummy variables
click_control = [randint(0,20) for i in range(10000)]
view_control = [randint(1,60) for i in range(10000)]

click_treatment = [randint(0,21) for i in range(10000)]
view_treatment = [randint(1,60) for i in range(10000)]

control = pd.DataFrame({'click':click_control,'view':view_control})
treatment = pd.DataFrame({'click':click_treatment,'view':view_treatment})

#variance estimation of metrics ratio
def var_ratio(x,y): #x/y
    mean_x = np.mean(x)
    mean_y = np.mean(y)
    var_x = np.var(x,ddof=1)
    var_y = np.var(y,ddof=1)
    cov_xy = np.cov(x,y,ddof=1)[0][1]
    result = (var_x/mean_x**2 + var_y/mean_y**2 - 2*cov_xy/(mean_x*mean_y))*(mean_x*mean_x)/(mean_y*mean_y*len(x))
    return result
    
#ttest calculation 
def ttest(mean_control,mean_treatment,var_control,var_treatment):
    diff = mean_treatment - mean_control
    var = var_control+var_treatment
    stde = 1.96*np.sqrt(var)
    lower = diff - stde 
    upper = diff + stde
    z = diff/np.sqrt(var)
    p_val = stats.norm.sf(abs(z))*2

    result = {'mean_control':mean_control,
             'mean_experiment':mean_experiment,
             'var_control':var_control,
             'var_experiment':var_treatment,
             'difference':diff,
             'lower_bound':lower,
             'upper_bound':upper,
             'p-value':p_val}
    return pd.DataFrame(result,index=[0])

var_control = var_ratio(control['click'],control['view'])
var_treatment = var_ratio(treatment['click'],treatment['view'])
mean_control = control['click'].sum()/control['view'].sum()
mean_treatment = treatment['click'].sum()/treatment['view'].sum()

ttest(mean_control,mean_treatment,var_control,var_treatment)
```

---

**reference**

- https://stats.stackexchange.com/questions/398436/a-b-testing-ratio-of-sums

- http://www.stat.rice.edu/~dobelman/notes_papers/math/TaylorAppDeltaMethod.pdf
- https://stats.stackexchange.com/questions/291594/estimation-of-population-ratio-using-delta-method/291652



