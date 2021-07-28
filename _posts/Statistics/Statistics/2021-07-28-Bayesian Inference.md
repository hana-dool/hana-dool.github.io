---
title:  "Bayesian Inference"
excerpt: "Large Sample 과 CLT"
categories:
  - Stat
tags:
  - 1
last_modified_at: 2021-07-28

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

#  1. 베이즈와 Freq 의 차이

- Frequantist 와 베이즈는 기본적으로 확률을 대하는 태도부터 차이가 납니다. 
- Frequentist
  - Freq 는 어떠한 사건의 확률을 긴 시간동안 발생하는 빈도 라고 정의합니다.
  - 즉 Frequentist 는 확률을 하나의 고정된 값(Long term Frequency)이라고 가정하고, 그에 따르는 에러가 존재한다고 생각랍니다.
  - 어떠한 모수에 대해 95% 신뢰구간을 형성할 떄에 그 신뢰구간 안에 '모수' 가 들어갈 확률이 95% 라는게 아니라, '신뢰구간을 무수히 형성할 때에' 모수가 신뢰구간 안에 들어갈 Long term Freqancy 가 95% 라는 뜻입니다.
- Bayesian 
  - 하지만 베이즈 입장에서 확률이란 그저 '주관적인 믿음의 정도' 입니다. 
  - 이러한 Framework 에서는, 모수는 '정답' 이 없으므로 주관적인 분포로 나타납니다.

<br>

# 2. Goal Of Bayesian Inference

- Bayesian Inference 의 목표는 '내 믿음을 잘 표현하는' Prior 를 만든뒤, 데이터를 활용하여 Poseterior 로 업데이트 하는것입니다. 

# 3. Bayesian , Freq CI

- 베이즈 Frame Work 에서 우리가 데이터를 업데이트 하여 Posterior 를 형성하고 나면 Credible Set 을 만들 수 있습니다. 

![png](/assets/images/Stat/18_1.png)

- 여기서 잘 봐야할것은 위에 randomness 가 theta 에 걸려있다는 것입니다. 
- 그리고 데이터는 Given 된 상태입니다. 
- 즉, 위 Credible Interval 은, 데이터가 주어진 상태에서, 우리의 '모수' 가 주어진 구간에 속할 확률입니다. 

![png](/assets/images/Stat/18_2.png)

- 위의 경우는 Frequentist 의 CI 입니다. 
- 여기서 잘 봐야하는것은 Randomness 가 L 과 U (즉 데이터) 에 주어져있는것을 볼 수 있습니다.
- CI 는 '데이터의 함수' 로서 , '고정된 모수를 포함할' 확률이 95% 일때 95% CI 라고 하는것입니다. 

<br>

# 4. Frequentist View

- 빈도론자는 추정량에 대해서 "Consistency" 와 Rate of Convergence 를 중요시 합니다.
  - The rate of convergence **quantifies how fast the estimation error decreases when increasing the sample size n** .
  - <http://www.dliebl.com/RM_ES_Script/estimation-theory.html>
- 하지만 베이즈에도 이러한 것이 있을까 궁금할 수 있습니다. 
- 베이즈에는 바로 Posterior Contraction 이라는것이 존재합니다. 

![png](/assets/images/Stat/18_4.png)

- 위와 같이, 베이지안의 경우에도 Consistency 와 rate of Convergency 를 정할 수 있습니다. 

<br>

# Bernstein-von mises Thm

![png](/assets/images/Stat/18_5.png)

- 위 정리를 요약하자면, Posterior 는 결국 Normal 에 근사한다는 이야기입니다. 

![png](/assets/images/Stat/18_10.png)

- https://www.cemfi.es/~arellano/bayesian-inference.pdf

- 다시 말하면 위와 같습니다.

- 이는 아래의, Frequentist 에서의 MLE 근사와 매우 비슷합니다.

![png](/assets/images/Stat/18_5.png)

- 연세대 수리통계학(2) 강의노트 - MLE 부분(Refer)

- 즉, 95% CI interval 을 Probabiliy Interval 로 해석할 수 있다는 의미입니다.

![png](/assets/images/Stat/18_7.png)

- https://users.nber.org/~confer/2007/si2007/WNE/Slides7-31-07/slides_7_bayes.pdf
- 위와 같이 Frequentist 의 Confidence Interval 과 Bayes 의 Probability Interval 이 같아집니다.

![png](/assets/images/Stat/18_8.png)

- https://www.cemfi.es/~arellano/bayesian-inference.pdf

- 즉 위와 같이, 이는 Large Sample 에서는, Posterior 가 결국 Normal 로 가므로,  Prior 가 크게 상관 없다는 이야기이도 합니다.

![png](/assets/images/Stat/18_9.png)

- 위에서와 같이 n 이 커질때에 mle 에 대한 inference 는 같아집니다. 
  - 그 차이는 , '통계량에 대한 분포' 를 말한다면, Freq 가 되고, 모수에 대한 분포를 말한다면 Bayes 가 되는 차이 뿐입니다.

- <https://eml.berkeley.edu/choice2/ch12.pdf>

- <https://www.ejwagenmakers.com/2008/BayesFreqBook.pdf>

<Br>

# Mean Inference And CLT

- 위의 정리가 이용되는 부분은 아래와 같습니다.

![png](/assets/images/Stat/18_11.png)

- https://ocw.mit.edu/courses/mathematics/18-443-statistics-for-applications-fall-2006/lecture-notes/lecture3.pdf

- 위와 같이 'Mean' 에 대한 MLE 를 형성해 Assymptic Normal 을 형성해 보면, CLT 와 같은 형태임을 알 수 있습니다.
- 이는 Mean Inference 를 할 떄에
  - Freq :  'CLT' 를 이용하여 Z 검정하는 것
  - Bayes : Prior 을 이용해 Posterior 로 검정하는것 
- 두개는 결국 '같은것을 바라본다' 라고 할 수 있습니다! 
  - Freq : 통계량의 분포를 이용해서, p-value(대립가설쪽의 확률) 이용해야지! 
  - Bayes : 모수의 분포를 이용해서, 모수의 대립가설쪽의 확률을 이용해야지! 
- 즉 위 결론은 2 - Sampe 일때에도 이어질 것입니다.

<br>

# 2 Sample Test With CLT and Bayesian



# Refer

- <https://bjlkeng.github.io/posts/normal-approximations-to-the-posterior-distribution/>

  
