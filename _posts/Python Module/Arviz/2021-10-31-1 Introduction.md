---
title:  "Introduction"
excerpt: "확률적 모델을 만들때 시각화를 담당하는 모듈"
categories:
  - Py_Arviz
last_modified_at: 2021-10-31
date : 2021-10-31 07:00:00 +0900

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Matplotlib 을 다루기 위한 마이크로 팁에 대해 알아보자!
{: .notice--warning}

# [Install](#link){: .btn .btn--primary}{: .align-center}

- Arvizs 는 [PyStan](https://pystan.readthedocs.io/) and [PyMC3](https://docs.pymc.io/) 과 같이 사용되게 but works fine with raw NumPy arrays.

> ## Installation

- Arviz 는 다음과 같이 설치할 수 있습니다.

```python
pip install arviz
```

> ## Dependencies

- Arviz 는 다음과 같은 Dependencies 를 가지고 있습니다. 

```
setuptools>=38.4
matplotlib>=3.0
numpy>=1.12
scipy>=0.19
packaging
pandas>=0.23
xarray>=0.16.1
netcdf4
typing_extensions>=3.7.4.3,<4
```

and

```
python>=3.6
```

> ## Optional Dependencies

- 이 dependencies 는 Ariz 의 사용성을 높혀주는 Dependency 입니다. 

```python
numba
bokeh>=1.4.0
ujson
dask
zarr>=2.5.0
```

- Numba
  - Necessary to speed up the code computation. The installation details can be found [here](https://numba.pydata.org/numba-doc/latest/user/installing.html). Further details on enhanced functionality provided in ArviZ by Numba can be [found here](https://arviz-devs.github.io/arviz/user_guide/Numba.html).
- Bokeh
  - Necessary for creating advanced interactive visualisations. The Bokeh installation guide can be found [over here](http://docs.bokeh.org/en/dev/docs/first_steps/installation.html).
- UltraJSON
  - If available, ArviZ makes use of faster ujson when [`arviz.from_json()`](https://arviz-devs.github.io/arviz/api/generated/arviz.from_json.html#arviz.from_json) is invoked. UltraJSON can be either installed via [pip](https://pypi.org/project/ujson/) or [conda](https://anaconda.org/anaconda/ujson)

- Dask
  - Necessary to scale the packages and the surrounding ecosystem. The installation details can be found [at this link](https://docs.dask.org/en/latest/install.html).

# [Arviz Quick Start](#link){: .btn .btn--primary}{: .align-center}

> ## Start

- 먼저 Arviz 를 어떻게 사용해야 하는지에 대해서 빠르게 알아봅시다.

```python
import arviz as az
import numpy as np
```

- 이제 Style Sheet 를 다르게 적용할 수 있습니다.

```python
# ArviZ ships with style sheets!
az.style.use("arviz-darkgrid")
```

- Feel free to check the examples of style sheets [here](https://arviz-devs.github.io/arviz/examples/styles.html#example-styles).

> ##Plotting

> Plot array

- Arviz 는 Pystan , Pymc 와 작동되도록 설계되었지만, Raw 한 Numpy array 에서도 작동이 잘 됩니다.

```python
az.plot_posterior(np.random.randn(1000));
```

![png](/assets/images/Python/46_1.png)

> Plot Dictionary

- array 로 이루어진 Dictionary 를 해석할떄에 Arviiz 는 다음과 같이 해석합니다.
  - 각각의 key 를 random variable 의 이름이라고 생각함.
  - key 안의 array 를 variables 의 sample 이라고 생각합니다. 

```python
size = (10, 50)
az.plot_forest(
    {
        "normal": np.random.randn(*size),
        "gumbel": np.random.gumbel(size=size),
        "student t": np.random.standard_t(df=6, size=size),
        "exponential": np.random.exponential(size=size),
    }
)
```

- 즉 위와 같이 size(10,50) 으로 이루어진 array 를 dict 의 key 에 매핑시킨다고 합시다.
  - 다시말하면 아래와 같이 'normal' 의 키에 다음과  같은 array 를 매핑합니다.

```python
np.random.randn(size = (10,50))
>>
array([[......], # chain 1
       [......], # chain 2
       [......], # chain 3
       ...    
       [......]]) # chain 10
```

- 위처럼 각각의 array 는 chain 이고, 각 chain 은 50개의 draws 로 이루어져 있습니다. 
- 다시 돌아와, 위에서 az.plot_forest 를 실행한다면 다음과 같이 여러 dict 로 이루어진 plot 이 나오게 됩니다.

![png](/assets/images/Python/46_2.png)

> ## Pymc3

- 앞에서 Pymc3 과 같이 작동된다고 하였죠? pymc3 에서 대부분의 diagnotic 및 plotting 기능이 Arviz 로 넘어가고 있는 중이기 떄문에 , Probability progamming 을 하시게 된다면, Arviz 를 잘 알아두셔야 할 것입니다. 

```python
import pymc3 as pm
J = 8
y = np.array([28.0, 8.0, -3.0, 7.0, -1.0, 1.0, 18.0, 12.0])
sigma = np.array([15.0, 10.0, 16.0, 11.0, 9.0, 11.0, 10.0, 18.0])
schools = np.array(
    [
        "Choate",
        "Deerfield",
        "Phillips Andover",
        "Phillips Exeter",
        "Hotchkiss",
        "Lawrenceville",
        "St. Paul's",
        "Mt. Hermon",
    ]
)
```

- 먼저 위와 같이 데이터를 형성하도록 하겠습니다. 

```python
with pm.Model() as centered_eight:
    mu = pm.Normal("mu", mu=0, sd=5)
    tau = pm.HalfCauchy("tau", beta=5)
    theta = pm.Normal("theta", mu=mu, sd=tau, shape=J)
    obs = pm.Normal("obs", mu=theta, sd=sigma, observed=y)

    # This pattern is useful in PyMC3
    prior = pm.sample_prior_predictive()
    centered_eight_trace = pm.sample()
    posterior_predictive = pm.sample_posterior_predictive(centered_eight_trace)
```

- 그 이후에는 위처럼 pymc 에서 Sampling 을 수행할 수 있습니다. 
- 그 이후에 az 에서 위에서 생성된 샘플링 Chain 을 그려낼 수 있습니다.

```python
az.plot_autocorr(centered_eight_trace, var_names=["mu", "tau"]);
```

![png](/assets/images/Python/46_3.png)

> ## Convert to Inference Data 

- Arviz 에서는 기본적으로 분석시에 이용하는 데이터는 IInference Data 타입을 이용합니다. 

```python
data = az.from_pymc3(
    trace=centered_eight_trace,
    prior=prior,
    posterior_predictive=posterior_predictive,
    model=centered_eight,
    coords={"school": schools},
    dims={"theta": ["school"], "obs": ["school"]},
)
data
```

-  위는 현재 'pymc3' 의 데이터 구조를 inferenceData 의 형태로 바꾸는 과정입니다.
- 위 데이터는 아래와 같은 구조를 띠게 됩니다.

```
arviz.InferenceData
>posterior
>posterior_predictive
>log_likelihood
>sample_stats
>prior
>prior_predictive
>observed_data
```

- 위처럼 posterior 를 그리기에 필요한것들을 모두 가지고 있으므로, Arviz 는 이러한 데이터만 인자로 받더라도 다양한것들을 그려낼 수 있습니다.

```python
az.plot_trace(data);
```

![png](/assets/images/Python/46_4.png)

---

**Reference**

- <https://arviz-devs.github.io/arviz/getting_started/Installation.html>
- <https://arviz-devs.github.io/arviz/getting_started/Introduction.html>

