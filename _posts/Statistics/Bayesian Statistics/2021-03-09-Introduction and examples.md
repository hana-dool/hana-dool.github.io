---
title:  "Inrtoduction and Example"
excerpt: "베이즈 통계에 대한 심도있는 개요"
categories:
  - Bayes
last_modified_at: 2021-09-26

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

- 우리는 종종 어떠한 양(quantity) 에 대한 우리의 믿음(belief)을 엉성하게 나마 확률로 표현해보려 애쓴다.
- 하지만 이런 information 을 확률로 표현하려는것을 체계화 할 수 있다. 
- 베이즈 통계는 믿음(belief)을 새로운 정보(데이터)와 통합해 업데이트할 수 있게 해준다. 
- 이러한 업데이트는 베이즈 룰을 통해서 가능하고, Baysian inference 라고 한다. 
- 베이즈 방법론은 다음과 같은 methods 를 제공한다.
  - 좋은 통계학적 성질을 이용한 parameter 추정
  - oberseved data 에 대한 간단한 설명
  - Missing data 에 대한 예측(na imputation)
  - model selection / validation 을 위한 computational framework

> ## baysian learning

- Statistical induction 은 oberseved data(즉 population 의 subset) 에서 population 의 특성을 추론하는 것이다. 
  - population 의 특성은 일반적으로 parameter $\theta$ 로 나타나진다. 그리고 data 의 descriptions 는 data set $y$ 로 나타나진다. 
- data set 이 얻어지기 전까지는 이러한 특성들을 알기 불가능하다. 
  - 데이터셋을 얻고난 이후 우리의 uncertainty about population 은 줄어들고, 얼마나 줄어드는지를 측정하는지가 Bayesian inference 의 목적이다. 
- 우선 논리를 이끌어내기 전에 몇개의 기호들을 정의하자. 
  - $\mathcal{Y}$  를 sample space 라 하자. 그러면 $\mathcal{Y}$ 는 set of all possible datasets 이 된다. 이  $\mathcal{Y}$ 로 부터 하나의 $\mathcal{y}$ 가 뽑히게 된다.
  - $\Theta$ 는 parameter space 라 하자. 그러면 $\Theta$ 는 set of all passible parameter value 가 된다. 우리는 $\Theta$  에서 true population을 제일 잘 나타내는 추정치를 얻어내고 싶다.
- 이제 베이지안 learning 이 어떻게 일어나는지 살펴보자. 베이지안 learning 은 ($\mathcal{Y}$, $\Theta$) 위에서 정의되는 joint belif $p(y\mid\theta)$ 에서부터 시작된다.

1. 각 $\theta \in \Theta$ 에 대해서 $p(\theta)$ 는 prior distribution 이라 하며 population 에 대한 우리의 믿음을 나타낸다. 
2. 각 $\theta \in \Theta$ 와 $y\in \mathcal{Y} $ 에 대해서 model $p(y\mid\theta)$ 는 $\theta$ 가 True 일때 y 에 대한 우리의 믿음을 나타낸다.
3. 만일 데이터 $y$ 를 얻는다면 우리의 마지막 step 은 $\theta$ 에 대한 우리의 믿음을 업데이트 하는것이다. 각각의 수적인 값 $\theta \in \Theta$에 대해, 우리의 사전 분포 $p(\theta)$는 $\theta$가 실제 모집단의 특성을 표현한다는 우리들의 믿음을 나타낸다.
   - 업데이트는 베이즈 룰에 따라 $p(\theta \mid y) = \frac{p(y\mid\theta)p(\theta)}{\int_{\theta}p(y\mid\tilde{\theta})p(\tilde{\theta})}$ 으로 주어진다.

# [Why Bayes?](#link){: .btn .btn--primary}{: .align-center}

- Cox(1946,1961) 와 Savage(1954,1973) 는 사람의 믿음을 $p(\theta)$ 와 $p(y\mid\theta)$ 으로 나타나게 된다면 베이즈 rule 이 사람의 belief about $\theta$ 와 $y$ 를 나타내기에 최고의 방법이라는것을 수학적으로 증명하였다. 
  - 이 결과는 베이즈 룰을 통한 업데이트가 정당하다는 큰 기반이 될 수 있었다. 
- 하지만 $p(\theta)$ 은 우리의 '믿음' 인데 이를 정확하게 수학적으로 묘사하기에는 무리가 있다. 
- 그래서 편의상 conjugate prior 를 써서 computational cost 를 낮추려고 하였다. 
  - 이때에 prior 에 대한 의문점이 들것이다.  prior 을 수학적으로 제대로 표현할 수 없다면 베이즈 통계에 대한 정당성은 어떻게 확보할 수 있을까?
- 사실 모든 모델은 틀린다. True 를 정확하게 캐치할 수 없기 떄문이다.
  -  $p(\theta)$ 는 우리의 믿음과 매우 달라서 '틀릴' 수 있다. 
  - 하지만 그렇다고해서 $p(\theta\mid y)$ 가 쓸모없는게 아니다.  베이즈 통계의 궁극적인 목적은 올바른 $p(\theta)$ 를 고르는게 아니라, 데이터를 통해서  $p(\theta\mid y)$ 를 업데이트 하면서 궁극적으로는 population 의 분포를 근사하는것에 있다. 
  - 그리고 데이터가 매우 많다면 prior 에 상관 없이 posterior 은 True model 로 향하는것이 증명되어있다.
- 또한 prior 에 큰 믿음이 없다면 거의 믿음을 주지 않는 Weak prior(요컨데 Uniform 분포) 를 줄 수 있다.

> ## Rare event Probability Estimation Example

- 작은 도시에 희귀한 병의 발병률에 대해 관심이 있다고 하자. 그래서 20명의 random sample data 를 얻었고, 이를 통해서 발병률을 조사하려고 한다.

> Bayesian 방법론

- **prameter**
  - $\theta$ 는 전염률을 나타낸다. 즉 $\theta \in \Theta = [0,1]$ 이 된다.
  - $y$ 는 전염된 사람의 총 숫자를 나타낸다.  즉 $y \in \mathcal{Y}=\{0,1,2...20\}$

- **sampling model**
  - 데이터를 살펴보기 전에는 감염된 사람의 수 $Y$ 는 알 수 없는 Random variable 이다.  
  - 즉 이 $Y$ 에 대해서 sampling model 을정의해야 한다. 이는 $Y\mid\theta \sim binomial(20,\theta)$ 가 된다. 

![png](/assets/images/Bayes/1_1.PNG)

- 왼쪽 그림은 각 $\theta$ 에 따른 $Y$ ~ $binomial(20,\theta)$ 이다. 
- 오른쪽 그림은 $\theta$ 에 대한 사전 / 사후 분포를 나타낸다. 사전분포가 뭔지 궁금할텐데, 다음 문단에서부터 어떻게 정의하는지 알아보자.
- **prior distribution**
  - 많은 조사끝에 우리 나라의 감염율은 약 0.05~0.20 이고 또한 평균은 0.1 임을 알아내었다. 
  - 이러한 prior information 은 우리의 prior distribution 이 어떤식으로 구성되어야 할지를 알려준다.
    - (0.05,0.20) 사이에 대부분의 확률이 위치해야한다.
    - $E[\theta]$ under $p(\theta)$ 는 대략 0.1 이여야 한다.
    - $\theta$ 는 확률이므로, support 는 $[0,1]$ 이여야 한다.
    - 필수적일 필요는 없지만 Computational 적으로 효율적이면 좋겠다.
  - 하지만 위의 성질을 만족하는 distribution 은 매우 많지만, $beta(a,b)$ 로 정하기로 하였다. 
  - 그러면 $E[\theta]$ = $\frac{a}{a+b}$  이 되고 mode 값은 $\frac{a-1}{a+b-2}$ 가 된다. 이를 이용해서 대충 prior 를 구성해본다면 $\theta \sim beta(2,20) $ 이 된다. 
  - 이 분포는 위 그림에서 회색의 사전분포이다. 이 분포는 우리가 구성하고자 하는 성질들을 만족하는데 
    - $P(0.05<\theta < 0.2) = 0.66$
    - $E[\theta] = 0.05$ 
    - $support\;of\;beta = [0,1]$
    - prior 가 conjugate 가 되어 계산량이 매우 줄어든다.(이건 나중에 더 할거에요)

- **posterior distribution**
  - 나중에 posterior 에 대해서 자세히 다루기 때문에, 여기에서는 그 결과만 적도록 하겠다. 베이즈 Rule 에 의해서 $Y\mid\theta \sim binomial(n,\theta)$ 이고 $\theta \sim beta(a,b)$ 이면 posterior $\theta \mid Y$ $\sim$ $beta(a+y,b+n-y)$ 가 된다. 
  - 예를들어서 우리의 20명 데이터에서 아무도 감염되지 않았으면 $y = 0$ 이 된다. 그러면 posterior 는 $beta(2+0,20+20-0)$ 이 된다. 이 예시는 위 그림에서 오른쪽 Fig 1.1 의 굵은색 분포이다.
  - 그림을 살펴보면서 prior+data -> posterior 의 과정을 잘 살펴보자. 우선 우리가 받은 데이터는 20명 중에서 감염자가 없는 0명의 데이터이다. 
  - 이 데이터의 증거(Evidence) 는 감염률이 매우 낮다는 것이다. 이를 prior 에 더해주면 posterior 는 이 증거를 받아들여 감염률($\theta$) 가 왼쪽으로 치우치게 된 것을 볼 수 있다. 

- **Sensitivity Analysis**
  - 우리의 prior 를 좀 더 일반적인 $\theta \sim beta(a,b)$ 라 하자. 
  - 그러면 $Y=y$ 하에서, posterior distribuiton of $\theta$ 는 $beta(a+y,b+n-y)$ 가 된다. 이 상태에서 posterior expectation 은 

$$\text{E}[\theta \mid Y = y] = \frac{a + y}{a + b + n}\\
= \frac{n}{a + b + n} \frac{y}{n} + \frac{a+b}{a+b+n} \frac{a}{a+b} \\
= \frac{n}{w + n} \bar{y} + \frac{w}{w + n} \theta_{0} $$

- 가 된다. 이제 각 값들에 대해서 그 의미를 살펴보자.

1.  $\theta_0 = \frac{a}{a+b}$ 은 prior expectation of $\theta$ (즉 prior 믿음에서 추정한 전염율)
2. $\bar{y}$ 는 sample mean (즉 데이터로부터 추정한 전염률)
3. $w = a + b$  ($w$ 가 클수록 $\theta_0$ 의 영향력이 커진다.)

- 위의 정보를 살펴본다면, 데이터로부터 업데이트 된 posterior 에서 전염률 추정은, proior 의 전염률 추정과 데이터에서의 전염률 추정의 weighted mean 임을 볼 수 있다. 

![png](/assets/images/Bayes/1_2.PNG)

**Fig 2.2** prior 에서 예측한 전염율 $\theta_0$ 와 내 확신 w 에 따른 posterior 의 추정 $E[\theta\mid Y=0]$ 와 $\Pr(\theta < 0.10 \mid Y = 0)$ 의 등고선이다. 

- 위 그림의 상황을 다시 복기해 보자. 현재 prior 은 $\theta \sim beta(a,b)$  인 상황이고 데이터는 $Y=0$ 으로 아무도 감염되지 않은 상태이다. 
- 즉 prior 에서 예측한 전염율은 아무도 감염되지 않은 데이터를 만나 posterior 에서는 감염율이 떨어짐을 예측할 수 있다. 
- 위 그림을 보면 그 예상과 맞아떨어진다. w 가 증가할수록 내 prior 에 대한 확신이 늘어나  $E[\theta\mid Y=0]$ 의 값이 높게 유지되고 있다. 
- 하지만 w 가 작은경우는 prior 에 대한 확신이 적고 Data 를 믿게 되어 거의 0 에 수렴하게 된다. 위의 그림을 보며, prior 과 데이터에 대해서 posterior 가 얼마나 민감한지에 대해서 insight 를 얻을 수 있다.

> Frequentist 방법론

- population 에서의 감염률 $\theta$ 를 추정하는 일반적인 방법은 data 로부터 sample mean $\bar{y} = \frac{y}{n}$ 으로 추정하는 것이다. 우리의 sample 에서는 당연히 $y=0$ 이므로 estimation 은 0 이 된다. 
- 물론 위와같이 점추정으로 해버리는것은 sample 에 대한 uncertainty 를 표시하지 않는 방법이다. ((n=5,y=0) 와 (n=10000,y=0)) 의 점추정은 0 으로 같다. 하지만 이 경우 누가 이 결과를 신뢰할 수 있을까?
- 그래서 좋은 방법은 95% CI 를 형성하는 구간 추정을 하는것이다. n 이 클 때에는 $\bar{y}$ 가 Normal 을 따르므로 이를 이용한다면 감염률(population proportion) $\theta$ 의 95% CI는 ${\bar{y}\pm\sqrt{\bar{y}(1-\bar{y})/n}}$ 이 되게 된다. 하지만 이런 방법에도 큰 오류가 있다.

1. 작은 n 에서는 작동되지 않는다.
   - 통입에서건 통방에서건 뭐 $20\le n$ 에서 성립한다 뭐다라고 했겟지만, 사실 CLT 가 성립하는 조건인 n 은 정해져 있지 않다. 위의 예시에서 n 이 50정도라 하더라고, 구간이 참 $\theta$ 를 포함할 확률은 80%가 채 안될것이다.
2. $\bar{y} = 0$ 인 우리의 데이터상에서는 신뢰 구간은 웬만하면 거의 0 근처로 나온다.
   - 즉 우리의 이전 상황과는 상관없이 무조건 감염률을 0 으로 추정하게 된다. 

- 위와 같은 상황을 피하기 위해 베이즈가 있는것이다. 베이즈에서는 prior 가 일종의 보험으로 작용한다. 위와 같이 적은 sample 에서의 Data 는 prior 에게 큰 영향을 끼치지 못한다. 
- 그래서 20명에게 감염률이 0 이였더라도 미국의 보건청에서 제시한 추정같은 강력한 prior 를 사용하게 된다면 감염률은 0 이 아니라 어느정도 값에서 0으로 살짝 이동할 뿐 크게 변하지 않는다. 

> ## EX : Build Predictive Model

- 당뇨병을 여러 설명변수를 이용해 추정하는 경우를 생각해보자. 
- 모델은 64개의 변수를 가지고 있다. 그리고  342 명을 이용하여 model 을 training 시키고 , test 는 100명의 patient 를 이용하여 진행할 것이다.

> model selection

- **Samping model and parameter space**
  - $Y_i$ 는 subject i 에 대해 당뇨병의 진행률 이라고 하자. $x_i = (x_{i,1}, … , x_{i,64})$ 는 설명 변수이라고 하자. 우리는 linear regression $Y_i = \beta_{1}x_{i,1} + \beta_{2}x_{i,2} + … + \beta_{64}x_{i,64} + \sigma_{\epsilon_i}$ 을 고려할 것이다. 
- **prior distribution**
  - 이때 parameter 가 65개나 되는데 이 joint distribution 을 prior 로 올바르게 정의하는것은 불가능에 가깝다. 
  - 나중에 이 예시를 자세하기게 하기 때문에 여기서 prior 를 어떻게 설정하는지는 간단하게만 설명하겠다. 
  - 대부분의 parameter 는 의미가 없을것이기 떄문에, 각각의 parameter 는 50% 확률로 0 일 것이라고 정의하려 한다. 

- **posterior distribution**
  - $\textbf{y} = (y_1, …, y_{342})$ 와 $\textbf{X}=(x_1, ... x_{342})$ 의 데이터가 주어졌다고 하자. 
  - 그러면 posterior distribution $p(\beta \mid \textbf{y},\textbf{X})$ 를 compute 할 수 있고, 이로부터 $Pr(\beta_j \not= 0 \mid \textbf{y},\textbf{X})$ 를  각각의 j 에 대해서 계산할 수 있게된다. 

![png](/assets/images/Bayes/1_3.PNG)

- **Fig 1.3 추정한 posterior**
  - 위 그림을 보게되면, 모든 coefficient에 대해 처음에 50대 50으로 0이 아니라고 가정했음에도 불구하고, 0.5 보다 높게 추정되는 변수는 고작 6개에 불과한것을 볼 수 있다. 

> Baysian 과 Frequentist 의 비교

- 이제 Baysian 방법론과 다른 방법론의 모델에 대해 test data 를 이용해 봄으로서 모델의 성능을 비교해 보자.

- **Bayes prediction**
  - $\hat\beta_{bayes}= E[\beta\mid \textbf{y},\textbf{X}]$ 를 poetserior 의 expection of $\beta$ 라 하자. 그리고 test 데이터(100*64)를 $\textbf{X}_{test}$ 라 하자.  
  - 우리는 $\hat y_{test} = \textbf{X} \hat \beta _ {Bayes}$ 처럼 예측값을 형성할 수 있다. 이제 이 예측치와 $y_{test}$ 를 같이 비교함으로서 베이즈 모델에 대한 평가를 할 수 있을것이다.

- **Freq prediction**
  - 여기에서는 OLS 를 사용해 보자. OLS 란 $\text{SSR}(\beta) = \Sigma^{n}_{i=1}(y_i - \beta^{T}x_i)^{2}$ 처럼 잔차의 제곱을 최소화 하는 $\beta$ 를 추정하는 방법이다. 
  - 그리고 이 방법은 $\hat{\beta}_{ols} = (X^{T} X)^{-1}X^{T} y$  으로 주어진다. $\hat y_{test} = \textbf{X} \hat \beta _ {Ols}$ 를 생성함으로서, ols 모델에 대한 평가를 할  수 있을것이다.

![png](/assets/images/Bayes/1_4.PNG)

**Fig1.4** 왼쪽은 베이즈 모델을 이용한 추정, 오른쪽은 OLS 를 이용한 추정 

- 이떄 x=y 선 위에 값들이 놓여져 있어야 잘 추정하고 있음을 알 수 있는데, bayes 의 경우가 더 추정이 잘 된 모습을 볼 수 있다. 
- 이러한 차이가 생긴것은 데이터가 너무나 적었기 때문이다. 이런 상황에서 OLS 는 모집단의 특성을 제대로 나타내지 못하기 떄문이다. 
- 이런 경우 OLS 보다는 Lasso 모델을 ($SSR(\beta : \lambda) = \sum^n_{i=1}(y_i-x_i^T\beta)^2 + \lambda \sum^p_{j=1} \mid\beta_j\mid$ 을 최소화) 통해 많은 원소들을 0 으로 만드는 penalty 를 부여하게 되면 좀 더 나은값을 제시한다. 

# [Conclusion](#link){: .btn .btn--primary}{: .align-center}

- 위의 예시들을 보면 알겠지만, 베이지안의 활용처는 무궁무진하다. 베이지안은 다음과 같은것들을 제공할 수 있다.

1. Sample size 가 크건 작건 잘 작동하는 모델
2. 복잡한 모델에서 적용 가능한 모델
3. prior 의 정보를 추가할 수 있는 모델

