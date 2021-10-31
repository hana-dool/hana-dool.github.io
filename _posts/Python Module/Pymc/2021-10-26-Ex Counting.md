---
title:  "Example &#58; Counting lies"
excerpt: "거짓말을 세는 가짓수"
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

- 사람은 항상 정직하게 답변하지 않습니다. 
  - 이러한 거짓말은 저희의 추론을 어렵게 만듭니다.
- 예시로 '당신은 시험에서 부정행위를 한 적이 있나요?' 라는 질문에 대해서 사람들은 실제로 부정행위를 한 사람이 거의 없을것이라는 이야기입니다. 
- 이렇게 솔직하지 않은 답변에 대해서 좀 더 정확한 추정을 가능하게 하는 방법을 알아봅시다. 

> ## Data 

- 우리는 이항분포를 사용하여 학생들이 시험중에 부정행위를 저지르는 빈도를 알아보려 합니다. 
- 시험을 치룬 총 학생 수를 N 으로 놓고, 시험 후 각 학생들을 인터뷰한다고 가정합시다. 
  - 각 학생은 부정행위를 했는지 / 안했는지에 대한 답변을 받게 됩니다. 
- 하지만 이러한 질문에 대해서 얼마나 많은 사람이 제대로 답할까요? 
  - 우리는 이러한 질문을 좀 더 세련되게 바꿔서 사용해 봅시다. 

학생들은 인터뷰할때 각각 숨겨둔 동전을 하나 던집니다. (인터뷰하는사람은 앞면인지 뒷면인지 모름) 동전이 앞면이 나온 학생은 정직하게 대답한다. 동전이 던져 뒷면이 나온다면 몰래 다시 한번 던져서 앞면이 나오면 '부정행위를 했습니다.' 라고 대답하고 뒷면이 나오면 '부정행위를 하지 않았습니다.' 라고 대답합니다. 이렇게 하면 프라이버시를 지키면서 정확한 답변을 얻을 수 있습니다. 
{: .notice}

- 이러한 알고리즘을 사용하여 우리는 Pymc 를 이용해 모델링할 수 있습니다. 
- 부정행위에 대하여 학생 100명을 조사한다고 합시다. 우리는 부정행위자의 비율인 p 를 구하려 합니다. 
  - 이제 아래에서 이를 모델링 해 봅시다. 

> ## Modeling

- 우리는 사전확률분포로부터, 부정행위자의 진짜 비율인 p 를 표본추출합니다. 
  - 우리는 p 에 대해서 전혀 모르므로 p 의 사전확률로 Uniform(0,1) 을 부여합니다.

```python
import pymc3 as pm
N = 100
with pm.Model() as model:
    p = pm.Uniform("freq_cheating", 0, 1)
```

- 위처럼 p 에 확률론적 변수를 부여합니다. 
- 이제 우리는 학생 100명에게 Bernouli 확률변수를 할당합니다. 
  - 1은 부정행위를 한 사람 / 0 은 하지 않은 사람을 나타냅니다. 

```python
with model:
    true_answers = pm.Bernoulli("truths", p, shape=N, testval=np.random.binomial(1, 0.5, N))
```

- 위처럼 우리는 100명의 srudent 에게 Bernouli random variables 를 할당합니다.
  - 1의 의미는 치팅을 했다는것을 의미합니다. 

```python
with model:
    true_answers = pm.Bernoulli("truths", p, shape=N, testval=np.random.binomial(1, 0.5, N))
```

- 다음 단계는 각 학생들이 시행하는 첫번쨰 동전던지기입니다.
  - 1/2 = p 를 이용하여 Bernouli 100개를 추출하여 다시 모델링합니다.

```python
with model:
    first_coin_flips = pm.Bernoulli("first_flips", 0.5, shape=N, testval=np.random.binomial(1, 0.5, N))
print(first_coin_flips.tag.test_value)
```

```
[0 0 1 0 1 1 0 1 0 1 1 1 0 0 0 1 1 1 0 0 0 0 0 1 0 1 0 1 1 1 0 0 0 1 0 1 1
 1 1 0 1 0 0 1 1 1 1 0 0 0 0 0 0 1 1 0 0 1 1 0 1 0 0 1 0 1 1 0 0 0 0 0 1 1
 1 0 1 0 1 1 1 0 1 0 0 0 1 0 0 0 0 1 0 1 0 1 0 0 1 0]

```

- 이제 두번째 flip 을 모델링 합니다.

```python
with model:
    second_coin_flips = pm.Bernoulli("second_flips", 0.5, shape=N, testval=np.random.binomial(1, 0.5, N))
```

- 우리는 두번쨰 동전 던지기에서 가능한 결과를 모델링 할 수 있습니다. 

```python
import theano.tensor as tt
with model:
    val = first_coin_flips*true_answers + (1 - first_coin_flips)*second_coin_flips
    observed_proportion = pm.Deterministic("observed_proportion", tt.sum(val)/float(N))
```

- `fc*t_a + (1-fc)*sc`는 프라이버시 알고리즘의 핵심이 포함되어 있습니다. 
  - i) 첫 번째 던지기가 앞면이고 학생이 부정행위를 하면 1 
  - i) 첫 번째 던지기가 뒷면이고 두 번째 던지기가 앞면인 경우도 1
- 마지막으로, 마지막 줄은 이 벡터를 합산하고 로 나누어 비율을 형성해 봅니다.

```python
observed_proportion.tag.test_value
```

```
array(0.5600000023841858)
```

- 다음으로 우리는 Dataset 이 필요합니다. 
  - 이러한 Coin fliped interview 를 통해서 연구자는 35개의 Yes 대답을 얻었습니다. 
- 모든사람이 결백하다면 이론적으로 1/4 가 '예' 일 것이라는거에 집중해주세요! 

```python
X = 35
with model:
    observations = pm.Binomial("obs", 
                               n = N, 
                               p = observed_proportion, 
                               observed=X)
```

- 위 모델에 대해서 pm.Binomial 을 적용합니다.
  - n 은 데이터의 수 
  - p 는 관측된 proportion 을 의미합니다. 

```python
with model:
    step = pm.Metropolis(vars=[p])
    trace = pm.sample(40000, step=step)
    burned_trace = trace[15000:]
```

```python
figsize(12.5, 3)
p_trace = burned_trace["freq_cheating"][15000:]
plt.hist(p_trace, histtype="stepfilled", density=True, alpha=0.85, bins=30, 
         label="posterior distribution", color="#348ABD")
plt.vlines([.05, .35], [0, 0], [5, 5], alpha=0.3)
plt.xlim(0, 1)
plt.legend();
```

![png](/assets/images/Python/41_4.png)

- 위와 같은 분포를 본다면, 우리는 부정행위자에 대한 비율을 0.05~0.35 사이로 좁힐 수 있었습니다. 
  - 사실 균등분포를 사전분포로 사용했기 떄문에, 약간 좁은 분포의 모양을 보이고 있음을 알 수 있습니다. 
- 이 사후분포를 볼떄에 우리는, p=0 근처에 있을 확률이 거의 0이므로 이는 부정행위자가 거의 없다고 생각할 수 있습니다. 

> ## Modeling 2 

$$\begin{align}
P(\text{"Yes"}) = & P( \text{Heads on first coin} )P( \text{cheater} ) + P( \text{Tails on first coin} )P( \text{Heads on second coin} ) \\\\
& = \frac{1}{2}p + \frac{1}{2}\frac{1}{2}\\\\
& = \frac{p}{2} + \frac{1}{4}
\end{align}$$

- 위 처럼 우리는 모델을 좀 더 다르게 할 수 있습니다.

```python
with pm.Model() as model:
    p = pm.Uniform("freq_cheating", 0, 1)
    p_skewed = pm.Deterministic("p_skewed", 0.5*p + 0.25)
```

```python
with model:
    yes_responses = pm.Binomial("number_cheaters", 100, p_skewed, observed=35)
```

```python
with model:
    # To Be Explained in Chapter 3!
    step = pm.Metropolis()
    trace = pm.sample(25000, step=step)
    burned_trace = trace[2500:]
```

```python
figsize(12.5, 3)
p_trace = burned_trace["freq_cheating"]
plt.hist(p_trace, histtype="stepfilled", density=True, alpha=0.85, bins=30, 
         label="posterior distribution", color="#348ABD")
plt.vlines([.05, .35], [0, 0], [5, 5], alpha=0.2)
plt.xlim(0, 1)
plt.legend();
```

![png](/assets/images/Python/41_5.png)

{: .notice--success}

