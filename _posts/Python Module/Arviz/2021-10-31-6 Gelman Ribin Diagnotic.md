---
title:  "Gelman Rubin Statistics"
excerpt: "얼마나 MCMC chain 이 잘 수렴되고 있는지 체크"
categories:
  - Py_Arviz
last_modified_at: 2021-10-31
date : 2021-10-31 12:00:00 +0900

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 MCMC 가 잘 수렴되었는지를 알려주는 통계량...
{: .notice--warning}

# [Gelman Rubin Diagnotics](#link){: .btn .btn--primary}{: .align-center}

> ## Brooks Gelman-Rubin Statistics (BGR)

- 이 값은MCMC 가 얼마나 잘 수렴했는지를 나타내는 지표입니다.
- 여러 체인이 있을텐데, 체인간의 분산과 체인 내의 분산을 비교하는 값입니다. idea 는 다음과 같습니다. 
- '모든 MC chain 이 어느정도 수렴하여 대표성을 지닌다면 
  - 모든 체인은 비슷한 샘플(모분포) 를 나타내게 되므로 체인간의 분산 (즉 체인 평균의 분산) 은 감소합니다.'

> Calculation

1.먼저 M 개의 chain 을 생성하고, 각각의 Chain 은 2*N 개의 iteration 을 형성합니다. 

2.처음 N 개의 draws(Sample) 을 버립니다. 

3.체인 내의 Variation 과 체인간의 Variation 을 계산합니다 .

$$W = \frac{1}{M} \sum_{j=1}^Ms_j ^ 2 \text{ ($s_j$ 는 Step 2 에서 각 체인의 분산)}) $$

$$B = \frac{N}{M-1}\sum_{j=1}^M({\bar{\theta_j} - \bar{\theta}}) \text{  ($\bar{\theta}$ 는 M개 체인 평균의 평균)}$$

 4.이제 각각을 이용하여 $\theta$ 에 대한 분산의 추정치를 구합니다.

$$\hat{Var(\theta)} = (1-\frac{1}{N})W + \frac{1}{N}B$$

- 이떄 위의 추정치는 Unbiased 입니다. 
  - $E(W) = E(B) = E(s^2_j) = \sigma^2$
  - $E(\hat{var(\theta)}) = E((1-\frac{1}{N})W + \frac{1}{N}B) = \sigma^2$
- 하지만 이 경우에 N 이 엄청 커지지 않는 이상... B 라는 녀석 떄문에 overestimate 된다.
  - Chain 들은 initial point 가 달라져서 다른 값을 가지는 경우까지 Variation 에 고려가 되므로 B 는 일반적인 공식보다 커지기 떄문입니다.
- W 라는 애들은 체인 안의 값들의 분산을 나타냅니다.
  - 이 값은 '같은' initial 에서 출발한 샘플들의 분산입니다. 즉 ! 전체의 분산보다 좀 더 작은 값을 나타낼 것입니다. 

5.Potential scale reduction factor ($\hat{R}$) 을 계산합니다.

$$\hat{R} = \sqrt{\hat{var(\theta)}/W}$$

> Usage

- N 이 작을떄에는, B 때문에 $\hat{R}$ 은 1보다 큰 값을 가지게 됩니다. 
  - 왜냐하면 체인들끼리 다른 형태를 가지고, (아직 수렴이 덜되서) 이러한 노이즈 떄문에 $B$ 값이 겁나 크기 떄문입니다.
- $W$ 는 일종의 scaling 역할을 하게됩니다. 각 체인의 분산이 이미 큰 상태라면, $B$ 또한 어느정도는 큰 값을 가지며 변동하기 떄문입니다.
  - $W$ 로 나누는것 없이 $B$ 만 쓰게 된다면, '데이터 자체에서 오는' 분산을 고려하지 않게 됩니다! 
- N 이 점점 커짐에 따라서 W 의 값만 남게 되고 , 이는 점점 1로 수렴하게 됩니다. 
  - 즉 1로 가까워지면 좋은것입니다. 
- 즉 $\hat{R}$ 이 크다면 (일반적으로 1.2) 우리는 convergence 를 좀 더 개선하기 위하여 많은 iteration 이 필요하다고 할 수 있습니다.

> ## Code

- 이 경우 plotting 은 없긴 하고, 계산하는 방식으로는 잘 구현되어 있습니다.

```python
import arviz as az
data = az.load_arviz_data("non_centered_eight")
az.rhat(data)
```

- 이때는 az.summary 에도 잘 들어있는 부분이긴 합니다.

```python
with basic_model:
    display(az.summary(trace, round_to=2))
```

![png](/assets/images/Python/44_2.png)

> ## dataframe 으로 바꾸어보기

- 사실 inference data 의 형태가 귀찮을떄가 있습니다. 
- 이떄에는 to_dataframe() 으로 바꿔서 볼 수 있습니다.

```python
import arviz as az
data = az.load_arviz_data("non_centered_eight")
az.rhat(data).to_dataframe()
```

---

**Reference**

- <https://arviz-devs.github.io/arviz/api/generated/arviz.rhat.html>



