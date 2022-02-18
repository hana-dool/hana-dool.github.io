---
title: "Delta Method"
excerpt: "Delta 방법론"
tags :
  - AB_Stat
last_modified_at: 2022-01-01

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

Analysis Unit 과 Randomization Unit 이 다른 경우 Ratio metric 에 대해서 어떻게 분석할까?
{: .notice--warning}

# [Delta Method](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

> Test Procedure

- A / B 테스트 분석에서는 대게 Treatment 과 Control 의 평균 차이가 잇는지 없는지를 검정합니다. 
- 이때 Continuous 변수인 경우 아래와 같이 Two Sample T test 를 수행할 수 있습니다.

$$T=\frac{\bar{X}_{B}-\bar{X}_{A}}{\sqrt{\operatorname{Var}\left(\bar{X}_{A}\right)+\operatorname{Var}\left(\bar{X}_{B}\right)}}$$

$$\operatorname{Var}(X)=\frac{1}{n-1} \sum_{i}^{n}\left(X_{i}-\bar{X}\right)^{2}$$

> Problem1 : IID

- 하지만 위처럼 정의되는 경우는 $X = \{x_1,x_2 .... x_n\}$ 의 값들이 모두 iid 일떄에나 가능합니다.
- 실제 비즈니스에서는 위와 같은 정의가 잘 작동하지 않을 수 있습니다.
  - 한 예로 \#Clicks / \#Views 로 CTR 이 정의되었고 $CTR_A$ 와 $CTR_B$ 를 비교하려 한다고 합시다. 
  - 그리고  Views 마다 A 와 B 를 배분하는것이 아니라 유저 key 에 따라서 A 와 B 실험군에 분배하였습니다.
  - 그리고 데이터는 아래와 같았습니다.

| row  | experiment_key | User_id | Views_id (agg) | Clicks |
| ---- | -------------- | ------- | -------------- | ------ |
| 1    | A              | 142     | Af2f           | 13     |
| 2    | A              | 142     | 2df9d          | 9      |
| 3    | A              | 142     | f0bm           | 10     |
| 4    | B              | 3362    | 0hns           | 0      |
| 5    | B              | 3362    | 9ddm           | 2      |

- 위의 표는 Views 에 대해서 집계된 Clicks 수입니다.
  - 위와 같은 경우 우리는 Vies_id 를 샘플 수 (n) 으로 설정하여서 click 수를 Two Sampe T Test 를 수행하게 될 것입니다.
- 하지만 이 경우 "Views" 는 유저에 대해서 Correlated 되어있습니다. 
  - 위 예시를 보면 User_id = 142 인 유저의 경우 활발한 유저여서 , 클릭수가 많게 찍힙니다.
  - 그에 반해서 User_id = 3362 인 유저의 경우 게으른 유저여서 클릭수가 적게 찍힙니다.
- 즉 위 같은 경우, Views_id 를 기준으로 T test 를 적용하면 IID 가정이 깨지게 된다는것을 알 수 있죠.

> Problem 2 : AGG

- 또한 실제 적용시 더 문제되는 부분은 "Aggregation" 이 잘 되지 않을 수 있다는 것입니다. 
- 위 예시에서 우리는 Views_id 로 Aggregation 을 했습니다. 하지만 로그데이터에서 한번 Views 할때마다 생성되는 key 가 있으면 집계를 할 수 있겠지만, 이게 없을때에는 어떻게 해야할까요? 
  - 그런 경우에는 아예 '집계' 자체가 우리가 분석하려는 단위로 되지 않기떄문에 Aggregation 을 할 수 없습니다.
- 그러므로 이러한 경우에는 아예 분석을 할 수 없다는 것이죠.

> So... What To do ? 

- 즉, 우리는 CTR 처럼 Ratio metric 에 대해서 흥미가 있습니다만, 실험 세팅으로 인해서 t-test 를 적용하기 힘든 경우가 있었습니다.
- 그렇다면 ratio metric 은 적용할 수 없는것일까요? 
  - 오로지 randomization unit 과 analysis unit 이 일치할때에만 ratio metric 을 쓸 수 있는것일까요? 
- 아래 세션에서는 이런 경우에 어떻게 하면 분석할 수 있는지에 대해서 알아보겠습니다.

> ## Note : Delta Method

- 우선 Delta Method 가 어떤것인지부터 알아봅시다.
  - https://en.wikipedia.org/wiki/Delta_method#Multivariate_delta_method 

- By definition, a consistent estimator $B$ converges in probability to its true value $\beta$
- Then often a central limit theorem can be applied to obtain asymptotic normality:

$$\sqrt{n}(B-\beta) \stackrel{L}{\longrightarrow} N(0, \Sigma)$$

- where $n$ is the number of observations and $\sum$ is a (symmetric positive semi-definite) covariance matrix.
- Suppose we want to estimate the variance of a scalar-valued function $h$ of the estimator $B$. 
- Keeping only the first two terms of the Taylor series, and using vector notation for the gradient, we can estimate $h$ (B) as

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
- The delta method therefore implies that

$$\sqrt{n}(h(B)-h(\beta)) \stackrel{\nu}{\longrightarrow} N\left(0, \nabla h(\beta)^{T} \cdot \Sigma \cdot \nabla h(\beta)\right)$$

- or in univariate terms,

$$\sqrt{n}(h(B)-h(\beta)) \stackrel{\nu}{\longrightarrow} N\left(0, \sigma^{2} \cdot\left(h^{\prime}(\beta)\right)^{2}\right) .$$

> ## Ratio 메트릭에 대한 Delta Method

- Ratio metric 의 경우에는 CLT 를 어떻게 적용할 수 있을까요?
  - 먼저 아래와 같이 공식에 대해서 다시 Remind 해 봅시다.


$$\sqrt{n}(h(B)-h(\beta)) \stackrel{\nu}{\longrightarrow} N\left(0, \nabla h(\beta)^{T} \cdot \Sigma \cdot \nabla h(\beta)\right)$$

> Step 1 : h 정의

- ratio 를 만드는 함수로서 f (위 식에서는 h) 를 아래처럼 정의합시다.

$$f\left(\left[\begin{array}{c}
\bar{y} \\
\bar{x}
\end{array}\right]\right)=\bar{y} / \bar{x}$$

- 그리고 아래처럼 $\vec{\mu}$ (true) 값에 대해서도 f 를 적용할 수 있습니다.

$$f(\vec{\mu})=f\left(\left[\begin{array}{l}
\mu_{y} \\
\mu_{x}
\end{array}\right]\right)=\mu_{y} / \mu_{x}$$

- 이 두 Quantity 는 위에서 살펴본 (refer : https://en.wikipedia.org/wiki/Delta_method#Multivariate_delta_method  ) 에서 각각  $h(B)$ and $h(\beta)$  라고 할 수 있습니다.

> Step 2 : 각 Qauntity 계산

- 그 이후에 partial derivatives of $f(\vec{\mu})$ 를 구해보면 아래와 같습니다.

$$\nabla f(\vec{\mu})=\left[\begin{array}{c}
\frac{1}{\mu_{x}} \\
\frac{-\mu_{y}}{\mu_{x}^{2}}
\end{array}\right]$$

- 또한 $\left[\begin{array}{l}\bar{y} \\ \bar{x}\end{array}\right]$ 에 대한 variance covariance matrix of the vector 를 구해야 합니다.
  - 즉 $\Sigma$ = $$\left[\begin{array}{cc}\operatorname{var}(\bar{x}) & \operatorname{cov}(\bar{x}, \bar{y}) \\ \operatorname{cov}(\bar{x}, \bar{y}) & \operatorname{var}(\bar{y})\end{array}\right]$$를 구해야 됩니다.


- 이는 아래와 같이 계산됩니다. ($$\sigma^2_x = var(x)$ , $\sigma_{xy} = cov(x,y)$$) 

$$\left[\begin{array}{cc}
\sigma_{y}^{2} / n & \sigma_{y x}/n \\
\sigma_{y x}/n & \sigma_{x}^{2} / n
\end{array}\right]$$

> Step 3 : 공식에 정의

- 먼저 Delta Method 를 다시 Remind 해 봅시다.

$$\sqrt{n}(h(B)-h(\beta)) \stackrel{\nu}{\longrightarrow} N\left(0, \nabla h(\beta)^{T} \cdot \Sigma \cdot \nabla h(\beta)\right)$$ 

- 위 공식에 대해서 n 이 fixed constant 이고 또한 충분히 커서, Delta Method 를 적용할 수 있다고 합시다. 
  - 그러면 $\sqrt{n}$ 을 오른쪽으로 옮길 수 있습니다. 

$$(h(B)-h(\beta)) \stackrel{approx}{\longrightarrow} N\left(0,\frac{1}{n} \nabla h(\beta)^{T} \cdot \Sigma \cdot \nabla h(\beta)\right)$$ 

- 위 식에 대해서, 우리가 계산한 값들을 집어넣어서 위 식을 풀어 써 봅시다.

$$\begin{aligned}
\frac{1}{n} \nabla f(\vec{\mu})^{T}\left[\begin{array}{cc}
\sigma_{y}^{2} & \sigma_{y x} \\
\sigma_{y x} & \sigma_{x}^{2}
\end{array}\right] \nabla f(\vec{\mu}) &=\left[\begin{array}{c}
\frac{1}{\mu_{x}} \\
\frac{-\mu_{y}}{\mu_{x}^{2}}
\end{array}\right]^{T}\left[\begin{array}{cc}
\sigma_{y}^{2} / n & \sigma_{y x} / n \\
\sigma_{y x} / n & \sigma_{x}^{2} / n
\end{array}\right]\left[\begin{array}{c}
\frac{1}{\mu_{x}} \\
\frac{-\mu_{y}}{\mu_{x}^{2}}
\end{array}\right] \\
&=\left[\frac{1}{\mu_{x}} \cdot \frac{\sigma_{y}^{2}}{n}-\frac{\mu_{y}}{\mu_{x}^{2}} \cdot \frac{\sigma_{x y}}{n}, \frac{1}{\mu_{x}} \cdot \frac{\sigma_{x y}}{n}-\frac{\mu_{y}}{\mu_{x}^{2}} \cdot \frac{\sigma_{x}^{2}}{n}\right]\left[\begin{array}{c}
\frac{1}{\mu_{x}} \\
\frac{-\mu_{y}}{\mu_{x}^{2}}
\end{array}\right] \\
&=\frac{\sigma_{y}^{2}}{n \mu_{x}^{2}}-\frac{\mu_{y} \sigma_{x y}}{n \mu_{x}^{3}}-\frac{\mu_{y} \sigma_{x y}}{n \mu_{x}^{3}}+\frac{\mu_{y}^{2} \sigma_{x^{2}}^{2}}{n \mu_{x}^{4}} \\
&=\frac{\sigma_{y}^{2}}{n \mu_{x}^{2}}-2 \frac{\mu_{y} \sigma_{x y}}{n \mu_{x}^{3}}+\frac{\sigma_{x}^{2} \mu_{y}^{2}}{n \mu_{x}^{4}} \\
&=\frac{1}{n} \frac{\mu_{y}^{2}}{\mu_{x}^{2}}\left[\frac{\sigma_{y}^{2}}{\mu_{y}^{2}}-2 \frac{\sigma_{x y}}{\mu_{x} \mu_{y}}+\frac{\sigma_{x}^{2}}{\mu_{x}^{2}}\right]
\end{aligned}$$

> Step 4 : Test - Estimator

- 이제 위에서 계산된 Variation 을 아래처럼 정의합시다.

$$\sigma_{R}^{2}=\frac{\sigma_{y}^{2}}{n \mu_{x}^{2}}-2 \frac{\mu_{y} \sigma_{x y}}{n\mu_{x}^{3}}+\frac{\sigma_{x}^{2} \mu_{y}^{2}}{n \mu_{x}^{4}},$$

- 그러면 아래와 같이 ratio - Test estimator 는 아래처럼 정의됩니다.

$$\left(\frac{\bar{y}}{\bar{x}}-\frac{\mu_{y}}{\mu_{x}}\right) \sim N\left(0, \sigma_{R}^{2}\right)$$

- 이제 위처럼 Normal 을 따른다는것을 알았으므로, 이를 이용해서 Testing Procedure 를 만들 수 있습니다.

> ## Test Procedure : one Variation

- $H_0$ : $\frac{\mu_y}{\mu_x} = 1 $  vs $H_1 : \frac{\mu_y}{\mu_x} \not = 1$  
  - 위처럼 Mean 에 대한 Hypothesis 를 위처럼 정의한다고 합시다.
- 그러면 Test - Statistics 는 Under the Null Hypothesis 하에서 아래와 같이 정의됩니다.

$$\left(\frac{\bar{y}}{\bar{x}}-1\right) \sim N\left(0, \sigma_{R}^{2}\right)$$

- 이때 $\sigma^2_R$ 도 추정해야 하므로 최종적으로 아래와 같이 추정됩니다.
  - True Variance : $$\sigma_{R}^{2}=\frac{\sigma_{y}^{2}}{n \mu_{x}^{2}}-2 \frac{\mu_{y} \sigma_{x y}}{n\mu_{x}^{3}}+\frac{\sigma_{x}^{2} \mu_{y}^{2}}{n \mu_{x}^{4}},$$
  - Estimated Variance : $$\hat{\sigma^2_R} =\frac{s_{y}^{2}}{n \bar{x}^{2}}-2 \frac{\bar{y} s_{x y}}{n\bar{x}^{3}}+\frac{s_{x}^{2} \bar{y}^{2}}{n \bar{x}^{4}} $$

$$\left(\frac{\bar{y}}{\bar{x}}-1\right) \sim N\left(0, \hat\sigma_{R}^{2}\right)$$

> Confidence Interval

- 이때 Confidence interval 은 위에 의해서 아래와 같이 추정됩니다.

$$\underbrace{\frac{\bar{Y}}{\bar{X}}-1}_{\text {point estimate }} \pm \underbrace{\frac{z_{\alpha / 2}}{\sqrt{n} \bar{X}} \sqrt{s_{y}^{2}-2 \frac{\bar{Y}}{\bar{X}} s_{x y}+\frac{\bar{Y}^{2}}{\bar{X}^{2}} s_{x}^{2}}}_{\text {uncertainty quantification }}$$

> ## Test Procedure : Two Variation

> Remark : Two Sample Z Test

- If $X_{1}, X_{2}, \ldots, X_{n}$ and $Y_{1}, Y_{2}, \ldots, Y_{m}$ are independent with $X_{i} \sim N\left(\mu_{X}, \sigma_{X}^{2}\right)$ and $Y_{i} \sim N\left(\mu_{Y}, \sigma_{Y}^{2}\right)$ then

$$Z=\frac{(\bar{X}-\bar{Y})-\left(\mu_{X}-\mu_{Y}\right)}{\sqrt{\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}}} \sim N(0,1)$$

- 위 정리는 아래와 같이 증명 가능합니다.
  - $ \bar{X}-\bar{Y} \sim N\left(\mu_{X}-\mu_{Y}, \frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}\right)$
  - so the mean of $\bar{X}-\bar{Y}$ is $\mu_{X}-\mu_{Y}$ and the variance is $\sqrt{\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}}$.
  - Then $$\frac{(\bar{X}-\bar{Y})-\left(\mu_{X}-\mu_{Y}\right)}{\sqrt{\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}}} \sim N(0,1)$$

> Application in Delta Method

- Delta Method 에서도 똑같이 적용할 수 있습니다.
- 먼저 아래와 같이 값들을 정의합시다.
  - control 의 분자평균 : $\mu^C_y$
  - control 의 분모평균 : $\mu^C_x$
  - Treatment 의 분자평균 : $\mu^T_y$
  - Treatment 의 분모평균 : $\mu^T_x$
- 이제 Test 에 대한 Hypothesis 는 아래와 같습니다.
  - $H_0$ : $\frac{\mu^C_y}{\mu^C_x}-\frac{\mu^T_y}{\mu^T_x} = 0 $  vs $H_0$ : $\frac{\mu^C_y}{\mu^C_x}-\frac{\mu^T_y}{\mu^T_x} \not= 0 $ 
- 위에 대해서 이제 각각 아래의 같은 정리가 성립합니다.
  - Control : $$\left(\frac{\bar{y^C}}{\bar{x^C}}-\frac{\mu^C_{y}}{\mu^C_{x}}\right) \sim N\left(0, \sigma_{R}^{C^{2}}\right)$$
  - Treatment : $$\left(\frac{\bar{y^T}}{\bar{x^T}}-\frac{\mu^T_{y}}{\mu^T_{x}}\right) \sim N\left(0, \sigma_{R}^{T^{2}}\right)$$
- 위 정리를 이용하면 Null Hypothesis 하에서 아래와 같은 Test - Estimator 를 얻을 수 있습니다
  - Two Sample : $$\left(\frac{\bar{y^T}}{\bar{x^T}}-\frac{\bar{y^C}}{\bar{x^C}}\right) \sim N\left(0, \sigma_{R}^{C^{2}} + \sigma_{R}^{T^{2}}\right)$$
- 이제 위를 이용해서 Testing 을 하면 됩니다!

> ## Two Variation Example

- Treatment 와 Control 이 있다고 합시다. 
  - 이때 우리의 측정항목은 CTR = 클릭수/조회수입니다. 
  - 먼저 각 Variant 에 대한 CTR 의 평균을 계산해봅시다.

$$\begin{aligned}
\overline{C T R}_{\text {treatment }} &=\frac{\text { Total Clicks }}{\text { Total Views }} \\
\overline{C T R}_{\text {control }} &=\frac{\text { Total Clicks }}{\text { Total Views }}
\end{aligned}$$

- 그런 다음 Y는 클릭이고 X는 조회수인 비율에 대한 분산 공식을 사용하여 CTR의 분산을 계산합니다.

$$\operatorname{Var}(C T R) \approx \frac{1}{n} \frac{\mu_{y}^{2}}{\mu_{x}^{2}}\left[\frac{\sigma_{y}^{2}}{\mu_{y}^{2}}-2 \frac{\operatorname{Cov}(X, Y)}{\mu_{x} \mu_{y}}+\frac{\sigma_{x}^{2}}{\mu_{x}^{2}}\right]$$

- 마지막으로 t-값을 계산할 수 있습니다. 
  - 절대 t-값이 임계값보다 크면 귀무 가설을 기각합니다. 
  - 반대로 절대 t-값이 임계값보다 작으면 귀무 가설을 기각하지 못합니다.


$$T=\frac{\overline{C T R}_{\text {treatment }}-\overline{C T R}_{\text {control }}}{\sqrt{\operatorname{Var}\left(\overline{C T R}_{\text {treatment }}\right)+\operatorname{Var}\left(\overline{C T R}_{\text {control }}\right)}}$$

> ## Code Example

- 아래와 같이 파이썬에서 구현한 Code Example 을 통해서 확인해볼 수 있습니다.

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
             'mean_treatment':mean_treatment,
             'var_control':var_control,
             'var_treatment':var_treatment,
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

# [Real Application](#link){: .btn .btn--primary}{: .align-center}

> ## Two Sample T Test : When Analysis unit = Randomization Unit

| row  | experiment_key | User_id | # User | Clicks |
| ---- | -------------- | ------- | ------ | ------ |
| 1    | A              | 142     | 1      | 13     |
| 2    | B              | 155     | 1      | 9      |
| 3    | A              | 160     | 1      | 10     |
| 4    | B              | 324     | 1      | 0      |
| 5    | B              | 992     | 1      | 2      |

- 위와 같이 유저당 클릭수 값에 대해서  A 와 B 를 비교하는 경우에는 딱히 Delta Method 가 아니라 T-Test 를 써도 될 것입니다. (왜냐하면 면  Analysis Unit 과 Randomization Unit 이 같기 때문이죠.)
  - 하지만 이런 경우에 어떻게든 Delta Method 를 쓰게 되면 어떤 일이 벌어질까요? 
  - 혹시 그 결과가 달라지지는 않을까요? 

> Delta Method

- 먼저 Delta Method 에 대해서 Remind 해 봅시다.
- 먼저 아래와 같이 값들을 정의합시다.
  - control 의 분자평균 : $\mu^C_y$
  - control 의 분모평균 : $\mu^C_x$
  - Treatment 의 분자평균 : $\mu^T_y$
  - Treatment 의 분모평균 : $\mu^T_x$
- 이제 Test 에 대한 Hypothesis 는 아래와 같습니다.
  - $H_0$ : $\frac{\mu^C_y}{\mu^C_x}-\frac{\mu^T_y}{\mu^T_x} = 0 $  vs $H_0$ : $\frac{\mu^C_y}{\mu^C_x}-\frac{\mu^T_y}{\mu^T_x} \not= 0 $ 
- 위에 대해서 이제 각각 아래의 같은 정리가 성립합니다.
  - Control : $$\left(\frac{\bar{y^C}}{\bar{x^C}}-\frac{\mu^C_{y}}{\mu^C_{x}}\right) \sim N\left(0, \sigma_{R}^{C^{2}}\right)$$
  - Treatment : $$\left(\frac{\bar{y^T}}{\bar{x^T}}-\frac{\mu^T_{y}}{\mu^T_{x}}\right) \sim N\left(0, \sigma_{R}^{T^{2}}\right)$$
- 위 정리를 이용하면 Null Hypothesis 하에서 아래와 같은 Test - Estimator 를 얻을 수 있습니다
  - Two Sample : $$\left(\frac{\bar{y^T}}{\bar{x^T}}-\frac{\bar{y^C}}{\bar{x^C}}\right) \sim N\left(0, \sigma_{R}^{C^{2}} + \sigma_{R}^{T^{2}}\right)$$
- 이제 위 Procedure 를 똑같이 Two Sample Test 로 수행해 보겠습니다.

> $\frac{\bar{y^T}}{\bar{x^T}}-\frac{\bar{y^C}}{\bar{x^C}}$ 계산

- 이때 위의 계산은 'x' 가 샘플 수로 계산되므로, mean 으로 계산한다면 $\bar{x}^T = \bar{x}^C =1$ 입니다. 
- 즉 $\frac{\bar{y^T}}{\bar{x^T}}-\frac{\bar{y^C}}{\bar{x^C}}=\bar{y^T} - \bar{y^C}$ 가 됩니다.

> $\sigma_{R}^{C^{2}} + \sigma_{R}^{T^{2}}$ 계산

- 우선 일반적인 $\sigma_R^{2}$ 에 대해서 계산해봅시다. 이때 $$\sigma_{R}^{2}=\frac{\sigma_{y}^{2}}{n \mu_{x}^{2}}-2 \frac{\mu_{y} \sigma_{x y}}{n\mu_{x}^{3}}+\frac{\sigma_{x}^{2} \mu_{y}^{2}}{n \mu_{x}^{4}}$$ 입니다.
- 여기에서 $X = \{x_1,x_2...x_n\} = \{1,1,1,...1\}$ 을 고려하면 $\mu_x = 1$ ,$\sigma_x = 0$ 입니다. 
  - 즉 $$\sigma_{R}^{2}=\frac{\sigma_{y}^{2}}{n}-2 \frac{\mu_{y} \sigma_{x y}}{n}$$ 가 됩니다.
- 그리고 $Cov(x,y) = E[(X-\mu_x)(Y-\mu_y)]=E[(0)(Y-\mu_y)]=0$ 이 됩니다.
  - 즉 $$\sigma_{R}^{2}=\frac{\sigma_{y}^{2}}{n}$$ 가 됩니다. 
- 즉 $\sigma_{R}^{C^{2}} + \sigma_{R}^{T^{2}} =\frac{\sigma_{y}^{C^2}}{n_C}+ \frac{\sigma_{y}^{T^2}}{n_T}$ 가 됩니다.

> 계산

- 즉 이를 종합하면 아래와 같이 계산되게 됩니다.
- Two Sample : $$\bar{y^T} - \bar{y^C} \sim N\left(0, \frac{\sigma_{y}^{C^2}}{n_C}+ \frac{\sigma_{y}^{T^2}}{n_T}\right)$$
- 앗! 이는 Two Sample Mean Test 와 같은 형식입니다.
  - 즉 Delta Method 를 적용한다고 하더라도 Two Sample Z Test 와 같은 테스트를 하게 되는 것입니다.

> 추정시에도 동일한가? 

- $\frac{\bar{y^T}}{\bar{x^T}}-\frac{\bar{y^C}}{\bar{x^C}}$ 은 $\frac{\bar{y^T}}{n_T}-\frac{\bar{y^C}}{n_C}$ 로 추정됩니다. 
- $$\hat{\sigma^2_R} =\frac{s_{y}^{2}}{n \bar{x}^{2}}-2 \frac{\bar{y} s_{x y}}{n\bar{x}^{3}}+\frac{s_{x}^{2} \bar{y}^{2}}{n \bar{x}^{4}}$$ 
  - $$s_{xy}=\operatorname{Cov}(X, Y)=\frac{\sum_{i}^{n}\left(X_{i}-\bar{X}\right)\left(Y_{i}-\bar{Y}\right)}{n-1}$$ 으로 추정됩니다. 이때 $X = \{x_1,x_2...x_n\} = \{1,1,1,...1\}$ 을 고려하면 $s_{xy} =0$ 입니다.
  - $\bar{x} = 1$ , $s_x=0$ 입니다. 
- 즉 정리하면 $$\hat{\sigma^2_R}= \frac{s_y^2}{n}$$ 으로 추정되고, 이는 Two Sample Mean Test 와 같은 값을 가지게 될 것입니다.

> 결론

- Delta Method 의 Test Statistics : $$\left(\frac{\bar{y^T}}{\bar{x^T}}-\frac{\bar{y^C}}{\bar{x^C}}\right) /\sqrt{\left( \sigma_{R}^{C^{2}} + \sigma_{R}^{T^{2}}\right)}$$
- $x_T$ 에 Analysis Unit 이 적용될때의 Delta Method Test Statistics : $$\left(\frac{\bar{y^T}}{n_T}-\frac{\bar{y^C}}{n_C}\right) /\sqrt{\left( \frac{\sigma_{y}^{C^2}}{n_C}+ \frac{\sigma_{y}^{T^2}}{n_T}\right)}$$
- Two-Sample Z Test 의 Test Statistics :  $$\left(\frac{\bar{y^T}}{n_T}-\frac{\bar{y^C}}{n_C}\right) /\sqrt{\left( \frac{\sigma_{y}^{C^2}}{n_C}+ \frac{\sigma_{y}^{T^2}}{n_T}\right)}$$
- 즉, 위에 따라서 Analysis Unit 과 Randomization Unit 이 같다면 Two Sample T Test 와 Delta Method 는 같은 결론을 내게 됩니다.

> ## Two Sample T Test : Filter 

| row  | experiment_key | User_id | # User | Clicks |
| ---- | -------------- | ------- | ------ | ------ |
| 1    | A              | 142     | 0      | 0      |
| 2    | B              | 155     | 1      | 9      |
| 3    | A              | 160     | 1      | 10     |
| 4    | B              | 324     | 0      | 0      |
| 5    | B              | 992     | 1      | 2      |

- 위와 같이 "Randomization Unit" 과 "Analysis Unit" 이 같긴 하지만, 유저를 필터링해서 분석하는 경우도 있습니다.
  - 한 예시로 웹페이지 메뉴의 "help" 메뉴를 개선했다고 합시다. 그러면 help 메뉴를 사용하는 유저에 한해서 메트릭을 분석하고자 하려는 니즈가 있을 것입니다.
  - 그런 경우에 위와같이 User 집계시에 필터링을 걸어서 그 유저에 대해서만 분석하려고 할 수 있습니다. (0 : 필터링 되어서 제외된 유저)
- 필터링된 유저에 대해서는 Two - Sample - T Test 를 수행할 수 있습니다.
- 물론 이때 쌩으로 Delta Method 를 적용하더라도 평균은 같게 비교하게 됩니다.
  - $n'$  = 필터링되고 남은 유저 수 라고 합시다. 그러면 위 표의 전체 사람에 대해서 $n'=3$ 이 됩니다.
  - 그리고 $n'$ 를 이용해서 계산된 평균을 $\bar{x}'$ 라고 합시다. 그러면 위 표에서 B variation 의 평균은 (9+2) / 2 입니다.
  - 즉 $\frac{\bar{y^T}}{\bar{x^T}}-\frac{\bar{y^C}}{\bar{x^C}}= \frac{\sum y^T}{\sum x^T} - \frac{\sum y^C}{\sum{x^C}} = \frac{\bar{y^T}'}{\bar{x^T}'}-\frac{\bar{y^C}'}{\bar{x^C}'}$ 가 됩니다. 
  - 즉 Delta method 의 비교시에는 $\frac{\bar{y^T}}{\bar{x^T}}-\frac{\bar{y^C}}{\bar{x^C}}$  을 쓰고, T Test 시에는 $\frac{\bar{y^T}'}{\bar{x^T}'}-\frac{\bar{y^C}'}{\bar{x^C}'}$ 를 사용하는데 두 값이 같으므로 차이는 같게 추정하게 되죠. 
- 그러면 Delta method 를 적용했을떄와 T-Test 를 적용했을때의 결과가 같게 될까요? (즉 분산 추정도 같게 될까요?)

> Delta Method

- 다시 Delta Method 에 대해서 Remind 해 봅시다.
- 먼저 아래와 같이 값들을 정의합시다.
  - control 의 분자평균 : $\mu^C_y$
  - control 의 분모평균 : $\mu^C_x$
  - Treatment 의 분자평균 : $\mu^T_y$
  - Treatment 의 분모평균 : $\mu^T_x$
- 이제 Test 에 대한 Hypothesis 는 아래와 같습니다.
  - $H_0$ : $\frac{\mu^C_y}{\mu^C_x}-\frac{\mu^T_y}{\mu^T_x} = 0 $  vs $H_0$ : $\frac{\mu^C_y}{\mu^C_x}-\frac{\mu^T_y}{\mu^T_x} \not= 0 $ 
- 위에 대해서 이제 각각 아래의 같은 정리가 성립합니다.
  - Control : $$\left(\frac{\bar{y^C}}{\bar{x^C}}-\frac{\mu^C_{y}}{\mu^C_{x}}\right) \sim N\left(0, \sigma_{R}^{C^{2}}\right)$$
  - Treatment : $$\left(\frac{\bar{y^T}}{\bar{x^T}}-\frac{\mu^T_{y}}{\mu^T_{x}}\right) \sim N\left(0, \sigma_{R}^{T^{2}}\right)$$
- 위 정리를 이용하면 Null Hypothesis 하에서 아래와 같은 Test - Estimator 를 얻을 수 있습니다
  - Two Sample : $$\left(\frac{\bar{y^T}}{\bar{x^T}}-\frac{\bar{y^C}}{\bar{x^C}}\right) \sim N\left(0, \sigma_{R}^{C^{2}} + \sigma_{R}^{T^{2}}\right)$$
- 이제 위 Procedure 를 똑같이 Two Sample Test 로 수행해 보겠습니다.

> $\frac{\bar{y^T}}{\bar{x^T}}-\frac{\bar{y^C}}{\bar{x^C}}$ 계산

- $n'$  = 필터링되고 남은 유저 수 라고 합시다. 그러면 위 표에서 $n'=3$ 이 됩니다.
- 그리고 $n'$ 를 이용해서 계산된 평균을 $\bar{x}'$ 라고 합시다. 그러면 위 표에서 B variation 의 평균은 (9+2) / 2 입니다.
- 즉 $\frac{\bar{y^T}}{\bar{x^T}}-\frac{\bar{y^C}}{\bar{x^C}}= \frac{\sum y^T}{\sum x^T} - \frac{\sum y^C}{\sum{x^C}} = \frac{\bar{y^T}'}{\bar{x^T}'}-\frac{\bar{y^C}'}{\bar{x^C}'}$ 가 됩니다.

> $\sigma_{R}^{C^{2}} + \sigma_{R}^{T^{2}}$ 계산

- 우선 일반적인 $\sigma_R^{2}$ 에 대해서 계산해봅시다. 이때 $$\sigma_{R}^{2}=\frac{\sigma_{y}^{2}}{n \mu_{x}^{2}}-2 \frac{\mu_{y} \sigma_{x y}}{n\mu_{x}^{3}}+\frac{\sigma_{x}^{2} \mu_{y}^{2}}{n \mu_{x}^{4}}$$ 입니다.
- 여기에서 $X = \{x_1,x_2...x_n\} = \{1,0,0,...1\}$ 을 고려하면 $\mu_x = n'/n$ ,$\sigma_x^2 = (n-n')n'/n^2$ 입니다. 
  - 즉 $$\sigma_{R}^{2}=\frac{n\sigma_{y}^{2}}{n'^2}-2 \frac{n^2\mu_{y}\sigma_{xy}}{n'^3}+\frac{n(n-n') \mu_{y}^{2}}{n'^3}$$ 가 됩니다.
- 그리고 $Cov(x,y) = E[(X-\mu_x)(Y-\mu_y)]=E[XY]-\mu_x\mu_y=\mu_y-(n'/n)\mu_y$ 이 됩니다.
  - 즉 $$\sigma_{R}^{2}=\frac{\sigma_{y}^{2}}{n}$$ 가 됩니다. 
- 즉 $$\sigma_{R}^{2}=\frac{n\sigma_{y}^{2}}{n'^2}-2 \frac{n^2\mu_{y}\frac{n-n'}{n}\mu_y}{n'^3}+\frac{n(n-n') \mu_{y}^{2}}{n'^3} = \frac{n\sigma_{y}^{2}}{n'^2}-\frac{n(n-n') \mu_{y}^{2}}{n'^3} $$

> Conclusion

- 즉 값이 다르게 됩니다. (실제 코드 레벨로 볼때 다름..)
- 이 이유는 사실 Two Sample T - Test 의 경우 'Filter' 된 데이터만이 모집단이라고 생각하고 계산되고, 그에 반해서 Delta Method 는 필터되기 전 값 모두를 모집단이라고 생각하기때문에 여기에서 차이가 나게 됩니다.

> ## Two Sample Proportion Test : When Analysis unit = Randomization Uni

- 이 경우에는 다소 당연하지만 , 일치합니다. 
  - 이전과 같은 로직 따라가면 되어요. 
  - 어짜피 Proportion Test 도 결국에는 Mean Test 이니깐용
- 그런데.. 이떄  Agg Unit 이 안되는 경우의 CTR 도 존재하기 땜시... 

> ## Code Level Check

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
             'mean_treatment':mean_treatment,
             'var_control':var_control,
             'var_treatment':var_treatment,
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

# [Conclusion](#link){: .btn .btn--primary}{: .align-center}

> ## Issue

- Delta Method 를 이용하면 아래와 같은 문제가 있는 경우에도 분석을 할 수 있습니다.
  - 예시로 아래처럼 views 당 click 수를 분석하려고 한다고 합시다.

> Randomization unit $\not=$ Analysis Unit

- Views 당 click 수 분석을 하는데, experiment_key 배정은 User_id 기준으로 이루어졌다고 합시다.
- 이때에 아래처럼 Randomization 가정이 깨져서 분석할 수 없습니다.

| row  | experiment_key | User_id | Views_id (agg) | Clicks |
| ---- | -------------- | ------- | -------------- | ------ |
| 1    | A              | 142     | Af2f           | 13     |
| 2    | A              | 142     | 2df9d          | 9      |
| 3    | A              | 142     | f0bm           | 10     |
| 4    | B              | 3362    | 0hns           | 0      |
| 5    | B              | 3362    | 9ddm           | 2      |
| 6    | A              | 93      | 4gbb           | 5      |
| 7    | A              | 93      | F0vk           | 4      |

> AGG is Impossible

- 또한 Randomization unit 과 Analysis unit 이 달라서 어거지로 분석하려 한다고 해도 아래와 같은 문제가 있을 수 잇습니다.

| row  | experiment_key | User_id | Views_id (agg) | Clicks |
| ---- | -------------- | ------- | -------------- | ------ |
| 1    | A              | 142     | 집계불가       | 32     |
| 2    | B              | 3362    | 집계불가       | 2      |
| 3    | A              | 93      | 집계불가       | 9      |

- 위와 같이 AGGREGATION 이 불가능한 경우가 있을 것입니다. 
  - 이런 경우에는 애초에 Views_id 기준으로 clicks 을 나눌수도 없기때문에 분산 ($s_{clicks}$) 을 구할 수 없습니다. 
  - 또한 Random Sample 자체가 $X_{clicks} = \{x_1,x_2...x_n\}$ 정의가 안되기때문에 Views 당 Clicks 수를 정의할수도 없죠

> ## Delta Method ! 

- 위와 같은 상황에서 바로 Delta Method 를 쓸 수 있는 것입니다! 
- AGG Unit 이 '유저' 라는것은 보장된 상황에서 집계가 가능하다면 우리는 Test 를 할 수 있습니다.

---

**reference**

- https://medium.com/@ahmadnuraziz3/applying-delta-method-for-a-b-tests-analysis-8b1d13411c22
- https://alexdeng.github.io/public/files/jsm2011-deng.pdf
- https://arxiv.org/pdf/1803.06336.pdf
- https://stats.stackexchange.com/questions/398436/a-b-testing-ratio-of-sums
- http://www.stat.rice.edu/~dobelman/notes_papers/math/TaylorAppDeltaMethod.pdf
- https://stats.stackexchange.com/questions/291594/estimation-of-population-ratio-using-delta-method/291652



