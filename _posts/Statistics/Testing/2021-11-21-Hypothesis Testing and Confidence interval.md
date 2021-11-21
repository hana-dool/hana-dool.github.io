---
title:  "Hypothesis Testing and Confidence interval"
excerpt: "Hypothesis Testing 과 CI Testing"
categories:
  - Stat_Testing
last_modified_at: 2021-11-14

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 가설검정과 Confidence interval 은 관련이 있는데 어떤 관련이 있을까요? 
{: .notice--warning}

# [Hypothesis and Confidence interval](#link){: .btn .btn--primary}{: .align-center}

> ## Hypothesis Testing

> Example

- 아래와 같은 Hypothesis Testing 을 시험하려 한다고 합시다. 이때 with a significance level of $\alpha$ 로 아래의 테스트를 진행하려 한다고 합시다. 

$$\begin{aligned}
&H_{0}: \mu=\mu_{0} \\
&H_{a}: \mu \neq \mu_{0}
\end{aligned}$$

- 이때에 Testing Method 는 Z Testing 입니다.

> Using Z statistics 

- 기각역을 이용한 Hypothesis Testing 을 사용한다고 합시다. 그렇다면 Decision Rule 은 아래와 같습니다.

We would reject $H_{0}$ at $\alpha=0.05$ if:

$$\frac{\bar{X}-\mu_{0}}{\sigma / \sqrt{n}} \leq-1.96 \text { or } \frac{\bar{X}-\mu_{0}}{\sigma / \sqrt{n}} \geq 1.96$$

> Using Confidence interval

- Confidence interval 을 이용한 Hypothesis Testing Decision Rulw 은 다음과 같습니다.

we would reject $H_{0}$ at $\alpha=0.05$ if:

$$\mu_{0} \geq \bar{X}+1.96 \frac{\sigma}{\sqrt{n}} \text { or } \mu_{0} \leq \bar{X}-1.96 \frac{\sigma}{\sqrt{n}}$$

> Relation 

- 사실 둘의 Decision Rule 은 같습니다. 

$$\frac{\bar{X}-\mu_{0}}{\sigma / \sqrt{n}} \leq-1.96 \text { or } \frac{\bar{X}-\mu_{0}}{\sigma / \sqrt{n}} \geq 1.96$$

$$\mu_{0} \geq \bar{X}+1.96 \frac{\sigma}{\sqrt{n}} \text { or } \mu_{0} \leq \bar{X}-1.96 \frac{\sigma}{\sqrt{n}}$$

- 위처럼 일치하는것을 볼 수 있습니다!

> ## Equality of CI and Hypothesis Testing

- 일반적으로 Hypothesis testing 과 Confidence interval 를 이용한 Testing 은 같습니다.
  - 그 이유는 Confidence interval 을 Construct 하는 과정만 봐도 알 수 있습니다. 

> Construct CI

- Confidence Interval for $\mu$ Under Normality 인 상황이라고 합시다.

$$\begin{aligned}
1-\alpha &=P\left(-t_{\alpha / 2, n-1}<T<t_{\alpha / 2, n-1}\right) \\
&=P\left(-t_{\alpha / 2, n-1}<\frac{\bar{X}-\mu}{S / \sqrt{n}}<t_{\alpha / 2, n-1}\right) \\
&=P\left(-t_{\alpha / 2, n-1} \frac{S}{\sqrt{n}}<\bar{X}-\mu<t_{\alpha / 2, n-1} \frac{S}{\sqrt{n}}\right) \\
&=P\left(\bar{X}-t_{\alpha / 2, n-1} \frac{S}{\sqrt{n}}<\mu<\bar{X}+t_{\alpha / 2, n-1} \frac{S}{\sqrt{n}}\right)
\end{aligned}$$

Once the sample is drawn, let $\bar{x}$ and $s$ denote the realized values of the statistics $\bar{X}$ and $S$, respectively. Then a $(1-\alpha) 100 \%$ confidence interval for $\mu$ is given by

$$\left(\bar{x}-t_{\alpha / 2, n-1} s / \sqrt{n}, \bar{x}+t_{\alpha / 2, n-1} s / \sqrt{n}\right)\left(\bar{x}-t_{\alpha / 2, n-1} s / \sqrt{n}, \bar{x}+t_{\alpha / 2, n-1} s / \sqrt{n}\right)$$

> Note

- 즉 위와 같이 Confidence interval 을 Construct 할 때에는 다음과 같습니다.
  - CI : Assumption $\to$ 통계량 분포 찾아냄 $\to$ 통계량으로부터 interval 정함  
  - Test : Assumption $\to$ 통계량 분포 찾아냄 $\to$ 통계량으로부터 기각역 정함
- 즉! 두개는 완전히 같은 Procedure 를 따르므로 두개는 일치하는 것입니다.

> ## Pooled Variance and CI : t (two sample mean)

- Pooled Variance 를 사용하는 Testing 의 경우에는 살짝 달라집니다. 
- 아래의 Testing 은 등분산을 가정한 Two sample mean testing 을 실시한다고 합시다.

> two sample mean test with equal variance S

Assume $X$ is distributed $N\left(\mu_{1}, \sigma^{2}\right)$ and $Y$ is distributed $N\left(\mu_{2}, \sigma^{2}\right)$, where $\sigma^{2}$ is the common variance of $X$ and $Y$. As above, let $X_{1}, \ldots, X_{n_{1}}$ be a random sample from the distribution of $X$, let $Y_{1}, \ldots, Y_{n_{2}}$ be a random sample from the distribution of $Y$, and assume that the samples are independent of one another. 

Let $n=n_{1}+n_{2}$ be the total sample size. Our estimator of $\Delta$ is $\bar{X}-\bar{Y}$. Our goal is to show that a pivot random variable, defined below, has a $t$-distribution.

Because $\bar{X}$ is distributed $N\left(\mu_{1}, \sigma^{2} / n_{1}\right), \bar{Y}$ is distributed $N\left(\mu_{2}, \sigma^{2} / n_{2}\right)$, and $\bar{X}$ and $\bar{Y}$ are independent, we have the result

$$\frac{(\bar{X}-\bar{Y})-\left(\mu_{1}-\mu_{2}\right)}{\sigma \sqrt{\frac{1}{n_{1}}+\frac{1}{n_{2}}}} \text { has a } N(0,1) \text { distribution. }$$

This serves as the numerator of our $T$-statistic. Let

$$S_{p}^{2}=\frac{\left(n_{1}-1\right) S_{1}^{2}+\left(n_{2}-1\right) S_{2}^{2}}{n_{1}+n_{2}-2}$$

Note that $S_{p}^{2}$ is a weighted average of $S_{1}^{2}$ and $S_{2}^{2}$. It is easy to see that $S_{p}^{2}$ is an unbiased estimator of $\sigma^{2} .$ It is called the pooled estimator of $\sigma^{2} .$ 

Also, because $\left(n_{1}-1\right) S_{1}^{2} / \sigma^{2}$ has a $\chi^{2}\left(n_{1}-1\right)$ distribution, $\left(n_{2}-1\right) S_{2}^{2} / \sigma^{2}$ has a $\chi^{2}\left(n_{2}-1\right)$ distribution, and $S_{1}^{2}$ and $S_{2}^{2}$ are independent, we have that $(n-2) S_{p}^{2} / \sigma^{2}$ has a $\chi^{2}(n-2)$ distribution 

Finally, because $S_{1}^{2}$ is independent of $\bar{X}$ and $S_{2}^{2}$ is independent of $\bar{Y}$, and the random samples are independent of each other, it follows that $S_{p}^{2}$ is independent of 분자, 분모

 Therefore, we have that

$$\begin{aligned}
T &=\frac{\left[(\bar{X}-\bar{Y})-\left(\mu_{1}-\mu_{2}\right)\right] / \sigma \sqrt{n_{1}^{-1}+n_{2}^{-1}}}{\sqrt{(n-2) S_{p}^{2} /(n-2) \sigma^{2}}} \\
&=\frac{(\bar{X}-\bar{Y})-\left(\mu_{1}-\mu_{2}\right)}{S_{p} \sqrt{\frac{1}{n_{1}}+\frac{1}{n_{2}}}}
\end{aligned}$$

has a $t$-distribution with $n-2$ degrees of freedom. From this last result, it is easy to see that the following interval is an exact $(1-\alpha) 100 \%$ confidence interval for $\Delta=\mu_{1}-\mu_{2}$

$$\left((\bar{x}-\bar{y})-t_{(\alpha / 2, n-2)} s_{p} \sqrt{\frac{1}{n_{1}}+\frac{1}{n_{2}}},(\bar{x}-\bar{y})+t_{(\alpha / 2, n-2)} s_{p} \sqrt{\frac{1}{n_{1}}+\frac{1}{n_{2}}}\right)$$

> Note

- 우와 같은 경우에도 살짝 Pooled Variance 를 적용하는 부분이 있지만, 이는 'Assumption' 을 만족할때에 당연히 성립하는 부분이므로, 이전과 특별히 다른 부분은 없습니다.
- CI : Assumption $\to$ 통계량 분포 찾아냄 $\to$ 통계량으로부터 interval 정함  
- Test : Assumption $\to$ 통계량 분포 찾아냄 $\to$ 통계량으로부터 기각역 정함
- 즉! 두개는 완전히 같은 Procedure 를 따르므로 이 경우에도 Testing 의 결과는 일치합니다.

# [Pooled Variance and CI (proportion)](#link){: .btn .btn--primary}{: .align-center}

> ## Pooled Variance and CI (proportion)

> Test Statistics

$$\frac{\left(\hat{p}_{X}-\hat{p}_{Y}\right)-\left(p_{X}-p_{Y}\right)}{\sqrt{\frac{p_{X}\left(1-p_{X}\right)}{n}+\frac{p_{Y}\left(1-p_{Y}\right)}{m}}}$$

has an approximate standard normal distribution.

> Test Statistics + Null Hypothesis

Under the null hypothesis that $p_{X}=p_{Y}=p$,

$$\frac{\left(\hat{p}_{X}-\hat{p}_{Y}\right)}{\sqrt{p(1-p)\left(\frac{1}{n}+\frac{1}{m}\right)}}$$

has an approximate standard normal distribution.

> Confidence Interval

$$\hat{p}_{1}-\hat{p}_{2} \pm z_{\alpha / 2} \sqrt{\frac{\hat{p}_{1}\left(1-\hat{p}_{1}\right)}{n_{1}}+\frac{\hat{p}_{2}\left(1-\hat{p}_{2}\right)}{n_{2}}}$$

> ## Testing Results Not align with CI ?

- 아니? 이번에는 Confidence interval 과 Test Statistic 이 약간 다른것 같습니다. 
- 이는 아래와 같은 차이가 있기 때문인데요
  - CI : Assumption $\to$ 통계량 분포 찾아냄 $\to$ 통계량으로부터 interval 정함  
  - Test : Assumption $\to$ Null hypothesis 의 정보까지 넣음 $\to$  통계량 분포 찾아냄 $\to$ 통계량으로부터 기각역 정함
- 위처럼 이번에는 Null hypothesis 의 정보 ($p_{X}=p_{Y}=p$) 까지 넣기 때문인데요,  Hypothesis Testing 의 Procedure 은 '귀무가설의 입장에서 데이터를 바라볼때에 내 데이터가 얼마나 이상한가? 를 생각한다는것을 명심하세요'
  - 즉 '귀무가설의 입장' 을 잘 나타낼수록 좋은 Testing 이 되겠죠? 그래서 귀무가설의 정보량 ($p_{X}=p_{Y}=p$) 까지 넣어서 p-value(또는 기각역) 를 설정하는 것입니다. 
  - 하지만 proportion 이전에 다른 Testing 에서 Null hypothesis 를 활용하지 않은 이유는 $\mu$ 에 대한 정보를 안다고 해도, $\mu$ 는 애초에 모수이기때문에 어떻게 할수있는 부분이 아니였고 , $\sigma$ 에 대한 추정은 불가능했기 때문입니다. 
- 그러므로 위와 같이 Testing 의 결과와 Confidence interval 의 결과가 약간 다를 수 있습니다.

> ## Confidence interval not using null

- 하지만 Confidence interval 을 Construct 할때에는 위와 같은 Null Hypothesis 의 정보를 활용하지 않습니다.
  - 왜 Null hypothesis 를 활용하지 않을까요? CI 의 정의에 대해서 알아봅시다.

> Confidence interval definition

Let $X_{1}, X_{2}, \ldots, X_{n}$ be a sample on a random variable $X$, where $X$ has $p d f \ f(x ; \theta), \theta \in \Omega$. Let $0<\alpha<1$ be specified. Let $L=L\left(X_{1}, X_{2}, \ldots, X_{n}\right)$ and $U=U\left(X_{1}, X_{2}, \ldots, X_{n}\right)$ be two statistics. We say that the interval $(L, U)$ is a $(1-\alpha) 100 \%$ confidence interval for $\theta$ if $1-\alpha=P_{\theta}[\theta \in(L, U)]$

> Confidence interval not using null

- 즉 위와 Confidence interval 은 한마디로 말해서 range of plausible values for an unknown [parameter](https://en.wikipedia.org/wiki/Statistical_parameter) 입니다.
  - 즉 모수에 대해서, 값이 나올듯한 범위를 제공할 뿐, Null Hypothesis 의 정보를 쓰지는 않는다는 것입니다.

> ## So... How can i do?

- 이 경우에는 두가지 방향성이 있다고 합니다. (<https://online.stat.psu.edu/stat415/lesson/9/9.4>) 
  - Pooled 를 쓰면 아주쪼금 더 정확해짐 $\to$ Confidence interval 추정과 결과가 맞지 않음
  - UnpPooled 를 쓰면 Pooled 보다 쪼끔안좋음 $\to$ Confidence interval 추정과 결과가 맞음

> 두가지 Statistics 

For testing $H_{0}: p_{1}=p_{2}$, some statisticians use the test statistic:

$$Z=\frac{\left(\hat{p}_{1}-\hat{p}_{2}\right)-0}{\sqrt{\frac{\hat{p}_{1}\left(1-\hat{p}_{1}\right)}{n_{1}}+\frac{\hat{p}_{2}\left(1-\hat{p}_{2}\right)}{n_{2}}}}$$

instead of the one we used:

$$Z=\frac{\left(\hat{p}_{1}-\hat{p}_{2}\right)-0}{\sqrt{\hat{p}(1-\hat{p})\left(\frac{1}{n_{1}}+\frac{1}{n_{2}}\right)}}$$

An advantage of doing so is again that the interpretation of the confidence interval - does it contain 0? - is always consistent with the hypothesis test decision.

> Examples

- Pooled variance 
  - https://online.stat.psu.edu/stat415/lesson/9/9.4
  - <https://courses.lumenlearning.com/wmopen-concepts-statistics/chapter/hypothesis-test-for-difference-in-two-population-proportions-3-of-6/>
- Not pooled variance
  - <https://stats.libretexts.org/Bookshelves/Introductory_Statistics/Book%3A_Introductory_Statistics_(Shafer_and_Zhang)/09%3A_Two-Sample_Problems/9.04%3A_Comparison_of_Two_Population_Proportions>

---

**reference**

- wiki 
- <https://online.stat.psu.edu/stat415/lesson/9/9.4>)
- hogg 의 introduciton to mathematical statistics 7ed
- 기타등등..

