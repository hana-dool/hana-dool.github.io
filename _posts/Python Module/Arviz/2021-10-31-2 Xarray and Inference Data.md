---
title:  "Xarray and Inference Data"
excerpt: "Arviz 가 Plot 을 그리기 위한 데이터 모양"
categories:
  - Py_Arviz
last_modified_at: 2021-10-31
date : 2021-10-31 08:00:00 +0900

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Arviz 는 아무 데이터나 받는게 아닙니다. Inference data type 을 대표적으로 받는데요, 이러한 데이터 타입은 대체 어떤 꼴인지에 대해서 알아봅시다! 
{: .notice--warning}

# [Data Structure](#link){: .btn .btn--primary}{: .align-center}

- 물론 이전에 보듯이 Numpy array 를 쓰더라도 plotting 할 수 있었습니다.
- 하지만 대표적으로 쓰이는 Data Structure 는 따로 있습니다. 다음과 같은 Data Structure 를 이용합니다.
  - [`xarray.Dataset`](http://xarray.pydata.org/en/stable/generated/xarray.Dataset.html#xarray.Dataset)
  - [`arviz.InferenceData`](https://arviz-devs.github.io/arviz/api/generated/arviz.InferenceData.html#arviz.InferenceData)
  - [netCDF](https://arviz-devs.github.io/arviz/getting_started/XarrayforArviZ.html#netcdf)

> ## Why more than one data structure? 

- 왜 간단하게 하나의 데이터 (trace data) 만 있으면 될텐데 , 왜 귀찮게 특별히 data structure 를 이용할까요? 
- Bayesian Inference 를 수행할떄에는 다양한 데이터들을 만들어내기 떄문입니다.
  - N 개의 Variable 에 대한 Prior distribution 
  - N 개의 Variable 에 대한 Posterior Distribution 
  - Prior Predictive Distribution 
  - Posterior Predictive Distriburion 
  - 각 Chain 에 대한 Trace ..... 
- 그러므로 이러한 데이터를 모두 담을 Structure 가 필요했고, 이를 이용하게 된 것입니다.

> ## Why not pd.Dataframe or Numpy array? 

- Probabilistic Programing 의 데이터는 기본적으로 고차원입니다. 
  - 이러한 고차원 데이터를 잘 다룰만한 Data Structure 가 필요했습니다.
- 그래서 pd.Dataframe 또는 Np.array 를 사용하지 않고 xarray 패키지를 이용하여 Data strucutre 를 구현하기로 하였습니다.

![png](/assets/images/Python/46_5.png)

- data stucture 는 위와 같습니다. 
  - 이러한 구조를 이용하면 Bayesian inference 의 과정을 모두 담을 수 있고, 또한 시가과 하는데에 필요한 정보도 모두 담을 수 있습니다.

> ## az.InferenceData 

- InferenceData 의 객체가 어떤 구조로 되어있는지 알아보기 위하여 아래처럼 library 에서 data sample 을 load 하였습니다.

```python
# Load the centered eight schools model
import arviz as az

data = az.load_arviz_data("centered_eight")
data
```

```
arviz.InferenceData
>posterior
>posterior_predictive
>sample_stats
>prior
>observed_data
```

- 위와 같이 data  를 load 하면 다양한것들을 살펴볼 수 있습니다. 

> ## get attribute

```python
# Get the posterior dataset
posterior = data.posterior
posterior
```

- 위와 같이 data(Inference Data 객체) 에 대해서 posterior Attribute 를 호출하면 다음과 같이 나오게 됩니다.

![png](/assets/images/Python/46_7.png)

- 위처럼 posterior 의 경우 어떤식으로 MCMC 가 이루어졌는지를 알 수 있습니다.
  - chain 은 4개를 사용했고, draw 는 500개씩 뽑았으며 어떤 모수를 사용하였는지 (mu,theta,tau) 도 알 수 있습니다. 

```python
# Get the observed xarray
observed_data = data.observed_data
observed_data
```

- 또한 위처럼 observed data 를 얻을 수있습니다. 
  - 이 경우 observed data 는 겨우 8개의 길이입니다.
  - 즉 '각각의 key' 마다 크기도 다르고, chain 이 없는 경우도 있는 등 일반적인 pd.Dataframe 또는 np.array 를 사용하면 꽃필 에로사항이 많습니다.
- 이러한 이유로 새로운 데이터 형태(Inference Data) 를 쓰게 됩니다.

# [Creating Inference Date](#link){: .btn .btn--primary}{: .align-center}

- 그러므로 우리는 Pymc3 을 쓰던 numpy 를 쓰던 pystan 을 쓰던지간에 , arviz 에서 잘 이용하려면 , 여기에서 사용하는 형태로 바꿀 필요가 있게 됩니다. 
- 그러므로 여기에서는 어떻게 Inference Data 를 생성하는지에 대해서 알아봅시다.

```python
import arviz as az
import numpy as np
```

> ## 1D numpy array 

- 1D numpy array -> Inference Data 

```python
size = 100
dataset = az.convert_to_inference_data(np.random.randn(size))
dataset
```

```
arviz.InferenceData
>posterior
```

> ##nD numpy array 

- n차원 넘파이 -> Inference Data

```python
shape = (1, 2, 3, 4, 5)
dataset = az.convert_to_inference_data(np.random.randn(*shape))
dataset
```

```
arviz.InferenceData
>posterior
```

> ## Dictionary

- DIctionary 에서 Inference Data

```python
datadict = {
    "a": np.random.randn(100),
    "b": np.random.randn(1, 100, 10),
    "c": np.random.randn(1, 100, 3, 4),
}
dataset = az.convert_to_inference_data(datadict)
dataset
```

```
arviz.InferenceData
>posterior
```

> ## Dataframe

- Pymc3 데이터로부터 Inference Data 만들기

```python
import pandas as pd
import xarray as xr

data = np.random.rand(100,2)
df = pd.DataFrame({'a':data[:,0], 'b':data[:,1]})
df["chain"] = 0
df["draw"] = np.arange(len(df), dtype=int)
df = df.set_index(["chain", "draw"])
xdata = xr.Dataset.from_dataframe(df)

dataset = az.InferenceData(posterior=xdata)
dataset
```

```
arviz.InferenceData
>posterior
```

> ## Pymc3

- pymc3 데이터로부터 Inference data 만들기

```python
import pymc3 as pm

draws = 500
chains = 2

eight_school_data = {
    "J": 8,
    "y": np.array([28.0, 8.0, -3.0, 7.0, -1.0, 1.0, 18.0, 12.0]),
    "sigma": np.array([15.0, 10.0, 16.0, 11.0, 9.0, 11.0, 10.0, 18.0]),
}

```

```python
with pm.Model() as model:
    mu = pm.Normal("mu", mu=0, sd=5)
    tau = pm.HalfCauchy("tau", beta=5)
    theta_tilde = pm.Normal("theta_tilde", mu=0, sd=1, shape=eight_school_data["J"])
    theta = pm.Deterministic("theta", mu + tau * theta_tilde)
    pm.Normal(
        "obs", mu=theta, sd=eight_school_data["sigma"], observed=eight_school_data["y"]
    )

    trace = pm.sample(draws, chains=chains)
    prior = pm.sample_prior_predictive()
    posterior_predictive = pm.sample_posterior_predictive(trace)

    pm_data = az.from_pymc3(
        trace=trace,
        prior=prior,
        posterior_predictive=posterior_predictive,
        coords={"school": np.arange(eight_school_data["J"])},
        dims={"theta": ["school"], "theta_tilde": ["school"]},
    )
pm_data

```

```python
arviz.InferenceData
>posterior
>posterior_predictive
>log_likelihood
>sample_stats
>prior
>prior_predictive
>observed_data
```

# [Working with Inference Date](#link){: .btn .btn--primary}{: .align-center}

> ## Combine Chains and Draws

- MCMC 의 결과로 만들어진 Chain , Draws 들을 모두 합칩니다.

```python
idata = az.load_arviz_data("centered_eight")
idata
idata.posterior
```

```
xarray.Dataset
Dimensions: (chain: 4 draw: 500 school: 8)
```

- 위의 MCMC Results 는 위의 결과를 보다시피 4개의 chain 와 각 500개의 draws 로 이루어져 있습니다. 

```python
stacked = idata.posterior.stack(draws=("chain", "draw"))
stacked
```

```
xarray.Dataset
Dimensions: (draws: 2000 school: 8)
```

- 위처럼 stack 의 method 를 이용하면 여러 chain 에서의 sample 을 모두 합치게 됩니다.

> ## Obtain a NumPy array for a given parameter

- parameter 에 대해서 MCMC 로 형성된 Posterior 분포들을 얻을 수 있습니다.

```python
stacked.mu.values
```



```
array([-3.47698606, -2.45587061, -2.82625433, ...,  4.59705819,
        5.89850592,  0.16138927])
```

> ## Get the number of variables

- 우리 계층모델에 대해서 얼마나 많은 Grouop 이 있는지에 대해서 살펴봅니다.

```python
len(idata.observed_data.school)
```

```
8
```

> ## Get the variable's names

- 계층 모델에 대해서 groups 의 이름은 어떨까? 

```python
idata.observed_data.school.values
```

```
array(['Choate', 'Deerfield', 'Phillips Andover', 'Phillips Exeter',
       'Hotchkiss', 'Lawrenceville', "St. Paul's", 'Mt. Hermon'],
      dtype=object)
```

> ## Get a subset of chains

- Chain 의 일부만 보고 싶을떄

```python
idata.sel(chain=[0, 2]).posterior
```

> ## Remove the first n draws (burn-in)

- 첫 100개의 Samples 를 삭제하고 싶다고 합시다. 
  - 이떄에 모든 chain 에 대해서 삭제하고 싶습니다.

```python
burnin = idata.sel(draw=slice(100, None))
```

- 위와 같은 경우, 우리는 burnin 객체를 통하여 posterior ,posterior_predictive , prior , sample_states 가 이전의 500개의 데이터에서 400개의 데이터가 된 것을 볼 수 있을것입니다. 
- 이떄에 observe_data 그룹은 영향을 지 않습니다. (당연히 그냥 데이터이므로 burn in 에 속할 이유가 없음)

---

---

**Reference**

- <https://arviz-devs.github.io/arviz/getting_started/Installation.html>
- <https://arviz-devs.github.io/arviz/getting_started/Introduction.html>

