---
title:  "Example &#58; SMS Counting"
excerpt: "pymc 를 이용한 모델링 Examples"
categories:
  - Py_Pymc
last_modified_at: 2021-10-24
toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 매우 간단한 모델링의 예시를 알아봅시다. 이 예시에서는 그냥 이런게 가능하다! 정도만 알아두는게 좋을것 같습니다. 이 이후에 어떠한 모델링이 가능한지에 대해서는 차근차근 알아보도록 하겠습니다.
{: .notice--warning}

# [Example 1 : 문자 메세지 Count](#link){: .btn .btn--primary}{: .align-center}

> ## Data

- 우리는 어떠한 사용자가 매일 주고받은 문자 데이터를 가지고 있다고 합시다. 
  - 데이터의 이름은 count_data 로서, 아래와 같습니다. 
- 우리는 사용자의 메시지 습관이 시간별로 어떻게 변하는지에 대해서 알고싶다고 합시다. 어떻게 이를 모델링 할 수 있을까요? 

array([13., 24.,  8., 24.,  7., 35., 14., 11., 15., 11., 22., 22., 11., 57., 11., 19., 29.,  6., 19., 12., 22., 12., 18., 72., 32.,  9., 7., 13., 19., 23., 27., 20.,  6., 17., 13., 10., 14.,  6., 16., 15.,  7.,  2., 15., 15., 19., 70., 49.,  7., 53., 22., 21., 31., 19., 11., 18., 20., 12., 35., 17., 23., 17.,  4.,  2., 31., 30., 13., 27.,  0., 39., 37.,  5., 14., 13., 22.])
{: .notice}

> ## Modeling

- 어떻게 모델링을 할 수 있을까요? 
- 먼저 Poisson Distribution 은 이러한 Count data 에 잘 맞으므로 특정일자 i 의 메시지 갯수 $C_i$ 는 다음과 같이 표시할 수 있을것입니다. 

$$C_i \sim Poi(\lambda)$$

![png](/assets/images/Python/38_1.png)

- 이때에 위 그림을 보면 마지막 부그의 데이터는 대체로 높아보입니다.
  - 즉 관측기간중 어느날 ($\tau$) 후에 갑자기 확 뛰어오른다고 생각할 수 있습니다. 
  - 즉 우리는 $\tau$ 이전과 이후에 대해서 모수를 2개 가진다고 생각할 수 있습니다. 

$$\lambda = \lambda_1 \ if \ t < \tau \\ \lambda = \lambda_2 \ if \ t \ge \tau $$ 

- 우리는 이러한 $\lambda$ 를 모델링 하려고 합니다.  
  - $\lambda$ 는 양수여야 하므로 다음과 같이 exp 분포를 이용하여 모델링 하겠습니다.

$$\lambda_1 \sim Exp(\alpha)\\ \lambda_2 \sim Exp(\alpha)$$

- 위와 같은 모수 $\alpha$ 는 모수에 영향을 주는 모수로서 초모수(hyperparameter) 또는 부모변수 (parent variable) 이라고 합니다. 
- 이때에 $\alpha$ 는 어떻게 정해야할까요? 

$$\frac{1}{N} \sum C_i \approx E[\lambda \mid \alpha] = 1/\alpha$$

- 위와 같이, 데이터 평균의 역수를 이용해 $\alpha$ 를 결정합니다. 
  - 이때에 각 $\lambda_i$ 에 대해서 사전확률을 2개씩 가지는것을 추천합니다.
- $\tau$ 의 경우는 어떻게 할까요? 아직 알고있는 정보가 하나도 없으므로 Uniform Prior 를 이용하도록 하겠습니다.

$$\tau \approx DiscreteUniform(1,70)$$

- 위와 같이 모델링을 마칠 수 있었습니다. 이를 이제 어떻게 하면 Pymc 를 이용해서 분석할 수 있을까요? 

> ## Pymc

```python
import pymc3 as pm

with pm.Model() as model:
    alpha = 1.0/count_data.mean()  
    lambda_1 = pm.Exponential("lambda_1", alpha)
    lambda_2 = pm.Exponential("lambda_2", alpha)
    tau = pm.DiscreteUniform("tau", lower=0, upper=n_count_data)
```

- $\lambda_1 , \lambda_2$ 에 해당하는 pymc 변수를 만듭니다. 
- 그리고 pymc 의 확률론적변수 (stochastic varibles) 에 변수를 할당합니다. 
  - 이떄에 확률론적 변수라고 부른 이유는 뒤쪽에서 난수 발생기에 의하여 처리되기 떄문입니다. 

```python
print('Random output:', tau.random(), tau.random(), tau.random())
```

```
62 57 66
```

- 위와 같이 tau 객체에 대해서, random 을 이용하여 확률론적으로 변수들을 계속 호출하게 됩니다.

```python
with model:
    idx = np.arange(n_count_data) # Index
    lambda_ = pm.math.switch(tau > idx, lambda_1, lambda_2)
```

- 위 코드는 새로운 함수 lambda_ 를 만들어냅니다. 
  - 하지만 이를 우리는 R.V 로 생각하게 됩니다. 
- switch 함수는  `tau` 값에 따라서 `lambda` 에게 `lambda_1`또는 `lambda_2` 의 값을 부여하게 됩니다.

```python
with model:
    observation = pm.Poisson("obs", lambda_, observed=count_data)
```

- 위처럼 observation 에 대해서 poisson 분포를 가정합니다.

```python
with model:
    step = pm.Metropolis()
    trace = pm.sample(10000, tune=5000, step=step, return_inferencedata=False)
```

- 위와 같이 Metripolis 모듈을 통하여 MCMC 를 진행합니다.

```python
lambda_1_samples = trace['lambda_1']
lambda_2_samples = trace['lambda_2']
tau_samples = trace['tau']
```

- 그 이후 3만개의 Sample (40000 - 10000) 에 대하여 아래와 같이 분포를 얻을 수 있습니다.

```python
figsize(12.5, 10)
#histogram of the samples:

ax = plt.subplot(311)
ax.set_autoscaley_on(False)

plt.hist(lambda_1_samples, histtype='stepfilled', bins=30, alpha=0.85,
         label="posterior of $\lambda_1$", color="#A60628", density=True)
plt.legend(loc="upper left")
plt.title(r"""Posterior distributions of the variables
    $\lambda_1,\;\lambda_2,\;\tau$""")
plt.xlim([15, 30])
plt.xlabel("$\lambda_1$ value")

ax = plt.subplot(312)
ax.set_autoscaley_on(False)
plt.hist(lambda_2_samples, histtype='stepfilled', bins=30, alpha=0.85,
         label="posterior of $\lambda_2$", color="#7A68A6", density=True)
plt.legend(loc="upper left")
plt.xlim([15, 30])
plt.xlabel("$\lambda_2$ value")

plt.subplot(313)
w = 1.0 / tau_samples.shape[0] * np.ones_like(tau_samples)
plt.hist(tau_samples, bins=n_count_data, alpha=1,
         label=r"posterior of $\tau$",
         color="#467821", weights=w, rwidth=2.)
plt.xticks(np.arange(n_count_data))

plt.legend(loc="upper left")
plt.ylim([0, .75])
plt.xlim([35, len(count_data)-20])
plt.xlabel(r"$\tau$ (in days)")
plt.ylabel("probability")
```

![png](/assets/images/Python/38_2.png)

> ## interpret

- Bayes statistics 는 분포를 반환합니다. 
  - 즉 우리는 미지의 $\lambda$ 와 $\tau$ 를 표현하는 분포를 가지게 되었습니다.
- 현재 우리가 얻은것은 우리의 추정에서의 불확실성을 볼 수 있게 되었습니다. 
  - 분포가 넓다는것은 우리의 사후 믿음이 확실하지 않다는 것입니다. 

![png](/assets/images/Python/38_2.png)

- 위에서의 그림을 보면, $\lambda_1$ 은 대략 20 , $\lambda_2$ 는 대략 15 입니다. 
  - 즉 두개의 $\lambda$ 값이 명확하게 구분되며 이는 사용자의 문자 습관에 정말 변화가 있었다고 생각할 수 있습니다. 
- 또한 우리는 $\tau$ 의 분포를 반환했다는것에 주목합시다. 
  - 이 경우에 45일 부근에서 사용자의 행동이 바뀔 확률이 50% 임을 의미합니다.
  - 만일, 아무 변화가 없거나 점진적으로 변하는 경우였다면 $\tau$ 의 사후확률은 prior 를 uniform 으로 잡았었으므로, posterior 또한 넓게 펴져있었을 것입니다.

> ## 사후분포는 어떤 좋은점?

- 사후분포를 가지고 다음과 같은 질문에 답할 수 있습니다. 

날짜 $t (0\le t \le 70)$ 에서 문자 메시지 갯수의 기댓값은 얼마일까? 
{: .notice}

- 이떄 포아송 변수의 기댓값은 그 분포의 모수 $\lambda$ 와 같다는 것을 기억해봅시다. 그렇다면 위의 질문은 사실 아래와 같이 변환될 수 있습니다. 

날짜 $t$ 에서 $\lambda$ 의 기댓값은 얼마일까? 
{: .notice}

- 주어진 일자 $t$ 에서 만일 $t<\tau_i$ (즉 아직 변화가 일어나지 않음) 이라면 $\lambda_i = \lambda_{1,i}$ 을 이용하여 모든 가능한 $\lambda_i$ 의 평균을 계산합니다. 
- 그렇지 않다면 $\lambda_i = \lambda_{2,i}$ 를 이용합니다.

```python
figsize(12.5, 5)

# tau_samples, lambda_1_samples, lambda_2_samples은
# 해당 사후확률분포에서 얻은 표본 N개가 포함된다.
N = tau_samples.shape[0]
expected_texts_per_day = np.zeros(n_count_data)  # 데이터 포인트 수

for day in range(0, n_count_data):
    # ix는 'day' 값 이전에 발생한 변환점에 해당하는
    # 모든 tau 표본의 불(boolean) 인덱스다.
    ix = day < tau_samples
    
    # 각 사후확률분포의 표본은 tau 값에 해당한다. tau값은 변환점 이전인지 (lambda_1)
    # 이후인지(lambda_2)를 가리킨다.
    # lambda_1/2의 사후확률분포 표본을 취함으로써 모든 표본을 평균하여 그날의
    # lambda 기대값을 얻을 수 있다.
    # 문자 메시지 개수 확률변수는 푸아송분포를 따르므로
    # lambda(푸아송 모수)는 메시지 개수의 기대값이다.
    expected_texts_per_day[day] = (lambda_1_samples[ix].sum() + lambda_2_samples[~ix].sum()) / N
    
plt.plot(range(n_count_data), expected_texts_per_day, lw=4, 
         color='#E24A33', label='수신한 문자 메시지의 기대값')
plt.xlim(0, n_count_data)
plt.xlabel('일', fontsize=13)
plt.ylabel('문자 메시지의 개수', fontsize=13)
plt.title('수신산 문자 메시지의 기대값')
plt.ylim(0, 60)부
plt.bar(np.arange(len(count_data)), count_data, color='#348ABD',
        alpha=0.65, label='관측된 문자 메시지의 개수(하루당)')
plt.legend(loc='upper left')
print(expected_texts_per_day)
```

![png](/assets/images/Python/40_1.png)

- 위의 데이터 분포를 보게되면, 우리가 수신한 문자 메시지와 수신한 메시지의 분포를 볼 수 있습니다. 
  - 이 결과는 변환점에서의 영향력을 강하게 나타냅니다. 
- 이 결과를 볼때에, 문자 메시지의 기댓값에는 불확실성이 존재하지 않는다는것을 기억하세요 (우리가 기댓값을 형성하려고 평균을 떄려박아서 그렇습니다.)
- 이러한 분석 결과는 사용자의 행동이 변했다는 믿음을 지지합니다. (그렇지 않으면 $\tau, \lambda_1 , \lambda_2$ 모두 비슷한 값을 가질것입니다.) 
  - 어떤것이 이러한 변화를 일으키는지 (최근의 업데이트 등) 를 살펴봐야 할 것입니다.

> ## 두 $\lambda$ 가 얼마나 다른지 알 수 있을까? 

- 우리는 $\lambda_1, \lambda_2$ 의 사후분포를 시각적으로 조사해, 두 분포가 다르다는것을 알 수 있었습니다.
  - 하지만 위처럼 Clear 한 경우가 아니라 만일 분포가 일부 겹치는 경우라면 어떻게 해야할까요? 
- 한가지 방법은 바로 $P(\lambda_1 < \lambda_2 \mid Data)$ 를 계산하는 것입니다. 
  - 이러한 값이 50% 에 가깝다면 우리는 $\lambda_1 , \lambda_2$ 가 다르다고 결론내리기는 힘들것입니다. 
- 이러한 계산은 아래와 같이 수행하면 간단합니다. 

```python
print(lambda_1_samples < lambda_2_samples)
```

```
[ True  True  True ...  True  True  True]
```

- 위의 계산을 이용하여 비율(비율은 확률이다!) 을 계산할 수 있습니다. 

```
print((lambda_1_samples < lambda_2_samples).mean())
```

```
0.998
```

- 또한 위처럼 단순히 다른것이 아니라, '그 값이 최소한 1 차이가 날 확률은 얼마일까?' 와 같은 더 복잡한 문제도 계산할 수 있습니다. 

```python
for d in [1, 2, 5, 10]:
    v = (abs(lambda_1_samples - lambda_2_samples)>=d).mean()
    print("What is the probability the difference is larger than {}? {:.2f}".format(d, v))
```

```
What is the probability the difference is larger than 1? 1.00
What is the probability the difference is larger than 2? 0.99
What is the probability the difference is larger than 5? 0.49
What is the probability the difference is larger than 10? 0.00
```

**Reference**

- 프로그래머를 위한 Bayesian with python

