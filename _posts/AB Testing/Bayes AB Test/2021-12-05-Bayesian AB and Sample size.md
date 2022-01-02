---
ntitle: "Bayesian AB and Sample Size"
excerpt: "베이즈 AB Test 에서 샘플 사이즈가 필요 없는가"
categories:
  - AB_Bayes
last_modified_at: 2021-12-05

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

Sample Size 가 필요 없...나? 
{: .notice--warning}

# [Bayesian A/B Sample Size](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

- 다양한 출처에서, Bayesian A/B Testing 의 경우 고정된 Sample Size 가 필요 없다고 합니다. 

> <https://vwo.com/tools/ab-test-sample-size-calculator/> : vwo 가이드

[VWO SmartStats](https://vwo.com/why-us/technology/bayesian-statistics/) relies on Bayesian inference which unlike a frequentist approach doesn’t need a minimum sample size. This allows you to run A/B tests on parts of your website or apps that might not get a lot of traffic to improve them. However, getting more traffic on your tests allows VWO to determine your conversion rates with more certainty allowing you to be more confident about your test results.
{: .notice}

> <https://mobiledevmemo.com/its-time-to-abandon-a-b-testing/>

Bayesian tests do not require fixed sample sizes to provide valid results. You can even evaluate the results repeatedly (which is considered almost a blasphemy with NHST) and the results will still hold
{: .notice}

- 이러한 맥락에서 왜 Bayesian A/B Testing 의 경우 Sample size 가 필요 없는지에 대해서 알아보도록 합시다.

> ## Bayesian Sample size 

> Power Analysis (Freq)

- Frequentist 에게 Sample size 를 계산하는것은 매우 중요한 일입니다. 
- 왜냐하면 애초에 '실험을 설계' 할때 Error 를 조절하면서 좋은 품질의 실험을 제공하는것을 목표로 삼는데, 이때 Type 1 , Type 2 Error 는 샘플사이즈에 대해 영향을 받게 되기 때문입니다.

> Power Analysis (Bayes)

- 통상적으로 Frequentist 에서 수행되는 Type 1 , Type 2 에러를 고려하면서 계산되는 Power Analysis 는 Bayes 에서 수행되지 않습니다.
  - 왜냐하면 Bayesian Context 에서 목표는 우리의 prior 를 잘 업데이트 하는것이 중심이기 때문입니다. !
  - 이러한 목표에서 본다면, 우리는 '샘플 사이즈가' 크게 필요 없습니다. 추정된 Posterior 가 어느정도 만족스러우면 그때 실험을 중지하면 그만입니다.
- 또한 베이즈는 Binary Decision (맞다 아니다) 에 집중하는게 아니라, degree of belief 를 업데이트하는 방법입니다. 
  - 그러므로 사실 위와 같이 샘플이 얼마나 필요해요? 는 '실험을 정확하게 하려면 얼마나 많은 샘플 수가 필요해요?' 가 됩니다. 
  - 이때 "실험을 정확하게" 하려고 한다는것은 결국 Binary Decision (차이가있음 / 차이가 없음) 을 얼마나 정확하게 하려는지를 물어본다는것이고, 이는 모든 모수를 R.V. 로 보는 Bayesian Framework 에서는 사실 적당한 질문이 아닌 것입니다.
- 하지만 샘플사이즈가 아예 필요 없다는것은 아닙니다. 극단적으로 Noninformative Prior 를 사용했고, 3개의 데이터만 조사했을때 이 Posterior 를 그대로 믿을수는 없을것입니다. 그러므로 아래와 같이 샘플 사이즈를 어느정도 짐작하는 방법이 있습니다.

> ## Prior Decision and Sample size

- 우리의 믿음(Prior) 과 조절하여 필요한 샘플사이즈를 조절할 수 있습니다. 
- 만일 Beta(10,40) 과 Beta(1000,4000) 로 Prior 를 설정했다고 합시다.
  - Beta(10,40) : 이 Prior 를 바꾸기 위해서는 적은 샘플로도 충분
  - Beta(1000,4000) : 이 Prior 를 바꾸기 위해서는 많은 샘플이 필요 
- 즉 사전에 믿음이 크면 (많은 과거데이터 + 전문가의 견해 등) 확신이 있는 Prior 를 설정하여 요구되는 Sample size 를 크게 할 수 있습니다.

> ## Simulation and Sample size

- 우리가 비록 베이즈 프레임워크를 쓰더라도 Decision Rule (실험의 승자를 정하는 프로세스) 이때 결국 Type 1 , Type 2 에러가 발생하게 됩니다.
- 사전에 Assumption 했던 Data generating process (데이터는 bernoulli 이다 or 데이터는 감마분포이다 등) 을 이용하여 시뮬레이션을 진행할 수 있고, 우리가 필요한 샘플 사이즈가 얼마인지 알아낼 수도 있습니다. 

Example : A,B 가 gamma 를 따른다고 가정하고, Bayesian A/B Testing 의 Decision Rule 을 Loss = 0.01 로 정했다고 합시다. 서로 다른 평균을 가지는 A 데이터와 B 데이터를 generating 한 이후에 우리의 decision rule 이 이러한 차이를 샘플 크기에 따라서 얼마나 잘 잡는지를 분석하여 필요한 샘플 수 를 어림짐작 할 수 있습니다.
{: .notice}

> ## Bayesian Power 

- https://www.rdatagen.net/post/2021-06-01-bayesian-power-analysis/
- $P(L O g(O R)<0)$ 이러한 값이 궁금하다고 합시다. $P(L O g(O R)<0)>0.95$ 를 승자로 선언하는 Decision Rule 로 정했다고 합시다.
- If we want to assess what kind of sample sizes we might want to target in study based on this relatively simple design (binary outcome, two-armed trial), we can conduct a Bayesian power analysis that has a somewhat different flavor from the more typical frequentist Bayesian that I typically do with simulation. There are a few resources I’ve found very useful here: this book by [Spiegelhalter et al](https://onlinelibrary.wiley.com/doi/book/10.1002/0470092602) and these two papers, one by [Wang & Gelfand](https://projecteuclid.org/journals/statistical-science/volume-17/issue-2/A-simulation-based-approach-to-Bayesian-sample-size-determination-for/10.1214/ss/1030550861.full) and another by [De Santis & Gubbiotti](https://www.mdpi.com/1660-4601/18/2/595)
- When I conduct a power analysis within a frequentist framework, I usually assume set of *fixed/known* effect sizes, and the hypothesis tests are centered around the frequentist p-value at a specified level of $\alpha$
- The Bayesian power analysis differs with respect to these two key elements
  - a distribution of effect sizes replaces the single fixed effect size to accommodate uncertainty, 
  - and the posterior distribution probability threshold (or another criteria such as the variance of the posterior distribution or the length of the 95% credible interval) 
  - replaces the frequentist hypothesis test.
- We have a prior distribution of effect sizes. De Santis and Gubbiotti suggest it is not necessary (and perhaps less desirable) to use the same prior used in the model fitting. That means you could use a skeptical (conservative) prior centered around 0,
  -  in the analysis, but use a prior for data generation that is consistent with a clinically meaningful effect size. In the example above the *analysis prior* was

$$\beta \sim t_{s t u d e n t}(d f=3, \mu=0, \sigma=5)$$

- and the *data generation prior* was

$$\beta \sim N(\mu=-1, \sigma=0.5)$$

- To conduct the Bayesian power analysis, I replicated the simulation and model fitting shown above 1000 times for each of seven different sample sizes ranging from 100 to 400. 

![jpg](/assets/images/Stat/120_1.jpg)

- The plots below show a sample of 20 posterior distributions taken from the 1000 generated for each of three sample sizes. As in the frequentist context, an increase in sample size appears to reduce the variance of the posterior distribution estimated in a Bayesian model. We can see visually that as the sample size increases, the distribution collapses towards the mean or median, which has a direct impact on how confident we are in drawing conclusions from the data; in this case, it is apparent that as sample size increases, the proportion of posterior distributions meet the 95% threshold increases.

![jpg](/assets/images/Stat/120_2.jpg)

- Here is a curve that summarizes the probability of a posterior distribution meeting the 95% threshold at each sample size level. At a size of 400, 80% of the posterior distributions (which are themselves based on data generated from varying effect sizes specified by the *data generation prior* and the *analysis prior*) would lead us to conclude that the trial is success.

> ## Other Simulation Example

- https://towardsdatascience.com/bayesian-ab-testing-part-iii-test-duration-f2305215009c

---

**reference**

- <https://mobiledevmemo.com/its-time-to-abandon-a-b-testing/>
- <https://stats.stackexchange.com/questions/110346/power-analysis-from-bayesian-point-of-view>
- <https://ocw.mit.edu/courses/mathematics/18-05-introduction-to-probability-and-statistics-spring-2014/readings/MIT18_05S14_Reading20.pdf>
- <https://www.rdatagen.net/post/2021-06-01-bayesian-power-analysis/>



