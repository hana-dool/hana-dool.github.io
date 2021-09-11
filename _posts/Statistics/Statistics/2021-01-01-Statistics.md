---
title:  "단편적인 통계모음"
excerpt: "그냥 내 느낌을 정리해놓은 포스트"
categories:
  - Stat
tags:
  - 3
last_modified_at: 2021-03-04

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: false

use_math : true
---

# intro 

- 이 Post 는 제가 공부하다가 애매했던거 올리는거니까 참조하지마세요!
- 계~속 업데이트될거같아요... 



# 용어모음

종속변수 : 우리가 측정하고자 하는 변수. 흔히 Y 변수라고 한다.

독립변수 : 종속변수에 영향을 주는 변수. 흔히 X 라고 한다.



# 귀무가설이 옳다? 

많은 글에서 '귀무가설을 기각하게 된다. 그러므로 대립가설이 옳다' 라는 표현을 볼 수 있을것이다. 그런데 이러한 주장이 맞는것일까?

이는 틀린말이다. Frequentist 의 test 는 귀무가설이 맞다는 상테에서 '내 데이터가 이거에 얼마나 이상할까?' 를 체크할 뿐이다. 절대로 귀무가설에 대한 확률, 옳고 그름을 논하는게 아니다.

통계학이라는것은 주어진 데이터를 바탕으로 추론하는것이고 , P- value 는 하나의 지표점이 될 뿐 그 자체로 맞다 틀리다의 기준이 되면 안된다. 



# 표준편차와 표준오차

표준 편차는 '데이터가 얼마나 퍼져있는지' 를 나타내는 것이다.

표준 오차는 '데이터의 함수인 통계량이 얼마나 퍼져있는지' 를 나타내는 것이다. 



# P - value

1. "귀무가설이 틀릴 확률" 이 P-value 일까?

(X) 이다. P-value 는 귀무가설이 맞다고 할 때에, 우리의 데이터가 얼마나 이상한지에 대해서 알려주는것이다. 즉 귀무가설 입장에서 데이터가 '이상한 정도' 라고 하는것이 더 정확하다.



# 신뢰구간과 Test

왜 신뢰구간에 포함되지 않는것으로 Test 를 대체할 수 있을까? 신뢰구간이 뭐냐? 그건 바로.. 귀무가설을 가정한 상태에서



# Type 1,2 error

Type 1 error : 귀무가설이 맞는데도 귀무가설을 기각할 확률

- 위가 더 심각하다. '일반적으로 사실로 받아들여지는 사실' 을 기각하는것이므로 낮게 설정하는게 좋다.

Type 2 error : 귀무가설이 틀린데 귀무가설을 채택할 확률

- 이 역시 심각하긴 하나 '기존에 받아들여지고 있는것을' 계속 받아들인다는 의미로, Type1 error 보다는 덜 심각하다. 



- Test 를 할 떄에는 기본적으로 유의수준부터 고정하고 그다음 검정력을 조절하면서 최적의 Test 를 찾는다. 
- 그렇가면 왜 유의수준부터 고정하는것일까? 그것은 유의수준이 더 중요하기 때문이다.
- 우리가 하는 테스트의 대부분은 '기존에 적용하고 있는것이 효과가 있다!' 를 검정하고싶은것이 아니라 '기존의 것은 틀렸어! 새로운게 맞아!' 를 밝혀내려 한다. 
- 즉 귀무가설을 기각하려하는게 주 목적이라는 것이다. 이러한 '귀무가설 기각' 의 기준치를 정하는게 유의수준이다. 즉 유의수준을 정하는것이(Type 1 error), Type 2 error를 조절하는것 보다 훨씬 중요하다는 것이다.

<br>

# Sample size 와 TEST

- 일반적으로 Test 란 Test statistics 의 분포를 가지고 얘가 $H_0$ 일 때에는 어떤 분포를 가지는데, 우리 데이터를 넣었을 떄의 Test statistics 는 이 분포에서 정상적이다! 이면  $H_0$ 을 선택하는것이고, 그렇지 않으면 $H_0$ 을 기각하는것이다.

- 하지만 일반적으로 Sample size 가 늘게되면, 일반적으로 Test statistics 의 분산이 감소한다. 그러므로 분포가 더 뾰족해지고, 그러면 Type 1, 2 error 가 모두 감소한다.



# Baysian

- inferece : Posterior distribution 을 이용한 estimation 과 hypothesis Test
- prediction 또한 posterior 를 이용한다. 

# QQ-plot

- Q-Q plot은 두 확률 분포를 그것들의 quantiles를 그려넣음으로써 비교 하는 것이다. 첫 째로, quantiles의 간격이 선택 된다. Q-Q plot의 첫 번째 한 점 (x, y)는 첫 번째 분포의 첫 번째 quantile이 x값이 되고, 두 번째 분포의 첫 번째 quatile이 y값이 된다. 즉, 100-quantiles로 선택했다고 치면, 두 분포에서 1%에 해당하는 샘플을 각각 x, y값으로 넣어서 점을 찍는 것이다

- QQ plot의 목적은 두 데이터 셋이 같은 분포로부터 왔는지를 보이는 것이다. 실용적으로 많은 데이터 셋이 가우시안 분포와 비교된다고 하는데, **보통은 두 개의 분포가 없이 그냥 한 분포를 R에서 qqnorm 함수를 사용해서 그 분포가 얼마나 가우시안 분포와 비슷한지를 알 수 있다. 하지만, 기본적으로 Q-Q plot은 가우시안 뿐만 아니라, 어떤 분포든 두 분포의 유사성을 보는 것으로, 두 분포가 포아송 분포라면 이것 역시 선으로 나타난다.**



# VIF

- 설명에 앞서 먼저 입력 데이터의 구성을 아래와 같이 약속하자.
  분석에 사용될 데이터가 입력변수 n개와 종속변수 1개로 구성된다고 하자. 총 변수는 n+1 이다.
  이 데이터의 변수들은 모두 수치형(양적) 변수이어야 한다.

그럼, *VIFk* 는 (여기서, 1<= k <= n 의 관계)
변수 k를 종속변수로 지정하고, 나머지 n-1 개의 입력변수를 입력변수로 지정하여 회귀분석을 수행한다.
즉, 이 회귀분석에서 종속변수 Y는 제외시킨다. 왜냐하면, 다중공선성은 입력변수들 간의 상관관계를 측정하는 것이기 때분이다.

위 수행된 회귀분석에서의 결정계수 *Rj*2 을 구한 후 아래의 수식으로 *VIFk* 를 구한다.

*VIFk* = 1 / (1 - *Rj*2)

중요한건 이게 범주형 변수에도 쓰일 수 있다는 것이다. one hot vector 처리를 한 데이터에서 이런것을 쓸 수 있다! 호호호

# CLT

CLT 는 무슨 분포에서든지 사용 가능할거같지만 몇가지 제한사항이 있다.

1. 실험은 Random experiment 이여야 한다.

코로나 사태의 주식차트로 생각해보자. 1970~ 2020 의 데이터를 모아서 1년간의 코스피 지수의 평균을 $\bar{X}$  라고 하자. CLT 에 의하면, $\bar{X}$ 는 n 이 충분히 크므로 어느정도 안정된 그래프를 그려야하지만, $\bar{X}$ 는 계속 증가하는 형태를 볼 수 있다. 이는 CLT 가 적용되지 않은것이다. 이는 시계열 데이터의 특징으로, 시간이 끼어들어서 Population 이 계속 변해서, $\bar{X}$ 의 sample space 가 일정하지 않았던것이다! 

코로나 말고도 Dacon 에서도 자주볼 수 있는데, 내가 예측했던 태양광 예측 대회에서도 Public score 와 Private score 가 매우 차이가 났었다.(Public 에서 순위가 높은사람은 모두 나락으로 떨어졌다.)  Private 의 데이터는 아예 년도가 달랐었기 떄문에 Training 때 사용한 데이터와 Population 이 달라서 일어난 참사였다.

2. 분산이 존재해야한다. (즉 Second moment)

분산이 존재하면 평균이 존재하므로, 위 말은 분산과 평균이 존재하는 정상적인 분포여야한다는 것이다. 이것을 만족하지 않으면 CLT 는 성립하지 않는다.

# Frequentist VS Baysian

1. **Frequentist**

   먼저 빈도론자가 어떤생각을 가지고 있는지가 중요하다. 빈도론자들에게 있어서 $Parameter \theta $ 는 fixed constant 일 뿐이다. 이러한 생각에서 데이터를 모은다. 데이터의 경우에도 Random experiment 에서 수집한 iid 데이터, 즉 $x_1,x_2... x_n  \sim iid \sim f(x,\theta)$ 를 가정한다.  

   1. 분포$f(x,\theta)$ 를 가정한다. 
       - 즉 현실의 복잡한 데이터의 세상을 이쁜 세상으로 강제로 끌고오는것이다. 
       - $X_i$ 의 Sample 들이 어떠한 분포를 따른다는 가설을 설정 
       - 또한 $X_i$ 는 Random experiment 이여야 한다. 
       - 물론 이러한 가정 없이도 clt 를 이용해 $\bar{X}$ 의 분포를 알아낸 뒤에 Test 를 할 수도 있다! 
   2. 가정한 분포에 대해서 Statistics 를 설정한다.
       - Statistics 는 $ T:[X_1,X_2...X_n] -> \mathbb{R}$ 처럼 데이터의 함수이다. 
       - 통계적 목적을 위해 설정되며 추정 목적으로 사용되면 Estimator / 가설검정 목적이면 Test statistic 이라 한다.
       - 대표적으로 mean , median , sample variance 등이 있다.
   3. Sampling distribution 을 구한 뒤 Testing / Estimating 을 수행한다.
     - 분포를 알고있다면, Estimation(95% CI 를 통한) 과 Testing 이 가능하다. 
     - Test 의 예시를 들어보자. $X \sim N(\mu,\sigma^2) $ 이라고 하자.($\sigma$ 는 정해진 값) 이 떄에 $\mu$ 에 대해서 추정하고 싶다고 하자. <br>
       그러면 Test statistics 는 자연스럽게 $\bar{X}$ 가 된다. 이 Test statistics 의 표본분포는 $\bar{X} \sim N(\mu,\frac{\sigma^2}{n}) $ 가 된다. <br>
       이제 $H_0 : \mu = 0$ 와  $H_1 : \mu \not= 0 $ 을 검정하고 싶다고 하자. p-value 를 구하기 위해  $H_0$ 을 가정하게 된다면 $\bar{X} \sim N(0,\frac{\sigma^2}{n})$ 이 된다. 미지수가 없는 완전한 Sampling distribution 을 구하게 된 것이다. <br>
       이를 통해서 내 데이터 $\{1,2,3,3,3,4,5\}$ 로부터 $\bar{X}$ 를 3으로 구할 수 있게되고, 이 값이 얼마나 이상한 값인지 P-value(대립가설쪽으로 관측될 확률) 를 구해본다면 약 0.003 이 나오게 된다. 이는 $H_0$ 이 맞다고 하기엔 매~우 이상한 값이다. 즉 $H_0$ 을 기각하게 된다.<br>
     - 또는 신뢰구간을 구할 수 있게된다. 이 역시 위와 비슷한 과정으로 진행된다.  $\bar{X} \sim N(\mu,\frac{\sigma^2}{n}) $ 에서 $L(X_1 .... X_n)<=\mu<=U(X_1....X_n)$ 처럼 모수값이 구간에 있을 확률이 95% 가 되게 95% CI for mu 을 계산할 수 있게된다. (정확하게는 구간이 모수를 포함할 확률이다. 모수는 움직이지 않음) 



2. Baysian

   parameter $\theta$ 를 Unkown 인 Random Variable 로 취급한다. 그리고 Prior Belief of $\theta$ 를 정한 뒤에 데이터를 측정하고,  데이터를 이용해 posterior 를 업데이트하기만 하면 된다. 

   inference

   - $\theta$ 를 확률변수로 보는 입장이므로, 모수의 추론은 어떠한 CI, Estimator 값이 아니라 분포(posterior) 로 제공된다.

# sampling distribution

- 위 용어는 'Sampe 을 R.V. 취급하는 Freq 에서 쓰이는 말입니다. (베이즈의 경우에는 데이터는 'Fixed' 라고 생각합니다.)

- 빈도론자의 입장에서는, 미지의 세계인 모수를 들여다 보기 위해서는  Sampling distribution 을 구하는것이 필수입니다. 
- 하지만 이를 구하는것은 매우 고역 입니다. $\bar{X}$ 같은 값은 어느정도 쉽겠지만 (CLT) 우리가 궁금한게 $\bar{X}$ 뿐만이 아니라 모수, 복잡한 통계량 등일 떄가 많은데, 이럴때에 Sampling distribution 을 구하는게 매우 힘들다.

- exactly 한 Sampling distribution 을 구하는것은 매우 힘들다. 그래서 Limiting distribution 을 이용하기도 한다. 예시로 CLT 를 이용하면 $\bar{X}$ 의 극한분포를 구할 수 있고, 이를 이용해 Estimation, Testing 이 가능해진다.

- 하지만 Limiting distribution 을 구하는것도 마냥 쉽지는 않다. 학회지에 나오는 논문들을 보면, 새로운 분포를 만든 후 제일 시간이 오래 걸리는 작업이 Sampling distribution 을 해석학적으로 어떠한 분포를 Exactly 또는 Assymptotic 하게 따르는지 증명해내는 작업이라고 한다.
- 이러한 Assymptotic Disribution 을 구할 수 없을때에 울며 겨자먹기로 하는게 바로 Bootstrap 이라고 합니다...

# H_0 이 맞을 확률?

**Frequentist**

Frequentist 는 $p(Data\mid H_0) \le \alpha$ 이면 $H_0$ 을 기각한다는 논리이다. 하지만 사람들은 그 의미를 $p(H_0\mid Data) \le \alpha$  로 받아들인다. 즉 $H_0$ 이 틀릴지 아닐지로 받아들인다는 것이다. 하지만 이것은 틀린것이다. 

생각해 보자. $H_0 : \theta = 0 $ 의 꼴로 귀무가설이 설정된다. 하지만 Frequentist 입장에서 $\theta$ 는 fixed constant 이기 때문에 확률이 존재할리가 없고 '맞고 틀림' 만 존재할 뿐이다. 즉 귀무가설을 확률로 받아들인다는것 자체가 빈도론자 입장에서는 낭설이다.

즉 결국 빈도론자 입장에서는  $p(Data\mid H_0)$ 의 확률을 논할수 밖에 없다. 귀무가설이 맞다고 가정했을때에, 데이터가 얼마나 이상한지를 살펴봄으로서, $H_0$ 을 기각할지 말지를 결정해야하는 것이다. 

하지만 위의 logic 은 헛점이 많은데, 너무 이분법적인 사고라는 것이다.  만일 $H_0$ 을 기각했다고 하자. 그러면 대립가설이 선택될텐데, 이때 $H_1$ 에서 어떤 $\theta$ 가 Probable 할까? 같은 정보는 알려주지 않는다. 즉 '데이터를 고려하였을 때 $H_0$ 은 좀 아닌거같아~' 만 알 수 있을뿐이다. 

   

**Bayesian**

하지만 베이즈입장에서는 다르다. 베이즈 입장에서는 $\theta$ 가 random variable 이기 때문에 귀무가설이 맞을 확률을 논할 수 있다. 왜냐하면 $p(H_0\mid Data)$ 가 분포로 나오기 때문이다. 즉 귀무가설의 '확률' 을 논할 수 있게 된다는 것이다.

이렇게 보면 베이즈가 훨씬 더 우월해보인다. 하지만 꼭 그렇지만도 않다. 베이즈는 그냥 확률론적인 도구를 가지고 귀납적 사고를 사람들에게 설득하려고 정한 약속이라, 정답이 있는게 아니다. 그래서 Prior 을 정하는게



# Hard Task in Statstics

**Frequentist**

- Sampling distribution(Test 또는 Estimator) 를 구하기가 핵심. Limiting 으로 구하던, Exact 로 구하던 매우 어려운건 사실이다. 주로 해석학을 이용해 Limiting 을 구한다고 한다. 

**Baysian**

- 어떻게 Unnormalized posterior 를 Normalize 할지가 핵심.<br>
  주로 Conjugacy 를 쓰거나 MCMC 를 쓴다. 



# Data 의 수집 의도

데이터를 수집할 때 '의도' 에 따라 분포가 달라진다. 

1.동전을 계속 던지면서 H,T 를 기록한다. -> Binomial <br>
2.앞면이 나올때까지 던진다 -> Neg-Binomial <br>

즉 Frequentist 는 데이터를 받을때에 그 '의도' 또한 중요하다. 잘 정의된 실험계획에 따라 수집된 데이터를 이용해야 가설검정이 잘 된다. 하지만 일반적인 관측데이터의 경우 이러한 '의도' 가 제대로 정의되지 않아, 무작정 Frequentist 방법을 쓰기가 애매하다.

Freq 들은 수집 의도에 따라 Likelihood 까지 달라지기때문에.. test 에 따라 달라지게된다. 

# 짜증나는 시계열

Dacon이나 기타 여럿 경진대회에 보면 시계열에 대해서 예측하라는 대회가 많아서 한번 여기다가 써본다.

시계열이란게 사실은 통계학의 영역이 아니라 그냥 Pattern recognition 이라고 생각한다. 그 이유는 너~무 불안정하다. 시간에 따라서 Population이 계속 변한다. 1년 전에 Fitting 한 model 은 요번년도에서는 거의 쓸모가 없으며 내년 예측에는 Trash 나 다름없을 정도다.

애초에 통계학은 Population이 어느정도 안정되어 있는 상태에서 분포가정을 통해 데이터를 해석하는거다. 즉 이런 통계학을 시계열에 적용하려는 시도 자체가 어불성설인 셈..

그래서 통계학의 장점인 해석 자체가 거의 불가능한거다. 회귀는 각 변수의 값이나 중요도가 나오기라도 하지, 시계열은 그런거 없. . 다. .....

그러므로 그냥 시계열은 LSTM / GRU / .. 머 이런거 떄려박아서 패턴만 학습한다음에 예측하는게 전부이지 않을까.. ? 하는 생각이 든다. 



# 베이지안과 Sufficient Statsitcs

이건 경훈이형이 말해준 무용담에서 나온 내용이다. 떄는 대학원 통계전산 수업인데, conjugate 를 안쓰면 엄청나게 Computational cost 가 커서 컴퓨터가 감당할 수 없는건 다 알거다. 이 수업에서 그런 문제가 있었는데, Likelihood 를 sufficient Statistics 를 통해서 간단하게 표현할 수 있고 그에 따라서 빠르게 처리했다는 말을 들었다.

s.s. 가 저렇게도 쓰일 수 있구나... 싶다. 대단! 



# 베이지안과 Frequentist CI

두 CI 의 차이는 뭐.. 베이지안은 sample 을 constant 취급한다음에 모수를 r.v 로 취급해 확률 interval 을 만드는거고 freq 는 모수를 c.t 취급한담에 모수를 contant 취급한다는건데, 이 두 부분에 차이가 있다. 하지만 샘플 수가 커지면 두 ci 는 결국 같아진다고한다~ 흠흠.... 

사실 Sample 이 inf 로 가면 뭐... 웬만하면 Population 을 그냥 맞출 수 있어서 의미가 있나 싶긴 한데 어쩃던 베이지안과 Freq 가 어느정도 연결점 하나는 존재하는구나~ 싶었음. 아래 내용은 Bayes 3번 게시물에 있는 내용~

**Frequentist 와 Bayesian coverage**<br>Freq 일때와 bayes 일때의 VI 가 모두 같을 수 있을까? <br>Hartigan(1966)은 95% Bayesian coverage 는 다음과 같은 property 추가적으로 를 가진다고 하였다.

$$Pr(l(Y) < \theta < u(Y)\mid \theta) = 0.95 + \epsilon_n \ \ (\mid\epsilon_n\mid < \frac{a}{n}, a = \text{for some constant})$$

즉 위에서 $Y$ 가 r.v. 으로 취급되고, $\theta$ 는 constant 로 취급되는 사실에 주목하자. 즉 최소한 assymptotic 하게라도(n을 늘리면 되므로) 95% Baysian coverage 는 95% Frequentist coverage 와 같아진다는 것이다. 이는 베이지안, non베이지안 모두 어짜피 sample 수가 많아지면 같은 CI로 근접함을 나타낸다. 



# Likelihood 의 합이 1일까요~?

답은 아!니!요~ 이다. Likelihood 는 $p(data \mid \theta)$  이다. 이를 모든 data 에 대해 합을 취하면(discrete 일때는 합/ conti 일때는 integral) 1 이겠지만은.. $\theta$ 에 대해서 다르게하면서 합을 취한다는것은 다른의미이다. $\theta$ 의 변화에 따라서 data 가 얼마나 probable 한가를 측정하는것이기 때문에, 그 합은 다른것이다!



# 베이즈에서 Likelihood 의 상수부

사실 베이즈에서는 Likelhood 에서의 constant 가 곱해지는 부분은 의미가 없다. 어짜피 나중에 / 형태가 되게 되면 둘이 없어지니까 상관없슴다!



# 표본분산 공식

아래와 같은 계산식이 유용할때가 있다.. 

$\frac{1}{N-1} \sum_{i=1}^{N}(X_i - \bar{X}) $

$=\frac{1}{N-1}\bigg((\sum_{i=1}^NX_i)^2 - 2\bar{X}\sum_{i=1}^{N}X_i+N\bar{X}^2\bigg)$

$= \frac{1}{N-1} \bigg((\sum_{i=1}^NX_i)^2 - N\bar{X}^2\bigg)$



# Law of iteration

$E[E[X \mid Y]] = E[X]$ 의 간단한 식이다. 하지만 이 의미를 어떻게 알 수 있을까?

아래와 같이 증명할 수 있다. 

![png](/assets/images/{Statistic}/1_2.PNG)

사실 위 이유는 간단하다. $E[E[X \mid Y]]$ 에서 안의 E 는 X 에 대한 expactation 이고, 바깥은 Y 에 대한 expactation 이다. Y 에 대한 Expactation 계산할때, $p(x\mid y)$ 에서 분모가 $p(y)$ 이므로 약분되어서 없어지는것이다!



# 합동 표본분산(pooled variance

두 모비율 차이를 가설검정할 때에 다음과 같이 가설을 세운다.

$H_0 : p_1 = p_2$

$H_1 : p_2 \not= p_2$

이떄에 모비율의 검정통계량은 신뢰구간에서 사용하는 공식과 다르다! 

![png](/assets/images/{Statistic}/1_3.PNG)

그 이유는 다음과 같다. 

![png](/assets/images/{Statistic}/1_4.PNG)

단일 모비율의 경우는 구체적으로 수치를 주기떄문에 검정시에도 크게 문제가 없다.(검정통계량을 구하는 이유는 $H_0$ 을 가정한 상태에서 이 값이 얼마나 이상한지를 검정하는것임을 기억하자!) 하지만 두 표본의 경우에,  각각의 모비율은 CLT 에 의해 Normal 을 따르고 또한, $E[\hat{p_1} - \hat{p_2}] = p_1- p_2$ 이고 $Var[\hat{p_1} - \hat{p_2}] = \frac{p_1q_1}{n_1} + \frac{p_2q_2}{n_2}$ 가 된다. 하지만 이 값을 정확히 알수가 없으므로 추정량  $Var[\hat{p_1} - \hat{p_2}] = \frac{\hat{p_1}\hat{q_1}}{n_1} + \frac{\hat{p_2}\hat{q_2}}{n_2}$ 이 된다. 이때에 '귀무가설에서' $p_1 = p_2$ 이였으므로 공통비율 $p_1 = p_2 = p =\frac{m_1 + m_2}{n_1+n_2}$ 를 사용하게 된다. 그러므로 두 모비율의  차이는 위와 같이 합동표본비율 $p_0$ 을 사용하게 된다. 좀 더 정확한 측정을 통해서 검정력을 높히자는것.



#  신뢰구간과 확률구간(Credible interval)

신뢰구간은 매번 sample 될때마다 달라질 수 있다. 이 안에 모수가 있을 확률이라고 말할 수 없음. 어쩃든 Upper 과 Lower이 r.v 가 되기 떄문이다. 

probability / credible interval 이 확률구간인데, 이 용어를 쓰게된다면 확률변수를 모수로 받아들이기때문에 구간 안에 모수가 들어가있을 확률이 된다. 





# 결정계수와 변수의 수

다음과 같은 regression model 을 생각하여보자. 

$y_i = \beta_0 + \beta_1 x_{1i} + ... +\beta_k x_{ki} + \epsilon _i$

이떄 $R^2 = 1- \frac{SSE}{SST} = 1-\frac{\sum(y_i-\hat{y})^2}{\sum (y_i - \bar{y})^2}$  이 된다. 

이제 약간 화제를 돌려보자. 우리가 $\beta$ 를 fitting 할때 어떻게 할까? $\beta = min_\beta (y_i - X_i \beta)^2 =  min_\beta \sum \epsilon_i ^2 = min_\beta SSE$ 라는 것이다. 즉 이는 원래 beta 를 fitting 할때부터 sse를 최소화 하려고 하는것이다. 이는 X 변수가 많아질수록 SSE 는 무조건 같거나 작아진다는것을 의미한다. 즉 R^2 는 쓰레기 변수를 넣든, 안넣든 작아질수밖에 없다. 



# 검정력과 유의수준

유의수준을 올린다. -> reject region 이 커진다. -> 그에 따라서 검정력이 올라간다. 

(reject region 이 올라가면 당연히 검정력이 올라간다. 그 이유는 검정력의 경우 '귀무가설이 틀릴때 귀무가설을 기각할 확률' 이라는것을 기억하자. 즉! '귀무가설이 틀릴때 데이터가(통계량이) reject region 으로 들어갈 확률' 임을 기억하자. 그러므로, reject region 이 커지면 검정력이 올라간다.)

# 검정력이 영향을 받는요인

1. 유의수준 alpha
   - 유의수준에 따라서 reject region 이 달라진다. 그에 따라서 검정력이 바뀌는것은 당연하다.
   - 유의수준이 올라가면 검정력도 올라간다.
2. Sample size n
   - n 이 올라갈수록 power 도 커진다. 왜냐하면 일반적으로 sample size 가 커지면 그에 따라서 통계량의 분포가 뾰족해지기 때문이다. 그에 따라서 우리의 통계량이 어느 분포에서 왔는지 판단하기가 더 쉬워진다. 
   - 뭉툭한 2개의 distribution 을 생각해보자. 두 distribution 이 겹쳐있는 구간은 어느정도 probability 가 높아서 H_1 분포에서 온 통계량인지 / H_0 분포에서 온 통계량인지 말하기가 매우 힘들어진다. 
   - 하지만 그에 반해서 2개의 뾰족한 distribution 을 생각해보자. 두 통계량이 겹쳐있는 구간은 매우 적다. 그러므로 H_0 에서 온 통계량인지 / H_1 분포에서 온 통계량인지 말하기가 어느정도 쉬워진다

3. response variable 에 내재된 variance
   - 이게 무슨의미냐면, 우리가 사람들의 소득에 대한 모델을 짜고싶고, 그에 따라서 test statistics 를 Mean 으로 정의했다고 하자. 이 떄에 사람들이 소득에 대해서 제대로 답하려하지 않는다고 해보자. 그러면 우리가 가지고있는 값에 대한 변동성 자체가 있다는뜻이고 (Measurement error) 그에 따라서 검정력 자체가 작아질 수 있다.
4. hypothesis value of parameter 와 진짜 값의 차이
   - 진짜 값이라고 해서 약간 Frequentist 적인 서술이 되었지만 우선 여기서는 이렇게 언급한다고 하자.
   - 차이가 클수록 검정력이 크다. 



# Bonfferroni

우리는 어떠한 가설을 검정하기 위해서 실험을 진행한다. 하지만! 실험이란게 비용이 발생하는거라서 한번 할때마다 여러개의 귀무가설을 묶어서 실험하면 어떨까라는 생각이 들 수 있다.

하지만 이럴 경우 하나 이상의 metric 이 틀릴 확률이 높아진다. 예시 하나를  들어보자. 각각의 알람시계가 고장률이 매우 낮다고 하자. 출근시간을 맞추기 위해서 1개의 알람시계를 사용할때에는 고장률이 낮아서 믿음직하다. 하지만 10개를 사용한다면 되려 1개 이상 고장나있는 알람이 있을 확률이 높다! 

그러므로 위의 경우 어떻게 해결하냐면, 각각의 알람 시계에 대한 신뢰수준을 높혀버린다. 이렇게 되면 각각 알람시계가 고장날 확률이 매우 적으므로, 어느정도 상쇄가 된다. 이걸 해주는게 Bonfferoni 임.



# effect size

<https://www.statisticssolutions.com/statistical-analyses-effect-size/>

effect size 는 통계학적인 정의로, 두개의 그룹에 대한 차이를 정량화 한 것이다. 예를 들어서 남/녀의 키를 비교하였다고 해보자. 두 그룹의 분포 차이가 명확할 때에(남자키 평균과 여자키 평균의 거리가 매우 멀거나.. 등등) effect size 가 크다고 한다. 

하지만 '두 분포가 다른 정도' 를 어떻게 measure 할 수 있을까? 이 방법은 여러가지가 있다. 

1. pearson r correlation
   - 두 그룹의 형성을 체크한다. 
   - 이 값이 크다면 두 분포는 선형적으로 '비슷' 한 것이다.

2. standard mean difference
   - $\frac{\mu_1 - \mu_2}{\sigma}$
   - 두 그룹의 mean 을 std 로 정규화 한것. 하지만 일반적으로 population parameter 를 알 지 못하므로 아래 공식을 많이 사용한다.
3. cohen's d effect size 
   - $d = \frac{\bar{x_1} - \bar{x_2}}{s}$



