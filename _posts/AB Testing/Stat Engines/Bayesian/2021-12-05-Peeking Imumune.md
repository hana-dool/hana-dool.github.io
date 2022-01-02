---
title: "Bayesian Test Early Stopping"
excerpt: "Early Stopping 에 이슈는 없는가?"
tags :
  - AB_Stat
last_modified_at: 2021-12-05

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

Stack Exchange 에서 A/B 테스트를 수행하는 방식을 Freq 에서 Bayes 로 바꾸지 않고 Freq 를 유지했던 이유는?
{: .notice--warning}

# [A/B Testing at StackExchange](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

- 데이비드 로빈슨이 2015 년 06월에 StackExchange 에서 데이터 과학자로 합류한 이후, 첫번째 프로젝트는 기존의 A/B 테스트 시스템을 재고하는것이였습니다.
  - 이때 A/B Test 사이트 시스템은 p-value 를 승자 판단의 기준으로 삼고 있었습니다. 

> 문제점

- 하지만 이때 팀에서 테스트를 할떄 실행중인 테스트를 보고 p-value 가 특정 임계값(0.05) 에 다달했을때 즉시 테스트를 중지하는 습관이 있었습니다. 
  - 이러한 방법은 합리적으로 보이지만 결국 `p-value` 를 신뢰할 수 없게 만들고 False Positive 의 확률을 높히게 됩니다. 

> 1.해결책 : 특정 시간동안 실험을 실행하기로 약속하고 조기에 중단하지 않기

- 즉 초기에 계획한대로 실험을 하자는 것입니다. 
- 하지만 이는 비즈니스 환경에서는 지켜지기 힘든일입니다. 
  - 처음에 10000명을 실험하기로 했는데 , 실험이 30% 가 진행되자 p-value 가 계속 0.05 이하라고 합니다. 그러면 상사 또는 동료들은 빨리 실험을 중지하고 다음 실험을 하고싶을 것입니다. 

> 2.해결책 : 빈도주의 NSHT 보다 베이지안 방법론 사용

- Freq 방법론과는 달리 Bayes 방법은 이러한 문제에 영향을 받지 않습니다. 
- 또한 실행되는 동안 어느정도 데이터를 얻었다면 Peeking 이 가능하다고 주장합니다. 

> ## Early Stopping 가 가능하다는 주장

- 베이즈의 경우 Early Stopping 이 과연 허용될까요? 우선 허용된다고 주장하는 사람들을 먼저 살펴봅시다.

> the author of “How Not To Run an AB Test” followed up with [A Formula for Bayesian A/B Testing](https://www.chrisstucchio.com/blog/2014/bayesian_ab_decision_rule.html):

Bayesian statistics are useful in experimental contexts because you can stop a test whenever you please and the results will still be valid. (In other words, it is immune to the “peeking” problem described in my previous article).
{: .notice}

> Similarly, Chris Stucchio writes in [Easy Evaluation of Decision Rules in Bayesian A/B Testing](https://www.chrisstucchio.com/blog/2014/bayesian_ab_decision_rule.html) 

This A/B testing procedure has two main advantages over the standard Students T-Test. The first is that unlike the Student T-Test, you can stop the test early if there is a clear winner or run it for longer if you need more samples.
{: .notice}

> Swrve offers a similar justification in [Why Use a Bayesian Approach to A/B Testing](http://docs.swrve.com/faqs/resource-a-b-testing/25001697/):

As we observe results during the test, we update our model to determine a new model (a posteriori distribution) which captures our belief about the population based on the data we’ve observed so far. At any point in time we can use this model to determine if our observations support a winning conclusion, or if there still is not enough evidence to make a call.
{: .notice}

- 위와 같은 주장을 검증하기 위하여 시뮬레이션 분석을 수행해 보았습니다. 
  - 결론부터 말하자면 베이지안 테스트의 이점은 과정되었다는 것입니다. 베이지안 A/B 테스트는 엿보기(Peeking) 및 조기 중지(Early Stopping)에 "면역"되지 않습니다. 빈도주의적 방법과 마찬가지로 엿보기는 테스트를 잘못 중지할 가능성을 높입니다.

> ## p-value : Early Stopping Problem

- p-value peeking 의 문제점을 일찍히 많은 포스트에서 언급한적이 있지만 여기에서는 우선 시뮬레이션을 해 보겠습니다. 
- Freq 의 방법론으로는 Chi-square 비율 테스트를 사용합니다. 데이터는 아래와 같습니다.

> Chi-sqaure Method

|      | 클릭수 | 노출수 |
| :--- | -----: | -----: |
| NS   |    127 |   5734 |
| NS   |    174 |   5851 |

- 이 데이터에 대해 테스트를 수행하고 p-값 0.012103을 얻습니다.
- 이는 새로운 기능이 클릭률을 개선했으며 A에서 B로 변경해야 함을 나타냅니다.

> Peeking Simulation

- 이제 어떤 테스트를 사용할지를 결정했으므로 본격적으로 시뮬레리션을 해봅시다. 
- Setting
  - A 와 B 의 Conversion 은 모두 동일하게 0.1%입니다.
  - 20일동안 실험을 진행하고, 매일 10000개의 데이터를 얻습니다. 
  - Peeking 을 한다면 하루마다 두 비율 차이에 대한 Chi-square test 를 수행하고 p-value 를 기록합니다. 
  - 위와 같은 실험을 100회 반복합니다.

> 1.20일째에 p-value 를 살펴볼때

![jpg](/assets/images/Stat/119_3.jpg)

- 위와 같이 20일째에서 p-value 를 살펴보게 되면 5개의 실험이 '차이가 있다' 라고 결론을 내린것을 볼 수 있습니다
- 즉 우리가 의도한 Type 1 error 의 수치와 동일한 결과이며 이는 실험을 잘 수행했다는것을 나타냅니다.

> 2.매일 p-value 를 검사하며 0.05 이하로 떨어지면 중지

![jpg](/assets/images/Stat/119_4.jpg)

- 위아 같이 시뮬레이션이 효과가 없음에도 약 23%의 실험이 차이가 있다 라고 결론을 내리게 됩니다. 
- 즉 우리가 사전에 정의한 유의수준 0.05 을 지키지 못하고 있는 것입니다. (실험 세팅이 잘못됨) 

> ## Bayes : Early Stopping Problem

- 이제 베이즈방법론에 대해서도 과연 위와 같은 문제가 없는지에 대해서 알아봅시다.

> Loss Method

- 베이지안 테스트 방법론으로는 Evan Miller와 Chris Stucchio가 제안하고 조사한 베이지안 결정 규칙을 고려합니다. 
- 대부분의 베이지안 방법과 마찬가지로 [이 절차](https://web.archive.org/web/20150419163005/http://www.bayesianwitch.com/blog/2014/bayesian_ab_test.html)는 귀무가설을 가정하지 않습니다. 이는 [사후 기대 손실,](https://en.wikipedia.org/wiki/Bayes_estimator) 즉 A에서 B로 전환할 때 잃을 평균 금액 과 같은 Loss 에 관심이 있습니다.
- 자세한 방법은 다른 게시글을 확인해주세요. (VWO 논문이 좋을듯..)

> Peeking Simulation

- 아래와 같은 Setting 에서 실험을 진행해 보았습니다.
  - A : 0.1% ,  B : 0.09 % 
  - 20일동안 실험을 진행하고, 매일 10000개의 데이터를 얻습니다. 
  - Prior 는 beta ( 10 , 90 ) 을 사용합니다. 
  - decision rule 이 되는 Expected Threshold 는 0.00001 로 설정합니다.
  - Peeking 을 한다면 하루마다 두 비율 차이에 대한 Bayesian Testing 을 수행하고 Expected Loss 가 Treshold 이하로 떨어졌을떄 실험을 멈춥니다.

> 1.Not Peeking

![jpg](/assets/images/Stat/119_5.jpg)

- 위와 같이 Peeking 을 진행하지 않았을때에는 2.5% 의 실험만 틀린 결정 ('B 가 더 좋다!') 을 내립니다.

> 2.Peeking

![jpg](/assets/images/Stat/119_6.jpg)

- 위와 같이 Peeking 을 진행하게 되면 , 11.8% 의 실험이 잘못된 결정 ('B 가 더 좋다!') 을 내리고 있습니다. 
- Peeking 을 통해서 우리는 4배나 더 높은 Error 를 얻게 된 것입니다. 

> Threshold Change?

- 위와 같은 결과가 단순히 Threshold 를 변경한다면 해결할 수 있는 문제일까요?

![jpg](/assets/images/Stat/119_7.jpg)

- 위에서 빨간색 : Not Peeking , 파란색 : Peeking 의 경우입니다. 
- y 축은 B 가 더 좋다고 결론내리는 실험의 비율입니다. 
- 즉, 그림을 보면 항상 with peeking 의 경우가 잘못된 결론을 내리는 비율이 크다는것을 알 수 있습니다.

# [Whats going on?](#link){: .btn .btn--primary}{: .align-center}

> ## 왜 이런일이..?

- 베이지안이 위와 같이 중지에 면역이 되지 않는 이유는 뭘까요? 메서드 구현이나 이론에 문제가 있었을까요?
- 아닙니다. 위와 같은 현상은 베이지안 방법은 특정 약속을 하지 않기 떄문입니다.

> 베이지안방법은 1종 오류를 제한하지 않음

- 베이즈 방법은 1종오류를 제한하지 않습니다. 
  - 그래서 귀무가설(차이가 없음) 을 가정한 상태에서 에러를 조절하려 하지도 않죠.
  - 대신에 베이즈 방법은 예상 손실(Loss) 를 조절합니다. 
- 즉 우리는 Peeking을 할때에 베이즈 방법론도 '에러율' 을 제어하지 못하게 됩니다. 

> 사전 지식의 영향을 받음

- 베이지안 방법론은 사전 추론이 적절한지에 따라 결과가 달라질 수 있습니다. 
- 사전분포를 $\beta(\alpha, \beta)$ distribution, where $\alpha=100$ and $\beta=99900$ 로 설정한다고 합시다. 이렇게 설정할 경우 Simulation 결과는 사뭇 달라집니다.

> ## Threshold Error

- 베이지안 방법론은 threshold of caring ( a maximum expected loss that we’re willing to accept ) 을 설정한다는것을 기억합시다.

![jpg](/assets/images/Stat/119_8.jpg)

- 위의 그림에서 빨간색 : Peeking , 파란색 : Not Peeking 을 의미합니다. 
  - x 축은 우리가 Threshold 를 어떻게 설정하였는지를 나타냅니다.
  - 그리고 y 축은 각각 방법론 (Peek vs Not Peek) 을 이용하여 승자를 선택하였을때, Expected Loss 가 어떤 값을 가지는지를 나타냅니다.

> Peeking

- 당연히 Peeking 을 할때에는 Loss 가 우리가 설정한 Threshold 이하가 되면 바로 중지하므로 (엄밀히 말하면 하루마다 검사하므로 완전히 바로는 아닙니다. 그래서 y=x 에 완벽하게 일치하지는 않죠) x=y 선 가까이에 위치하게 됩니다. 
- Decision Rule 자체가, Loss 보다 낮아졌을때 승자를 결정하게 되므로 y=x 아래에 Bounded 시키게 됩니다.

> Not Peeking

- Peeking 을 하지 않을때에는 Threshold 이하가 된다 하더라도 주어진 실험 기간을 모두 채우게 되므로 위와 같이 Expected Loss 가 더 낮은것을 볼 수 있습니다.

> Type 1 error

![jpg](/assets/images/Stat/119_9.jpg)

- 하지만 여전히 위와 같이Peeking 을 하였을때에  1종 오류율이 높다는것을 기억합시다.!
- 이때 Bayes 방법을 수행할때 Type 1 Error 가 얼마나 높아질까요? 이런 현상을 어느정도 예측할 수 있을까요? 
  - 베이즈 방법론은 이러한 Error 에 대해 '애초에 고려하지 않음' 으로, 사실 계산하는 방법은 없습니다. Simulation 이나 별도의 게산(복잡..)이 필요합니다.

> ## Then... 

- p- vlaue 는 옆 링크와 같이 다양한 문제가 일어날 수 있습니다 ([terrible](http://www.ejwagenmakers.com/2007/pValueProblems.pdf) [at](http://lesswrong.com/lw/g13/against_nhst/) [almost](http://www.researchgate.net/publication/5272766_A_Dirty_Dozen_Twelve_P-Value_Misconceptions) [everything](http://www.johndcook.com/blog/2008/11/18/five-criticisms-of-significance-testing/) [else](http://www.nature.com/news/scientific-method-statistical-errors-1.14700?WT.mc_id=PIN_NatureNews).) 그럼에도 사용하는 이유는 1종 오류를 제어할 수 있다는 이유인데 , 이를 제어할 수 없다면 (Peeking 처럼요...) 이 방법은 좋은 구석이 하나도 없는것입니다.
- 이런 의미에서 베이지안 방법은 매력적입니다. 아무리 엿봐도, 유지합니다. 베이지안 통계학자들은 1종 오류율에 대한 빈도주의 초점이 잘못되었고, 예상되는 손실율 이 훨씬 더 좋은 비즈니스 해석이라고 말합니다. 
- 하지만! 우리는 오류율에 관심을 가져야합니다. 
  - A,B 가 차이가 없는 경우 전환 비용이 별로 들지 않으므로, False Positive 를 고려하는것은 별 상관이 없다고 할 수 있습니다.. 
  - 하지만 이를 개발하기 위해 엄청난 개발자의 노력이 들어갑니다. 그러므로 '실험이 의미 없더라도, 이 실험의 효과에 대해서 올바른 결정' 을 하는것이 중요하겠죠. 그런 입장에서 오류율을 제어하는것도 필요하구요. 

> ## 베이지안 A/B 테스트로 바꾸지 않는 이유

> 베이지안 테스트는 조기중지의 영향을 받는다.

- 우리가 여태 살펴본것처럼 베이지안 테스트도 결국은 조기중지의 영향을 받게됩니다. 
  - Freq  와 같이 효과가 없거나, 부정적인 결과를 받아들일 확률이 커지게 됩니다.
  - 이는 Optimization 입장에서는 큰 상관 없을지 몰라도, 우리가 '무언가를 배우는가?' 의 입장에서는 큰 손해입니다.

> Expected Loss

- Expected Loss 에 촛점을 마추다 보니 실제로 효과가 없는 실험이 테스트를 통과하는 (즉 승자가 되는) 상황이 올 수 있습니다. 

> 너무 어렵다.

- 베이지안 방법은 너무 어려워서 실험 조직ㅇ이 받아들이기 힘듭니다. 
  - Note : 이 게시물에서 논의된 문제를 관리하려면 민감도 분석 등 고급 분석이 필요합니다! 
- P value 는 그나마 "우리가 알고있는 악마!" 라는것을 기억합시다. Bayesian 의 경우는 "우리도 모르는 악마" 가 될수도 있습니다.

> Prior

- Prior 설정도 매우 조심스럽습니다. 잘 선택하면 실험이 정확해지고 Early Stopping 이슈도 완화(해결은 아님) 되지만 , Prior 가 잘못될경우 테스트의 품질이 떨어집니다.

> ## 논의중인 해결책..?

> **Frequentist approaches to sequential testing**.

- Sequential Test 를 고려해보기 
  - example, [this](http://elem.com/~btilly/ab-testing-multiple-looks/part1-rigorous.html) and [this](http://auduno.com/post/106141177173/rapid-ab-testing-with-sequential-analysis)

> ## Conclusion

- 물론 일부 베이지안,Freq 접근 방식은 Early Stopping 의 영향을 받지 않을 수 있습니다.
- 이 게시글은 '베이즈 전체' 에 대해서 비판하는게 아니라, 하나의 주의점입니다. 베이지안 방법은 엿보기에 자유롭지 않을 수 있다는것을 말하는 것입니다. 
  - 아마 엿보기에 대해 자유롭다는 주장은 ,Likelihood 가정 (즉 데이터에 대한 분포 가정) 만 잘 수행하게 되면 Stopping 을 언제 하던지, 그 업데이트 과정에는 해를 끼치지 않으므로 inference 에는 문제가 없다! 가 될것 같습니다. 하지만 이는 '수학적으로 잘 작동 하는가' 에 대한 정당화일 뿐이고, 실험의 품질에는 어떠한 영향을 끼칠까? 는 위 예시에서 처럼 그다지 좋은 영향을 미치는거같지는 않네요...
- 아직 우리는 베이즈 방법론이 더 강력하고 안정적이라는 판단을 하지 않아서 Freq 를 유지하고 있습니다. (Stack Exchange)

---

**reference**

- <http://varianceexplained.org/r/bayesian-ab-testing/>



