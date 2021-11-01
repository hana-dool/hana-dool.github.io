---
title:  "MAP and MLE"
excerpt: "베이즈 Inference 중에서 MAP 와 MLE"
categories:
  - Bayes
last_modified_at: 2021-11-01

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 MLE 와 MAP 는 같은 Pointer estimator 를 돌려준다는 매우 닮았습니다. 이 둘의 차이는 뭔지에 대해서 알아봅시다.
{: .notice--warning}

# [MLE and MAP](#link){: .btn .btn--primary}{: .align-center}

> ## MAP (Maximum Posteriori Estimation)

- 다들 아시겠지만 MLE 는 주어진 관측결과에 대해서 , 발생 가능한 가능성이 가장 높은 모수를 고르게 됩니다.

$$\hat{\theta}_{mle} = argmax_\theta f(D \mid \theta)$$

- 하지만 MAP 는 MLE 와 완전히 철학적으로 다른 개념을 가집니다. 
- MAP 는 주어진 관측 결과와 사전지식을 결합한 사후확률에 대해서 최적의 모수를 찾아내는 방법입니다. 
  - 즉 주어진 관측결과와 prior 를 고려할때 최대확률을 가지는 $\hat{\theta}_{MAP}$ 을 찾는 방법입니다.

$$\hat{\theta}_{MAP} = argmax_\theta P(\theta \mid D) = argmax_{\theta} P(D \mid \theta) P(\theta)$$

- 이떄에 중요한 점중에 하나는 'MAP' 만 구하는것이라면 우리가 지긋지긋하게 힘들어했던 $p(D)$ 를 구하는것을 하지 않아도 된다는 점입니다. 

> ## Compare with MLE

- 통계학적 방법으로 특정한 문제에 대해 '이거에요!' 라고 말할 수 있는 추정치는 크게 MLE 와 MAP 가 있습니다. 

> Example 

- 바닥에 떨어진 머리카락의 길이(z)를 보고 그 머리카락이 남자 것인지 여자 것인지 성별(x)을 판단하는  문제를 생각해 봅시다.
- **ML(Maximum Likelihood) 방법:** ML 방법은 남자에게서 그러한 머리카락이 나올 확률 $p(z \mid 남)$ 과 여자에게서 그러한 머리카락이 나올 확률 $p(z \mid 여)$을 비교해서 가장 확률이 큰, 즉 likelihood가 가장 큰 클래스(성별)를 선택하게 됩니다.

- **MAP(Maximum A Posteriori) 방법:** MAP 방법은 z라는 머리카락이 발견되었는데 그것이 남자것일 확률 $p(남\mid z)$, 그것이 여자것일 확률 $p(여 \mid z)$를 비교해서 둘 중 큰 값을 갖는 클래스(성별)를 선택하는 방법입니다. 즉, 사후확률(posterior prabability)를 최대화시키는 방법으로서 MAP에서 사후확률을 계산할 때 베이즈 정리가 이용된다.

> Note

- 이때 두 방법론이 어떤 점에서 다를까요? 그것은 바로 '사전정보를 넣어서' 더 정확한 추정을 할 수 있느냐에 대한 차이입니다.
- 만일 인구의 90%가 남자고 여자는 10% 밖에 없다고 합시다.  (성별에 대한 사전정보 $p(z)$
  - ML은 남녀의 성비는 완전히 무시하고 순수하게 남자중에서 해당 길이의 머리카락을 가질 확률, 여자중에서 해당 길이의 머리카락을 가질 확률만을 비교하는 것이다. 
  - 반면에 MAP는 각각의 성에서 해당 머리카락이 나올 확률 뿐만 아니라 남녀의 성비까지 고려하여 최종 클래스를 결정하게 됩니다.

> ##Pros and cons

> 장점

- MLE 는 데이터에 지배되는 값이지만 , MAP 는 사전확률도 고려한다는 점에서 더 자연스럽습니다.
- 다양한 정보량을 제공하지 못합니다. 

![png](/assets/images/Stat/90_1.png)

- 위의 경우는 같은 MAP 를 가지지만 그 분포가 매우 상이합니다. (Multimodal 이면 훨씬 더 심해집니다.)

> 단점

- MLE 만으로는 Point estimator 이기 떄문에 불확실성을 표현하기 힘들어서 별로 선호되지 않는것처럼 MAP 도 똑같은 맥락으로 , 제공되는 정보량이 적다는 점에서 별로 선호호되는 방법은 아닙니다.

---

**reference**

- <https://stats.stackexchange.com/questions/545084/bayesian-estimation-mcmc-vs-map>
- <https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=61stu01&logNo=221274904677
- <https://towardsdatascience.com/mle-map-and-bayesian-inference-3407b2d6d4d9>
- <https://darkpgmr.tistory.com/62>

MAP 를 굳이 자주 쓰는것 같지는 않고, 그냥 이런게 있다~ 정도만 알아두는게 좋을것 같습니다!
{: .notice--success}

