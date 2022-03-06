---
title: "Choice of the Randomization Unit in Online Controlled
Experiment"
excerpt: "Randomized Unit 선택하기"
categories:
  - AB_Paper
last_modified_at: 2021-11-06

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 Metric 을 분석할때 Randomization Unit 과 Analysis Unit 이 다를때에는 어떻게 해야 될까
{: .notice--warning}

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## Abstract 

- Controlled Experiment 는 온라인 비즈니스를 위한 의사 결정을 지원하기위해서 널리 사용되곤 했습니다. 
  - 이때 적절하게 Experiment Unit 을 Randomization 함으로서, Casual Inference 를 가능하게 합니다. 
- 이때 Randomization 을 위해서 Experment unit 을 선택하는 기준은 매우 다릅니다.
  - User 또는 Page View 가 대표적으로 많이 선택되지만, 이것 말고도 다양한것들을 선택할 수 있습니다. 
- 하지만 이때 Randomization Unit 과 Experiment Unit 이 다른경우가 종종 발생합니다. 
  - ex : 유저 레벨로 Randomization 을 했지만 비교하는것은 평균 클릭수 / 평균 페이지 뷰 
- 이떄 사용할 Experiment Unit 을 선택하는것은 장단점이 있습니다. 어떤것을 선택하느냐에 따라서 실험 분석 방법에 영향을 끼칩니다.
  - 일반적으로 페이지별 Randomization 은 분산이 감소하고 샘플수가 늘어나 Power 가 큽니다. 
- 이 논문에서는 두개의 실험 단위를 비교하고, 2계층 Randomization Framework 하에서 페이지뷰에 대한 Randomization Experiment 를 올바르게 분석하는법을 알려드리려 합니다.

> ## Introduction

- A/B 테스트라고 불리는 통제 실험은 인과 관계를 확실하게 평가할 수 있는 방법론이라 할 수 있습니다. 이러한 A/B 테스트는 IT 회사에 경우 매우 발전되어 왔습니다. 
- 이때 널리 사용되는 방법은 Two Sample T-Test 를 사용하곤 하는데, 대부분의 문헌에서는  iid 가정 하에서 잘 작동되는 방법론만을 Naive 하게 소개하고 있습니다.
- 하지만 여기에서는 Randomization Step 에서부터 시작해서 어떻게 하면 더 정확한 분석을 할 수 있는지에 대해서 알아보려 합니다. 
- 우선 아래와 같은 표기법을 사용하려 합니다.
  - Let $n$ be the total number of unique users. 
  - Let $X_{i, j}$ be the perpage measurement (e.g. number of clicks on the page) on user $i$ 's $j^{\text {th }}$ page view 
  - $X_{i, j}$ has mean $\mu_{i}$ and variance $\sigma_{i}^{2}$. 
  - Denote $K_{i}$ the total number of page views from user $i$ 
  - $N=\sum_{i=1}^{n} K_{i}$ be the total number of page views
  - We assume for any $i, X_{i, j}, j=1, \ldots, K_{i}$ are i.i.d. and uniformly bounded above by some finite constant. 
  - we allow $\left(\mu_{i}, \sigma_{i}^{2}\right)$ to differ from user to user. 
  - We also assume $K_{i}, i=1, \ldots, n$ are i.i.d.
  - independent of $\left(\mu_{i}, \sigma_{i}^{2}\right), i=1, \ldots, n$. 
- 마지막 가정 (independent of $\left(\mu_{i}, \sigma_{i}^{2}\right), i=1, \ldots, n$. ) 은 사실 , 이론적으로 풀어내기 위해 가정한것이라 한번 확인해보는것이 필요할것입니다. 
  - 우리는 empirical data 를 사용하여 웹 실험의 몇 가지 주요 메트릭에 대해 이 가정을 확인했으며 이 가정은 타당하다는것을 확인했습니다!
- Randomize Experiment 에서 우리는 무작위화가 수행되는 단위를 (Randomized Unit)무작위화 단위라고 부르게 됩니다. 
- 그리고 분석 단계에서는 메트릭이 자연스럽게 이러한 단위와 연관되는데, 이를 분석 단위라고 합니다. 
  - 예를 들어서 사용자당 클릭과 같은 사용자 수준 메트릭은 분석 단위로 사용자(User)와 연결됩니다.
  - 클릭률(click through rate)과 같은 페이지 뷰 수준 메트릭은 페이지 뷰와 연결됩니다.

> Table of Contents

- 섹션 2에서는 먼저 사용자가 무작위화 단위로 사용되는 경우를 검토해 볼 것입니다. 
  - 특히 페이지 뷰 수준 메트릭에 관심이 있을때에는 델타 방법을 사용하는게 좋다는것을 말하려고 합니다. 
    - 만일 이 방법을 사용하지 못할 경우 편향에 대한 공식을 제공합니다.

- 섹션 3에는, 무작위화 단위를 페이지로 했을때의 경우를 살펴보려 합니다. 
  - 우리는 사용자 그룹을 먼저 모은 후에 페이지 뷰를 Treatment / Control 로 나누는 2계층 무작위 프레임워크에서의  페이지 뷰 수준 메트릭에 대한 Assumptotic 하게 일관된 분산 공식을 제시하려 합니다.

- 섹션 4는 시뮬레이션 결과를 제시한다. 
- 5절에서는 페이지뷰를 무작위화 단위로 사용할 경우의 장단점을 논의합니다.

> ## User As Randomization Unit

- 이 절에서는 무작위화 단위가 사용자인 경우에 초점을 맞춘다. 실제로 사용자는 로그인 ID 또는 단순히 브라우저에 저장된 쿠키로 식별되게 됩니다.
- 사용자 무작위 실험의 전통적인 적용은 사용자 수준 메트릭의 이동을 연구하는 것이다. 
  - 통계적 관점에서, 이러한 세팅은 Control 과 Treatment 그룹이 i.i.d 가정 하에서 동일하다가정 하에서 일반적인 two Sample T Test 를 적용할 수 있습니다. 

- 보다 구체적으로 말하게 된다면, 사용자 수준 메트릭은 사용자 수준애 대한 평균입니다.
  - 이때 User 는 Control 또는 Treatment 수준으로 무작위화되므로,  사용자 수준 측정은 독립적이고 동일하게 분포되어 있다고 가정해도 무방할 것입니다 .

- 섹션 1의 계층 모형에서는, 이는 각 사용자에 대해 독립적으로 $$(\mu_i, \sigma^2_i)$$를 가정한 다음,  특정 사용자에 대한 사용자 수준 측정을 해당 분포에서 도출한다는 것을 의미한다.
  -  $$\widetilde{X}_{T} \text { and } \widetilde{X}_{C}$$ 가 제어 및 처리하는 사용자 수준 측정 기준을 나타내며, 이 측정 기준은 독립적이라는 것이 분명합니다. 중심 한계 정리에 의해


$$\frac{\widetilde{X}_{T}-\widetilde{X}_{C}}{\sqrt{\operatorname{Var}\left\{\widetilde{X}_{T}-\widetilde{X}_{C}\right\}}} \rightarrow Z \qquad ...(1)$$

- where $Z$ is standard normal. The two sample t-test is to replace $$\mathbb{V} \operatorname{ar}\left\{\widetilde{X}_{\widetilde{T}}-\widetilde{X}_{C}\right\}$$ by its estimate. 
- In this particular case since $\widetilde{X}_{T}$ and $\widetilde{X}_{C}$ independent, $$\operatorname{Var}\left\{\widetilde{X}_{T}-\widetilde{X}_{C}\right\}= \mathbb{V} a r \widetilde{X}_{T}+\mathbb{V} a r \widetilde{X}_{C}$$ and both terms in the right hand side can be simply estimated via sample variances. 
- Also, for web experiment, $n$ is large (much much larger than most applications of two sample t-test). Therefore we might as well treat t-statistics as standard normal.
- For page view level metrics, $(1)$ still holds when $\widetilde{X}_{T}$ and $\widetilde{X}_{C}$ are replaced by page view level metrics $\bar{X}_{T}$ and $\bar{X}_{C}$. 
- However, $$\mathbb{V} a r\left\{\bar{X}_{T}-\bar{X}_{C}\right\}$$ can not be estimated by sample variances. Delta method is needed for variance estimation of $$\mathbb{V} a r \bar{X}_{g} , \ g=T,C$$ see Section 2.1. Moreover, when randomization unit is not user, $\bar{X}_{T}$ and $\bar{X}_{C}$ are not even independent and we need to estimate $\mathbb{V} a r\left\{\bar{X}_{T}-\bar{X}_{C}\right\}$ directly. This will be our topic in Section 3 .

> ## 2.1 Page Level Metrics and Delta Method

- Under our hierarchical model introduced in Section 1, a page level metric can be denoted by:

$$\bar{X}=\frac{\sum_{i=1}^{n} \sum_{j=1}^{K_{i}} X_{i, j}}{N}$$

- When user is the randomization unit, $\bar{X}_{T}$ and $\bar{X}_{C}$ are independent and $\mathbb{V} a r\left\{\bar{X}_{T}-\right.$ $\left.\bar{X}_{C}\right\}=\mathbb{V} a r \bar{X}_{T}+\mathbb{V} a r \bar{X}_{C} .$ 
  - Therefore we only need to focus on estimating $\mathbb{V} a r \bar{X}$. 
- To this end, it is tempting to treat page level metrics $X_{i, j}, j=1, \ldots, K_{i}, i=1, \ldots, n$, as i.i.d.
- and $\bar{X}$ under this assumption is an average of i.i.d. 
  - samples so the variance of $\bar{X}$ can be easily estimated by

$$\frac{1}{N^{2}}\left(\sum_{i=1}^{n} \sum_{j=1}^{K_{i}}\left(X_{i, j}-\bar{X}\right)^{2}\right)$$

- This estimator, which we call the naive estimator, is not consistent because in our model the user effect $\left(\mu_{i}, \sigma_{i}^{2}\right)$ are also a random sample from a distribution and page view level measurements $X_{i, j}$ of the same user are only independent conditioned on $\left(\mu_{i}, \sigma_{i}^{2}\right)$.
- Nevertheless, it is true in our model that the user level measurement $\left(\sum_{i=1}^{K_{i}} X_{i, j}, K_{i}\right), i=1, \ldots, n$ are i.i.d. 
- By letting $Y_{i}=\sum_{i=1}^{K_{i}} X_{i, j}$ and express $\bar{X}$ as $\sum_{i=1}^{n} Y_{i} / \sum_{i=1}^{n} K_{i}$, it is then a straightforward application of the delta method to get an asymptotically consistent estimator for $\mathbb{V a r} \bar{X}$ :

$$\left.\frac{1}{n}\left\{\frac{1}{\widehat{\mathbb{E} K_{i}}^{2}} \widehat{\mathbb{V} a r Y_{i}}+\frac{\widehat{\mathbb{E} Y_{i}}^2}{\widehat{\mathbb{E} K_{i}}^{4}} \widehat{\mathbb{V} \operatorname{arK}_{i}}-2 \frac{\widehat{\mathbb{E} Y_{i}}}{\widehat{\mathbb{E} K_{i}}^{3}} \operatorname{Cov} \widehat{\left(Y_{i}, K_{i}\right.}\right. )\right\}$$

- 위의 접근법을 요약하면, page level 로 Randomization 이 되어있지 않으므로, 각 메트릭값을 User level 로 집계한 다음에 delta method 를 이용해서 분산을 구해야 한다는 것입니다.
  - 예를 들어서 page 당 조회수가 (1,3,0,0,1,1,2,0,0,0,0,1,....) 과 같다고 합시다. 이를 User 별로 aggregate 하게 되면 (유저별 페이지수 , 유저별 조회수) 로 집계되면 ( (10,20), (8,33)... ) 과 같이 계산되게 됩니다. 여기에서 Ratio 의 평균 메트릭을 구하면 됩니다!
- where these "hatted" quantities are the sample mean, variance or covariance.
  For asymptotic analysis, we will let $n \rightarrow \infty$ (so $N \rightarrow \infty$ a.s.). 
- To normalize the naive estimator and delta method estimator, we multiply them by $n$ so that they will converge to some nonzero numbers. We introduce the normalized naive estimator

$$\widehat{\sigma_{n}^{2}}=n \frac{1}{N^{2}}\left(\sum_{i=1}^{n} \sum_{j=1}^{K_{i}}\left(X_{i, j}-\bar{X}\right)^{2}\right) \quad ...(2)$$

- and the normalized delta method estimator

$$\widehat{\sigma_{d}^{2}}=\frac{1}{\widehat{\mathbb{E} K_{i}}^{2}} \widehat{\mathbb{V} a r Y}_{i}+\frac{\widehat{\mathbb{E} Y}_{i}^{2}}{\widehat{\mathbb{E} K_{i}}^{4}} \widehat{\mathbb{V} a r K_{i}}-2 \frac{\widehat{\mathbb{E} Y_{i}}}{\widehat{\mathbb{E} K_{i}}^{3}} \operatorname{Cov(Y_{i},K_{i})} \quad ...(3)$$

- A natural question to ask is how biased is the naive estimator $\widehat{\sigma_{n}^{2}}$ relative to the true normalized variance $n \mathbb{V} a r \bar{X}$. This is answered in the following theorem.

> Theorem 

- Let $C=\frac{\mathbb{E} K_{i}^{2}}{\left(\mathbb{E} K_{i}\right)^{2}}$. Then, as $n \rightarrow \infty$,

$$\begin{aligned}n \mathbb{V a r} \bar{X} & \rightarrow C \mathbb{V} a r\left(\mu_{i}\right)+\mathbb{E}\left(\sigma_{i}^{2}\right) / \mathbb{E}\left(K_{i}\right) \quad ...(4) \\
\widehat{\sigma_{d}^{2}} & \rightarrow C \mathbb{V} a r\left(\mu_{i}\right)+\mathbb{E}\left(\sigma_{i}^{2}\right) / \mathbb{E}\left(K_{i}\right) \quad ...(5) \\\widehat{\sigma_{n}^{2}} & \rightarrow \frac{1}{\mathbb{E}\left(K_{i}\right)}\left(\mathbb{V} \operatorname{ar}\left(\mu_{i}\right)+\mathbb{E}\left(\sigma_{i}^{2}\right)\right) \quad ...(6)\end{aligned}$$

- Let $\rho:=\mathbb{V} \operatorname{ar}\left(\mu_{i}\right) /\left(\mathbb{V} \operatorname{ar}\left(\mu_{i}\right)+\mathbb{E}\left(\sigma_{i}^{2}\right)\right)$ be the user effect coefficient(variances that explained by between user variation), then

$$\frac{n \mathbb{V} a r(\bar{X})}{\widehat{\sigma_{n}^{2}}} \rightarrow\left(\mathbb{E}\left(K_{i}\right) C-1\right) \rho+1$$

- The convergence in (5) and (6) are in probability.

> Proof

- (5) follows directly from the property of the delta method. To prove $(4)$, we first apply conditional variance formula by conditioning on $\left(\mu_{i}, \sigma_{i}^{2}, K_{i},\right.$, $i=1, \ldots, n)$. This gives

$$\begin{aligned}
& \mathbb{V a r} \bar{X}=\mathbb{V} a r\left(\mathbb{E}\left(\frac{\sum_{i=1}^{n} \sum_{j=1}^{K_{i}} X_{i, j}}{N} \mid K_{i}, \mu_{i}, \sigma_{i}^{2}, i=1, \ldots, n\right)\right) \\
+& \mathbb{E}\left(\mathbb{V} a r\left(\frac{\sum_{i=1}^{n} \sum_{j=1}^{K_{i}} X_{i, j}}{N} \mid K_{i}, \mu_{i}, \sigma_{i}^{2}, i=1, \ldots, n\right)\right) \\
=& \mathbb{V} a r\left(\frac{1}{N} \sum_{i=1}^{n} K_{i} \mu_{i}\right)+\mathbb{E}\left(\frac{1}{N^{2}} \sum_{i=1}^{n} K_{i} \sigma_{i}^{2}\right)
\end{aligned}$$

- Let $w_{i}=K_{i} / \sum_{i=1}^{n} K_{i}=K_{i} / N$. Since $K_{i}$ independent of $\left(\mu_{i}, \sigma_{i}^{2}\right)$ and $N / n \rightarrow \mathbb{E} K_{i}$ as $n \rightarrow \infty$, we can further simplify the right hand. First, by applying iterative expectation(frist conditioning on $\left.w_{1}, \ldots, w_{n}\right)$, we have

$$n \mathbb{E}\left(\frac{1}{N^{2}} \sum_{i=1}^{n} K_{i} \sigma_{i}^{2}\right)=\sum_{i=1}^{n} \mathbb{E}\left(\frac{n}{N} w_{i} \sigma_{i}^{2}\right)=\frac{1}{\mathbb{E} K_{i}}\left(\sum_{i=1}^{n} w_{i}\right) \mathbb{E} \sigma_{i}^{2}=\frac{\mathbb{E} \sigma_{i}^{2}}{\mathbb{E} K_{i}} \quad ...(8)$$

- where the second equality is by bounded convergence theorem(since $N / n \rightarrow \mathbb{E} K_{i}$ and $\sum w_{i} \sigma_{i}^{2}$ bounded $)$ and the last equation is from $\sum w_{i}=1$. Since $\left(\mu_{i}, \sigma_{i}^{2}\right)$ are i.i.d.,

$$\begin{aligned}
&n \mathbb{V} \operatorname{ar}\left(\sum_{i=1}^{n} w_{i} \mu_{i}\right)=n \mathbb{E}\left(\mathbb{V} a r\left(\sum_{i=1}^{n} w_{i} \mu_{i} \mid w_{1}, \ldots, w_{n}\right)\right)+n \mathbb{V} \operatorname{ar}\left(\mathbb{E}\left(\sum_{i=1}^{n} w_{i} \mu_{i} \mid w_{1}, \ldots, w_{n}\right)\right)\quad ...(9) \\ 
&=n \mathbb{E}\left(\sum_{i=1}^{n} w_{i}^{2} \mathbb{V} \operatorname{ar}\left(\mu_{i}\right)\right)+n \mathbb{V} \operatorname{ar}\left(\left(\sum_{i=1}^{n} w_{i}\right) \mathbb{E} \mu_{i}\right)=n \mathbb{E}\left(\sum_{i=1}^{n} w_{i}^{2}\right) \mathbb{V} \operatorname{ar}\left(\mu_{i}\right) \quad ...(10)
\end{aligned}$$

- where the last equality is from the fact that the second term is 0 . By simple algebra, $n \sum_{i=1}^{n} w_{i}^{2}=\frac{\overline{K_{i}^{2}}}{\overline{K_{i}} \times \overline{K_{i}}}$, where $\overline{K_{i}^{2}}$ and $\overline{K_{i}}$ are sample mean of $K_{i}^{2}$ and $K_{i}$, respectively. By strong law of large number, $\overline{K_{i}^{2}} \rightarrow \mathbb{E} K_{i}^{2}$ a.s., $\overline{K_{i}} \rightarrow \mathbb{E} K_{i}$ a.s., therefore $n \sum_{i=1}^{n} w_{i}^{2} \rightarrow \frac{\mathbb{E} K_{i}^{2}}{\left(\mathbb{E} K_{i}\right)^{2}}$ a.s. Combine this result with (8) and (10), we've proved (4). We now turn to the limit of $\widehat{\sigma_{n}^{2}}$.

$$\begin{aligned}
\widehat{\sigma_{n}^{2}} &=n \frac{1}{N^{2}}\left(\sum_{i=1}^{n} \sum_{j=1}^{K_{i}}\left(X_{i, j}-\bar{X}\right)^{2}\right)=\frac{n}{N^{2}}\left\{\sum_{i=1}^{n} \sum_{j=1}^{K_{i}} X_{i, j}^{2}-N \bar{X}^{2}\right\} \\
& \rightarrow \lim _{n \rightarrow \infty}\left(\frac{n^{2}}{N^{2}}\right) \mathbb{E}\left(\sum_{j=1}^{K_{i}} X_{i, j}^{2}\right)-\lim _{n \rightarrow \infty}\left(\frac{n}{N}\right)\left(\mathbb{E} \mu_{i}\right)^{2}
\end{aligned}$$

- The last limit is from $(1 / n) \sum_{j=1}^{K_{i}} X_{i, j}^{2} \rightarrow \mathbb{E}\left(\sum_{j=1}^{K_{i}} X_{i, j}^{2}\right)$ and $\bar{X} \rightarrow \mathbb{E} \mu_{i}$ a.s., both by the strong law of large number. By $N / n \rightarrow \mathbb{E} K_{i}$, and also $\mathbb{E}\left(\sum_{j=1}^{K_{i}} X_{i, j}^{2}\right)=$ $\mathbb{E} K_{i} \mathbb{E} X_{i, j}^{2}=\mathbb{E} K_{i}\left(\mathbb{E} \mu_{i}^{2}+\mathbb{E} \sigma_{i}^{2}\right),(6)$ follows.

> ## Note

- (4) in Theorem 1 shows the variance of a page level metrics can be decomposed into two parts. 
- The first part $C \mathbb{V} a r \mu_{i}$ is contributed by user effect $\left(\mu_{i}, \sigma_{i}^{2}\right) .$ We call this between user variance. 
- The second part $\mathbb{E}\left(\sigma_{i}^{2}\right) / \mathbb{E}\left(K_{i}\right)$ represents the variance not explained by user effect and we might call this within user variance. 
- When $\mathbb{E} K_{i}$ large, note that $C=\mathbb{E} K_{i}^{2} /\left(\mathbb{E} K_{i}\right)^{2} \geq 1$ by Jensen's inequality, the between user variance will dominate. 
  - This is intuitively easy to understand since within user variance decrease to 0 as each user has more and more page views.
- In empirical data, we do see between user variance contributed a large proportion of the total variance, especially for those experiments ran for a few weeks.
  - This observation motivated us to use page view as randomization unit for some experiments if the key metrics we are interested in are at page view level.
- A caveat here is that not all experiment can be done with page view level randomization, mainly due to the inconsistent user experience. We leave the discussion later in Section 5 and only focus on theoretical property in the next section.

$$\begin{aligned}n \mathbb{V a r} \bar{X} & \rightarrow C \mathbb{V} a r\left(\mu_{i}\right)+\mathbb{E}\left(\sigma_{i}^{2}\right) / \mathbb{E}\left(K_{i}\right) \quad ...(4) \\
\widehat{\sigma_{d}^{2}} & \rightarrow C \mathbb{V} a r\left(\mu_{i}\right)+\mathbb{E}\left(\sigma_{i}^{2}\right) / \mathbb{E}\left(K_{i}\right) \quad ...(5) \\\widehat{\sigma_{n}^{2}} & \rightarrow \frac{1}{\mathbb{E}\left(K_{i}\right)}\left(\mathbb{V} \operatorname{ar}\left(\mu_{i}\right)+\mathbb{E}\left(\sigma_{i}^{2}\right)\right) \quad ...(6)\end{aligned}$$

> 뒤의 내용은 일단... 생략..

---

**reference**

- https://alexdeng.github.io/public/files/jsm2011-deng.pdf

