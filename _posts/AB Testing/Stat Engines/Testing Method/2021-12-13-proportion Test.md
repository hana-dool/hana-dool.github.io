---
title: "z-test t-test chi-square fisher-exact"
excerpt: "proportion 을 검정하기 위한 다양한 방법들"
tags:
  - AB_Stat

last_modified_at: 2021-12-13
toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

A/B Testing 에서 Proportion 검정하는방법
{: .notice--warning}

# [A/B Testing and Proportion](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

- A/B Testing 에 대해서 조사하다 보면, Proportion 을 검정하는데, 방법론이 여러가지가 쓰이는것을 알 수 있습니다. 

```
Version  Visits  Conversions
A        2069     188
B        1826     220
```

- 위와 같은 데이터를 검정한다고 할떄에 다음과 같은 방법을 쓸 수 있습니다.

> 1.For instance, this article uses [z-score](http://20bits.com/article/statistical-analysis-and-ab-testing): 

$$z=\frac{p-p_{c}}{\sqrt{\frac{p(1-p)}{N}+\frac{p c(1-p c)}{N_{c}}}}$$

> 2.[This article](http://conversionxl.com/pulling-back-curtain-p-values-learned-love-small-data/) uses the following formula 

$$\frac{\text { Meanof }^{\prime} B^{\prime}-\text { Meanof }^{\prime} A^{\prime}}{\sqrt{\text { Variance of }^{\prime} B^{\prime}+\text { Variance of }^{\prime} A^{\prime} * \sqrt{1 / n}}}$$

> 3.[This paper](http://ai.stanford.edu/~ronnyk/2009controlledExperimentsOnTheWebSurvey.pdf) references the t test(p 152):

$$t=\frac{\overline{O_{B}}-\overline{O_{A}}}{\widehat{\sigma_{d}}}$$

> 4.But according to [this thread](https://stats.stackexchange.com/questions/153044/fishers-exact-test-vs-chi-squared) fisher's exact test should only be used with smaller sample sizes 

- 등등등.... 
- 다양한 방법론이 있는데 , 어떤 방법을 써야 할까요?

> ## $\chi^{2}$ TEST of PROPORTIONS IS IDENTICAL TO Z-TEST SQUARED:

> Lemma

- we can prove that $\chi_{1 d f}^{2}$ is equivalent to $X^{2}$ with $X \sim N(0,1)$ 

> Note

- So I get all these points, yet I still don’t know how they apply to the actual implementation of these two tests for two reasons:

1. *A z-test is not squared.*
2. *The actual test statistics are completely different:*

$$\chi^{2}=\sum_{i=1}^{n} \frac{\left(O_{i}-E_{i}\right)^{2}}{E_{i}}=N \sum_{i=1}^{n} p_{i}\left(\frac{\frac{O_{i}}{N}-p_{i}}{p_{i}}\right)^{2}=\frac{n\left(n_{11} n_{22}-n_{12} n_{21}\right)^{2}}{n_{+1} n_{+2} n_{1+} n_{2+}}$$

- $\chi^{2}=$ Pearson's cumulative test statistic, which asymptotically approaches a $\chi^{2}$ distribution. $O_{i}=$ the number of observations of type $i$; $N=$ total number of observations; $E_{i}=N p_{i}=$ the expected (theoretical) frequency of type $i$, asserted by the null hypothesis that the fraction of type $i$ in the population is $p_{i} ; n=$ the number of cells in the table.
- Of note the last expression of the $\chi^{2}$ statistic applies to $2 \times 2$ tables and the nomenclature is as follows:

$$\begin{array}{|c|c|c|}
\hline n_{11}=X & n_{12}=n_{1}-X & n_{1}=n_{1+} \\
\hline n_{21}=Y & n_{22}=n_{2}-Y & n_{2}=n_{2+} \\
\hline n_{+1} & n_{+2} & \\
\hline
\end{array}$$

> Z -Test

$Z=\frac{\frac{x_{1}}{n_{1}}-\frac{x_{2}}{n_{2}}}{\sqrt{p(1-p)\left(1 / n_{1}+1 / n_{2}\right)}}$ with $p=\frac{x_{1}+x_{2}}{n_{1}+n_{2}}$, where $x_{1}$ and $x_{2}$ are the number of "successes", over the number of subjects in each one of the levels of the categorical variables, i.e. $n_{1}$ and $n_{2}$.

These two tests statistics are clearly different, and result in different results for the actual test statistics, as well as for the $p$-values: $5.8481$ for the $\chi^{2}$ and $2.4183$ for the z-test.

 The $p$-value for the $\chi^{2}$ test is $0.01559$, while for the z-test is $0.0077$. The difference explained by two-tailed versus one-tailed: $0.01559 / 2=0.007795$. 

In the example on the last hyperlink the $\chi^{2}$ is almost the square of the z-test statistic, but not quite, and the p-values are different.

- 위처럼 다른값이 나온 이유는 Yates' continuity correction 떄문입니다. 

```R
> chisq.test(x)
Pearson's Chi-squared test with Yates' continuity correction
data:  x
X-squared = 0.85714, df = 1, p-value = 0.3545
```

- 위와 같이 기본적으로 R 에서는 `Yates' continuity` 를 사용하기 때문에 차이가 나게 되는것이에요. (아마 다른 패키지도 비슷할듯?)

> Proof

- Performing the chisq.test ( ) with correct=FALSE yields exactly the square of the z-test: in the output numbers included in the end of the question $2.4183^{2}=5.84817$.
- These are two identical tests. $Z$ squared is the chi-square statistic. Let you have $2 x 2$ frequency table where columns are the two groups and the rows are "success" and "failure". Then the so called expected frequencies of the chi-square test in a given column is the weighted (by the groups' $N)$ average column (group) profile multiplied by that group's $N$. Thus, it comes that chi-square tests the deviation of each of the two groups profiles from this average group profile - which is equivalent to testing the groups' profiles difference from each other, the z-test of proportions.
- Let us have a $2 x 2$ frequency table where columns are two groups of respondents and rows are the two responses "Yes" and "No". And we've turned the frequencies into the proportions within group, i.e. into the vertical profiles:

```
      Gr1   Gr2  Total
Yes   p1    p2     p
No    q1    q2     q
      --------------
     100%  100%   100%
      n1    n2     N
```

- The usual (not Yates corrected) $\chi^{2}$ of this table, after you substitute proportions instead of frequencies in its formula, looks like this:

$$n_{1}\left[\frac{\left(p_{1}-p\right)^{2}}{p}+\frac{\left(q_{1}-q\right)^{2}}{q}\right]+n_{2}\left[\frac{\left(p_{2}-p\right)^{2}}{p}+\frac{\left(q_{2}-q\right)^{2}}{q}\right]=\frac{n_{1}\left(p_{1}-p\right)^{2}+n_{2}\left(p_{2}-p\right)^{2}}{p q} .$$

- Remember that $p=\frac{n_{1} p_{1}+n_{2} p_{2}}{n_{1}+n_{2}}$, the element of the weighted average profile of the two profiles (p1, q1) and (p2, q 2), and plug it in the formula, to obtain

$$\ldots=\frac{\left(p_{1}-p_{2}\right)^{2}\left(n_{1}^{2} n_{2}+n_{1} n_{2}^{2}\right)}{p q N^{2}}$$

Divide both numerator and denominator by the $\left(n_{1}^{2} n_{2}+n_{1} n_{2}^{2}\right)$ and get

$$\frac{\left(p_{1}-p_{2}\right)^{2}}{p q\left(1 / n_{1}+1 / n_{2}\right)}=Z^{2},$$

- the squared z-statistic of the z-test of proportions for “Yes” response.
- Thus, the 2x2 homogeneity Chi-square statistic (and test) is equivalent to the z-test of two proportions. The so called expected frequencies computed in the chi-square test in a given column is the weighted (by the group `n`) average vertical profile (i.e. the profile of the “average group”) multiplied by that group’s `n`. Thus, it comes out that chi-square tests the deviation of each of the two groups profiles from this average group profile, - which is equivalent to testing the groups’ profiles difference from each other, which is the z-test of proportions.
- This is one demonstration of a link between a variables association measure (chi-square) and a group difference measure (z-test statistic). Attribute associations and group differences are (often) the two facets of the same thing.

> Lemma

Showing the expansion in the first line above:

$$\begin{aligned}
&n_{1}\left[\frac{\left(p_{1}-p\right)^{2}}{p}+\frac{\left(q_{1}-q\right)^{2}}{q}\right]+n_{2}\left[\frac{\left(p_{2}-p\right)^{2}}{p}+\frac{\left(q_{2}-q\right)^{2}}{q}\right] \\
&=\frac{n_{1}\left(p_{1}-p\right)^{2} q}{p q}+\frac{n_{1}\left(q_{1}-q\right)^{2} p}{p q}+\frac{n_{2}\left(p_{2}-p\right)^{2} q}{p q}+\frac{n_{2}\left(q_{2}-q\right)^{2} p}{p q} \\
&=\frac{n_{1}\left(p_{1}-p\right)^{2}(1-p)+n_{1}\left(1-p_{1}-1+p\right)^{2} p+n_{2}\left(p_{2}-p\right)^{2}(1-p)+n_{2}\left(1-p_{2}-1+p\right)^{2} p}{p q} \\
&=\frac{n_{1}\left(p_{1}-p\right)^{2}(1-p)+n_{1}\left(p-p_{1}\right)^{2} p+n_{2}\left(p_{2}-p\right)^{2}(1-p)+n_{2}\left(p-p_{2}\right)^{2} p}{p q} \\
&=\frac{\left[n_{1}\left(p_{1}-p\right)^{2}\right][(1-p)+p]+\left[n_{2}\left(p_{2}-p\right)^{2}\right][(1-p)+p]}{p q}\\
&=\frac{n_{1}\left(p_{1}-p\right)^{2}+n_{2}\left(p_{2}-p\right)^{2}}{p q} .
\end{aligned}$$

> ## Answer

1. z-test. A z-test assumes that our observations are independently drawn from a Normal distribution with unknown mean and *known variance.* A z-test is used primarily when we have quantitative data. (i.e. weights of rodents, ages of individuals, systolic blood pressure, etc.) However, z-tests can also be used when interested in proportions. (i.e. the proportion of people who get at least eight hours of sleep, etc.)
2. t-test. A t-test assumes that our observations are independently drawn from a Normal distribution with unknown mean and *unknown variance.* Note that with a t-test, we do not know the population variance. This is far more common than knowing the population variance, so a t-test is generally more appropriate than a z-test, but practically there will be little difference between the two if sample sizes are large.

With z- and t-tests, your alternative hypothesis will be that your population mean (or population proportion) of one group is either not equal, less than, or greater than the population mean (or proportion) of the other group. This will depend on the type of analysis you seek to do, but your null and alternative hypotheses directly compare the means/proportions of the two groups.

1. Chi-squared test. Whereas z- and t-tests concern quantitative data (or proportions in the case of z), chi-squared tests are appropriate for qualitative data. Again, the assumption is that observations are independent of one another. In this case, you aren't seeking a particular relationship. Your null hypothesis is that no relationship exists between variable one and variable two. Your alternative hypothesis is that a relationship does exist. This doesn't give you specifics as to how this relationship exists (i.e. in which direction the relationship goes) but it will provide evidence that a relationship does (or does not) exist between your independent variable and your groups.
2. Fisher's exact test. One drawback to the chi-squared test is that it is *asymptotic.* This means that the p-value is accurate for very large sample sizes. However, if your sample sizes are small, then the p-value may not be quite as accurate. As such, Fisher's exact test allows you to exactly calculate the p-value of your data and not rely on approximations that will be poor if your sample sizes are small.

I keep discussing sample sizes - different references will give you different metrics as to when your samples are large enough. I would just find a reputable source, look at their rule, and apply their rule to find the test you want. I would not "shop around", so to speak, until you find a rule that you "like".

Ultimately, the test you choose should be based on a) your sample size and b) what form you want your hypotheses to take. If you are looking for a specific effect from your A/B test (for example, my B group has higher test scores), then I would opt for a z-test or t-test, pending sample size and the knowledge of the population variance. If you want to show that a relationship merely exists (for example, my A group and B group are different based on the independent variable but I don't care which group has higher scores), then the chi-squared or Fisher's exact test is appropriate, depending on sample size.

Does this make sense? Hope this helps!

> ## Conclusion

- 다 같은 한통속이다! 
- 샘플이 작다면 Exact Test 를 추천한다.

---

**reference**

- <http://rinterested.github.io/statistics/chi_square_same_as_z_test.html>
- A/B Testiing platforms 
- Bayesian A/B Testing
- Frequentust A./B Testing 
- 



