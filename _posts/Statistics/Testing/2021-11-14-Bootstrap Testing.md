---
title:  "Bootstrap Hypothesis Testing"
excerpt: "부트스트랩을 이용한 가설검정"
categories:
  - Stat_Testing
last_modified_at: 2021-11-14

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 부트스트랩을 이용한 가설검정 절차
{: .notice--warning}

# [Hypothesis Testing with the Bootstrap](#link){: .btn .btn--primary}{: .align-center}

> ## Bootstrap Hypothesis Testing

- Bootstrap Hypothesis Test 는 Test statistics t(x) 를 정의함으로 부터 출발합니다.
- 그리고 우리는 achived significance level 을 다음과 같이 정의하고, 이 값을 계산하려 합니다. 

$$A S L=\operatorname{Prob}_{H_{0}}\left\{t\left(\boldsymbol{x}^{*}\right) \geq t(\boldsymbol{x})\right\}$$

- 이때 $x^*$ 은 distribution specified by null hypothesis $H_0$ 입니다. (이는 $F_0$ 으로 표기되기도 합니다.)

> Two Sample problem

- 우리는 두개의 sample 을 관측했다고 합시다.

$$\begin{array}{ll}
F \rightarrow & \boldsymbol{z}=\left(z_{1}, z_{2}, \ldots, z_{n}\right) \text { independently of } \\
G \rightarrow & \boldsymbol{y}=\left(y_{1}, y_{2}, \ldots, y_{m}\right)
\end{array}$$

- 글고 우리는 다음과 같은 null hypothesis 를 테스트 하려고 합니다. 

$$H_{0}: F=G$$

> Bootstrap Hypothesis Testing F = G

- Denote the combined sample by $x$, and its empirical distribution by $\widehat{F}_{0}$.
- Under $H_{0}, \hat{F}_{0}$ provides a non parametric estimate for the common population that gave rise to both $z$ and $y$

(1) Draw $\boldsymbol{B}$ samples of size $n+m$ with replacement from $\boldsymbol{x}$. Call the first $\mathrm{n}$ observations $$\mathbf{z}^{*}$$ and the remaining $$m-\boldsymbol{y}^{*}$$

(2) Evaluate $t(\cdot)$ on each sample $-t\left(\boldsymbol{x}^{* \boldsymbol{b}}\right)$

(3) Approximate $A S L_{\text {boot }}$ by

$$\widehat{A S L}_{b o o t}=\#\left\{t\left(\boldsymbol{x}^{* \boldsymbol{b}}\right) \geq t(\boldsymbol{x})\right\} / B$$

- In the case that large values of $t\left(\boldsymbol{x}^{* \boldsymbol{b}}\right)$ are evidence against $H_{0}$

> Note

- 하지만 우리가 테스트하려는건 위처럼 '두 분포가 같을까?' 가 아닌 경우가 많습니다.
- 대게 제일 많이 궁금해 하는것은 바로 '두 분포의 평균이 같을까?' 와 같은 고민이죠. 그래서 위와 같은 테스트 방식은 우리가 알려고 하는것과는 다소 거리가 있을 수 있습니다.

> ## Testing Euality of Means

> How to?

Instead of testing $H_{0}: F=G$, we wish to test $$\mathrm{H}_{0}: \mu_{z}=\mu_{y}$$, without assuming equal variances. We need estimates of $F$ and $G$ that use only the assumption of common mean

(1) Define points $$\tilde{z}_{i}=z_{i}-\bar{z}+\bar{x}, i=1, \ldots, n$$, and $$\tilde{y}_{i}=y_{i}-$$  $$\bar{y}+\bar{x}, i=1, \ldots, m$$. The empirical distributions of $\tilde{z}$ and $\widetilde{y}$ shares a common mean.

(2) Draw $B$ bootstrap samples with replacement $$\left(\mathbf{z}^{*}, \boldsymbol{y}^{*}\right)$$ from $$\tilde{z}_{1}, \tilde{z}_{2}, \ldots, \tilde{z}_{n}$$ and $$\tilde{y}_{1}, \tilde{y}_{2}, \ldots, \tilde{y}_{m}$$ respectivly

(3) Evaluate $t(\cdot)$ on each sample

$$t\left(\boldsymbol{x}^{* \boldsymbol{b}}\right)=\frac{\bar{z}^{*}-\bar{y}^{*}}{\sqrt{\bar{\sigma}_{z}^{*} 1 / n+\bar{\sigma}_{y}^{*} 1 / m}}$$

(4) Approximate $A S L_{\text {boot }}$ by

$$\widehat{A S L}_{\text {boot }}=\#\left\{t\left(\boldsymbol{x}^{* \boldsymbol{b}}\right) \geq t(\boldsymbol{x})\right\} / B$$

> ## permutation Test vs Bootstrap Test

- Accuracy: In the two-sample problem, $A S L_{p e r m}$ is the exact probability of obtaining a test statistic as extreme as the one observed. In contrast, the bootstrap explicitly samples from estimated probability mechanism. $\widehat{A S L}_{\text {boot }}$ has no interpretation as an exact probability.
- Flexibility: When special symmetry isn't required, the bootstrap testing can be applied much more generally than the permutation test. (Like in the two sample problem - permutation test is limited to $H_{0}: F=G$, or in the one-sample problem)

> ## one sample mean Test

> Problem

We observe a random sample:

$$F \rightarrow \quad \boldsymbol{z}=\left(z_{1}, z_{2}, \ldots, z_{n}\right)$$

And we wish to test whether the mean of the population equals to some predetermine value $\mu_{0}$

$$H_{0}: \mu_{z}=\mu_{0}$$

> $H_0$ 을 따르는 분포를 어떻게 만들지?

Bootstrap Hypothesis Testing $\mu_{z}=\mu_{0}$ What is the appropriate way to estimate the null distribution?
The empirical distribution $\widehat{F}$ is not an appropriate estimation, because it does not obey $H_{0}$. As before, we can use the empirical distribution of the points:

$$\tilde{z}_{i}=z_{i}-\bar{z}+\mu_{0}, i=1, \ldots, n$$

Which has a mean of $\mu_{0}$. 

> test statistics

The test will be based on the approximate distribution of the test statistic 

$$t(\boldsymbol{z})=\frac{\bar{z}-\mu_{0}}{\bar{\sigma} / \sqrt{n}}$$

We sample $\boldsymbol{B}$ times $$\tilde{z}_{1}^{*}, \ldots, \tilde{z}_{n}^{*}$$ with replacement from $$\tilde{z}_{1}, \ldots, \tilde{z}_{n}$$, and for each sample compute

$$t\left(\tilde{\boldsymbol{z}}^{*}\right)=\frac{\overline{\tilde{z}}-\mu_{0}}{\overline{\tilde{\sigma}} / \sqrt{n}}$$

And the estimated $A S L$ is given by

$$\widehat{A S L}_{b o o t}=\#\left\{t\left(\tilde{\boldsymbol{z}}^{* \boldsymbol{b}}\right) \geq t(\mathbf{z})\right\} / B$$

( In the case that large values of $t\left(\tilde{\mathbf{z}}^{* b}\right)$ are evidence against $H_{0}$ )

> Example

Taking $\mu_{0}=129$, the observed value of the test statistic is

$$t(\mathbf{z})=\frac{86.9-129}{66.8 / \sqrt{7}}=-1.67$$

(When estimating $\sigma$ with the unbiased estimator for standard deviation). For 94 of 1000 bootstrap samples, $t\left(\tilde{\mathbf{z}}^{*}\right)$ was smaller than $-1.67$, and therefor

$$\widehat{A S L}_{\text {boot }}=.094$$

For reference, the student's t-test result for the same null hypothesis on that data gives us

$$A S L=\operatorname{Prob}\left\{t_{6}<-\frac{42.1}{66.8 / \sqrt{7}}\right\}=0.07$$

> Note 

- 즉 위에서 핵심은 $H_0$ 을 따르는 분포를 만들때에 어떻게 해야될까? 가 됩니다.
- 왜냐하면 우리가 가지고 있는 데이터는 A 와 B 인데, 지금 상태는 $H_0$ 을 따르는 데이터의 상태가 아니기 때문입니다. 
- 그래서 $H_0 $​ 을 따르게 하기 위해서 $\tilde{z}_{i}=z_{i}-\bar{z}+\mu_{0}, i=1, \ldots, n$ 와 같은 변환을 하는 것입니다. 

> ## Summary

- A bootstrap hypothesis test is carried out using the followings:
  - (a) A test statistic $t(x)$
  - (b) An approximate null distribution $$\hat{F}_{0}$$ for the data under $$H_{0}$$ Given 

- these, we generate $B$ bootstrap values of $t\left(\boldsymbol{x}^{*}\right)$ under $\hat{F}_{0}$ and estimate the achieved significance level by

$$\widehat{A S L}_{b o o t}=\#\left\{t\left(\boldsymbol{x}^{* \boldsymbol{b}}\right) \geq t(\boldsymbol{x})\right\} / B$$

The choice of test statistic $t(x)$ and the estimate of the null distribution will determine the power of the test. In the stamp example, if the actual population density is bimodal, but the Gaussian kernel density does not approximate it accurately, then the suggested test will not have high power.'



---

  **Reference**

- <https://statweb.stanford.edu/~candes/teaching/stats300c/Lectures/Lecture01.pdf>
- <https://en.wikipedia.org/wiki/Bootstrapping_(statistics)#Bootstrap_hypothesis_testing>
- <https://stats.stackexchange.com/questions/92542/how-to-perform-a-bootstrap-test-to-compare-the-means-of-two-samples>



