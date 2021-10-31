---
title:  "MCMC Method Practical comparison"
excerpt: "MCMC 에 대한 다른 방법론들에 대한 비교"
categories:
  - Bayes
last_modified_at: 2021-10-30
date : 2021-10-30 10:00:00 +0900

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 MCMC 방법론에 대해 비교해 보고, 어떤게 좋을지에 대해서 좀 조사해봅시다.
{: .notice--warning}

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## Gibbs Sampling 

> Pros

- joint dist는 바로 그리기엔 복잡할 수 있지만, 조금 덜 복잡한 conditional dist에서 바로 sampling을 할 수 있음
- conditional dist가 joint dist에 비해 낮은 차원을 가지고 있고, 다른 sampling 기법들을 적용하기에 더욱 알맞을 수 있음

> Cons

- Gibbs sampler를 쓰기 위해선 각각의 변수들에 대한 posterior conditional들을 찾을 수 있어야 합니다.
- 변수들간의 correlation이 증가할 수록 Gibbs sampler의 성능은 떨어짐
- conditional dist를 뽑아냈어도 알려진 형태가 아닐 수 있기에 이를 기반으로 그림을 못 그릴 수도 있음
  - Known form 의 분포가 아닐경우에는 하기 힘들다고 한다.
- 여러개의 conditional dist에서 뽑아내 그리는 것이 느리고 비효율적일 수 있음
  - Variavble 이 여러개면 그리는것도 힘들고 (변수가 많아서...)

> ## MH Algorithm

> Pros

- 적용하기 매우 간편함, condtional dist를 결정할 필요가 없음
- correlation이 높거나 고차원의 분포들로부터도 괜찮게 sampling이 가능함

> Cons

- step size $\sigma$가 너무 크면 reject되는 sample이 많아짐, 반면 $\sigma$가 너무 작으면 매우 적은 step을 만들어서 분포를 explore하는데 긴 시간이 걸리게 됩니다. $\sigma$에 민감함)
  - $\sigma$ parameter 를 잘 정의해야 한다는거...
- 고차원의 공간에서는 MH 알고리즘의 Random-walk 성질 때문에 그 공간을 매우 비효율적으로 돌아다님
  - 즉 무작위로 돌아다녀서... 
- isolated local minimum들 사에에 있는 긴 거리 $\sigma$ 보다 매우 큰)를 돌아다닐 수 없음 
  - 그러므로 multi-modal dist에서 조금 힘든 경우가 생길 수 있습니다.

> ## Hamiltonian Monte Varlo

- 하나의 iteration을 하는 데에 드는 '비용'이 더 높지만, 그럼에도 불구하고 HMC는 더 효율적임

- 대부분의 new state를 accept함 
- 여전히 isolated local minumum들이 있는 분포에서 sampling 하는 것은 어려움
  - 여전히 isolated 된 상황에서는 별로 안좋음...

> Pros

- $\tau, \epsilon$ 을 잘 세팅한다면 매우 효율적임 
- 연속적으로 생성되는 점 사이의 거리가 보통 크기 때문에, representative sampling을 얻기 위해 드는 iteration 수가 적음

> Disadvantage 

- $\tau, \epsilon$ 을 세팅하기가 어려움 
- Local 한곳을 Explore 하는것은 괜찮으나 Multimodal 인 경우에는 별로 좋지는 못함
- gradient도 함께 사용함 -> gradient가 존재하는 케이스에만 활용할 수 있음

> ## No U Turn Sampler

- Hamiltonian Monte Carlo 알고리즘의 변주
- HMC가 desired number of steps parameter L ($\epsilon$ 은 step size parameter) 에 의존하는 것을 없애주면서 여전히 HMC처럼 독립적인 sample들을 효율적으로 만들어냄
- Matthew D.Hoffman et al.(2014) 
- ,**The No-U-Turn Sampler: Adaptively Setting Path Lengths in Hamiltonian Monte Carlo**

---

**Reference**

- [https://chi-feng.github.io/mcmc-demo/](https://chi-feng.github.io/mcmc-demo/)
- <https://arogozhnikov.github.io/2016/12/19/markov_chain_monte_carlo.html>
- <https://towardsdatascience.com/can-you-do-better-sampling-strategies-with-an-emphasis-on-gibbs-sampling-practicals-and-code-c97730d54ebc>

위와 같이 엄밀한 확률의 정의를 통하여, 확률 공간이 무한할떄의 역설을 해결하였고, 학문으로서의 기초를 다졌습니다.
{: .notice--success}

