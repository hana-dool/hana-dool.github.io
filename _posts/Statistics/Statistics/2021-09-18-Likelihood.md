---
title:  "Likelihood and Probability"
excerpt: "Likelihood 와 확률은 대체 뭐가 다른거야?"
categories:
  - Stat
last_modified_at: 2021-09-18

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 개인적으로 , 제가 면접관이라면 물어볼거라고 생각되는것중에 하나입니다. Likelihood 와 Probability.. 솔직히 생긴것은 똑같거든요. 대체 왜 두개를 구분하는것이고, 어떤 차이가 있는지 알아봅시다!
{: .notice--warning}

# [Probability And Likelihood](#link){: .btn .btn--primary}{: .align-center}

> ## Probability And Likelihood

- 우선 확률은 당연히 빈도론자 (또는 현대 통계학의 일반적인 정의) 하에서 생각합시다. 
  - 베이지안 입장에서 생각하면 확률은 그냥 '주관적인 확률~' 이라고 퉁쳐버리고 끝나는거라서요 

> 확률은 주어진 모델 파라미터값에 대해서 데이터가 관측될번한 가능성이다. 

- 확률이 어떻게 표현되는지 살펴봅시다. 

$$f(x\mid \theta)$$

- 위처럼, population 이 고정되어 있는 상태 (즉 theta 가 고정되어 있는 상태) 에서 우리의 데이터가 이러한 population 에 대해서 우리의 sample 이 얼마나 probable 한지를 나타내는 것입니다. 

> 가능도는 주어진 데이터에 대해서, 모델 파라미터가 변할떄마다 얼마나 가능한지에 대해서 나타내는 값입니다.

- 가능도가 어떻게 표현되는지 살펴봅시다. 

$$L(\theta\mid x)$$

- 가능도는  parameter 를 다르게하면서 특정 사건이 일어날 가능성을 비교하고자 만들어진 값으로 확률이 아닙니다. 
  - 백번 양보해서 확률이라고 합시다. 그럼 어떤 값이 r.v. 가 되나요
    - parameter? 우리는 parameter 에 대해서 Constant 로 취급했으므로 이는 불가능합니다.
    - Data? 지금 데이터는 고정하고 있습니다! 
- 이는 어디까지나 고정된 $\theta$ 에 대한 추론에 불과하므로 가능성의 합은 1이 아닙니다.

> ## [Ronald Fisher 의 해석](#link){: .btn .btn--primary}

- 통계학의 레전드, 피셔는 다음과 같이 말했습니다.

Knowing the population we can express our incomplete knowledge of, or expectation of, the sample in terms of probability; knowing the sample we can express our incomplete knowledge of the population in terms of likelihood
{: .notice}

- Population 을 알때에 샘플에 대해 설명할때에 Probability  를 사용합니다.
  - 이는 R.V. 인 Sample 에 대한 확률적 해석입니다.
- 샘플을 알때에 population 에 대해서 추론할때에 Likelihood 를 사용합니다.
  - 이는 고정된 population 에 대한 추론과정입니다. 주어진 데이터를 가장 잘 표현하는 모수를 탐색하는것을 그래프로 보여준게 Likelihood 입니다.
  - 추론은 그저 , '아 내 데이터를 가정하면 parameter 는 ~일거같아~' 라고 말하는것이므로 확률일리가 없습니다.

> ## [그럼 왜 이게 왜 헷갈리는가?](#link){: .btn .btn--primary} 

- 이는 Likelihood 과 probability 가 같은 form 을 가질때가 많기 때문입니다.

$$L(\theta\mid x) = Pr(X=x\mid \theta)=f(x\mid\theta) $$

- 물론 data point(x) 에서 바라보면 식은 같습니다만, 그 둘이 어떤것을 바라보느냐가 다르다는것을 명심하세요.
- Likelihood 는 $\theta$ 를 바꿔가면서 살펴보고, Probability 는 data 를 바꿔가면서 살펴봅니다.
  - Likelihood 는 parameter 의 추론! 
  - probability 는 sample 을 가능성을 설명! 

![png](/assets/images/Stat/58_1.png)

- 위의 예시를 보면 좀 더 이해가 될것입니다.
  - 왼쪽은 앞면이 나올 확률이 0.4 일때에, 앞면의 총 횟수에 따른 확률(Probability) 을 나타낸 것입니다.
  - 오른쪽은 앞면의 갯수가 4개일떄에 가장 가능성이 높은 $\theta$ 에 대한 추론을 그저 함수로 나타낸것입니다.

---

**Reference**

- <https://swjman.tistory.com/104>
- <https://en.wikipedia.org/wiki/Likelihood_function#Background_and_interpretation>
- <https://blog.naver.com/sw4r/221361565730>
- [slideshare](https://www.slideshare.net/StephenSenn1/take-it-to-the-limit-quantitation-likelihhod-modelling-and-other-matters)

 통계학좀 공부했다고 말하고싶다면 Likelihood 와 Probability 의 차이만큼은 알아둡시다! 
{: .notice--success}

