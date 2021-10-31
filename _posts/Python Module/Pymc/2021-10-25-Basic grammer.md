---
title:  "pymc grammer"
excerpt: "베이지안 통계를 다루는 프레임워크"
categories:
  - Py_Pymc
last_modified_at: 2021-10-24
toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 여기에서는 pymc 의 기초적인 디자인 패턴을 알아보고 베이지안 관점에서 어떻게 하면 모델링할 수 있는지에 대해서 알아보려고 합니다.
{: .notice--warning}

# [Modeling Structures](#link){: .btn .btn--primary}{: .align-center}

> ## 부모와 자식관계

- 베이지안 Structure 설명의 용이성을 위하여, 부모변수와 자식변수에 대해서 알아보도록 하겠습니다.
  - 부모변수 : 다른 자식변수에 영향을 줌 
  - 자식변수 : 다른 변수의 영향을 받는 변수 ( 부모변수에 종속 )

> 모델객체 형성하기

```python
import pymc3 as pm

with pm.Model() as model:
    parameter = pm.Exponential("poisson_param", 1.0)
    data_generator = pm.Poisson("data_generator", parameter)
```

- with 구문과 함꼐 model 이 쓰인다면, 이 구문 안에서 생성된 변수들은 모두 자동적으로 model 안의 변수로 들어가게 됩니다.
  - with 구문을 사용하여, 모델을 열고 / 자동으로 닫는것을 구현한 것입니다.

```python
with model:
    data_plus_one = data_generator + 1
```

- 위처럼 with 이 이미 생성한 모델 객체의 이름을 사용하여, 동일한 변수에 대해 수정을 할 수 있습니다.
  - 하지만 모델이 더 많은 변수를 인식하려면 모델을 정의할떄의 Context 내부에 있어야 합니다.

```python
parameter.tag.test_value
```

```
array(0.693147177890573)
```

> 변수 재지정하기

- 각각의 변수는 자기만의 이름을 가지고 정의가 됩니다.
- 이전에 사용한 변수와 같은 이름으로 다른 모델객체를 만드려면 첫번쨰 코드블록을 다시 시랭하면 됩니다.

```python
with pm.Model() as model:
    theta = pm.Exponential("theta", 2.0)
    data_generator = pm.Poisson("data_generator", theta)
```

```
Applied log-transform to theta and added transformed theta_log_ to model.
```

- 위처럼 우리는 변수에 대래 새로 재지정해 보았습니다. 

> 완전히 분리된 모델 정의하기

```python
with pm.Model() as ab_testing:
    p_A = pm.Uniform("P(A)", 0, 1)
    p_B = pm.Uniform("P(B)", 0, 1)
```

```
Applied interval-transform to P(A) and added transformed P(A)_interval_ to model.
Applied interval-transform to P(B) and added transformed P(B)_interval_ to model.
```

- 우리는 위처럼 완전히 별도의 모델을  정의할수도 있습니다. 
  - 모델 이름은 원하는대로 자유롭게 (여기에서는 ab_testing) 지정해주면 됩니다. 
- 다른 이름을 쓴다면 이전 모델을 덮어쓰지 않고 다른 모델이 적용되게 됩니다.

> ## PyMC Variables

- 모든 PyMC3 변수는 initial value 를 가집니다. 

```python
print("parameter.tag.test_value =", parameter.tag.test_value)
print("data_generator.tag.test_value =", data_generator.tag.test_value)
print("data_plus_one.tag.test_value =", data_plus_one.tag.test_value) 
```

```
parameter.tag.test_value = 0.693147177890573
data_generator.tag.test_value = 0
data_plus_one.tag.test_value = 1
```

- 위와 같이 값을 print 한다면, 아래와 같이 그 값이 나오게 됩니다.
- test_value 는 오로지 sampling 의 시작점 기능만 하게 됩니다.

```python
with pm.Model() as model:
    parameter = pm.Exponential("poisson_param", 1.0, testval=0.5)

print("\nparameter.tag.test_value =", parameter.tag.test_value)
```

- 이러한 test_value 는 아무런 조작을 가하지 않으면 같은 값만 가지게 됩니다. 
  - 이떄에, testval 의 값을 조작하게 된다면 이러한 initial 값은 변하게 됩니다.
- pymc 변수는 두가지 유형의 프로그래밍 변수가 존재합니다.

> Stochastic variables

- 확률적 변수는 결정되어있지 않은 변수입니다.
- 즉 변수의 매개변수 , 구성 요소를 알고 있더라도 Random 성을 가지고 있는 변수입니다.
- 이러한 변수는 Poisson, DiscreteUniform, Exponential 등이 있습니다.

> Deterministic Variables

- deterministic variables 는 구성요소를 알고있다면 고정되는 변수입니다.

> ## Initializing Stochastic Variables

> 확률적 변수 만들기

- 확률적 변수를 만들어내기 위해서는 name argument 와 추가적인 매개 변수가 필요합니다. 

```python
some_variable = pm.DiscreteUniform("discrete_uni_var", 0, 4)
```

- 위의 경우, 0,4 는 DiscreteUniform 에 대한 하한 / 상한선 값입니다. 
- name 변수는 이러한 분포에 붙은 라벨으로, 이 분포를 잘 설명하는 값으로 설정하는게 좋습니다.
  - 나중에 이 이름을 가지고 분포를 찾게 됩니다.

> 여러 변수 (array) 만들기

- beta(0,1) 의 분포를 가지는 하나의 Variables 를 만들기 위해서는 아래와 같이 실행해야 합니다.

```python
beta_1 = pm.Uniform("beta_1", 0, 1)
beta_2 = pm.Uniform("beta_2", 0, 1)
```

- 하지만 언제 N 개의 array 를 만들겠어요! 그니까 N 개 사이즈를 가지는 array 를 다음과 같이 만들 수 있습니다. 

```python
betas = pm.Uniform('betas',0,1,shape = N)
```

> ## Deterministic Variables

- 이제 위에서 했던것과 비슷하게 Deterministic variables 를 만들어낼 수 있습니다.
  - 우리는 단순히 아래와 같이 deterministic class 를 이용하여 호출하면 됩니다.

```
deterministic_variable = pm.Deterministic("deterministic variable", some_function_of_variables)
```

- 위와 같이 pm.deterministic 을 이용해 계산되고, 각 값은 모델에 저장됩니다.
- 아래와 같은 연산은 Deterministic variables 를 반환하게 됩니다.

```python
with pm.Model() as model:
    mu = pm.Normal('mu', mu=0., sd=1.)
    mu_d= mu+5 #this just adds 5 to all samples of mu, but samples are not stored
    Y_obs = pm.Normal('Y_obs', mu=mu_d, sd=1,observed=data)
```

- 위와 같이 mu_d 는 mu+5 의 샘플인것은 맞지만, 이러한 샘플은 저장되지 않습니다.
- 즉 우리는 pm.Deterministic('mu_d',',mu+5') 을 이용한다면 이러한 deterministic variables 는 저장될 수 있으며 나중에 trace object 로부터 계산이 가능해집니다.

```python
with pm.Model() as model:
    lambda_1 = pm.Exponential("lambda_1", 1.0)
    lambda_2 = pm.Exponential("lambda_2", 1.0)
    tau = pm.DiscreteUniform("tau", lower=0, upper=10)
new_deterministic_variable = lambda_1 + lambda_2
```

- sampling 에 의거하여 deterministic variable 을 뽑아낵기 위해서는 constructor 에 의하여 아래와 같이 성립될 수 있습니다.

$$\lambda =  \begin{cases}\lambda_1  & \text{if } t \lt \tau \cr \lambda_2 & \text{if } t \ge \tau \end{cases}$$

- 이는 pymc 로 다음과 같이 정의됩니다.

```python
import numpy as np
n_data_points = 5  # in CH1 we had ~70 data points
idx = np.arange(n_data_points)
with model:
    lambda_ = pm.math.switch(tau >= idx, lambda_1, lambda_2)
```

- 당연하게도, $\tau, \lambda_1 , \lambda_2 $ 를 안다면 $\lambda$ 는 Completely 알게 됩니다. 
  - 그러므로 이 변수는 deterministic variables 입니다.
- Deterministic variable 내에서는 확률적 변수도 numpy 또는 scalar 처럼 작동하게 됩니다.

```python
def subtract(x, y):
    return x - y
stochastic_1 = pm.Uniform("U_1", 0, 1)
stochastic_2 = pm.Uniform("U_2", 0, 1)

det_1 = pm.Deterministic("Delta", subtract(stochastic_1, stochastic_2))
```

- 위처럼 deterministic 내부에 들어가는 확률적 변수는 numpy 배열과 같이 작동됩니다.

> ## Theano

- Pymc3 이 수행하는 대부분의 무거운 작업은 theano 패키지에서 처기됩니다. 
  - 이 표기는 Numpy 와 매우 유사합니다. 
  - 자세한것은 문서 참조... 

# [Modeling process](#link){: .btn .btn--primary}{: .align-center}

> ## Including obsrvation in Model

- 우리는 다음과 같은 질문을 할 수 있습니다.
  - 과연 우리의 $\lambda_1$ prior 는 어떻게 생겼을까? 

```python
%matplotlib inline
from IPython.core.pylabtools import figsize
import matplotlib.pyplot as plt
import scipy.stats as stats
figsize(12.5, 4)
samples = lambda_1.random(size=20000)
plt.hist(samples, bins=70, density=True, histtype="stepfilled")
plt.title("Prior distribution for $\lambda_1$")
plt.xlim(0, 8);
```

![png](/assets/images/Python/40_2.png)

- 위와 같이 $P(A)$ 를 구체적인 Distribution 모양으로 정의할 수 있습니다.
- 위를 어떻게 하면 업데이트 할 수 있을까요? 
  - keyword argument 인 `observed` 를 이용할 수 있습니다.
- observed 변수의 역활은 매우 간단합니다. 변수의 현재 값을 고정하는 역할을 합니다.
  - 즉 값을 변경 불가능하게 합니다. 

```python
import numpy as np
data = np.array([10, 5])
with model:
    fixed_variable = pm.Poisson("fxd", 1, observed=data)
print("value: ", fixed_variable.tag.test_value)
```

```
value:  [10  5]
```

- 위 처럼 초깃값을 명시하면 됩니다. 
  - 위와 같이 정의한다면, observed data 를 포함한 fixed data 가 됩니다.

```python
# We're using some fake data here
data = np.array([10, 25, 15, 20, 35])
with model:
    obs = pm.Poisson("obs", lambda_, observed=data)
print(obs.tag.test_value)
```

- 위는 이렇게 , Pymc3 variables 를 observations 에 통합하는 과정입니다.

> ## Modeling Approches

- 베이즈 모델링에서 가장 좋은 출발점은 데이터가 어떻게 생성되었는지에 대ㅐ서 생각하는 것입니다.
  - 전지전능한 위치에서 데이터가 어떻게 생성되었는지를 살펴보아야 합니다.
- 이전의 SMS 문자 데이터 모델링을 예시로 들겠습니다.

1. 처음에는 Count data 를 가장 잘 설명하는 랜덤 변수는 어떤것일까? 라고 생각하면서 시작하였습니다. Poisson Random Variables 로 정하였습니다.
2. 그 이후로 SMS 가 Poisson 분포라고 가정할떄에 어떤것이 필요할까요? 바로 매개변수 $\lambda$ 에 대한 모델링이 필요합니다. 
3. $\lambda$ 에 대해서 우리는 늘 같은값을 가진다고 생각하지 않습니다. 즉 우리는 $\lambda$ 가 특정한 시점을 전후로 행동이 바뀐다고 생각합니다! 그러므로 이러한 전환에 대한 Switch point 인 $\tau$ 를 정의합니다. 
4. 이떄 두 $\lambda$ 에게 좋은 distribution 은 어떤것이 있을까요? 우리는 양수의 Support 를 가지는 Exponential 을 생각할 수 있습니다. 하지만 이떄에 이러한 Exponential 분포는 또한 parameter $\alpha$ 를 가집니다. 
5. 이떄에 $\alpha$ 에 대한 적절한 값은 얼마일까요? $\lambda$ 들의 값은 10~30 사이라고 생각할 수 있습니다. 즉 이에 맞게 작은 $\alpha$ 값이 (작은 alpha 는, exponential 의 평균이 크다는것(역수) 을 의미합니다.) 를 정할 수 있습니다. 좋은 지침은 $\lambda$ 의 mean 을 $\alpha$ 로 삼는것입니다. 
6. $\tau$ 에 대해서는 어떠한 정보도 없는 상태이므로 여기에서는 Uniform distirubtion 을 따른다고 가정하겠습니다. 

![png](/assets/images/Python/40_3.png)

- 우리는 위처럼 이러한 관계를 Visualization 할 수 있습니다.
- Pymc 및 다른 확률적 프로그래밍 언어는 이러한 스토리를 잘 나타내도록 설계되었습니다.

> ## Same Story , Different results

- 재미있게도, 우리는 위와 같은 strory  재해석해서 새로운 데이터셋을 만들어낼 수 있습니다.
- 위의 6가지 단계를 반대로 뒤집어서 데이터셋의 실현 가능성을 Simulation 할 수있습니다.

```python
tau = np.random.randint(0, 80)
print(tau)
```

```
59
```

- 위처럼 사용자 행둉을 $DiscreteUnif(0,80)$ 에서 추출합니다.

```python
alpha = 1./20. # alpha 를 1/20 으로 준다는것은, 평균을 20으로 본다는 의미
lambda_1, lambda_2 = np.random.exponential(scale=1/alpha, size=2)
print(lambda_1, lambda_2)
```



```
49.7521280843 10.1226712418
```

- 그 이후에는 위처럼 $Exp(\alpha)$ 분포에서 $\lambda_1, \lambda_2$ 의 값을 뽑아냅니다. 

```python
data = np.r_[stats.poisson.rvs(mu=lambda_1, size=tau), stats.poisson.rvs(mu=lambda_2, size = 80 - tau)]
```

- 위에서 추출된 $\tau$ 와 $\lambda_1 ,\lambda_2$ 값을 바탕으로, SMS sampling 을 실시합니다.
  - 즉 $\tau$ 전의 SMS 데이터는 $Poi(\lambda_1)$ , $\tau$ 이후의 데이터는 $Poi(\lambda_2)$ 에서 샘플링하는 것입니다. 

```python
plt.bar(np.arange(80), data, color="#348ABD")
plt.bar(tau-1, data[tau - 1], color="r", label="user behaviour changed")
plt.xlabel("Time (days)")
plt.ylabel("count of text-msgs received")
plt.title("Artificial dataset")
plt.xlim(0, 80)
plt.legend();
```

![png](/assets/images/Python/40_4.png)

- 위와 같은 데이터가 우리가 관측한 데이터셋과 약간 달라보여도 괜찮습니다. 
  - 처음 Sampling 을 하자마자 좋은 표현 (우리가 가지는 데이터) 을 가지는 parameter 를 찾는것은 매우 어렵습니다.
  - Pymc 는 이러한 좋은 parameter ($\tau, \lambda_i$) 을 잘 찾도록 설계되었습니다. 

```python
def plot_artificial_sms_dataset():
    tau = stats.randint.rvs(0, 80)
    alpha = 1./20.
    lambda_1, lambda_2 = stats.expon.rvs(scale=1/alpha, size=2)
    data = np.r_[stats.poisson.rvs(mu=lambda_1, size=tau), stats.poisson.rvs(mu=lambda_2, size=80 - tau)]
    plt.bar(np.arange(80), data, color="#348ABD")
    plt.bar(tau - 1, data[tau-1], color="r", label="user behaviour changed")
    plt.xlim(0, 80);

figsize(12.5, 5)
plt.title("More example of artificial datasets")
for i in range(4):
    plt.subplot(4, 1, i+1)
    plot_artificial_sms_dataset()
```

![png](/assets/images/Python/40_5.png)

- 위와 같이 여러 분포를 Generating 해볼 수 있습니다. 
  - 어떤 분포가 우리 Dataset 에 제일 잘 맞는지는 이후에 조금 더 해보겠습니다.

**Reference**



- 프로그래머를 위한 Bayesian with python

{: .notice--success}

