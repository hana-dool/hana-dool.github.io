---
title:  "4.Normal models"
excerpt: "정규분포 모델"
categories:
  - Bayes
tags:
  - 1
last_modified_at: 2021-03-10

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# <center><font size="20"> Normal with known variance</font></center>

**likelihood** :  $y\mid \mu$ $\sim$ $N(\mu , \sigma ^2)$ 

**prior** : $\mu \sim N(\mu_0 , \tau^2_0)$ 이라 하자.  그렇다면 

$P(\mu) = \frac{1}{\sqrt{2\pi\tau_0 ^2}}\exp(-\frac{1}{2\sigma^2}(\mu - \mu_0)^2)$  이 된다. 

$P(y_1....y_n \mid \mu) = \prod_{i=1}^n \frac{1}{\sqrt{2\pi\sigma ^2}} \exp(-\frac{1}{2\sigma^2}(y_i - \mu)^2 )$

**posterior** : $p(\mu \mid y ) \propto \exp(-\frac{1}{2\tau_0 ^2}(\mu - \mu_0)^2 - \frac{1}{2\sigma^2}\sum(y_i - \mu)^2)$ ..... 계속 계산하다보면 

$\propto \exp(-\frac{1}{2\tau_n}(\mu - \mu_n)^2)$ 의 꼴이 나오게 된다. 이 때에 

$\mu_n =\{ \frac{1}{\tau_0^2}/{(\frac{1}{\tau_0^2}}+\frac{n}{\sigma^2}) \} \mu_0 + \{ \frac{n}{\sigma^2}/{(\frac{1}{\tau_0^2}}+\frac{n}{\sigma^2}) \} \bar{y}$  가 되고 , $\tau_n ^2 = \frac{1}{\frac{1}{\tau_0 ^2} + \frac{n}{\sigma^2}}$ 가 된다.  정리하면

$\mu \mid y \sim N(\{ \frac{1}{\tau_0^2}/{(\frac{1}{\tau_0^2}}+\frac{n}{\sigma^2}) \} \mu_0 + \{ \frac{n}{\sigma^2}/{(\frac{1}{\tau_0^2}}+\frac{n}{\sigma^2}) \} \bar{y} \ \ , \ \  \frac{1}{\frac{1}{\tau_0 ^2} + \frac{n}{\sigma^2}}) $ 

이는 해석을 다음과 같이 해볼 수 있다. precision 을 variance 의 역수라 하자. (이 때에 variance 의 역수가 정확성이므로, 정확성이 크다는것은 분산이적다(퍼짐이적다) 가 된다. ) 그렇다면

 $\frac{1}{\tau_0}$ 은 prior 의 precision 이 된다. 

 $\frac{n}{\sigma^2}$ 는 data 의 precision 이 된다. 

posterior 의 precision 은 $\frac{1}{\tau^2}+\frac{n}{\sigma^2}$ 으로, prior 와 데이터의 정확성이 더해져 업데이트되고있다.

그리고 posterior 의 mean 은 precision 의 비율만큼 가중평균되어 업데이트되고있다.

**interpret** : prior 은 sample mean 이 $\mu_0$ 이고, precision 이 $\frac{1}{\tau^2}$ 인 데이터라고 해석할 수 있다.

## Prediction

둘다 Normal 일 경우에 쓸 수 있는 좋은 성질이 있다. 우선 prediction 이 어떻게 이루어지는지 살펴보자.

$p(\tilde{y} \mid y ) $

$= \int p(\tilde{y},\theta \mid y) d\theta $

$= \int p(\tilde{y} \mid \theta, y )p(\theta \mid y)$ # 이때 모수가 주어지면, 어짜피 과거값은 의미가 없으므로

$= \int p(\tilde{y}\mid\theta)p(\theta \mid y) d\theta$

위와 같은 형태로 prediction 이 이루어진다.  이를 이용한다면 

$p(\tilde{y} \mid y)$

= $\int p(\tilde{y}\mid \mu) p(\mu \mid y)d\mu $

= $\int \exp(-\frac{1}{2\sigma^2}(\tilde{y}-\mu)^2)\exp(-\frac{1}{2\tau_n^2}(\mu-\mu_n)^2)d\mu$ 가 된다. 이는 pdf 가 $\tilde{y}$ 의 exponential 2차항 꼴임을 알 수 있다.  그러므로 Normal distribution 이다. Normal 의 모수는 평균과 분산이므로 , 이를 구한다면 우리는 그 분포를 알 수 있게된다. 

<br>

 $E[\tilde{y} \mid y]$

$ = E[E[\tilde{y}\mid \mu] \mid y]$ =  # (law of iteration 의 일반적인 모양. see wiki). $\mu$ 가 주어지면 당연히 $\tilde{y}$ 의 평균은 모수가 주어졌으므로 $\mu$

$=E[\mu \mid y]$

$= \mu_n$

<br>

$Var(\tilde{y} \mid y)$

$= E[Var[\tilde{y} \mid \mu ] \mid y]$ + $Var[E[\tilde{y} \mid \mu] \mid y]$ 

$= E[\sigma^2 \mid y] + Var[\mu \mid y]$

$= \sigma^2 + \tau_n^2 $    # n 이 커지면 $\tau_n^2$ 이 0 으로 간다.

$>= \sigma^2$ 

<br> 즉 정리하자면 

 $\tilde{y} \mid y \sim$  $N(\mu_n,\sigma ^2 + \tau_n^2)$ 이 된다.



## Note

위 posterior 를 정확하게 유도하는 식을 사진으로 첨부한다.



# <center><font size="20"> Distributions </font></center>

이 이후에 넘어가기 전에 몇가지 분포들을 알아보고 가자.

![png](/assets/images/Bayes/4_1.PNG)

![png](/assets/images/Bayes/4_2.PNG)

![png](/assets/images/Bayes/4_3.PNG)

# <center><font size="20"> Normal with known mean</font></center>

사진첨부







# <center><font size="20"> Two parameter model</font></center>

대부분의 통계학은 대부분 모르는 모수를 2개 이상 가지고 있다. 앞에서 우리가 했던 1 parameter model 은 매우 이상적인 상황! 즉 여기서부터는 Two parameter model 에 대해서 알아보도록 하자.

베이즈 추론의 틀은 다음과 같이 3단계로 이루어져있다.

1) Likelihood 를 파악한다. 2) Prior 를 정의한다. 3) Poseterior 를 구한다.  

이때에 Conjugacy 에서 prior 와 posterior 가 같은 분포라는것은 이미 알고있으므로, Posterior 를 구할때에 $\theta$ 가 없는 부분은 그냥 상수취급할 수 있다. 

## How to get marginal distribution?

1. 첫번째 방법

    모든 모르는 모수에 대한 joint posterior 를 구한다. (정규분포일 경우 $P(\mu, \sigma^2 \mid y)$ 가 된다.) 그 이훼 관심이 없는 모수에 대하여 integral out 시킨다. $P(\mu \mid y) = \int P(\mu , \sigma^2 \mid y)d \sigma^2$ 

2. 두번째 방법

   Simulation 관점에서 얻을 수 있다. 우선 sample 을 joint posterior distribution 에서 뽑는다. 그리고 그 sample 에서 관심있는 모수만 보고, 관심없는 모수는 제외한다면 marginal distribution 을 얻을 수 있다.  즉 $(\mu , \sigma^2) ~ P(\mu , \sigma^2 \mid y) \to \text{ignore $\sigma^2$} \to \mu \sim P(\mu \mid y)$

왜 위에서 Marginal distribution 얘기가 나왔을까? 베이즈가 현실에서 잘 적용되지 않았던 이유는 분모의 적분이 어렵다는것이다. 이를 approximate 하게 얻는 방법이 MCMC(sampling)를 통해서 얻을 수 있다



## nuisance parameter

파라미터가 $\theta$ = ($\theta_1, \theta_2$) 와 같이 2개로 이루어져있다고 하자. 이 때에 우리는 $\theta_1$ 에만 관심이 있다고 하자. 그렇다면 관심없는 나머지변수 $\theta_2$ 를 nuisance 파라미터라고 한다. 이때에

 $P(\theta_1 \mid y)$

$= \int p(\theta_1 , \theta_2 \mid y) d\theta_2 $

$= \int P(\theta_1 \mid \theta_2 , y) P(\theta_2 \mid y )d\theta_2$

가 성립한다. 이는 multiparameter model 을 구성하고 계산하는데에 매우 중요한 공식이다. Posterior distribution 이 우리가 여태 했던 conjugate , 또는 손수 적분으로 구해지지 않는 경우가 있다. 그런 경우에는 marginal / conditional simulation 으로부터 계산될 수 있는데 그 simulation 은 아래와 같다.

$\theta_2 \sim (\theta_2 \mid y ) , \theta_1 \sim (\theta_1 \sim \theta_2,y)$ 으로 시뮬레이션을 한다면 $(\theta_1, \theta_2) \sim (\theta_1 , \theta_2 \mid y)$ 가 된다. 즉 이렇게 구한 $(\theta_1, \theta_2)$ 를 가지고 위의 적분을 근사적으로 수행할 수 있다. 



## prior 를 주는법

prior 를 주는법은 2가지가 있다.

1) parameter 각각에 prior 주기 

- $P(\mu, \sigma^2) = P(\mu)P(\sigma^2)$ # 즉 independent 하다고 가정한것임

2) joint prior 로 주기

- $P(\mu, \sigma^2) = P(\mu \mid \sigma^2)P(\sigma^2)$



# Normal with noninformative prior distribution

이 경우는 prior 를 independent 하다고 가정하여 준 방법이다. #(자세한 계산 과정은 책 참조, 여기에서는 그 결과를 최대한 서술한다.)

**Prior** 

$P(\mu , \sigma^2)$

$ = P(\mu)P(\sigma^2)$

$= 1 \cdot(\sigma^2)^{-1} $

$ \propto (\sigma^2)^{-1}$ 

이때 이게 왜 uniform 인지 궁금할 수 있는데, 각각 uniform 으로 주는 대상이 달랐던것이다.  $p(\log \sigma^2) \propto 1$  $\to$  $p(\sigma^2) \propto 1/\sigma^2$ 

**likeliood** 

$y \mid \mu , \sigma^2$ $\sim N(\mu, \sigma^2)$

$y \propto \sigma^{-n} \exp[-\frac{1}{2\sigma^2} \sum (y_i-\mu)^2]$

**posterior**

$p(\mu , \sigma^2 \mid y)$

$= p(\mu \mid \sigma^2 ,y ) p(\sigma^2 \mid y)$



# Normal with Conjuate prior

**prior**

이 방법은 prior 를 joint 로 주는 방법이다. 

# Multinomial