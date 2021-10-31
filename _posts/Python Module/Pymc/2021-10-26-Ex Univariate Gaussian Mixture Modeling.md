---
title:  "Example &#58; Univariate Gaussian Mixture Modeling"
excerpt: "베이지안 통계와 A/B Test"
categories:
  - Py_Pymc
last_modified_at: 2021-10-24
toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 여기에서는 베이즈 A/B Testing 을 모델링하는 방법에 대해서 알아봅시다.
{: .notice--warning}

# [Modeling](#link){: .btn .btn--primary}{: .align-center}

> ## Model

- 우선 다음과 같이 Mixture Model 을 정의합니다.

$$p\sim Dir(\alpha)$$

$$z_i  \mid p_k \sim Cat(p)$$

$$\mu_k \stackrel{iid}{\sim} N(0,10) $$

$$\sigma \stackrel{iid}{\sim} HalfCauchy(1)$$

$$y_i \mid z_i = k \sim N(\mu _k , \sigma_k)$$

> ## Sample

- 위의 모델은, Mixture gaussian 으로서, 이를 Generating 해 봅시다.

```python
import pymc3 as pm
import numpy as np 
import matplotlib.pyplot as plt
seed = 68492
np.random.seed(seed)

mus = [0,6,-5]
sigmas = [1,1.5,3]
ps = [.2, .5, .3]
N = 1000
y = np.hstack([np.random])
y = np.hstack([np.random.normal(mus[0], sigmas[0], int(ps[0]*N)),
np.random.normal(mus[1], sigmas[1], int(ps[1]*N)),
np.random.normal(mus[2], sigmas[2], int(ps[2]*N))])
plt.hist(y, bins=20, alpha=0.5) 
plt.xlabel('Simulated values')
plt.ylabel('Frequencies')
plt.show()
```

![png](/assets/images/Python/45_4.png)

- 우리는 위처럼 3개의 잠재변수에 의해 각각의 Gaussian 으로 
  - 이떄 3개의 변수는 (0.2 , 0.5,  0.3) 
- 3개의 인종 (백 황 흑) 에 대해서, 키의 분포를 모델링한것이라 생각하면 됩니다.
  - 각 인종은 비율이 다르고 (0.2, 0.5, 0.3)
  - 각 인종마다 키의 분포가 다를것입니다 (N(0,1) N(6,1.5) N(-5,3))

> ## Modeling

- 각각의 $y_k$ 변수는 평균이 $\mu_k$ 이고, 표준편차가 $\sigma_k$ 인 Normal 분포를 따릅니다.
- 그리고 또한 k 는 category 별로 비율이 정해져 있습니다.
  - 이러한 비율은 디레클레 분포로 모델링 됩니다.

```python
## Build model
gmm = pm.Model()
# Specify number of groups
K = 3

with gmm:
    # Prior over z
    p = pm.Dirichlet('p', a=np.array([1.]*K))
    # z is the component that the data point is being sampled from.
    # Since we have N data points, z should be a vector with N elements.
    z = pm.Categorical('z', p=p, shape=N)
    # Prior over the component means and standard deviations
    mu = pm.Normal('mu', mu=0., sd=10., shape=K)
    sigma = pm.HalfCauchy('sigma', beta=1., shape=K)
    # Specify the likelihood
    Y_obs = pm.Normal('Y_obs', mu=mu[z], sd=sigma[z], observed=y)
```

- 이떄에 우리의 모델은 K 개의 R.V. 을 가지므로 Shape 도 k 를 가지게 모델링 합니다.
  - 그리고 Likelihood 를 선언하는데, 이떄에 하나의 Y_obs 가 모델링될떄 어떻게 되는지 그 흐름을 써 넣습니다.
- 위의 모델을 시각화 하면 아래와 같습니다.

```python
pm.model_to_graphviz(gmm)
```

![png](/assets/images/Python/45_5.png)

> ## Sampling 

- 이제 샘플링을 해야합니다. 

```python
with gmm:
    # Specify the sampling algorithms to use
    step1 = pm.NUTS(vars=[p, mu, sigma])
    step2 = pm.ElemwiseCategorical(vars=[z])

    # Start the sampler!
    trace = pm.sample(draws=2000,
            nchains=4,
            step=[step1, step2],
            random_seed=seed)
```

- 표본추출을 하기 위해서 pm.sample() 을 선언합니다. 

```python
with gmm:
    # Specify the sampling algorithms to use
    step1 = pm.NUTS(vars=[p, mu, sigma])
    step2 = pm.ElemwiseCategorical(vars=[z])

    # Start the sampler!
    trace = pm.sample(draws=2000,
            chains = 4,
            step=[step1, step2],
            random_seed=seed)
```

```
 100.00% [12000/12000 01:27<00:00 Sampling 4 chains, 0 divergences]
Sampling 4 chains for 1_000 tune and 2_000 draw iterations (4_000 + 8_000 draws total) took 103 seconds.
```

- 위와 같은 샘플링 작업을 통하여 결과는 trace 에 저장되고, 이는 우리의 inference 에 쓰기에 됩니다.
- 만일 알고리즘을 지정하지 않으면, pymc 가 적절한 방법론을 이용하여 샘플링 하게 됩니다.
  - 연속 변수의 경우에는 NUTS
  - 이산 변수의 경우에는 Gibs Sampling 사용

> Note

- draws
  - 몇개의 Sample 을 posterior 의 inference 에 사용할지를 결정합니다. 
- nchains
  - 몇개의 Markov Chain 을 만들이제 대해서 결정합니다.
- random_seed
  - 랜덤을 결정합니다.
- tune (default = 1000)
  - Markov chain 의 수렴성을 위하여, 앞의 몇개의 sample 을 버릴지를 결정합니다.

> ## plot_trace

```python
pm.plot_trace(trace, 
             var_names=['mu','p','sigma'], # Specify which variables to plot
             lines=[('mu',{},mus),('p',{},ps),('sigma',{},sigmas)],  # Plots straight lines - useful for simulations
             compact=True #Don't split up variable plots by group
)
# suplot 을 통해서 높이 조절 (환경에 따라서 겹치기도 하더라...)
plt.subplots_adjust(hspace =0.5)
plt.show() ; 
```

![png](/assets/images/Python/45_6.png)

- 위처럼 trace 에 대해서 plot 을 할 수 있습니다.
  - 위를 참조한다면 우리는 사후분석을 시행할 수 있습니다.
- 왼쪽은 Posterior distribution 에 대한 marginal 분포를 보여줍니다.
- 오른쪽은 샘플링이 어떻게 수행되었는지를 보여주는 그래프가 나옵니다. (오른쪽과 같은 그래프를 trace plot 이라고 합니다.)
- Trace plot 이 어느정도 제대로 수행된듯 합니다. (chain 끼리도 비슷하고, sampling 되는 샘플도 전체 공간을 잘 움직이는듯)

{: .notice--success}

