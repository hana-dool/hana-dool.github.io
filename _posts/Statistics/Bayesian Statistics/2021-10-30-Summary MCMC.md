---
title:  "Summary of MCMC method"
excerpt: "MCMC 방법론에 대한 Summary"
categories:
  - Bayes
last_modified_at: 2021-10-30
date : 2021-10-30 12:00:00 +0900

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 이전 글에서는 MCMC 를 너무 전문적(?) 으로 알아본탓에 이해가 약간 어려울 수 있으것같은데요, 여기에서는 좀 쉽게 알아보도록 하겠습니다. 
{: .notice--warning}

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## Markov Chain property

![png](/assets/images/Stat/88_1.png)

- Marcov chain 은 다양한 property 가 존재합니다. 

> Transition proability 

- 이전에 $A_i$ 에 위치할때에 $A_j$ 로 이동하는 확률을 $p_{ij}$ 로 설정합니다. 이러한 확률값을 transition probability 라고 합니다. 

> Memoryless propery 

- 이는 한마디로 하면 '다음 Step 은 오로지 현재 Step 의 영향만 받는다.' 가 됩니다. 

> Time homogenouos 

- 시간이 언제든지 상관 없이 확률값은 일정하다는 것입니다. 
  - 즉 t 가 어떻든지 $A_i \to A_j$ 의 확률은 같다는 것입니다. 

> irreducible

![png](/assets/images/Stat/88_2.png)

- irreducible 위의 상단 그래프처럼 '특정한 Cycle 에 빠져서 다른곳으로 못 가는 상황' 이 없는 상황입니다.
  - 즉 위의 하단 그래프와 같이 같이 충분한 시간이 지나게 되면 특정한 위치에서 어느 위치로든지 갈 수 있을때 irreducible 이라고 합죠

> aperiodic

![png](/assets/images/Stat/88_3.png)

- 이는 주기성이 없는 상태를 말합니다. 
  - 상단 그래프의 경우는 (edge 는 양방향으로 갈 수 있습니다.) $A_1 ,A_2, A_3,A_4$ 모두 시간이 얼마나 지나던지 자기 자신으로 돌아오려면 짝수번 움직여야 합니다. 즉 periodic
  - 하단 그래프의 경우는 $$A_1,A_2,A_3,A_4$$ 모두 오랜 시간이 지나고 나서는(let T) T +1 , T + 2. ...... 번 움직였을떄 자기 자신으로 돌아올 수 있습니다. 즉 자기 자신으로 돌아오기 위한 경로의 수의 gcd 가 1이므로 aperiodic 

> Reccurent 

$$P(\xi_n = j \ for \ some \ n\ge 1 \mid \xi _0 = j) = 1$$

- 위와 같이 언젠가는 자기 자신으로 돌아올 수 있을때에 Reccurent 라고 합니다.

> Positive reccurent 

$$m_i = \sum n f_n (i \mid i ) < \infty (mean \ reccurent \ time)$$ 

- 위처럼 '언젠가 자기 자신으로 돌아올 시간의 기댓값은 유한하다는것을 의미합니다.

> Erogodic

- state space가 유한하고, homogeneous한 이산형 마코브 체인에 대하여,

1.  Reccurent + Positive Reccurent (즉  $$^\forall i,j \in S, \;^\exists m<\infty \quad s.t.\quad p(X_{n+m}=j|X_n=i)>0 $$ )
2. 모든 상태의 주기가 $d(i)=1$ 이면(aperiodic) (혹은$^\exists n \quad s.t.\quad p_{ij}^{(n)} > 0 \quad ^\forall i,j\in S$ )

> ## MCMC porperty 

![png](/assets/images/Stat/88_4.png)

- 우리가 다루기 힘든 target distribution $p(x)$ 가 있다고 합시다. 
- 이를 다루기 위하여 markov chain $p_{ij}$ 를 만들고, 이를 Simulation 하면 이러한 분포는 다시 $p(x)$ 에 근사하게 됩니다.
- 즉 우리는 Markov chain 을 만들어야 합니다.
  - 이러한 Markov chain 은 transition probability 와 1대 1 대응이 되므로, 결국 Transition probability matrix 를 잘 만드는것이 우리의 과제가 됩니다.

![png](/assets/images/Stat/88_5.png)

- 하지만 markov chain 에 대해서, 

> Invariant measure

- $\mu = \sum \mu_j \delta_j$ 가 모든 $n\in \mathcal{N} , J \in S$ 에 대하여 아래 조건을 만족하면 invariant probability measure of a time homogeneuos Markov chain $\xi _n$ 이라고 합니다.

$$\sum \mu_i = 1 , \sum p_n (j\mid i) \mu_i = \mu_j(\mu P = \mu)$$   

- 즉 , 특정한 확률 matrix 에 대하여 장기적인 Equiliirium 이 존재한다면 그러한 상태를 Invariant measure 라고 부르게 된다는것이죠.

> Find mu

- 이러한 mu 를 정의를 하였지만 이를 구하는것은 매우 귀찮습니다. 

![png](/assets/images/Stat/88_6.png)

- 위와 같이 정의하게 되면 limiting 으로 보낸 $\pi$ 는 invariant measure 의 조건을 만족하게 됩니다. 

> Example 

![png](/assets/images/Stat/88_7.png)

- 위와 같이 정의를 하게되면 우리는 limiting distribution 이 $\mu$ 로 근사하게 된다는것을 알 수 있습니다. 
  -  즉 우리가 정한 Transition Probability 의 limiting distribution 이 $\mu$ 가 되게 만든것이죠

> Summary

![png](/assets/images/Stat/88_8.png)

- 우리는 알 수 없는 Target distribution P 를 마르코프 체인 $p_{ij}$ 을 이용하여 근사하고자 합니다.
- 이떄에 각각의 Markov chain 은 invariant measure (장기적인 평형상태) 가 존재하는데, 이게 Target distribution 과 같기를 원합니다.
- 그런데 이떄에 Regular 라는 조건이 있으면 , markov chain 의 limiting distribution $\pi$ 은 Target 과 같아집니다.
- 그러면 Markov 를 가지고 Sampling 을 하면 우리의 Target disribution 에 근사가 됩니다. 

> stationary distribution

 ![png](/assets/images/Stat/88_9.png)

- 위처럼 막 움직이는 Markov chain 에 대하여 극한의 확률 상태를 $\pi$ 라 합니다.
- $M^T \pi = \pi$ 의 의미는, 바로 eigen value 가 1일때 $M^T$ 의 eigenvector 라는것을 쉽게 알 수 있습니다.

 ![png](/assets/images/Stat/88_10.png)

- 위와 같이 , stationary distribution 의 해석은 '전체적인 평형상태' , 즉 들어오는 inflow 와 나가는 inflow 가 일치하는 양이 같은 상태를 의미합니다.

> Global balance

![png](/assets/images/Stat/88_11.png)

- 위처럼 인구의 이동 비율을 마치 확률로 취급하고 살펴보겠습니다.
- 모든 지역의 유입 / 유출이확률이 똑같아서 평형상태(변하지 않음) 라고 할 수 있습니다.

![png](/assets/images/Stat/88_12.png)

- 하지만 위와 같은 경우 '평형' 이 각각이 locally 하게 맞지가 않고 있습니다.
  - 마포 ->종로 는 0.10 이나, 종로 -> 마포는 0.09 
  - 마포 -> 여의도는 0.05 이나 여의도 -> 마포는 0.06

- 이것으로 Simulation 을 하게 된다면 정적(Stationary) 이라고 하기에는 살짝 찜찜.. (?)

> Detailed balance

![png](/assets/images/Stat/88_13.png)

- 위처럼 모든 도시에 대해서 들어온 인구와 나간 인구가 완전히 같은 경우를 Detailed Balance 라고 합니다.
  - 당연히 이러한 Detailed balance 를 만족하면 Global balance 를 만족하게 됩니다.
- Detailed balance 를 만족하면 $\pi$ 를 다루기가 매우 쉬워집니다.

> Example

![png](/assets/images/Stat/88_14.png)

- 위 그림과 같이 왼쪽의 Model 에 대한 $\pi$ 를 계산한다고 합시다. 
- Detailed balance 조건을 만족하다면 오른쪽 그림과 같이 $\pi$ 에 대해서 식들이 쉽게 도출됩니다.

![png](/assets/images/Stat/88_15.png)

- 그리고 $\pi_0 = 1$ 이라고 가정한뒤, 연쇄적으로 모든 $\pi_i$ 의 값을 구한뒤, $\sum \pi_i=1$ 의 조건을 이용하여, Normalizing 하게 되면 우리는 쉽게 $\pi$ 를 계산할 수 있게 됩니다. 
- 이떄 만약 Gloabal 한 상황이였다면 $M^t \pi = \pi$ 를 구하기 위해서는 모든 n 차 연립방정식을 사용해야 되기 떄문에 엄청 어려웠을 것입니다.

> ## Summary

![png](/assets/images/Stat/88_16.png)

- Target distirubiotn 을 Stationary distribution ($\pi$) 으로 가지는 Markov chain 을 정의한 다음에 , 이러한 chain 에서 sampling 을 하면 target distribution 으로 근사합니다.
- 하지만 이러한 invariant measure 에 대해서 다양한 markov chain 이 존재합니다.
  - 이 중에서 편한 markov chain 을 만드는게 계산상 유리 
  - 그래서 detailed balance , regular 를 만족하는 좋은 markov chain 을 만드는게 핵심
  - 이를 구현하는 markov chain 은 깁스샘플러 , 헤스팅 등 여러가지 방법론이 존재하는것입니다.

# [Various Markov Chain](#link){: .btn .btn--primary}{: .align-center}

![png](/assets/images/Stat/88_17.png)

- 위와 같은 경우 (1) (2) 와 같은 경우 어찌저찌 해를 구할 수 있겠지만, (3), (4) 의 경우는 하나의 Analytic 한 해를 얻기가 겁나 어려움
  - 참고로 (4) 는 Logistic function 의 Closed Form 입니다. 
- MCMC 를 왜 하느냐 ! 하면 이러한 해들을 구하고 싶으니까! 와 같은 맥락으로 이해하시면 좋습니다. 

![png](/assets/images/Stat/88_18.png)

- 위처럼 Freq 와 Bayesian 의 경우 '원하는 해' 가 다름
  - Freq 는 Lieklihood 의 최대화 해를 찾는것이 목적
  - Bayes 는 Posterior 를 구하는것이 목적 
- 위와 같은 경우, '해를 구하는것' 이기 떄문에 수치해석적인 계산이 많이 들어가게 됨

![png](/assets/images/Stat/88_19.png)

- 위와 같이 Posterior 의 적분식을 보더라도 엄청나게 끔찍함... 여기에서 어떻게 Normalizing term 을 구할 수 있는가? 
  - 불가능! 

> ## Matropolis hasting

- posterior distribtion 을 알고싶은 상태 ! 이를 $g(\theta)$ 라고 합시다. 
- 이떄에 posterior distriution 과 '비례' 하는 함수를 정의합니다. 
- proposal distribution 을 선택합니다. $h(\theta ' \mid \theta)$
  - 물론 어떠한 distribution 함수도 가능 

![png](/assets/images/Stat/88_20.png)

- 위와 같이 계산하게 됩니다. 하지만 이때에 h 함수의 경우 $h(\theta_0 \mid \theta ') = h(\theta ' \mid \theta_0)$  이라면 계산이 매우 쉬워집니다. 
- 또한 $g$ 가 확률 계산시 '비율' 로 계산된다는것을 기억합시다.
  - 즉 posterior 의 정확한 Normalizing constant 는 계산하지 않으셔도 되겠죠! 

![png](/assets/images/Stat/88_21.png)

- 그래서 우리는 Proposal distribution 을 일반적으로 대칭의 분포를 가지게 합니다. 

> Procedure in general

![png](/assets/images/Stat/88_22.png)

- 이떄에 우리는 Markov chain 이 과연 진짜 '수렴할까?' 가 궁금합니다. 
- 이러한 이유를 다음과 같이 알아볼 수 있습니다. 

![png](/assets/images/Stat/88_23.png)

> MH algorithm

![png](/assets/images/Stat/88_24.png)

- 우리가 점을 따다다닥 찍을텐데, 위와 같은 원(빨간색)의 둘레 분포를 sampling 하고자 할때에 어떻게 하면 효과적으로 할 수 있을까요? 
  - 즉 어떠한 proposal distribution 을 선정해야 효과적으로 MCMC 를 할 수 있을까요? 
- 즉 reject 되는 부분을 없애면 되지 않을까요? 
  - 효과적으로 하기 위해서는 바로 posterior 가 proposal 이 됩니다. (물론 이것은 순환오류..)

> when using?

![png](/assets/images/Stat/88_25.png)

- 우리는 MCMC 는 복잡한 posterior를 알 수 없을떄에 사용하게 됩니다.
  - 물론 target distribution 이 posterior 에 가깝게 하면 효율적인 알고리즘이 되지만, 그렇게 할 수 없기 떄문에 대부분 대칭인 Normal 분포를 쓰게 됩니다. (많은것들이 Normal 을 따르니까...)

> ## Gibs sampling

- 이것또한 MCMC 의 특수한 케이스임 
- proposal distribution 을 one dimension 에서한 한 경우입니다. 
  - 즉 한 방향으로만 한것 

> ## Hamiltonian Monte Carlo

- gibs 는 차원별로 정햇던 방식이라면 
- Hamiltonian 은 관성에 따라서 쭈우욱 간 뒤에 Accept 를 할지 말지를 결정합니다. 
  - 보면 갔다가 다시 꺾이고, 원위치로 오는 경우가 생김 (시간낭비 / 돈낭비)

> ##  NUTS

- 처음에 시작햇던 방향에 대해서 U turn 하지 않고 꺾이는 순간 알고리즘이 끝남..

https://chi-feng.github.io/mcmc-demo/

- 여러가지 알고리즘이 있지만 웬만하면 NUTS 까지로 구현되고 있습니다. 

> ## More...

- 베이지안의 MCMC 는 Freq 의 BOotstrap 과 매우 비슷
- Uncertainty 를 얘기하려면.. 결국 분포를 말해야합니다. 
  - 한쪽에서는 이러한 답을 통계량과  통계량의 분포로 말하게 됩니다.
  - 베이즈는 모수와 모수의 분포로 말하게 됩니다. 
- 위를 아는게 사실 통계학의 주 목적임.
- 수학을 알지 않더라도.. 사실 Bootstrap 만 졸라게 한다거나, MCMC 를 졸라게 하면 나오기는 하죠..
  - 하지만 문제는... 시간 + 비용이 많이 들고.. 할수 없는일도 있음
  - 회귀 분석을 할떄 2^p 개의 모델에 대해서 모든 모델을 다 알아야하는데... (모델선택시) 중간 단계를 스킵하기 위해서 근사적으로 구하는것들 (극한분포) 을 이용해서 구하기도 함...

---

**Reference**

- <https://www.youtube.com/watch?v=THx1ka9KWog>

MCMC 에 대해서 한번 훑어서 알아보았습니다. 한번 훑어볼때에 보기에 딱 좋은 수준인것 같습니다.
{: .notice--success}

