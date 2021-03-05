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

**Assumption?**
population 이 Normal 

**Test statistics**
$t = \frac{\bar{X_1} - \bar{X_2}}{\sqrt{\frac{s_1^2}{N_1}}+\sqrt{\frac{s_2^2}{N_2^2}}}$ $\sim$ $t(v)$  # v 는 approximation 해서 구한다. 자세한건 아래의 증명참조

**Proof**
https://digitalcommons.usu.edu/cgi/viewcontent.cgi?article=1014&context=gradreports

위의 46 Page 부터 그 증명방법이 소개되고 있다. 시간이 나게되면 나중에 증명해봐야겠다. 
student - T test 는 두 분포의 분산이 같음을 가정한다. (이는 매우 인위적인 가정) 
하지만 welch's Test 는 그러한 가정이 없이 진행된다.



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

크게 특별한건 없다. 다만 그룹끼리 independent 와, 각 sample 이 같은 선택 확률을 가진다라는 가정이 현실세계에서는 약간 안맞을 수 있겠다. 왜냐하면 각 사람의 재력이 다를텐데, 구매와 비구매를 저렇게 할 수 있을까? 그리고 그룹끼리 independent 하게 나눠질 수 있을까..? 

**proof**
https://arxiv.org/pdf/1808.09171.pdf
시간있을때 증명 보는것으로... 