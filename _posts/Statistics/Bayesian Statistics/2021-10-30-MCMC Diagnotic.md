---
title:  "MCMC Diagnotic"
excerpt: "MCMC 의 Convergence 를 진단하는방법"
categories:
  - Bayes
last_modified_at: 2021-10-27
date : 2021-10-30 11:00:00 +0900

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 MCMC DIagnotic 하는 방법에 대해서 알아봅시다.
{: .notice--warning}

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## Problem

![png](/assets/images/Stat/89_1.png)

- 위와 같이 Multimodal (Normal) 의 분포가 있다고 합시다. 
- 이를 Gibs sampler 를 이용하여 한번 Sampling 해 봅시다. 

![png](/assets/images/Stat/89_2.png)

- 위와 같이 Gibs sampling 을 했음에도 실제 분포(실선) 를 잘 Approximation 하지 못하고 있는것을 볼 수 있습니다. 
- 왜 이러한 일이 일어났을까요? 

> 우리의 Simulated Markov chain 이 Stationary Distrinution 에 converge 되었나? 

- $$p_{ij} \to \pi_{ij}$$ 가 잘 되었는지 ? (제일 중요함..)

> 얼마나 많은 iteration 이 필요할까? 

- 즉 잘 수렴했을떄에도 얼마나 많은 Sample 이 필요한지가 필요합니다.

> 하나의 체인 말고 여러개를 돌려야 한다면 몇개를 돌려야 할까? 

- 평균적으로 MCMC 를 수행할때에는 여러개의 체인을 돌립니다.
- 하지만 이때에 몇개를 돌려야 할까요? 

> Burned - in 이 언제 잘 되었는지 ? 

- Marcov chain 이 parameter space 를 잘 훑었을때에 Burn in 이 잘 되었다고 할 수 있을것입니다.
- 또한 Start 지점에 의해 초반에는 어느정도 영향이 있기떄문에 이를 없애기 위해서는 처음 몇개의 샘플을 버려야 할까요 ? 

> 샘플이 얼마나 Correlated  하고 있는지 ?

- Markov Chain 이라 전 샘플의 영향을 받을수밖에 없습니다. 
- 그러므로 Correlated Sample 이고 이러한 것들이 영향을 끼칠 수 있습니다.

> 시작점 (initial point) 이 효과적일지? 

- 저희가 MCMC 를 적용할떄에 시작점을 정하고 시작할텐데, 이게 과연 정말 효과적인 Start 인지에 대해서 의문이 있을 수 있습니다. 

> 더 효과적인 algorithm 이 있을지?

- MH, Gibs , 등등 다양한 방법론을 사용할 수 있을것입니다. 

> ## So many Problem...

- 위와 같이 고려할점이 되게 많은데... 이걸 어떻게 판단해야하는 기준이 명확한게 있을까요? 
- 우리의 MCMC 방법론은 분명히 Limiting distribution 으로 가게 된다면 우리가 원하는 분포로 수렴하게됩니다만,, '내가 돌리고 있는 MCMC 가 진짜 분포로 잘 근사되고 있는지?' 는 애초에 하느님밖에 모르는 것입니다.
- 그러므로 수렴이 되었는지 Chain 에서 적당히 살펴보고 가늠할 뿐입니다.
  - 대충 수렴한것 같으면 Chain 의 수 (m) , 얼마나 많은 샘플을 돌려야 할지(n) 가 뭐든간에 그냥 신경 쓰고 결과를 받아들인다고 합니다.

![png](/assets/images/Stat/89_6.png)

-  <http://www.robots.ox.ac.uk/~fwood/teaching/C19_hilary_2015_2016/mcmc.pdf>

# [Representative (Convergence)](#link){: .btn .btn--primary}{: .align-center}

> ## Trace plot

- 잘 수렴하는지를 그림을 통해서 알아보는 방법입니다. 

> Trace plot 

- 가장 쉽고 직관적인 방법입니다. 
- iteration 마다 어떤 값을 나타내는지 그려보는것을 Trace plot 이라고 합니다. (추적하는것)
- trace plot 은 한곳에 고여있으면 안될것입니다. (여러곳을 훑어야 함)
- Burn in period 를 제거해야 합니다 .
  - 모든 Parameter space 를 훑어야 하므로, 그래프의 앞쪽을 보통 짜르게 됩니다. 

> Standard error of mean (Naive Standard Error) 

- 보조적인 지표로서, MCMC 를 하면 Posterior 분포의 평균에 대한 SE 를 계산하게 됩니다.
  - SImulation 의 error of mean 을 캐치합니다.
  - 하지만 parameter 자체의 uncertainty 는 체크하지 않습니다. 
- 즉 그냥 '샘플링의 평균' 만 어떻게 변하는지 체크하는 것입니다.

$$\frac{posterior \ standard \ deviation}{\sqrt{n}} $$

- 위에서 n 은 몇번 iteration 했는지를 나타냅니다. (사실 중요한 DIagnotic 기준은 아님)

> Example

![png](/assets/images/Stat/89_3.png)

- 우리가 이전에 살펴본 예시에 대해서 Trace plot 을 그려본 것입니다. 
  - 원래는 축을 왔다갔다 하면서 분포를 계속 그려야 하는데, 지금은 한곳에만 몰려있는듯 보입니다. 
  - 그러므로 이전의 Posterior 가 왜곡된것을 알 수 있습니다. (좀 더 Sampling 을 해야한다는것을 알 수 있습니다.)

![png](/assets/images/Stat/89_4.png)

- 그래서 위처럼 더욱 더 Sampling 을 해보니 잘 왔다갔다 한것을 볼 수 있습니다.
  - 그리고 Naive SE 도 줄어든것을 볼 수 있습니다. 

> ## Brooks Gelman-Rubin Statistics (BGR)

- 이것 역시 MCMC 가 얼마나 잘 수렴했는지를 나타내는 지표입니다.
- 여러 체인이 있을텐데, 체인간의 분산과 체인 내의 분산을 비교하는 값입니다. idea 는 다음과 같습니다. 
  - '모든 MC chain 이 어느정도 수렴하여 대표성을 지닌다면! 체인 내의 분산과 체인간의 '

> Calclation

1.먼저 M 개의 chain 을 생성하고, 각각의 Chain 은 2*N 개의 iteration 을 형성합니다. 

2.처음 N 개의 draws(Sample) 을 버립니다. 

3.체인 내의 Variation 과 체인간의 Variation 을 계산합니다 .

$$W = \frac{1}{M} \sum_{j=1}^Ms_j ^ 2 \text{ (s_j 는 Step 2 에서 각 체인의 분산)}) $$

$$B = \frac{N}{M-1}\sum_{j=1}^M({\bar{\theta_j} - \bar{\theta}}) \text{  (bar_theta 는 M개 체인 평균의 평균)}$$

 4.이제 각각을 이용하여 $\theta$ 에 대한 분산의 추정치를 구합니다.

$$\hat{Var(\theta)} = (1-\frac{1}{N})W + \frac{1}{N}B$$

- 이떄 위의 추정치는 Unbiased 입니다. 
  - $E(W) = E(B) = E(s^2_j) = \sigma^2$
  - $E(\hat{var(\theta)}) = E((1-\frac{1}{N})W + \frac{1}{N}B) = \sigma^2$
- 하지만 이 경우에 N 이 엄청 커지지 않는 이상... B 라는 녀석 떄문에 overestimate 된다.
  - Chain 들은 initial point 가 달라져서 다른 값을 가지는 경우까지 Variation 에 고려가 되므로 B 는 일반적인 공식보다 커지기 떄문입니다.
- W 라는 애들은 체인 안의 값들의 분산을 나타냅니다.
  - 이 값은 '같은' initial 에서 출발한 샘플들의 분산입니다. 즉 ! 전체의 분산보다 좀 더 작은 값을 나타낼 것입니다. 

5.Calculate the Potential scale reduction factor

$$\hat{R} = \sqrt{\hat{var(\theta)}/W}$$

- 분자는 분산을 더 Overestimate 하게 됩니다.
- 분모는 분산을 좀 더 Underestimate 하게 됩니다. 
- N 이 작을떄에는, B 때문에 $\hat{R}$ 은 1보다 큰 값을 가지게 됩니다. 
- 하지만 N 이 점점 커짐에 따라서 W 의 값만 남게 되고 , 이는 점점 1로 수렴하게 됩니다. 
  - 즉 1로 가까워지면 좋은것입니다. 
- 즉 $\hat{R}$ 이 크다면 (일반적으로 1.2) 우리는 convergence 를 좀 더 개선하기 위하여 많은 iteration 이 필요하다고 할 수 있습니다.

# [Accuracy](#link){: .btn .btn--primary}{: .align-center}

- MC Chain 의 통량이 정확하기 위해서, Sample 수가 충분히 많을까? 에 대한 Measure

> ## Autocorrelation

- MCMC 샘플들은 어쩔수 없이 Correlation 되어있습니다. 
  - 그 전에게 직접적으로 영향을 받기 떄문입니다.
- IID sample 과 비교해서는, 이 샘플은 얼마나 유용할까? 와 같은 것을 보고싶습니다.
  - 서로 연관이 엄청 되어있으면 당연히 IID 와 거리가 멀것이므로 많은 Sample 이 필요하다고 볼 수 있습니다.

> Autocorrelation Function (ACF)

$$acf(\theta) = \frac{\sum _{i=1}^{n-k}(\theta_i-\bar{\theta})(\theta_{i+k} - \bar{\theta})}{\sum_{i=1^n}(\theta_i - \bar{\theta})^2}$$

- 위와 같이 ACF 는 이전 Step 의 값과 현재 Step 이 얼마나 Correlation 되어있는지를 측정하는 값입니다. 
  - 이 경우에 당연하게도 k 가 커질수록 작은 값을 가지게 됩니다. 
- k 커졌음에도 ACF 가 크다면, 이는 크게 Correlation 되어있다는것을 나타냅니다.

![png](/assets/images/Stat/89_5.png)

- 이전의 예시에 대해서 ACF 를 그려본 것입니다. 
  - Correlation 이 매우 완만하게 줄고있습니다. 자기들끼리 50개까지도 매우 연관이 있는것입니다. 
  - lag 를 400개 까지는 봐야 그 이후에 자기상관이 없어진다고 생각할 수 있을것입니다.

> ## Effective Sample Size (ESS) 

- 위를 토대로, 이렇게 Correlated 될수밖에 없는 샘플들인데.. 얼마만큼의 샘플을 뽑아야 independent 한 샘플과 정보량이 동일해질까! 와 같은 정보가 궁금해질 수 있습니다.

> Lemma

$$lim_{N\to\infty} MNvar(\bar{\bar{\theta}}) = (1+2\sum_{k=1}^\infty acf_k)var(\theta)$$

- 위에서 $\sum_{-\infty}^{\infty} acf_k$ = $(1+2\sum_{k=1}^\infty acf_k)$

> Calculation

- 이때에 ESS 는 어떻게 계산하게 될까요? iid 하다고 할 때에, Sample mean 에 대한 variance 는 $\lambda/n$ 이라고 합시다.  
- MCMC 의 chain 에 대하여 구성된 샘플에 대해서 sample mean 에 대한 variance 는 $var(\bar{\bar\theta})/n_{eff}$ 이 될 것입니다. 
- 그렇다면 sample 이 완전히 iid 하다면 $var(\bar{\bar{\theta}})=var(\theta)/NM$ 이라 할 수 있을것입니다.
- 하지만 지금 iid 하지가 않으므로 ,  $var(\bar{\bar{\theta}})=var(\theta)/n_{eff}$ 라 할 수 있고, 이는 정리하면 $n_{eff} = \frac{MN}{1+2\sum_{k=1} ^\infty acf_k}$

> Estimation

- iid 일때에 상정되는 샘플 수를 $n_{eff}$ 라고 한다면 아래와 같은 공식이 성립합니다.

$n_{eff} = \frac{MN}{1+2\sum_{k=1} ^\infty acf_k} \approx \frac{MN}{1+2\sum_{k=1} ^T acf_k }$

- 이때 T 는 acf 를 그렸을때 0에 가까워지는 지점의 T을 정한 뒤에, 이 값으로 근사하게 됩니다. (정확하게 구할수는 없으므로...)

> thinning ? 

- Thinning (모든 샘플을 다 사용하는게 아니라, thining 이 2 라면 2,4,6,8.... 번째 샘플을 사용하는 것입니다.)
- 하지만 이러한 Thining 은 크게 도움이 되지 않는다고 합니다.
  - 어짜피 정보를 버리는것이기 떄문에.... 

> ## Raftery and Lewis diagsnotic

- 믿을만한 posterior intervals 를 만들기 위하여 필요한 sample size 

$$n_{min} = (\Phi^{-1}(\frac{s+1}{2})\frac{ \sqrt{q(1-q) }}{r})^2$$

- 이 상황은 $P(\theta \in [q-r ,q+r]) =S $ 가 되게 하기 위한 최소한의 샘플 사이즈를 계산한 것입니다.

> ## Geweke Diagnotic

- 이 경우는 posterior Sampling trace (Markov Chain) 을 두가지 파트로 나눕니다.
  - 이떄에는 주로 앞 부분의 10% / 뒷부분의 50% 로 나누게 됩니다. 
- 이 두개 파트에 대해서 mean 을 비교합니다. 
  - Two sample Z Test 를 실시합니다.
- Two sample test 의 평균이 같다면? -> 10% 을 상한선으로 Burn in 이 가능하겠구나! 
- Two sample test 의 평균이 다르다면? -> 10% 이상을 Burn in 으로 써야겠네...

> ## Heidelberg and Welch Diagnotics 

- 우리의 Chain 이 stationary distribution 와 같은지를 검사하는 것입니다. 
- 이 역시 처음(10%) 과 마지막(50%) 을 비교함으로서 

1. Generate a chain of N iterations and define an α level. 
2. Calculate the test statistic on the whole chain. Accept or reject null hypothesis that the chain is from a stationary distribution. 
3. If null hypothesis is rejected, discard the first 10% of the chain. Calculate the test statistic and accept or reject null. 
4. If null hypothesis is rejected, discard the next 10% and calculate the test statistic. 5. Repeat until null hypothesis is accepted or 50% of the chain is discarded. If test still rejects null hypothesis, then the chain fails the test and needs to be run longer

# [Efficiency](#link){: .btn .btn--primary}{: .align-center}

- 대부분의 MC 의 경우 Sample 간 자기상관 떄문에 만족할 만한 ESS 와 MCSE 를 얻기 위해서는 엄청나게 긴 체인을 만들어야 합니다. 
- 이 경우에 좋은 Sampler 가 좋은게 많이 발명되고 있으므로, 이쪽을 보는것도 좋을것 같다.

# [More...](#link){: .btn .btn--primary}{: .align-center}

> ## More

- 사실 MCMC 가 수렴을 잘했냐 안했냐는.... 죽어도 모릅니다.
  - 왜냐하면.. 당연하 True Distribution 을 모르니까
- 기껏해야 보는건 Trace plot 정도 보는거임..
  - 이게 이상하면 바로 딱! 보임 대부분은 그냥 Trace plot 정도 딱 보는것 같음.... 
  - 굳이 Diagnotic 을 바로 하는것 같지는 않고, Trace plot 이 이상해보이면 그때 Diagnotic 을 해보는것 같습니다.

> ## Thinning 

- Thinning 은 Mcmc 특성상 자기상관이 되어있어 몇번쨰 변수를 건너 뛰면서 선택하는 방법입니다.
  - 2 로 설정하면 2,4,6,8....
- 하지만 이와 같이 설정하는것은 크게 의미 없다고 합니다. 

"But the thinned chain also has less information than the original chain, and estimates from a thinned chain are (on average) less stable and accurate than from the original chai (Link & Eaton, 2012) "
{: .notice}

- 사실 Thinning 이라는게 어짜피 샘플의 정보량을 버리는거이기도 해서, 저장 용량이 부족한게 아니면 Thinning 은 별 의미가 없다고 합시다. 

- [On thinning of chains in MCMC - Link - 2012 - Methods in Ecology and Evolution - Wiley Online Library](https://besjournals.onlinelibrary.wiley.com/doi/10.1111/j.2041-210X.2011.00131.x)

> ## many Chain? 

- 하나의 긴 체인을 돌려도 수렴을 잘 못하는 것 같으면 대신 출발 지점을 여러 개로 해서 여러 체인을 돌려 그 체인들을 합쳐야 한다는 의견이 있다. 
- 하지만 이 의견을 까는 사람도 있는데, “하나의 긴 체인에서 답이 안 나오면 여러 개의 짧은 체인을 돌리는 것도 부질없다"라고 한다
- http://users.stat.umn.edu/~geyer/mcmc/one.html

---

**reference**

- <https://www.youtube.com/watch?v=THx1ka9KWog>
- <https://hun-learning94.github.io/posts/bayesian-ml/week3/02-mcmc-approximation-for-bayesian-posterior/>
- <http://patricklam.org/teaching/convergence_print.pdf>
- <https://www.statlect.com/fundamentals-of-statistics/Markov-Chain-Monte-Carlo-diagnostics>

MCMC 에는 엄청 다양한 방법 및 Diagnotic 이 존재하는데요, Analytic 하게 계산되는게 아니라 어쩔 수 없는것 같기는 합니다! 
{: .notice--success}

