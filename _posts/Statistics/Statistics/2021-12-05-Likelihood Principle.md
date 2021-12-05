---
title:  "Likelihood Principle"
excerpt: "likelihood Principle 이란?" 
categories:
  - Stat
last_modified_at: 2021-12-05

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Likelihood Principle 에 대해서 알아보도록 합시다.
{: .notice--warning}

# [Likelihood Principle](#link){: .btn .btn--primary}{: .align-center}

> ## Intro

> Intro

- In statistics,the likelihood principle is a controversial principle of statistical inference which asserts that all of the information in a sample is contained in the likelihood function.
- consider a model which gives the [probability density function](https://psychology.fandom.com/wiki/Probability_density_function) of observable [random variable](https://psychology.fandom.com/wiki/Random_variable) *X* as a function of a parameter θ. Then for a specific value *x* of *X*, the function $$L(θ \mid x) = P(X=x \mid θ)$$ is a likelihood function of θ.
- Two likelihood functions are equivalent if one is a scalar multiple of the other; according to the likelihood principle, all information from the data relevant to inferences about the value of θ is found in the equivalence class.

> Note

- 즉  Likelihood 에서 parameter 의 모양만 같다면 그에대한 inference 도 같아야한다! 라는 Principle 입니다.

> ## Example

> Assumption

- $x$ is the number of successes in twelve independent Bernoulli trials with probability $\theta$ of success on each trial, and
- $Y$ is the number of independent Bernoulli trials needed to get three successes, again with probability $\theta$ of success on each trial

> Likelihood

- Then the observation that $X=3$ induces the likelihood function

$$L(\theta \mid X=3)=\left(\begin{array}{c}
12 \\
3
\end{array}\right) \theta^{3}(1-\theta)^{9}=220 \theta^{3}(1-\theta)^{9}$$

- and the observation that $Y=12$ induces the likelihood function

$$L(\theta \mid Y=12)=\left(\begin{array}{c}
11 \\
2
\end{array}\right) \theta^{3}(1-\theta)^{9}=55 \theta^{3}(1-\theta)^{9}$$

> Note

- 위 두개는 서로 scalar 가 곱해진 형태이므로 Likelihood Principle 에 의하면, 두개의 값중 어떤것을 가정하더라도, $\theta$ 에 대한 inference 는 같은 형태로 나타나야 합니다.
- 즉 위 예시에서 얻은 데이터는 동일 (12번중 앞면이 3번) 하지만 실험의 세팅이 다른 상황입니다. 이로 인해서 Liklihood 의 계수가 달라지고 있죠. 이떄 Likelihood Principle 는 실험 세팅이 다르더라도 , $\theta$ 에 대한 inference 는 같은 형태로 나타나야 함을 주장한다고 할 수 있습니다. 
- 즉 Likelihood Principle 은 가끔 다음과 같이 state 되곤 합니다.

The inference should depend only on the outcome of the experiment, and not on the design of the experiment.
{: .notice}

> ## The Law of Likelihood

- A related concept is the **law of likelihood**, the notion that the extent to which the evidence supports one parameter value or hypothesis against another is equal to the ratio of their likelihoods. That is,

$$\Lambda=\frac{L(a \mid X=x)}{L(b \mid X=x)}=\frac{P(X=x \mid a)}{P(X=x \mid b)}$$

- is the degree to which the observation $x$ supports parameter value or hypothesis $a$ against $b$. 
  - If ratio = 1 , the evidence is indifferent
  - if ratio > 1 , the evidence supports $a$ against $b$ 
  - if ratio < 1 , the evidence supports $b$ against $a$ 
- The use of Bayes factors can extend this by taking account of the complexity of different hypotheses.
- Combining the likelihood principle with the law of likelihood yields the consequence that the parameter value which maximizes the likelihood function is the value which is most strongly supported by the evidence. 
  - This is the basis for the widely-used [method of maximum likelihood](https://psychology.fandom.com/wiki/Maximum_likelihood).

> ## Historical remark

- The likelihood principle was first identified by that name in print in 1962 (Barnard et al., Birnbaum, and Savage et al.), but arguments for the same principle, unnamed, and the use of the principle in applications goes back to the works of [R.A. Fisher](https://psychology.fandom.com/wiki/Ronald_A._Fisher) in the [1920s](https://psychology.fandom.com/wiki/1920). 
- The law of likelihood was identified by that name by I. Hacking (1965). More recently the likelihood principle as a general principle of inference has been championed by A. W. F. Edwards. The likelihood principle has been applied to the [philosophy of science](https://psychology.fandom.com/wiki/Philosophy_of_science) by R. Royall.

- Birnbaum proved that the likelihood principle follows from two more primitive and seemingly reasonable principles, the conditionality principle and the sufficiency principle. 
  - The conditionality principle says that if an experiment is chosen by a random process independent of the states of nature $\theta$, then only the experiment actually performed is relevant to inferences about $\theta$. 
  - The sufficiency principle says that if $T(X)$ is a sufficient statistic for $\theta$, and if in two experiments with data $x_{1}$ and $x_{2}$ we have $T\left(x_{1}\right)=T\left(x_{2}\right)$, then the evidence about $\theta$ given by the two experiments is the same.

> ## Arguments for and Against the likelihood Principle

- The likelihood principle is not universally accepted.
- Some widely-used methods of conventional statistics, for example many [significance tests](https://psychology.fandom.com/wiki/Statistical_hypothesis_testing), are not consistent with the likelihood principle. 
  - Let us briefly consider some of the arguments for and against the likelihood principle.

> Expeimental design

- Unrealized events do play a role in some common statistical methods. 
  - For example, the result of a [significance test](https://psychology.fandom.com/wiki/Statistical_hypothesis_testing) depends on the probability of a result as extreme or more extreme than the observation, and that probability may depend on the design of the experiment. 
  - Thus, to the extent that such methods are accepted, the likelihood principle is denied.

> Example

- Some classical significance tests are not based on the likelihood. A commonly cited example is the optimal stopping problem. Suppose I tell you that I tossed a coin 12 times and in the process observed 3 heads. 
- You might make some inference about the probability of heads and whether the coin was fair. Suppose now I tell that I tossed the coin until I observed 3 heads, and I tossed it 12 times. Will you now make some different inference?
- The likelihood function is the same in both cases: it is proportional to

$$p^{3}(1-p)^{9}$$

- According to the likelihood principle, the inference should be the same in either case. Apparently paradoxical results of this kind are considered by some as arguments against the likelihood principle; for others it exemplifies its value and resolves the paradox.
- Suppose a number of scientists are assessing the probability of a certain outcome (which we shall call 'success') in experimental trials. 
  - Conventional wisdom suggests that if is there is no bias towards success or failure then the success probability would be one half. 
  - Adam, a scientist, conducted 12 trials and obtains 3 successes and 9 failures. Then he dropped dead.

> 12 번 던지기 (Bonomial)

- Bill, a colleague in the same lab, continued Adam's work and published Adam's results, along with a significance test. 
  - He tested the null hypothesis that *p*, the success probability, is equal to a half, versus *p* < 0.5. 
  - The probability of the observed result that out of 12 trials 3 or something fewer (i.e. more extreme) were successes, if *H*0 is true, is

$$\left(\left(\begin{array}{c}12 \\ 9\end{array}\right)+\left(\begin{array}{c}12 \\ 10\end{array}\right)+\left(\begin{array}{c}12 \\ 11\end{array}\right)+\left(\begin{array}{c}12 \\ 12\end{array}\right)\right)\left(\frac{1}{2}\right)^{12}$$

- which is 299/4096 = 7.3%. Thus the null hypothesis is not rejected at the 5% significance level.

> 세번 앞면이 나올떄까지 던지기

- Charlotte, another scientist, reads Bill's paper and writes a letter, saying that it is possible that Adam kept trying until he obtained 3 successes, in which case the probability of needing to conduct 12 or more experiments is given by

$$1-\left(\left(\begin{array}{c}10 \\ 2\end{array}\right)\left(\frac{1}{2}\right)^{11}+\left(\begin{array}{l}9 \\ 2\end{array}\right)\left(\frac{1}{2}\right)^{10}+\cdots+\left(\begin{array}{l}2 \\ 2\end{array}\right)\left(\frac{1}{2}\right)^{3}\right)$$

- which is 134/4096 = 3.27%. Now the result *is* statistically significant at the 5% level.
- To these scientists, whether a result is significant or not seems to depend on the original design of the experiment, not just the likelihood of the outcome.

> ## Bayesian arguments on the likelihood principle

- From a Bayesian point of view, the likelihood principle is a direct consequence of [Bayes' theorem](https://psychology.fandom.com/wiki/Bayes'_theorem). An observation *A* enters the formula,

$$P(B \mid A)=\frac{P(A \mid B) P(B)}{P(A)}=\frac{P(A \mid B) P(B)}{\sum_{B^{\prime}} P\left(A \mid B^{\prime}\right) P\left(B^{\prime}\right)}$$

- only through the likelihood function $P(A \mid B)$
- In general, observations come into play through the likelihood function, and only through the likelihood function; the information content of the data is entirely expressed by the likelihood function. 
- Furthermore, the likelihood principle implies that any event that did not happen has no effect on an inference, since if an unrealized event does affect an inference then there is some information not contained in the likelihood function.
-  Thus, Bayesians accept the likelihood principle and reject the use of frequentist significance tests. As one leading Bayesian, Harold Jeffreys, described the use of significance tests: "A hypothesis that may be true may be rejected because it has not predicted observable results that have not occurred."

> Note

- Bayesian analysis is not always consistent with the likelihood principle.
- Jeffreys suggested in 1961 a non-informative prior distribution based on a density proportional to $|(\theta)|^{-1 / 2}$ where $I(\theta)$ is the Fisher information matrix; this, known as the Jeffreys prior, can fail the likelihood principle as it may depend on the design of the experiment. 
- More dramatically, the use of the Box-Cox transformation may lead to a prior which is data dependent.

> Note

- 위에서 왜 Bayesian Inference 가 Likelihood principle 을 잘 만족하는지가 약간 자세히 안나온것 같은데요, 그 이유는 되게 심플합니다.
- 우선 Binomial 과 Beta 에서 Posterior 를 구하는 과정을 생각해봅시다. (어짜피 베이즈는 Posterior 구하는게 전부이므로 이 과정만 생각해봐도 충분합니다.)

$$\begin{aligned} p(\pi \mid y) & \propto p(y \mid \pi) p(\pi) \\ &=\operatorname{Binomial}(n, \pi) \times \operatorname{Beta}(\alpha, \beta) \\ &=\left(\begin{array}{l}n \\ y\end{array}\right) \pi^{y}(1-\pi)^{(n-y)} \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha) \Gamma(\beta)} \pi^{(\alpha-1)}(1-\pi)^{(\beta-1)} \\ & \propto \pi^{y}(1-\pi)^{(n-y)} \pi^{(\alpha-1)}(1-\pi)^{(\beta-1)} \\ p(\pi \mid y) & \propto \pi^{y+\alpha-1}(1-\pi)^{n-y+\beta-1} \end{aligned}$$

- 위와 같이 Posterior 를 구할때 에초에 '상수' 는 제외하고 구하게 됩니다. 
  - Likelihood Principle 이 성립하게 된다는것을 볼 수 있죠!

> ## Optional Stopping in clinical trials

- The fact that Bayesian and frequentist arguments differ on the subject of optional stopping has a major impact on the way that clinical trial data can be analysed. 
  - In frequentist setting there is a major difference between a design which is fixed and one which is sequential, i.e. consisting of a sequence of analyses. 
  - Bayesian statistics is inherently sequential and so there is no such distinction.
- In a clinical trial it is strictly not valid to conduct an unplanned interim analysis of the data by frequentist methods, whereas this is permissible by Bayesian methods. 
- Similarly, if funding is withdrawn part way through an experiment, and the analyst must work with incomplete data, this is a possible source of bias for classical methods but not for Bayesian methods, which do not depend on the intended design of the experiment. 
- Furthermore, as mentioned above, frequentist analysis is open to unscrupulous manipulation if the experimenter is allowed to choose the stopping point, whereas Bayesian methods are immune to such manipulation.

> Note

- 즉 Freq 의 경우 데이터 샘플링 Plan 까지 고려해야 해서 매우 복잡합니다. 또한 Stopping Point 를 잡을때에도 매우 조심스럽습니다. (Likelihood 가 원래 생각과 다르게 변형될까봐...) 
- 하지만 그에 비해 Bayesian 은 Likelihood Rule 을 따르기때문에 적용이 편하고 Stopping Point 도 임의로 잡을 수 있습니다!

---

**Reference**

- <https://www2.isye.gatech.edu/isyebayes/bank/handout2.pdf>
- <https://psychology.fandom.com/wiki/Likelihood_principle>
- <https://ocw.mit.edu/courses/mathematics/18-05-introduction-to-probability-and-statistics-spring-2014/readings/MIT18_05S14_Reading15a.pdf>







