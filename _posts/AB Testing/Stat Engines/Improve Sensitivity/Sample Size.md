https://bytepawn.com/five-ways-to-reduce-variance-in-ab-testing.html#five-ways-to-reduce-variance-in-ab-testing

> ## Intuition

- 일반적으로, 샘플의 수가 많아질수록 그 추정량이 정확해집니다.

![jpg](/assets/images/Stat/148_2.jpg)

- 그 이유는 위를 보다시피, 추정량이 정확해지기 때문에 같은 alpha 하에서 Testing 의 파워가 더 커지기 떄문입니다.

> ## Test 

- Two sample T test 를 사용한다고 합시다.

$$T=\frac{(\bar{X}-\bar{Y})-\left(\mu_{X}-\mu_{Y}\right)}{\sqrt{\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}}}$$

- 위처럼 통계량의 분산이 작아지기 때문에, 테스트의 Power 가 상승하게 되고, 좀 더 정확한 테스트를 할 수 있습니다.

> ## Example 

```python
import scipy
import numpy as np
from math import sqrt
from scipy import stats
from numpy import cov, linspace
from statistics import mean
from numpy.random import normal, exponential
import matplotlib.pyplot as plt
from random import random
%matplotlib inline

def lift(A, B):
    return mean(B) - mean(A)
def p_value(A, B):
    return stats.ttest_ind(A, B)[1]
def get_AB_samples(mu, sigma, treatment_lift, N):
    A = list(normal(loc=mu                 , scale=sigma, size=N))
    B = list(normal(loc=mu + treatment_lift, scale=sigma, size=N))
    return A, B

N = 1000
N_multiplier = 4
mu = 100
sigma = 10
treatment_lift = 2
num_simulations = 1000

print('Simulating %s A/B tests, true treatment lift is %d...' % (num_simulations, treatment_lift))

n1_lifts, n4_lifts = [], []
for i in range(num_simulations):
    print('%d/%d' % (i, num_simulations), end='\r')
    A, B = get_AB_samples(mu, sigma, treatment_lift, N)
    n1_lifts.append(lift(A, B))
    A, B = get_AB_samples(mu, sigma, treatment_lift, N_multiplier*N)
    n4_lifts.append(lift(A, B))

print('N samples  A/B testing, mean lift = %.2f, variance of lift = %.2f' % (mean(n1_lifts), cov(n1_lifts)))
print('4N samples A/B testing, mean lift = %.2f, variance of lift = %.2f' % (mean(n4_lifts), cov(n4_lifts)))
print('Raio of lift variance = %.2f (expected = %.2f)' % (cov(n4_lifts)/cov(n1_lifts), 1/N_multiplier))

bins = linspace(-2, 6, 100)
plt.figure(figsize=(14, 7))
plt.hist(n1_lifts, bins, alpha=0.5, label='N samples')
plt.hist(n4_lifts, bins, alpha=0.5, label=f'{N_multiplier}N samples')
plt.xlabel('lift')
plt.ylabel('count')
plt.legend(loc='upper right')
plt.title('lift histogram')
plt.show()
```

- 위와 같이 차이가 나는 데이터를 Simulation 합니다.
- 그 이후에 각각의 평균 데이터를 Histogram 으로 그려보겠습니다.

![jpg](/assets/images/Stat/148_1.jpg)

- 위 그림처럼 데이터의 수가 많을수록, 추정값이 좀 더 정확해집니다.
