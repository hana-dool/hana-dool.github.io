---
title:  "A/B Test Statistics"
excerpt: "A/B 테스트에서의 검정"
categories:
  - Others
tags:
  - 3
last_modified_at: 2021-03-05

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# Welch's T-test

이는 Unequal variance T-test 라고도 한다. 

**언제사용?** 
두 모집단의 평균 차이를 검정할 때에 사용한다. 즉 두 집단의 구매액수 차이, 머무른 시간 등에 대해서 궁금할 때에, 두 집단에 대해서 비교할때에 사용한다.

**Assumption?**<br>
population 이 Normal 

**Test statistics**
$t = \frac{\bar{X_1} - \bar{X_2}}{\sqrt{\frac{s_1^2}{N_1}+{\frac{s_2^2}{N_2^2}}}}$ $\sim$ $t(v)$  # v 는 approximation 해서 구한다. 자세한건 아래의 증명참조

**Proof**<br>
<https://digitalcommons.usu.edu/cgi/viewcontent.cgi?article=1014&context=gradreports>

위의 46 Page 부터 그 증명방법이 소개되고 있다. 시간이 나게되면 나중에 증명해봐야겠다. 
student - T test 는 두 분포의 분산이 같음을 가정한다. (이는 매우 인위적인 가정) 
하지만 welch's Test 는 그러한 가정이 없이 진행된다.

**note**<br>
사실 매우 큰 대표본의 경우는 자유도가 커질수록 Normal 과 같아지기 때문에, 그냥 Normal 을 쓸 수 있을것이다. 

<br>

# Chi-square Test

**언제 사용?**
구매한 각 제품의 갯수를 범주로 나누어서 두개의 이항분포의 확률들이 같은지 검정하게 된다. 

|       | 범주1(구매) | 범주2(안구매) | 비율                        |
| ----- | ----------- | ------------- | --------------------------- |
| A집단 | $X_a$       | $Y_a$         | $\frac{X_a}{X_a+Y_a} = p_a$ |
| B집단 | $X_b$       | $Y_b$         | $\frac{X_b}{X_b+Y_b}=p_b$   |

**Assumption**

1. The data in the cells should be **frequencies**, or counts of cases rather than percentages or some other transformation of the data.
2. The levels (or categories) of the variables are **mutually exclusive**. That is, a particular subject fits into one and only one level of each of the variables.
3. Each subject may contribute **data to one and only one cell** in the χ2. If, for example, the same subjects are tested over time such that the comparisons are of the same subjects at Time 1, Time 2, Time 3, etc., then χ2 may not be used.
4. The **study groups must be independent**. This means that a different test must be used if the two groups are related. For example, a different test must be used if the researcher’s data consists of paired samples, such as in studies in which a parent is paired with his or her child.
5. **There are 2 variables, and both are measured as categories**, usually at the nominal level. However, data may be ordinal data. Interval or ratio data that have been collapsed into ordinal categories may also be used. While Chi-square has no rule about limiting the number of cells (by limiting the number of categories for each variable), a very large number of cells (over 20) can make it difficult to meet assumption #6 below, and to interpret the meaning of the results.
6. The value of the **cell *expecteds* should be 5 or more** in at least 80% of the cells, and **no cell should have an expected of less than one** ([3](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3900058/#b3-biochem-med-23-2-143-3)). This assumption is most likely to be met if the sample size equals at least the number of cells multiplied by 5. Essentially, this assumption specifies the number of cases (sample size) needed to use the χ2 for any number of cells in that χ2. This requirement will be fully explained in the example of the calculation of the statistic in the case study example.
7. The sample data is a random sampling from a **fixed distribution or population** where every collection of members of the population of the given sample size **has an equal probability of selection**. 

크게 특별한건 없다. 다만 그룹끼리 independent 와, 각 sample 이 같은 선택 확률을 가진다라는 가정이 현실세계에서는 약간 안맞을 수 있겠다. 왜냐하면 각 사람의 재력이 다를텐데, 구매와 비구매를 저렇게 할 수 있을까? 

**proof**<br>
<https://arxiv.org/pdf/1808.09171.pdf><br>
시간있을때 증명 보는것으로... 



# Bayesian A/B

베이지안 방법론에서는 metric 에 대한 사전분포를 정의한 후에 업데이트 하는 방식으로 진행이 된다.

아래처럼 Rate 에 대해서 Prior 를 다음과 같이 설정하자. $P(\theta)$

![png](/assets/images/{Others}/8_1.png)	

그러면 $P(\theta\mid Data)$ 가 아래처럼 형성이 된다. 

![png](/assets/images/{Others}/8_2.png)

**note)** 아마도 Computational 적인 이슈때문에 그냥 prior 는 쓸 수 없을것이다. 일반적인 경우 결국 MCMC 를 적용해서 Posterior 를 normalizing 해야하는데, 각 과정에서 $\frac{P(\theta^*\mid D)}{P(\theta^t-1\mid D)}$ 를 계산해야되고, 이는 Data 가 크면 계산량이 너무 많다... 즉 아래처럼 conjugate model 을 써야할거 같다..  <https://en.wikipedia.org/wiki/Conjugate_prior>

형성된 Posterior 를 통해서 HDI 95% 에 속한다거나, 분포에서 0 이상의 누적확률은 얼마인지에 따라서 Test 를 진행할 수 있다.

**why Bayes?**

- prior 의 정보를 추가적으로 넣을 수 있다. 
- Frequentist 들의 이분법적 결정으로 인해 야기되는 문제($H_0$ 의 P-value 가 0.06이라면..?  그냥 기각하기에는 너무 아깝지 않나요?) 를 yes/no 대신 '분포' 로 해답을 제시함으로서 훨씬 많은 정보를 뽑아낸다.
- 극단적인 경우 좋은 안전장치가 된다. 예를들어서 각 마을의 후두암 사망자를 추정하고싶다고 하자. A 마을은 150명밖에 안되는데 운이 나쁘게 후두암 환자가 1명 있었다고 하자. 그럼 Freuntist 는 1/150으로 추정하게 된다.(데이터로부터 최고의 추정은 1/150임) 드러나 Baysian 은 이미 몇십만 인구수에서 얻은 Prior 을 통해서 0.0001 정도로 Prior 를 주었다고 하자. 이 데이터는 sample 수가 너무 작아 posterior 에게 영향을 주는 정도가 매우 작다. 그래서 0.00011 정도로 Posteior 가 나오게 된다.

**see also**

<https://databreak.netlify.app/2019-04-13-BayesianAB>

<https://assaeunji.github.io/bayesian/2020-03-02-abtest/>

