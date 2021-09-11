---
title:  "Frequentist VS Baysian"
excerpt: "빈도통계와 베이즈의 차이"
categories:
  - Stat
tags:
  - 1
last_modified_at: 2021-06-27

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# <center><font size="10">Intro</font></center>

![png](/assets/images/Stat/3_1.png)

- 베이즈 통계와 Frequentist 통계의 차이를 체계적으로 알아봅시다. 

- 두 방법론 모두 데이터를 이용해 우리 가설에 대한 판단을 할 수 있도록 도와줍니다. 

<br>

# <center><font size="10">Overview</font></center>

![png](/assets/images/Stat/3_2.png)

- 베이즈 정리 그 자체는 사실 예전부터 있던 정리입니다. 
- 중요한것은 그 정리를 '통계적 추정에 이용' 하였다는것이 매우 중요합니다. 
- 먼저 위 사진과 같이 $P(H\mid D)$ 를 정의합니다. (H 는 가설/ D 는 data)

![png](/assets/images/Stat/3_3.png)

- 베이즈 통계에서는 불확실성을 분포를 통해서 해결합니다. 
  - Prior 을 주관적으로 선택해야 되는 문제가 있습니다. 
  - 가설(모수)과 데이터에 대해 Probability 를 줍니다. 
  - prior 와 observed data 의 Likelihood 의 영향을 받습니다. 
  - 적분떄문에 계산량이 매우 많습니다.

- Freq 통계에서는 모수가 고정되어있다고 생각합니다. 
  - 가설에 대해서 분포가정을 절대 하지 않습니다. (고정된 값이기 때문)
  - 20 세기 통계학의 주류 
  - 계산량이 적은편입니다. 

<br>

# <center><font size="10">비판</font></center>

## 베이즈 통계에 대한 비판

![png](/assets/images/Stat/3_4.png)

- 베이즈 통계에서 항상 비판받아온것은 "Prior" 선택시에 사람의 주관이 들어간다는 것입니다. 
- 게다가 가설에 확률을 주는 (즉 모수가 정해져있는 값이 아니라 확률분포..?) 것은 거부감이 있었습니다.
  - Long term Frequency 를 관찰할 수 있는 실험 (동전던지기로 앞면 나올 확률을 재는 실험 등.) 에 대해서는 실험할수록 앞면의 확률이 안정적으로 수렴할것입니다.
  - 즉 '앞면이 나올 확률(모수)' 가 Constant 하다는 것이라 볼 수 있습니다. 
- 또한 베이즈통계에서는 '가설' 도 결국 맞다 틀리다가 아니라 '맞을 확률이 얼마다~' 라는식으로 해석합니다.
  - 하지만 이는 직관에 매우 반대됩니다. 동전은 '공정하던지/ 공정하지 않던지' 2가지 아니겠습니까? 

## 베이즈 통계에서 방어

![png](/assets/images/Stat/3_5.png)

- 가설에 대한 확률만 있어도 우리가 가설에 대한 결정을 내리는데에 충분하다. 
  - 또한 어려운 p-value 등을 이용한 communcation 보다는 베이즈처럼 '직관적인 확률' 을 이용한 communication 이 더 쉽다.
- 베이즈 정리는 매우 수학적으로 엄밀하다. 우리가 사용한 수학공식은 베이즈 룰 뿐이며 이는 전혀 문제될 일이 없다. 
- prior 의 선택을 달리 해봄으로서 우리의 결과가 prior 에 얼마나 민감한지 시험해 볼 수 있다. 
- 데이터가 오는대로 즉시즉시 사용할 수 있다. Frequentist 방법처럼 사전에 정의할 필요가 없다.

<br>

## Freq 통계에 대한 비판

![png](/assets/images/Stat/3_6.png)

- p-value 는 실험의 setup 에 크게 의존한다. (아래의 stopping rule 참조)
- 실험이 이전에 미리 계획되어야 한다. 
  - 이는 voltmeter story 같은 paradox 를 만든다. 
- p-value 와 CI 는 오해하기 매우 쉽다.
  - p-value 가 5% 라는것을 사람들은 귀무가설이 틀릴 확률이 5% 라고 착각한다. 

<br>

## Freq 통계에서 방어

![png](/assets/images/Stat/3_7.png)

- p-value 는 모든 통계학자들이 동의하였다. 즉 이를 사용해도 될 것이다.
- Freq 의 Hypothesis Testing 은 귀무가설에 대해서 얼마나 반대되는 Evidence 를 가지고 있는지를 평가한다. 
  - 사실 이 결과에 대한 해석은 순전히 사용자의 몫이다. 1종오류 , 2종오류를 조절하며 선택하는것은 사용자가 해야한다.
  - Freq 통계는 '결정' 의 기준을 제시한다기 보다는, Type 1 , Type 2 에러의 Trade off 에 대해서 말할뿐이다. 

<br>

# Stopping Rule

## Freq

![png](/assets/images/Stat/3_8.png)

![png](/assets/images/Stat/3_9.png)

- 우리는 실험을 할때에 아래와 같이 2개의 Rule 을 통상적으로 이용합니다.
  - 1.정확하게 N 번의 Trial 을 하고 멈추기
  - 2.특정한 결과값이 나올때까지 시도하고 멈추기
- 위의 Sampling Scheme 은 p-value 에 영향을 끼칩니다.  
- Coin toss example 에서 다음과 같이 실험을 진행해 봅시다.

> Experiment1 : 정확히 6번 던지고 데이터를 기록
>
> Experiment2 : 뒷면이 나올때까지 던지고 그 데이터를 기록

- 위 실험의 결과로 똑같이 HHHHHT 의 데이터를얻었다고 합시다. 이 경우 p -value 는 다른 값을 가집니다. 
- 가설을 $H_0 : \theta = 0.5$   , $H_1 : \theta >0.5$ 로 두고 p-value 를 계산하면 
  - 1번실험 : 0.1094 
  - 2번실험 : 0.0313
- 즉 2번실험과 1번실험에서의 결론이 다르게 됩니다 

<br>

## Bayes

![png](/assets/images/Stat/3_10.png)

- 베이지안의 경우는 약간 다릅니다. 

- 위 두 실험이 어떻게 행해졌는지는 베이즈의 관심사가 아닙니다. 왜냐하면 HHHHT 에 대한 likelihood 는 binomal 과 geometric 의 경우 모두 proportional 하기 떄문입니다. 

  - geometric : $(1-p)^5 p$
  - binomial : $\binom{6}{5} (1-p)^{5}p$

  - posterior 추정시 parameter 만 이용하게 되므로, 둘은 결국 일치한다고 볼 수 있습니다.

- beta(3,3) 의 사전분포에 대해서, 두 데이터는 모두 같은 Posterior 를 나타나게 됩니다. 
- 이 경우, 0.89 로 coin 이 Biased 라고 결론내리게 됩니다. 

<br>

# Decision

![png](/assets/images/Stat/3_11.png)

- 우리는 통계적 추론을 이용하여 현실적인 문제에서 결정을 내리려 합니다. 
- 이 경우 이용되는것이, '각 행동' 마다 Weight 를 주는것입니다.

>예시로, 투자로 100만원을 버는 '행동' 에는 100만이라는 Weight 를 주고, 10만원 손실에는 -10만 이라는 Weight 를 줄 수 있습니다. 

- 위의 weight 아 합쳐져서, 우리의 Decision rule 이 결정됩니다.

## Freq

- $E[U\mid H]$ 를 고려하게 됩니다. (U 는 Weight 값으로서, Utility 라고 합니다.) 
  - 가설 H 를 가정하였을떄에 기대되는 Weight 값입니다.
  - 위 투자 예시에서 보자면 이경우 $E[U\mid H] $ 는 기대되는 투자 수익이 될것입니다. 
- 그리고 이 경우 Expected Weight 값과 p-value 를 엮어서 추론하게 됩니다. 

## Bayes

- 베이즈 방법론에서 또한 $E[U\mid H]$ 를 고려하게 됩니다.
  - 하지만 이 경우 Expectation 을 구할때에 H는 Poseterior 로 추정되는  '확률변수' 가 되기 떄문에, Expectation 을 구하는것은 integral 이 들어가 살짝 어렵습니다. 







