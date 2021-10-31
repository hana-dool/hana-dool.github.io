---
title:  "Example &#58; A/B Testing"
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

# [AB Testing](#link){: .btn .btn--primary}{: .align-center}

> ## Intro

- A/B Testing 은 두가지 방법간의 효과 차이를 검정하기 위한 통계 디자인입니다.
- 예를 들어서 제약회사는 A,B 두가지 약에 대해서 효능차이가 얼마나 있는지에 대해서 궁금할 것입니다.
  - 또는 Website Optimizer 인 경우에는 전환율 / 구매율 등에 대해서 궁금할 것입니다. 
- 이러한 두 Variants 간의 차이는 Conrol / Treatment 를 50 : 50 으로 나누어서 테스트해볼 수 있을것입니다. 
- 이러한 사후실험 분석은 대게 비율검정 / 평균차이 검정과 같은 가설검정 (Hypothesis Testing) 을 통해서 진행됩니다. 
  - 하지만 혼동스러운 p-value 값에 대한 정의 등과 같은 문제때문에 베이지안으로 AB Testing 을 해결하는게 더 자연스럽다는 논의가 있습니다. 

> ## Problem

- 웹 개발 예제로 진행해 보겠습니다. 
- A 사이트는 N 명에게 노출되었고, n 명이 전환했다고 합시다. 이러한 경우 어떤 사람은 성급하게 $p_A = \frac{n}{N}$ 과 같은 결론을 애릴지도 모릅니다. 
  - 하지만 이는 '불확실성' 을 계량하지 못하는, 매우 안좋은 Point estimation 입니다. 
- 그러므로 우리는 이러한 전환율 ($p$) 을 분포를 사용하여 모델링하고자 합니다. 
- 우선 베이즈 모델을 설정하기 위해서는 미지의 값에 대해서 Prior 를 설정해야 됩니다.
  -  이떄에 prior 에 대한 확신이 거의 없으므로 $P_A$ 를 Uniform prior 로 가정하겠습니다.

```python
import pymc3 as pm
# The parameters are the bounds of the Uniform.
with pm.Model() as model:
    p = pm.Uniform('p', lower=0, upper=1)
```

- 이 예제에서 우리는 $p_A = 0.05$ , 사이트에 노출된 사용자 수 $N = 1500$ 이라고 가정하겠습니다.
  - 우리는 사용자가 구매를 했는지 / 안했는지에 대해서 Simulation 을 진행할 것입니다. 
  - N 번 시행하여 SImulation 하기 위하며 Bernoulli 를 사용하였습니다. 

```python
#set constants
p_true = 0.05  # remember, this is unknown.
N = 1500
# sample N Bernoulli random variables from Ber(0.05).
# each random variable has a 0.05 chance of being a 1.
# this is the data-generation step
occurrences = stats.bernoulli.rvs(p_true, size=N)

print(occurrences) # Remember: Python treats True == 1, and False == 0
print(np.sum(occurrences))
```

```
[0 1 0 ... 0 0 0]
92
```

- 위와 같이 Simulation 이 됩니다. 여기에서 관측된 빈도를 계산해 봅시다. 

```python
# Occurrences.mean is equal to n/N.
print("What is the observed frequency in Group A? %.4f" % np.mean(occurrences))
print("Does this equal the true frequency? %s" % (np.mean(occurrences) == p_true))
```

```
What is the observed frequency in Group A? 0.0613
Does this equal the true frequency? False
```

> ## Inference On A

- 관측된 데이터를 이용하여 추론 알고리즘을 실행해 보겠습니다. (자세한 내용은 나중에 MCMC 에서 보도록 합시다.)

```python
with model:
    obs = pm.Bernoulli("obs", p, observed=occurrences)
    step = pm.Metropolis()
    trace = pm.sample(18000, step=step)
    burned_trace = trace[1000:]
```

- 위에서 생성된 sample 에 대해서 distribution 을 그려보면 아래와 같습니다.

```python
figsize(12.5, 4)
plt.title("Posterior distribution of $p_A$, the true effectiveness of site A")
plt.vlines(p_true, 0, 90, linestyle="--", label="true $p_A$ (unknown)")
plt.hist(burned_trace["p"], bins=25, histtype="stepfilled", density=True)
plt.legend();
```

![png](/assets/images/Python/41_1.png)

- 위의 사후분포를 보면 $P_A$ 의 값은, 우리의 관측 p 값인 0.0613에서 큰 값을 가지고 있음을 알 수 있습니다.

> ## Inference On A/B

- B 사이트의 데이터에 대해서도, 위와 같은 로직을 적용하여 $P_B$ 의 사후(Posterior) 확률을 적용하여 , 분포를 알 수 있을것입니다. 
  - 그리고 $delta = p_A - p_B$ 를 이용하여 이 둘의 차이를 추론해보겠습니다.
- 우선 이러한 세팅을 위해 다음과 같이 정의할 것입니다. 
  - $p_B = 0.04 , delta = 0.01 , N_B = 750$
- 그리고 A 에서 했던것처럼 B 도 똑같이 SImulation 합니다.

```python
import pymc3 as pm
figsize(12, 4)

#these two quantities are unknown to us.
true_p_A = 0.05
true_p_B = 0.04

#notice the unequal sample sizes -- no problem in Bayesian analysis.
N_A = 1500
N_B = 750

#generate some observations
observations_A = stats.bernoulli.rvs(true_p_A, size=N_A)
observations_B = stats.bernoulli.rvs(true_p_B, size=N_B)
print("Obs from Site A: ", observations_A[:30], "...")
print("Obs from Site B: ", observations_B[:30], "...")
```

```
Obs from Site A:  [0 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 0 1 0 0 0 0 1 0] ...
Obs from Site B:  [0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0] ...
```

- 위 값에 대해서 평균(즉 전환 확률) 을 추정해 보겠습니다.

```python
print(np.mean(observations_A))
print(np.mean(observations_B))
```

```
0.058
0.04
```

- 이제 이러한 데이터에 대해서 Inference 를 진행해 보겠습니다.

```python
# Set up the pymc3 model. Again assume Uniform priors for p_A and p_B.
with pm.Model() as model:
    p_A = pm.Uniform("p_A", 0, 1)
    p_B = pm.Uniform("p_B", 0, 1)
    
    # Define the deterministic delta function. This is our unknown of interest.
    delta = pm.Deterministic("delta", p_A - p_B)

    # Set of observations, in this case we have two observation datasets.
    obs_A = pm.Bernoulli("obs_A", p_A, observed=observations_A)
    obs_B = pm.Bernoulli("obs_B", p_B, observed=observations_B)

    # To be explained in chapter 3.
    step = pm.Metropolis()
    trace = pm.sample(20000, step=step)
    burned_trace=trace[1000:]
```

- deterministic 변수는 우리가 보고자 하는 관심사항입니다.
- 이러한 세개의 미지수에 대한 분포 (p_A , p_B , delta) 를 그래프를 통하여 그리면 아래와 같습니다.

![png](/assets/images/Python/41_2.png)

- 이떄에 $p_B$ 의 사후분포가 더 평평한데, 이는 데이거가 좀 더 부족하여 확신이 부족했음을 나타냅니다. 

![png](/assets/images/Python/41_3.png)

- 위처럼 두 분포에 대해서 겹쳐 그릴 수 있고, 이를 통하여 분포를 형성할 수 있을것입니다.

```python
print("Probability site A is WORSE than site B: %.3f" % \
    np.mean(delta_samples < 0))
print("Probability site A is BETTER than site B: %.3f" % \
    np.mean(delta_samples > 0))
```

```
Probability site A is WORSE than site B: 0.032
Probability site A is BETTER than site B: 0.968
```

- 이를 delta sample 을 이용하여 A 사이트가 B 보다 나을 확률 등을 위처럼 계산할 수 있습니다.

{: .notice--success}

