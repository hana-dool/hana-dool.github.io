---
title: "Online Experiments Tricks-Variance Reduction"
excerpt: "Stratification, CUPED, Variance-Weighted Estimators,CUPAC,MLRATE"
categories:
  - AB_Article
last_modified_at: 2022-03-12

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

Variance 를 조금이라도 줄이기 위한 걸래짜내기
{: .notice--warning}

# [**Online Experiments Tricks — Variance Reduction**](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

- 우리가 온라인 실험, 또는 A/B 테스트를 할떄, 우리는 테스트가 높은 통계적 검정력을 가지기를 바랍니다. 
- 이러한 Statistical Power(통계적 검정력) 를 달성하기 위해서는 다음과 같은 factor 들이 고려되어야 합니다.
  - effect size 
  - Sample size 
  - metric's sampling variance 
  - significance level alpha
- 일반적으로 power 를 올리기위해서라면 sample size 를 올리면 됩니다. 
  - 하지만 minimum detectable effect 는  1/sqrt(sample_size) 에 비례하기 때문에, 어느정도의 수준을 넘게되면 샘플 사이즈가 많이 커져도 검정력에는 큰 차이가 없을 수 있습니다.
  - 또한 단순히 실험을 오래하거나 샘플을 늘리는것이 말은 쉽지만 적용하기 힘든 경우가 많습니다. 
- 위 다양한 factor 중에서 주로 사용되는 방법은 우리가 통제할 수 있는 factor 인 "metric의 분산을 줄이는" 방식으로 진행됩니다.
- 아래에서는 분산 감소 기법을 살펴보고 간단한 예시들을 살펴보려고 합니다.

> 우리가 살펴볼것 

- **Stratification and post-stratification**
- **CUPED** (controlled-experiment using pre-experiment data)
- **Variance-Weighted Estimators**
- ML - based 
  - **CUPAC** (control using predictions as covariates)
  - **MLRATE** (machine learning regression-adjusted treatment effect estimator)

> ## Stratification 

![jpg](/assets/images/Program/77_5.jpg){: .align-center}

- Stratified Sampling 의 Population 을 k 개의 버킷으로 나눕니다.
  - ex : 국가별로 한국 , 미국, 일본... 유저로 나눌 수 있습니다. 
- 그리고 각각의 stratum 에서 샘플을 뽑아냅니다.
- $Y_{strat}$ 를 이러한 Stratified 샘플링에서 측정되는 Treatment 효과라고 합시다. 
  - 우리는 $Y_{strat}$ 이 Unbiased Estimator 임을 기대할 것입니다.
- $p_k$ 를 각 계층 k 에서 샘플링 비율이라고 합시다.

$$\begin{aligned}
&E\left(Y_{\text {strat }}\right)=\sum p_{k} E\left(\bar{Y}_{k}\right)=\sum p_{k} \mu_{k}=\mu \\
&\operatorname{Var}\left(Y_{\text {strat }}\right)=\sum p_{k}^{2} \operatorname{Var}\left(\bar{Y}_{k}\right)=\frac{1}{n} \sum p_{k} \sigma_{k}^{2}
\end{aligned}$$

- 위처럼 우리가 구한 $Y_{strat}$ 추정량은 $\mu$ 에 대해서 Unbiased 추정량입니다. 
- 또한 Variance 는 일반적인 Simple Random Sampling 일떄보다 작습니다 
  - 이에 대해서는 https://www.kdd.org/kdd2016/papers/files/adp0945-xieA.pdf 참조 

> Pros and Cons 

- 장점

  - Stratification method 는 Treatment effect 가 unbiased estimator 임을 보장합니다. 
  - 그리고 또한 효과적으로 Strata 간의 variance 를 줄여줍니다.

- 단점 

  - 일반적으로 이렇게 실험 전에 데이터를 사용하여서 , 사용자를 분류하는것은 어렵습니다. 

  - “In the online world, because we collect data as they arrive over time, we are usually unable to sample from strata formed ahead of time.” (Deng, Xu, Kohavi, & Walker, 2013)
  - *In practice, implementing stratified sampling is complicated and expensive. It “requires a queue system and the use of multiple machines.” (Xie & Aurisset, 2016)*

> Post Stratification (사후 계층화)

- 실제로는 실험 이전에 계층화 하는것보다는, 실험 이후에 계층화를 수행하는것이 훨씬 더 실용적입니다. 
- 사후 계층화는 먼저 모집단을 무작위로 샘플링한 다음 개개인을 해당하는 계층에 배치하게 됩니다. 
- 이런 방법은, 이전의 Stratification 과 동일하게 분산 감소를 기대할 수 있습니다.

![jpg](/assets/images/Program/77_6.jpg){: .align-center}

- 아래 코드는 서로 다른 4개의 정규분포에서 데이터를 생성하고 (즉 4개의 stratum 에서) , 개개인을 Treatment 또는 Control 에 할당하고, Treatment 효과를 Treatment 에 추가한 뒤, bootstrap 을 통해서 Treatment 효과를 시각화 하는 예시입니다.
- 이떄 시뮬레이션 할떄 Treatment 효과를 만들기 위해, Treatment 에 속하는 모든 유저에 대해 Treatment 효과를 균일하게 더해주었습니다. 

```python
import pandas as pd
import numpy as np
import hvplot.pandas
from scipy.stats import pearsonr
from scipy.optimize import minimize

def generate_strata_data(treatment_effect, size):
    # for each strata, generate y from a normal distribution
    df1 = pd.DataFrame({'strata': 1, 'y': np.random.normal(loc=10, scale=1, size=size)})
    df2 = pd.DataFrame({'strata': 2, 'y': np.random.normal(loc=15, scale=2, size=size)})
    df3 = pd.DataFrame({'strata': 3, 'y': np.random.normal(loc=20, scale=3, size=size)})
    df4 = pd.DataFrame({'strata': 4, 'y': np.random.normal(loc=25, scale=4, size=size)})
    df = pd.concat([df1, df2, df3, df4])
    # random assign rows to two groups 0 and 1 
    df['group'] = np.random.randint(0,2, df.shape[0])
    # for treatment group add a treatment effect 
    df.loc[df["group"] == 1, 'y'] += treatment_effect
    return df   

def meandiff(df):
    return df[df.group==1].y.mean() - df[df.group==0].y.mean()

def strata_meandiff(df):
    get_sum = 0
    for i in df.strata.unique():
        get_sum += meandiff(df[df.strata==i])
    return get_sum/len(df.strata.unique())


meandiff_lst = []
strata_meandiff_lst = []
for i in range(100):
    df = generate_strata_data(treatment_effect=1, size=100)
    meandiff_lst.append(meandiff(df))
    strata_meandiff_lst.append(strata_meandiff(df))
    
(
    pd.DataFrame(strata_meandiff_lst).hvplot.kde(label='Stratification') 
    * pd.DataFrame(meandiff_lst).hvplot.kde(label='Original')
)
```

![jpg](/assets/images/Stat/158_2.jpg){: .align-center}

- 위와 같이 Stratification 을 적용한 상태에서의 Treatment effect 의 추정이 훨씬 더정확한것을 볼 수 있습니다!

> ## CUPED 

- CUPED (Controlled-experiment using pre-experiment data) 은 Microsoft 에서 2013 년 발표한 방법론입니다. 
- 이 방법론은 현재 Nefilx , Booking , Tripadvisor 등 여러 업체에서 매우 요긴하게 사용하고 있습니다. 
- CPUED 는 Pre-experiment data X 를 Control Covariate 로 사용하게 됩니다. ( 자세한것은, paper 참조 )

![jpg](/assets/images/Stat/158_3.jpg){: .align-center}

![jpg](/assets/images/Stat/158_4.jpg){: .align-center}

- 즉 다른말로, Y 의 분산은 (1-cor(X,Y)) 만큼 감소합니다. 
- CUPED 가 잘 작동하려면 X 와 Y 의 상관관계가 높아야 합니다.
  - 그래서 원본 논문에서는 실험 전의 Experiment Data 를 X 로 활용하고는 합니다. 

> Code Example

- Treatment 와 control 의 평균차이를 임의로 설정한 뒤에, 여러번 시뮬레이션 해보겠습니다.
- 아래의 예시를 보면  Treatment 와 Control 모두 분산이 감소한것을 볼 수있습니다.
- 또한 분산 감소 비율은 0.2789 로서, 1-corr(X<Y) 와 일치하는것을 볼 수 있습니다. 

```python

def generate_data(treatment_effect, size):
    # generate y from a normal distribution
    df = pd.DataFrame({'y': np.random.normal(loc=0, scale=1, size=size)})
    # create a covariate that's corrected with y 
    df['x'] = minimize(
        lambda x: 
        abs(0.95 - pearsonr(df.y, x)[0]), 
        np.random.rand(len(df.y))).x
    # random assign rows to two groups 0 and 1 
    df['group'] = np.random.randint(0,2, df.shape[0])
    # for treatment group add a treatment effect 
    df.loc[df["group"] == 1, 'y'] += treatment_effect
    return df    

df = generate_data(treatment_effect=1, size=10000)
theta = df.cov()['x']['y'] / df.cov()['x']['x']
df['y_cuped'] = df.y - theta * df.x

(
    df.hvplot.kde('y', by='group', xlim = [-5,5], color=['#F9a4ba', '#f8e5ad']) 
    + df.hvplot.kde('y_cuped', by='group', xlim = [-5,5], color=['#F9a4ba', '#f8e5ad'])
)
view rawvariance_reduction_cuped1.py hosted with ❤ by GitHub
```

![jpg](/assets/images/Stat/158_5.jpg){: .align-center}

![jpg](/assets/images/Stat/158_6.jpg){: .align-center}

- 이제 CUPED 를 적용한 실험과, 적용하지 않은 실험의 Treatment effect 를 한번 비교해 보겠습니다.

```python
def generate_data(treatment_effect, size):
    # generate y from a normal distribution
    df = pd.DataFrame({'y': np.random.normal(loc=0, scale=1, size=size)})
    # create a covariate that's corrected with y 
    df['x'] = minimize(
        lambda x: 
        abs(0.95 - pearsonr(df.y, x)[0]), 
        np.random.rand(len(df.y))).x
    # random assign rows to two groups 0 and 1 
    df['group'] = np.random.randint(0,2, df.shape[0])
    # for treatment group add a treatment effect 
    df.loc[df["group"] == 1, 'y'] += treatment_effect
    return df   

def meandiff(df):
    return df[df.group==1].y.mean() - df[df.group==0].y.mean()

def cuped_meandiff(df):
    theta = df.cov()['x']['y'] / df.cov()['x']['x']
    df['y_cuped'] = df.y - theta * df.x
    return df[df.group==1].y_cuped.mean() - df[df.group==0].y_cuped.mean()


meandiff_lst = []
cuped_meandiff_lst = []
for i in range(200):
    df = generate_data(treatment_effect=1, size=100)
    meandiff_lst.append(meandiff(df))
    cuped_meandiff_lst.append(cuped_meandiff(df))
    
pd.DataFrame(cuped_meandiff_lst).hvplot.kde(label='CUPED') * pd.DataFrame(meandiff_lst).hvplot.kde(label='Original')
```

![jpg](/assets/images/Stat/158_1.jpg){: .align-center}

> 장단점 

- CUPED 는 상대적으로 쉽고 적용이 쉽습니다. 
- 하지만 Covariate 를 고르는작업이 다소 Tricky 합니다. 
  - 특히 특정한 유저의 pre-experiment 가 없을때에 대처하기가 까다롭습니다.
  - 또한 공변량(X) 은 측정값 (Y) 와 상관있는 값이여야 합니다. 
- https://j-sephb-lt-n.github.io/exploring_statistics/cuped_cupac_and_other_variance_reduction_techniques.html#controlvariates
  - 위 게시물은 CUPED 를 하나의 공변량에서 여러 공변량으로 어떻게 확장할 수 있는지를 알려줍니다. 

> ## Variance-Weighted Estimators

- Variance-Weighted Estimators 방법론은  2020년 Facebook과 Lyft의 Kevin Liou와 Sean Taylor에 의해 개발되었습니다. 
- 이 방법의 주요 아이디어는 실험 전 분산이 낮은 사용자에게 더 많은 가중치를 부여하는 것입니다.

![jpg](/assets/images/Stat/158_7.jpg){: .align-center}

- 이 방법론은 등분산적이라는 가정을 완화하고 대신 각 개인이 고유한 메트릭 분산을 가질 수 있다고 가정합니다. 
  - 예를 들어, 위의 그림은 두 개인을 보여줍니다. 여기서 한 사람(녹색 선)은 다른 사람(파란색 선)보다 분산이 더 높습니다.
- 아래의 식에서 $\mathrm{Y}$ 는 관심 메트릭, $\delta$ 는 Treatment 효과, $\mathrm{Z}$ 는 Treatment 의 지표 함수입니다.

![jpg](/assets/images/Stat/158_8.jpg){: .align-center}

- 이때 Treatment 의 분산을 최소화 하기 위해서, 분산의 역수로 각 사용자에게 가중치를 부여하게 됩니다.
- 이때 주의깊게 보신분은 추정치를 계산할떄 , 사전에 변동량(variance) 을 추정해야한다는 것인데요,이 역시 사전 실험 데이터를 사용하게 됩니다. 
- 이 논문에서는 실험 전 시계열 데이터의 경험적 분산을 사용하고, ML 모델을 만들어 낸 뒤, 경험적 베이즈 추정기를 사용하여 분산을 추정하는 몇 가지 방법을 언급했습니다. 
  - 이중에서 가장 쉬운 방법은 empirical variance를 사용하는 것입니다.

> Bias 를 줄이는법

- 편향을 줄이기 위해 본 논문에서는 실험 전 분산을 기반으로 사용자를 버킷화하였습니다.
  - 그 이후에는 각 버킷에 대한 Treatment 의 평균을 계산했습니다..
  - 그 이후 각 버킷에 대한 pre-experiment variance 를 계산합니다.
  - 최종적으로는, strata 별로 계산된 variance 를 이용하여 weighted treatment mean 를 계산합니다.
- 즉 정리하면 variance 를 추정하고, 이를 기반으로 버켓을 나눈 뒤, 버켓당 inverse variance 를 추정하고 weighted treatment effect 를 계산해 냅니다.

> Code Example

- 다음은 이 방법을 보여주는 매우 간단한 예입니다.
- 4개의 계층으로 시작하여 각 계층의 메트릭 분산을 알고 있습니다. 
- 그런 다음 각 계층에 대한 역분산으로 치료 효과를 평가할 수 있습니다. 
- 이 예에서 분산 가중 추정기는 계층화 방법 외에도 분산 감소의 추가 이점을 제공합니다.

```python


def generate_strata_data(treatment_effect, size):
    # for each strata, generate y from a normal distribution
    df1 = pd.DataFrame({'strata': 1, 'pre_experient_variance':1, 'y': np.random.normal(loc=10, scale=1, size=size)})
    df2 = pd.DataFrame({'strata': 2, 'pre_experient_variance':2, 'y': np.random.normal(loc=15, scale=2, size=size)})
    df3 = pd.DataFrame({'strata': 3, 'pre_experient_variance':3, 'y': np.random.normal(loc=20, scale=3, size=size)})
    df4 = pd.DataFrame({'strata': 4, 'pre_experient_variance':4, 'y': np.random.normal(loc=25, scale=4, size=size)})
    df = pd.concat([df1, df2, df3, df4])
    # random assign rows to two groups 0 and 1 
    df['group'] = np.random.randint(0,2, df.shape[0])
    # for treatment group add a treatment effect 
    df.loc[df["group"] == 1, 'y'] += treatment_effect
    return df   

def variance_weighted_meandiff(df):
    weighted_effect_sum = 0
    weights_sum = 0
    for i in df.strata.unique():
        #For each strata, we then calculate its average treatment effect
        treatment_effect_strata = meandiff(df[df.strata==i])
        # estimate its weight based on the inverse within-group estimated variance (such as mean)
        weights_strata = 1/df[df.strata==i]['pre_experient_variance'].mean()
        # calculate the sum of weighted treatment effect
        weighted_effect_sum +=  treatment_effect_strata *  weights_strata
        # calculate the sum of weights
        weights_sum += weights_strata    
    return weighted_effect_sum/weights_sum

def strata_meandiff(df):
    get_sum = 0
    for i in df.strata.unique():
        get_sum += meandiff(df[df.strata==i])
    return get_sum/len(df.strata.unique())


meandiff_lst = []
variance_weighted_meandiff_lst = []
strata_meandiff_lst = []
for i in range(200):
    df = generate_strata_data(treatment_effect=1, size=100)
    meandiff_lst.append(meandiff(df))
    variance_weighted_meandiff_lst.append(variance_weighted_meandiff(df))
    strata_meandiff_lst.append(strata_meandiff(df))
   
(   pd.DataFrame(variance_weighted_meandiff_lst).hvplot.kde(label='Variance Weighted Estimator')
    * pd.DataFrame(meandiff_lst).hvplot.kde(label='Original')
    * pd.DataFrame(strata_meandiff_lst).hvplot.kde(label='Statification')
)
```

![jpg](/assets/images/Stat/158_9.jpg){: .align-center}

- 위를 보면 분산별로 Stratification 을 한 Estimator (노란색) 과, variance Weighted Estimator 을 이용한것 (파란색) 을 볼 수 있습니다.

> 장단점 

- variance-weighted estimator는 개별 실험 전 분산을 가중치로 사용합니다. 
- 이를 기반으로 Treatment effect 모델링하며 CUPED와 같은 다른 방법에 대한 대안으로 사용할 수 있습니다. 
- 이 방법론은 사용자 간에 편차가 매우 클떄 / pre-treatment variance 가 post-treatment variance. 에 대한 좋은 indicator 일때 효과적입니다.
- 그러나 pre-treatment 분산이 낮거나 실험 전후에 대한 분산이 일치하지 않는 경우 variance-weighted estimator가 작동하지 않을 수 있습니다. 
- 또한 분산 가중 추정기는 unbiased 가 아닙니다. biased 를 조절하는것은 매우 중요합니다! 

> ## ML-Based : Cupac

- [CUPAC](https://doordash.engineering/2020/06/08/improving-experimental-power-through-control-using-predictions-as-covariate-cupac/) (Control Using Predictions As Covariates) 은  2020년 Doordash의 Jeff Li, Yixin Tang 및 Jared Bauman에 의해 소개되었습니다.
- 이 방법은 한마디로 하면 CUPED의 확장입니다. 
- CUPED 는 어떤 Treatment 을 사용하던지, 공변량으로 Pre-experiment Data 를 사용했습니다. 
- 그에 반해서 CUPAC은 기계 학습 모델의 결과를 Covariate 변수로 사용합니다. 
- 기계 학습 모델의 목표는 "예측 공변량(prediction covariate = CUPAC)과 대상 메트릭 간의 부분 상관 관계를 최대화"하는 것입니다.

![jpg](/assets/images/Stat/158_10.jpg){: .align-center}

- 위 그림처럼 pre-experiment metric  X1, X2, X3 및 X4가 있다고 가정합니다. 
- 본질적으로 이 방법이 하는 일은 일부 기계 학습 모델을 사용하여 X1, X2, X3 및 X4를 사용하여 Y를 예측하는 것입니다. 
- 그런 다음 예측된 값을 CUPED의 공변량으로 사용할 수 있습니다.

> ## ML-Based : MLRATE 

- [MLRATE](https://arxiv.org/pdf/2106.07263.pdf) (기계 학습 회귀 조정 치료 효과 추정기)는 2021년 Princeton 및 Facebook의 Guo 등이 제안했습니다.
- CUPAC과 마찬가지로 MLRATE도 ML 모델을 사용하여 X에서 Y를 예측합니다. 
- 이떄 예측 값을 g(X)라고 합시다.
-  Y에서 g(X)를 빼는 대신 MLRATE는 회귀 모델에서 치료 지표와 함께 g(X)를 포함하고 회귀 조정된 치료 효과를 계산합니다.
-  아래 그림은 이 회귀 모델을 보여줍니다.

![jpg](/assets/images/Stat/158_11.jpg){: .align-center}

- First, we start with a vector of the covariate or a matrix of covariates X. We then learn and apply a cross-fitting supervised learning algorithm. Cross-fitting is used to avoid over-fitting bias. The cross-fitting procedure is as follows: We split our data into k splits. For each split, we train our data on the sample that’s not in the current split and get a function g. Then we use the X in the current split and get the predicted value of g(X) for the current split.
- Next, we conduct a regression model where we predict experiment metric Y with the regressors: T — treatment indicator, g(X) — predicted value from the cross-fitting ML, and T(g(x)-g).
- The OLS estimator for α1 is the treatment effect we are interested in.
- (나중에 공부...)

> ## Other ML 

- **Other ML-based methods**
- There are other ML-based methods used in the industry. For example, Poyarkov and others from Yandex developed the [Boosted decision tree regression adjustment](https://www.kdd.org/kdd2016/papers/files/adf0653-poyarkovA.pdf) in 2016.
- Overall, this article summarizes some of the popular variance reduction methods in the industry — post-stratification, CUPED, Variance-Weighted Estimators, and ML-based methods CUPAC and MLRATE. In practice, CUPED is widely used and productionalized in tech companies and ML-based methods are often used to incorporate multiple covariates. It is also common to combine multiple methods to achieve optimal variance reduction. Hope you find this article helpful. Thanks!
- **Acknowledgment**: Thank you so much Anthony Fu and Jim Bednar for providing guidance and feedback to this article. Thank you Kevin Liou and Sean Taylor for clarifying my questions around the Variance-Weighted Estimators.

---

**Reference**

- https://towardsdatascience.com/online-experiments-tricks-variance-reduction-291b6032dcd7
