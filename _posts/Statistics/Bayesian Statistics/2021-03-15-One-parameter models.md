---
ㅋtitle:  "One-parameter models and Conjugacy"
excerpt: "1변수 모델과 Conjugacy"
categories:
  - Bayes
last_modified_at: 2021-09-26

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [One Parameter Model](#link){: .btn .btn--primary}{: .align-center}

> ## Binomial model 

- 사람 $n$ = 129 명에 대해 행복한지 아닌지를 조사한다고 하자.

$$Y_i =  \begin{cases} 1 \ \ \text{참가자 i 가 행복하다고 답함} \newline 0 \ \ \text{o.w.} \end{cases}$$

- **justification**
  - 이 때에 $\theta$ 를 각각의 개인이 행복할 확률 이라고 하자. $Y_1...Y_n \mid \theta$ 는 iid 라고 생각할 수 있으며 또한 전체 모집단 N  은 매우 크므로 (사람은 70억..) repeatable 하다고 생각할 수 있다. 
  - 즉 de Finetti thm 에 의해서 우리의 model 은 $p(y_1...y_n) = \int\prod p(y_i \mid \theta)p(\theta)d\theta$ 로  생각할 수 있게된다. 

- **Likelihood**
  - Likelohood 는 위의 justification 과, Binary model 로 보려하므로 $p(y_1..y_{129} \mid \theta) = \theta ^{\sum{y_i}} (1-\theta)^{129-\sum y_i}$ 으로 생각할 수 있다. 

- **prior**
  - parameter $\theta$는 0~1 사이의 미지의 값이다. 아직 아무런 정보가 없다고 하자. 
  - 그럴떄에 Uniform 을 줌으로서, $\theta$ 에 대한 나의 객관성을 어느정도 유지할 수 있다. 이러면 Data 의 영향이 커질것이다. 즉 $p(\theta)=1$ for all $\theta \in [0.1]$ 

- **posterior**

$$p(\theta \mid y_1, …, y_{129}) \\= \frac{y_1, …, y_{129})p(\theta)}{p(y_1, …, y_{129})} \text{(Note : p($\theta$)=1)  }\\= p(y_1, …, y_{129}\mid\theta) \times \frac{1}{p(y_1, …, y_{129})} \text{ (분모는 $\theta$ 와 상관없다.)}\\ \propto p(y_1, …, y_{129}\mid\theta)$$

- 위의 과정을 통해서 구할 수 있다. 위 과정을 정리하면 아래 그림과 같아진다.

![png](/assets/images/Bayes/3_1.PNG)

- 이때 위 과정에서 Normalizing constant 를 직접 계산하지 않았는데, 그 이유는 r.v. 의 모양이 이미 우리가 잘 알고있는 beta distribution 의 모양이였기 떄문에 굳이 normal constant를 구할 필요가 없었기 때문이다.

> ## Conjugacy 

- A class $P$ of prior distribution for $\theta$ is called conjugate for a sampling model $p(y\mid \theta)$ if 

$$p(\theta) \in P \to p(\theta\mid y) \in P$$

- 즉 conjugacy 는 prior 의 class 와 posterior 의 class 가 일치하기때문에 계~속 업데이트를 하더라도 그 분포가 유지된다. 즉 Computational 적으로나 계산적으로나 이익이 된다! 

- **When?**
  - 언제 conjugate 가 잘 성립이 될까? exponential familiy 에 대해 아주 좋은 성질이 있다.

![png](/assets/images/Bayes/3_2.PNG)

> ## Data Information

![png](/assets/images/Bayes/3_4.PNG)

- Binomial 의 논의를 계속 이어가보자. posterior 을 얻고 난 이후, $E[\theta \mid y]$ 값은 그림과 같이 prior 에서의 $\theta$ 평균과, data 에서의 $\theta$ 평균(즉 data average) 의 가중평균과 같다. 
  - 이때 가중평균은 각각 a+b 와 n 에 비례한다. 즉 a와 b를 사전 데이터로 해석할 수 있을것이다. 
-  prior 를 데이터와 같이 해석하게 된다면 a 는 prior 에서 1의 갯수와 같아지고, b 는 0의 갯수, a+b 는 총 데이터의 갯수와 같아진다.
  - 그리고 만약 n >> a+b 라면 이는 데이터가 dominate 한 상황으로 그림의 맨 아래처럼 모든 예측이 거의 데이터에서의 예측과 같아진다. 
- 위와 같이 prior 를 데이터적인 접근으로 바라보게 된다면 훨씬 직관적으로 이해할 수 있다.

> ## Prediction

- 베이지안 추론의 중요한점은 새로운 observation 에 대한 예측 분포를 이용한다는 점이다. 
- 앞의 binomial 분포에서의 논의를 그대로 이어가자. $y_1....y_n$ 을 n 개의 binary random variable 이라고 하자. 그리고 $\tilde{Y}\in \{0,1\}$ 을 같은 모집단에서 나왔으며, 아직 관측되지 않은(즉 predict 하고자 하는) 데이터라고 하자. 
- prdictive distribution of $\tilde{Y}$ 는 $\tilde{Y} \mid Y_1=y_1 .... Y_n=y_n$  이 된다. 이를 구하면 다음과 같아진다. 

![png](/assets/images/Bayes/3_3.PNG)

이로부터 두가지 중요한 사실을 알 수 있다.

1. Predictive distribution 은 알려지지 않은 값에는 의존하지 않는다. 
2. Predictive distribution 은 observed data 에 의존한다. 

# [Confidence Regions](#link){: .btn .btn--primary}{: .align-center}

- 우리는 데이터 $y$ 를 얻고나면 parameter 의 실제값을(베이지안 입장에서 실제값이라고 하기에는 너무나 Frequentist 적이긴 하지만요..) 알고싶다. 
- 이를 위해서, 데이터 $Y = y$ 를 관측하고 난 이후 $l(y)< \theta < u(y)$ 를 크게 하는 interval $[l(y),u(y)]$ 를 construct 하여서, 이 interval 을 통해 true parameter $\theta$ 에 대한 추정을 하고싶다!

> ## Baysian Coverage

- 데이터 $Y = y$ 가 관측된 후  다음과 같은 경우에 interval $[l(y),u(y)]$ 은 95% Baysian Coverage for $\theta$ 라 한다. 

$$ Pr(l(y)<\theta <u(y) \mid Y=y) = 0.95$$

- 위 의미는 데이터 $y$ 가 '관측된 이후' random variable 인 $\theta$ 가 어디에 위치할지에 대한 확률이다. 즉 데이터는 constant 취급 / 모수는 r.v. 취급을 한다.

> ## **Frequentist Coverage**

- 데이터를 관측하기 전,  다음과 같은 경우에 Interval  $[l(y), u(y)]$ 은 95% Frequentist coverage for $\theta$ 라 한다. 

$$ Pr(l(y)<\theta <u(y) \mid \theta) = 0.95$$

- 위 의미는 데이터를 '관측하기 전' contant 인 $\theta$ 에 대해서, r.v. 인 데이터가 과연 $\theta$ 를 커버할지 하지 말지에 대한 확률이다. 

> ## **Frequentist Coverage의 단점**

- 데이터를 관찰하고 나서 Frequentist 의 Coverage 는 다음과 같이된다. 

$$Pr(l(y) < \theta < u(y)\mid\theta) = \begin{cases} 0 \ \ if \ \theta \notin [l(y), u(y)]\newline 1 \ \ if \ \theta \in [l(y), u(y)]\end{cases}$$

- 이는 Frequentist 의 post-experimental interpretation 이 얼마나 부족한지를 일깨워주는 부분이다.
- 데이터를 관측하고 나면 위의 Coverage 는 0 또는 1밖에 가지지 못한다. 
- 하지만 마냥 쓸모없는것은 아닌데, 만약 우리가 수 많은 unrelated experiment 를 시행하면서 95% Frequentist coverage 를 생성한다 하자. 
  - 그러면 95% 확률로 우리의 coverage 는 true parameter $\theta$ 를 포함한다고 말할 수 있다.

> ## **Frequentist 와 Bayesian coverage**

- Freq 일때와 bayes 일때의 CI 가 모두 같을 수 있을까? 
  - Hartigan(1966)은 95% Bayesian coverage 는 다음과 같은 property 추가적으로 가진다고 하였다.

$$Pr(l(Y) < \theta < u(Y)\mid \theta) = 0.95 + \epsilon_n \ \ (\mid\epsilon_n\mid < \frac{a}{n}, a = \text{for some constant})$$

- 즉 위에서 $Y$ 가 r.v. 으로 취급되고, $\theta$ 는 constant 로 취급되는 사실에 주목하자. 
  - 즉 최소한 assymptotic 하게라도(n을 늘리면 되므로) 95% Baysian coverage 는 95% Frequentist coverage 와 같아진다는 것이다. 
  - 이는 베이지안, non베이지안 모두 어짜피 sample 수가 많아지면 같은 CI로 근접함을 나타낸다. 

- For more discussion of the similarities between intervals constructed by Bayesian and non-Bayesian methods, see Severini (1991) and Sweeting (2001).

> ## **Quantile-based interval**

- interval 은 posterior quantile 을 이용해서 $100*(1-\alpha) \%$  의 CI 를 구성할 수 있다. 먼저 다음을 만족하는 $\theta_{a/2} < \theta_{1-a/2}$ 를 찾자.

1. $Pr(\theta<\theta_\alpha \mid Y= y) = \alpha/2$ 
2. $Pr(\theta>\theta_{1-a/2}\mid Y=y) = \alpha/2$ 

- 그렇게 된다면 $Pr(\theta \in [\theta_{\alpha/2},\theta_{1-\alpha/2}]\mid Y=y) = 1-\alpha$ 인 것은 쉽게 알 수 있다.

![png](/assets/images/Bayes/3_6.PNG)

> ## **HPD(Highes posterior density) region** 

- $100*(1-\alpha)\%$ HPD region consists of a subset of the parameter space, $s(y) \subset \Theta$ such that 

1. $Pr(\theta \in s(y) \mid Y=y) = 1-\alpha$ 
2. $\text{if $\theta_a \in s(y)$ and $\theta_b \notin s(y)$ then $p(\theta_a \mid Y=y)>p(\theta_b \mid Y=y)$} $

- 상당히 장황하게 써 놓았지만 사실은 아래 그림과 같이 높은 posterior 값을 가지는 $\theta$ 의 범위를 취한게 HPD 이다. 

![png](/assets/images/Bayes/3_5.PNG)

- 이떄 posterior 가 multipmodal 이면 interval 이 뚝뚝 끊기게 된다.  그리고 Quantile based interval 보다 무조건 그 길이가 짧을것이다. 

# [Conjugate Example](#link){: .btn .btn--primary}{: .align-center}

> ## Binomial model

- **Binomial**
  
  - $p(Y=x\mid \theta)$ = $\theta^x(1-\theta)^{1-\theta}$  $for \ \ x \in \{0,1\}$
  - $E[Y\mid \theta]$= $\theta$ , $V[Y \mid \theta]=\theta(1-\theta)$ 
  - 어떠한 사건의 발생 '빈도' 를 모델링할 때에 적합하다.
  
- **Likelihood :**  $Y_i \mid \theta \sim Ber(\theta)$

- **prior :** $\theta \sim Beta(a,b)$

- $\sum_i^n Y_i \mid\theta \sim Binom(n,\theta)$

- **posterior :**$\theta \mid D \sim beta(a+\sum y_i, b+n - \sum y_i)$
  
  - 이전에 증명하였으므로 생략
  
- **predict :**

  $p(\tilde{Y}=1\mid y_1, …, y_n)$   <br>

  $= \int Pr(\tilde{Y} = 1, \theta \mid y_1, …, y_n) d\theta$ <br>

  $= \int Pr(\tilde{Y} = 1\mid\theta, y_1,. ..,y_n)(\theta\mid y_1, …, y_n) d\theta$ <br>

  $= \int \theta p(\theta\mid y_1, …, y_n) d\theta $<br>

  $= E[\theta \mid y_1... y_n] = \frac{a+\sum y_i}{a+b+n}$ <br>

  - 즉 $\tilde{Y}\mid D \sim Ber(\frac{a+\sum_i ^ n y_i}{a+b+n} )$

- **information**

  - $E[\theta\mid y]$ = $\frac{a+\sum y_i}{b+n} = \frac{b}{b+n} \frac{a}{b} + \frac{n}{b+n} \frac{\sum y_i}{n} $
  - 위의 Expectation 값을 보았을 때, prior $Beta(a,b)$ 를 a+b개의 데이터 중 a의 성공, b의 실패가 있는 data 로 해석할 수 있다.
  - ![png](/assets/images/Bayes/3_7.PNG)
  - 위의 값을 보면 a가 클수록 오른쪽으로 쏠리며, a+b 가 클수록 첨도가 커지는것을 볼 수 있다.
  - n 이 크면 data 가 dominant 하여 $E[\theta\mid y]$ = $\bar{y}$ 인 것을 볼 수 있다.

> ## Poisson model

- **possion**
  
  - $p(Y=x\mid \theta) = \theta^x e^{-\theta} / x! \ \ for  \ \ x\in\{0,1,2...\} $
  
- $E[Y\mid \theta] = \theta$ , $V[Y\mid \theta] = \theta$
  
  - 어떠한 사건의 '발생 수' 를 modeling 할 때에 $poisson$ 분포를 쓰기 적절하다. 
  
- **Likelihood :** $Y_i \mid \theta \sim Poi(\theta)$

- **prior :** $\theta \sim \Gamma(a,b)$

- **posterior :** $\theta \mid D \sim \Gamma(\sum y_i +a , n+b)$
  
  - $p(y \mid \theta) = \prod e^{-\theta} \theta^{y_i}/y_i ! = e^{-n\theta}\theta^{\sum y_i}/\prod(y_i !)$
  - $p(\theta) = \frac{b^a}{\Gamma (a)} \theta^{a-1} e^{-\beta \lambda}$
  - $p(\theta \mid y) \propto  \theta ^ {\sum y_i + a -1} e^{-(n+b)\theta}$
  
- r.v. 인 $\theta$ 가 어떤 분포인지 살펴본다면 $p(\theta \mid y) \sim \Gamma (\sum y_i + a , n + b)$ 
  
- **information**

  - $E[\theta\mid y] = \frac{a+\sum y_i}{b+n}$ = $\frac{b}{b+n} \frac{a}{b} + \frac{n}{b+n} \frac{\sum y_i}{n}$
  - 위의 Expectation 값을 잘 보면 우리의 Prior 인 $\theta \sim \Gamma(a,b)$ 는 b interval 중 일어나는 사건의 수는 a 라고 해석할 수 있다.
  - ![png](/assets/images/Bayes/3_8.PNG)
  - 위 그림을 보게 되면 a 가 크면 오른쪽으로 치우치고 있음을 알 수 있다.  (발생수가 늘어남)
  - n 이 클 경우 $E[\theta\mid y]$ 는 $\bar{y}$ 가 되고, 이는 data 가 dominant 한 상황이 된다.  

- **predict**

  $p(\tilde{y}\mid y_1, …, y_n)$

   $= \int_0^{\infty} p(\tilde{y}\mid \theta, y_1, …, y_n)p(\theta\mid y_1, …, y_n) d\theta \ $

  $= \int p(\tilde{y}\mid \theta)p(\theta\mid y_1, …, y_n) d\theta \ \text{# $\theta$ 가 주어지면 데이터는 서로 독립}$

  $= \int pois(\tilde{y}\mid\theta)\Gamma(\theta\mid a+\Sigma y_i, b+n) d\theta$

  $= \int\{\frac{1}{\tilde{y}!} \theta^{\tilde{y}} e^{-\theta} \}\{( \frac{(b+n)^{a + \Sigma y_i}}{\Gamma(a+\Sigma y_i)} \theta^{a + \Sigma y_i -1} e^{-(b+n)\theta}\} d\theta$

  $= \frac{(b+n)^{a + \Sigma y_i}}{\Gamma(\tilde{y} + 1) \Gamma(a+\Sigma y_i)} \int^{\infty}_{0} \theta^{a + \Sigma y_i + \tilde{y} - 1} e^{-(b+n+1)\theta} \text{# 베타 분포의 pdf 를 생각하자.}$

  $= \frac{\Gamma(a+\Sigma y_i+\tilde{y})}{\Gamma(\tilde{y}+1)\Gamma(a+\Sigma y_i)}\bigg(\frac{b+n}{b+n+1}\bigg)^{a+\Sigma y_i} \bigg(\frac{1}{b+n+1} \bigg)^{\tilde{y}}$
  
  - 즉 $\tilde{Y}\mid data \sim NB(a+\sum y_i , \frac{1}{b+n+1})$

- **Problem**

  - overdispersion in Poisson model
  - 데이터가 생각보다 너무 분산이 큰 문제가 있다. 포아송을 가정한다면 $Y_i\mid \theta \sim Poi(\theta)$ 라면 분산과 평균 모두 $\theta$ 이다. ㅎ하지만 실제로는 이보다 분산이 훨씬 큰 경우가 비일비재하다. (포아송만으로 근사하기에는 여러 변수의 영향이 클떄가 많아서 fitting 이 잘 안될때가 많음)
  - 그래서 NB 분포를 사용할 수 있다. 모수가 2개라 평균과 분산을 따로 조절할 수 있다.
  - 또는 Hierachical Normal model 을 사용한다.


> ## Exponential model

Exponential 의 경우 parameter 가 2가지로 표현된다. 일반적인 rate parameter 와, scale parameter 이다. 

- 아래와 같이 Exponential 의 Conjugacy 는 gamma 임을 알 수 있다. (rate parameter 에 대한 conjugacy)

![png](/assets/images/Bayes/3_9.PNG)

![png](/assets/images/Bayes/3_10.PNG)

- 하지만 아래와 같이 sclae( 1 / rate) 의 경우에는 conjugacy 가 inverse gamma 임을 알 수 있다. 

![png](/assets/images/Bayes/3_11.PNG)

# [Exponential family and conjuate](#link){: .btn .btn--primary}{: .align-center}

- 앞에서 논의했던 분포(binomial) 은 사실 1변수 exponential family 모델이다. 
- exponential model 은 $p(y\mid\phi)$ = $h(y)c(\phi)\exp(\phi t(y))$ 의 형태를 가질때에 exponential 분포라 한다.

$$Y_i =  \begin{cases} 1 \ \ \text{$h(y)c(\phi)e^{\phi K(y)}$ if x$\in$ S } \newline 0 \ \ \text{o.w.} \end{cases}$$

- $S$ does not depend on $\phi$

- $\phi$ is a nontrivial continuous function of $\theta \in \Omega$ 
- if $Y$ is continuous, $K '(y) \not =0 $ and $h(y)$ is continuous function 
- IF $Y$ is descrete , $K(y)$ is nontrivial function 

- **Likelihood :**

$f(y_1, ... y_n \mid \phi)$

$= \prod  h(y_i)c(\phi)e ^ {\phi K(y_i)}$

$ \propto c(\phi)^n e^{\phi \sum K(y_i)} \text{# 베이지안이므로 데이터는 상수취급 }$

- **Prior :**

$p(\phi)$

$ = k(n_0, t_0)c(\phi)^{n_0} e^{n_0t_0\phi} $

$ \propto c(\phi)^{n_0} e^{n_0 t_0 \phi}$

- **Posterior :**

$p(\phi \mid y)$ <br>
$\propto p(\phi) f(y\mid \phi) $ <br>
$\propto  c(\phi)^{n_0} e^{n_0 t_0 \phi} c(\phi)^n e^{\phi\sum K(y_i)} $ <br>
$\propto c(\phi)^{n_0 +n} \exp (n_0 t_0 \phi + \phi \sum K(y_i))$ <br>
$\propto c(\phi)^{n_0+n} \exp(\phi(n_0t_0 + n\frac{\sum K(y_i) )}{n})$

- **interpret**
  - 위를 보면 $n_0 $ 는 prior sample size 라고 해석할 수 있다. 
  - $E[K(Y)] = E[E[K(Y)\mid \phi]] = E[-c'(\phi)/c(\phi)] = t_0$ 이 증명되어 있다. (1979 Diaconis ans Ylvisaker) 
  - 즉 $t_0$ 은 prior expected value of t(Y) 를 나타낸다. 
  - 즉 $t_0$ 는 prior guess  of $K(Y)$ (Likelihood 의 sufficiet statstics 즉 데이터의 정보를 모두 함축하고 있음) 라 할 수 있다. 
  - posterior 를 $\exp(\phi(n_0t_0 + n\bar{k}))$ 로 생각하면 좀 더 접근이 쉬울것이다.

> ## Binomial Example

- binomial 을 위의 형식에 맞추어 생각해보자.

- **Likelihood**

$p(y\mid\theta) = \theta^y(1-\theta)^{1-y}$

$= (\frac{\theta}{1-\theta})^y (1-\theta))$ 

$= e^{\phi y}(1-e^\phi)^{-1}\ \  \text{# $\phi$ = log[$\theta$/(1-$\theta$)]} , k(y) = y$ 

- **prior**

$p(\theta) \sim Beta(n_0t_0,n_0(1-t_0))$ 을 prior 라 설정하자. 그러면 아래와 같은 식이 성립한다.

$p(\theta)$

$\propto \theta^{n_0 t_0 -1 }(1-\theta)^{n_0(1-t_0)-1}$

$ \propto e^{\phi(n_0t_0-1)}(1+e^\phi)^{2-n_0}$

- **posterior**

$p(\phi \mid y)$

$\propto e^{\phi(n_0t_0 -1)}(1+e^\phi)^{2-n_0} e^{\phi y}(1+e^\phi)^{-n}$

$\propto e^{\phi(n_0 t_0 -1 +y)(1+e^\phi)^{2-n_0-n}}$

$\propto \theta^{(n_0t_0 +y)-1}(1-\theta)^{n_0(1-t_0)+(n-y)-1}$

이로부터 $p(\theta \mid y)$ ~ $beta(n_0t_0 + y , n_0 (1-t_0) + (n-y)$ 임을 알 수 있다.

- **summary**

$\phi$ = log[$\theta$/(1-$\theta$)]  $K(y) = y$ 

- prior $Beta(a,b)$ 를 a+b개의 데이터 중 a의 성공, b의 실패가 있는 data 로 해석할 수 있다는것을 기억하자.  $Beta(a,b)$ 에 대해서  $n_0 = a+b $ 이다. 즉 $n_0$ 은 데이터의 갯수라고 해석할 수 있다.
- 우리가 sufficient statistics $K(y) = y$ 였음을 기억하자.  
- $y$ 를 추정하기 위한  prior expected value of K(Y)=y 는 $E[K(Y)] = E[E[K(Y)\mid \theta]] = E[E[y\mid \theta]] = E[\theta] = \frac{a}{a+b} $ 이 된다.
-  즉 $t_0$ 은 prior 입장에서 추정한 $K(y)(sufficient \ \ statistics)$ 이다.  
- 그러므로 두 sufficient statics 추정치들은 posterior 에서 prior 와 data 의 수 비율만큼 합쳐진다! 

