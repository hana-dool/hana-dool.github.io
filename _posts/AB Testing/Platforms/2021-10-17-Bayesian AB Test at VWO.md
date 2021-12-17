---
title: "Bayesian A/B Testing at VWO (2015)"
excerpt: "VWO 에서 사용하는 베이지안 A/B Testing Framework"
categories:
  - AB_Platform
last_modified_at: 2021-10-17

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 VWO 에서 사용하는 Bayesian A/B Testing 방법에 대해서 technical Whitepaper 가 있어서 이를 리뷰해보고자 합니다. 중간중간 다소 난해한 부분이 있기는 하지만 전체적으로 적당한 수준인것 같아요. 
{: .notice--warning}

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## Abstract

- Visual 웹사이트 Optimizer에 가입하기 전에 AOL Patch에서 A/B 테스트를 실행하고 통계 컨설턴트로 활동했습니다. (Chris Stucchio)
- A/B 시험이 끝날 때마다 사람들은 나에게 다가와 결과에 대해 질문을 했습니다. 그 중에서 가장 흔한 질문 중 하나는 "버전 B가 버전 A보다 나을 확률은 얼마인가?" 였습니다. 
- 하지만 저는 Frequentist 방법론을 사용하기 때문에 많은 방법론에 대해서 제대로 답할 수 없었습니다.
  - 또한 저는 질문을 받은 대부분의 질문에 대답할 수 없었고, 대신 논리적이지 않은 대체 통계를 제시해야 했습니다. 
- Visual Website Optimizer 에서는 이러한 문제들을 Bayesian Framework 를 사용함으로서 해결하였습니다.
  - 새로운 방법은 A/B 테스트를 수행하는 많은 사람들이 만드는 몇 가지 오류들을 수정하도록 도와주었고 , 사용자를 과학적인 방법으로 이끌어주게 하였습니다.

> ## The problem

- 테스트 막바지에 저에게 늘 물어보던 질문은 다음과 같았습니다. 
  - Variation B 가 variation A 보다 좋을 확률은 얼마인가요? 즉 이를 수학적인 기호로 설명해보자면 아래와 같습니다.

$$P(\lambda _B > \lambda _A)$$

- 하지만 Standard 한 Frequentist 방법론으로는 위의 질문에 대답을 할 수 없습니다.
  - 대신에 Freq 방법은 Null hypothesis $H_0 : \lambda_A = \lambda _B$ 를 검정하게 됩니다. 
  - 그리고 우리는 데이터로부터 Test statistic $t_e$ 를 얻게됩니다. 
  - 그리고 다음과 같은 방식으로 p-value 가 계산됩니다.

$$p = P(t\ge t_e \mid H_0)$$

- p-value 는 '같은 Sample size 를 이용하여 A/A Test 를 진행하였을떄에 우리 데이터보다 더 극단적인 데이터를 가질 확률' 을 의미하게 됩니다. 
- 이러한 p-value 는 Decision 의 기준이 된다는 점에서 매우 중요하나, 제가 아는 한 어떠한 마케팅 전문가 / 웹 디자이너가 이러한것을 물어본 적이 없습니다. (매우 헷갈리고 다소 어려운 개념이나 아무조 신경쑤지 않음)
  - 더군다나 이러한 p-value 는 종종 $P(\mu_B > \mu_A)$ 로 잘못 해석되곤 합니다. 

> ## 용어

- $n_A , n_B$ 는 각 Variants A,B 의 총 유저수를 나타냅니다.
- $c_A,c_B$ 는 각 Variancts A,B 의 전환유저 수를 나타냅니다. 
- $\lambda_A , \lambda_B$ 는 각 Variants A,B 의 Conversion 을 나타냅니다. 

## Representing uncertainty 

- Freq 통계에서 제일 중요한 요소는 MLE 입니다.
  - MLE 는 데이터를 고려할때에 '가장 가능성 있는' 모수인 하나의 숫자라고 할 수 있습니다.
  - 하지만 이러한 숫자(MLE)를 제시하는것은 늘 오해를 불러일으키게 됩니다.
    - ex : 평균이 6(mle) 이라구요? 아 6일 확률이 100%라는거군요! 
- 통계는 늘 '정확한' 것은 없습니다. 항상 에러(불확실성)가 존재하게 됩니다.
  - 통계학자가 할 수 있는일은 이러한 불확실성을 계량화 하는것입니다. 
- VWO 에서는 credible interval(실제 값을 포함할 확률을 가지는 영역. Confidence interval 하고는 다름) 을 제공하여 이러한 '불확실성' 을 계량화 하게 됩니다.

# [Bayesian AB Testing](#link){: .btn .btn--primary}{: .align-center}

- 베이즈 통계의 기본은 다 건너띄고 깔끔하게 핵심만 요약하겠습니다. (자세한 유도 과정을 살펴보고 싶다면 논문을 참조해주세요. 그냥 기본적인 Conversion 에서의 Conjugate 를 유도하는 과정입니다.)
  - Conversion 의 경우 , Bernoulli 의 데이터 Distribution 을 이용하기 때문에 이에 대한 Conjugate 인 Beta Distribution 을 이용할 수 있습니다.
  - Conjugate 인 Beta 는 데이터를 이용해 업데이트할 수 있습니다. 
- 즉 Conversion $\lambda_A , \lambda_B$ 에 대해서 실험 데이터를 prior Beta(1,1) 을 이용하여 업데이트한다면 Conversion 에 대한 Postrorior 분포를 얻을 수 있을것입니다.
  - 그리고 이러한 '업데이트된 분포' 를 이용하여 A/B Testing 을 진행할 수 있습니다.

> ## The Joint Posterior for variants 

- 실험 이후에 우리는 각각의 posterior $P(\lambda_A) , P(\lambda_B)$ 를 계산할 수 있게 됩니다. 
  - 하지만 $\lambda_A,\lambda_B$ 두 값을 동시에 이용하여 Inference 를 진행해야 하므로 결국에는 'Joint posterior $P(\lambda_A,\lambda_B)$' 를 계산해야 합니다.
- 이떄에 우리는 Joint posterior of A,B 를 독립을 가정하여 다음과 같이 계산합니다. 

$$P(\lambda_A,\lambda_B) = P_A(\lambda_A)P_B(\lambda_B)$$

- 이제 위에서처럼 두 전환율에 대한 분포를 알았으므로 '어떤 기준' 을 통하여 승자를 결정해야 할까요? 
  - 우리는 위에서 계산된 A,B 의 전환율에 대한 Distribution 을 이용하여, Control 대신 Variant 를 선택하였을때 계산되는 loss 를 계산하고 이 값을 기준으로 승자를 결정하려고 합니다.

> ## Joint Posterior in Expereiments

![png](/assets/images/Stat/84_1.png)

- 위 경우는, 실험 시작하고 얼마 지나지 않은 뒤의 joint posterior 를 나타낸 것입니다. 
  - 파란색 Line 은 $\lambda_A = \lambda_B$ 인 선을 나타낸다고 생각하시면 됩니다.
  - 아직 데이터가 얼마 없기 떄문에 그 영역 (하얀색) 이 넓은 것을 볼 수 있습니다. 
  - 이러한 '넓은' 영역은 아직 Posterior 가 결정을 내리기에는 '불확실하다' 라는것을 의미합니다.

![png](/assets/images/Stat/84_2.png)

- 위 경우는 실험 후의 Posterior 를 타타낸 것입니다. 
  - 데이터가 많이 쌓이면서 Posterior 의 추정이 정확해지고 있는 모습입니다.
  - 파란색 Line 에 비추어 생각해 보았을떄에, Control 이 Variation 보다 더 좋다고 생각할 수 있습니다.

> ## Chance to beat Control 

- 우리가 Variant A 를 선택하게 될떄에, 이 선택으로 인해 얻을 Loss 가 어느정도일까요? 이를 Probability 입장에서 접근할 수 있습니다.

> definition of Error probability 

- Error probability A 는 A 를 선택하였는데 '잘못된 선택일 확률' 로 정의합니다.
  - 즉 위에서의 정의는 $P(\lambda_B >\lambda_A)$ 로서, 아래는 그 계산식입니다.

$$E[\mathcal{I}](A)=\int_{0}^{1} \int_{0}^{\lambda_{\mathcal{A}}} P\left(\lambda_{A}, \lambda_{B}\right) d \lambda_{B} d \lambda_{A}$$

- 비슷하게 $P(\lambda_A > \lambda_B)$ 를 아래와 같이 정의할 수 있습니다.

$$E[\mathcal{I}](B)=\int_{0}^{1} \int_{\lambda_\mathcal{A}}^{1} P\left(\lambda_{A}, \lambda_{B}\right) d \lambda_{B} d \lambda_{A}$$

- 이러한 기준(metric)을 이용한다면 우리가 A/B Test 의 결과를 이용해 판단을 내릴떄에 기준이 될 수 있을것입니다.
  - 하지만 이 기준(metric) 은 결점이 많은 정의입니다. 왜냐하면 모든 errors 를 equaly Bads 하다고 취급하기 떄문입니다. 

![png](/assets/images/Stat/84_3.png)

![png](/assets/images/Stat/84_4.png)

- 단적으로 P(A<B) 가 같은 100% 이지만 위와 같은 경우, 그 증거(Evidence) 가 매우 차이나는 경우가 있습니다. (아래의 그림이 훨씬더 강력한 증거임)
  - 이렇게 차이가 나는 이유는 '$\lambda_A , \lambda_B$' 의 값을 비교할때에 순전히 그 '크기차이만' 비교하게 되기 떄문입니다. 즉 $\lambda_A < \lambda_B$ 라는 사실만 알게되면 각각이 0.1 < 0.9 였는지, 0.89<0.9 였는지는 정보에 포함되지 않기 떄문입니다. 
- 그러므로 이러한 Chance to Beat 으로만 의사결정을 하게 되는것은 안좋다고 할 수 있을것입니다.

> ## The Loss Function 

- Loss function 은 이러한 '둘의 차이' 까지 같이 고려함으로써 문제를 해결해줍니다. 
  - Small 에러는 작게, Large 에러는 크게 취급하게 됩니다. 

> Definition of loss function

- Loss function 은 특정한 variant 를 선택함으로 기대되는 expected loss 입니다.
- 주어진 특정한값 $\lambda_A , \lambda_B$ 에 대해서 Loss 는 다음과 같이 정해집니다.

$$\mathcal{L}(\lambda_A, \lambda_B ,A) = max(\lambda_B - \lambda_A , 0)$$

$$\mathcal{L}(\lambda_A, \lambda_B ,B) = max(\lambda_A - \lambda_B , 0)$$

- 예시로  $\lambda_A = 0.1$ , $\lambda_B = 0.15$ 라고 합시다. 이떄에 A 를 선택하게 된다면 이떄 'A' 를 선택함으로서 얻는 손해(Loss) 는 $max(0.05 , 0)= 0.05$ 입니다. 그에 반해서 'B' 를 선택함으로서 얻는 손해(Loss) 는 $max(-0.05,0) =0$ 입니다.

> Definition of Expected loss function

- 그런데 우리는 '각 $\lambda$ 가 정해져 있는 상황' 이 아니므로 결국 확률적으로 접근해야 합니다.
  - 왜냐하면 베이즈 Frame work 의 중심 아이디어가 '모수는 정해져 있지 않은 분포' 라는 것이니까요.
- 그러므로 우리는 'Variant ' 의 선택으로 야기되는 '기대되는 손해' 를 계산할수밖에 없습니다. (모수가 고정된 값이 아니니까 정확한 Loss 가 얼마다! 가 아니라 '기대되는 loss 가 얼마다!' 라고 밖에 말할 수 없습니다. 마치 주사위의 눈을 정확히 말할수는 없지만 기대값은 3.5 라고 할 수 있는것 처럼요) 그 계산은 아래와 같습니다.

$$E[\mathcal{L}](?)=\int_{0}^{1} \int_{0}^{1} \mathcal{L}\left(\lambda_{A}, \lambda_{B}, ?\right) P\left(\lambda_{A}, \lambda_{B}\right) d \lambda_{B} d \lambda_{A}$$

- 이떄에 ? Symbol 은 우리가 선택한 A 또는 B 가 될 수 있습니다. 

> ## Compute the Loss , error function 

- 이러한 Loss 나 error function 을 계산하기 위해서 , 우리는 '근사' 하여 계산해야 합니다. 
  - 왜냐하면 Exactly 하게 적분을 구하는것은 수학적으로 엄청나게 힘든 일이기 떄문입니다. 
- 아래 방식은 적분을 격자 근사(리만 적분 근사)를 이용하여 계산한 방식입니다.

> Computing joint posterior 

```
posteriorA = ...do work here... 
posteriorB = ...do work here...
joint_posterior = zeros( shape=(100, 100) ) #The joint posterior is a 2d array 
for i in range(100): for j in range(100):
	joint_posterior[i,j] = posteriorA[i] * posteriorB[j]
```

- 위와 같이 이전의 independence 가정으로부터 joint posterior 를 근사할 수 있습니다. 

> Computin Error Functions

```
errorFunctionA = 0.0
	for i in range(100):
		for j in range(i, 100):
		errorFunctionA += joint_posterior[i,j]
```

- $\mathcal{L}(\lambda_A, \lambda_B ,A) = max(\lambda_B - \lambda_A , 0)$ 를 계산한 식입니다.
- 이와 같이 Error function 도 Sample 을 generating 하는 형식으로 구현할 수 있습니다.

> Computing Loss Functions 

```
def loss(i, j, var):
    if var == ’A’:
	    return max(j*0.01 - i*0.01, 0.0)
    if var == ’B’:
    	return max(i*0.01 - j*0.01, 0.0)
lossFunction = 0.0
for i in range(100):
	for j in range(100):
		lossFunction += joint_posterior[i,j] * loss(i,j,’A’)
```

- 위와 같이 loss function 또한 구현할 수 있습니다. 

> Exact Form

- 사실 위의 계산을 Exact 하게 수행할수도 있습니다.
  - <https://www.chrisstucchio.com/blog/2014/bayesian_ab_decision_rule.html>
- 하지만 Exact Form 은 오로지 Two Variants 일떄에 작동하는지라 여기서 다루지는 않겠습니다.

# [Running Bayesian AB Testing](#link){: .btn .btn--primary}{: .align-center}

> ## Running A/B Testing 

- 이전에 2개의 Variants 에 대해서는 A/B Testing 을 어떻게 수행하는지에 대해서 살펴보았습니다.
  - 그러면 3+ 개의 Variancts 에 대해서는 어떻게 해야될까요? 
  - 이때에는 어떻게 A/B Test 가 working 하는지에 대해서 설명해보도록 하겠습니다.
- $\epsilon$ 은 desired loss tolerance 로 정의됩니다. 
  - 즉 우리가 받아드릴 loss의 상한선이라고 생각하시면 됩니다. 
  - 예를 들어서 Variant B 의 loss가 0.000001 이면 이 loss 는 받아들일만큼 작으므로 이를 선택하는 식입니다. 
- 이러한 $\epsilon$ 의 해석은 '선택이 잘못되었다고 가정할떄에' 잃을 수 있는 기댓값을 나타냅니다. 
  - 이 양만큼 Loss 가 발생해도 큰 상관이 없을 정도로 낮게 설정해야될 것입니다.

> Algorithm 

1. A,B 에 대해서 실험을 실행합니다. 
2. 주기적으로 $n_A , c_A , n_B , c_B$ 를 계산합니다.  
3. $$E[\mathcal{L}](A),E[\mathcal{L}](B)$$를 계산합니다. 그리고 set $$\mathfrak{A}=\{x: E[\mathcal{L}](x)<\varepsilon\}$$ 을 정의합니다.  
   - 위에서 정의한 $\mathfrak{A}$ 는 우리가 정의한것보다 낮은 Loss 를 가지고 있는 '승자 set' 입니다. 
   - A 가 매우 좋은 Variants 라면 적은 샘플만으로도 $$\mathfrak{A} = \{A\}$$ 가 될 것입니다.
4. 만약 $\mathfrak{A}$ 가 empty 면 다시 step 1 로 가서 계속 실험을 진행합니다. 비어있지 않으면 $\mathfrak{A}$ 에 있는 element 를 승자로 선언하고 종료합니다. 

> ## Running more than two variants 

- 위에서 실험이 대충 어떻게 흘러가는지 알았으므로, 여기에서는 Loss 를 어떻게 정의해야되는지에 대해서 살펴보겠습니다.
  - 만약 variants 3개라면 loss function 은 다음과 같이 정의가 됩니다. 

$$\mathcal{L}(\lambda_A , \lambda_B , \lambda_C , A) = max(\lambda_B - \lambda_A , \lambda_C - \lambda_A , 0)$$

$$\mathcal{L}(\lambda_A , \lambda_B , \lambda_C , B) = max(\lambda_A - \lambda_B , \lambda_C - \lambda_B , 0)$$

$$\mathcal{L}(\lambda_A , \lambda_B , \lambda_C , C) = max(\lambda_A - \lambda_C , \lambda_B - \lambda_C , 0)$$

- 위와 같은식으로 3개 이상의 variants 에 대해서도 정의할 수 있습니다. 

> Alorithm 

1. A,B,C... 의 variancts 에 대해서 A/B Testing 을 실시합니다. 
2. 주기적으로 $n_a ,c_a .......$ 를 계산합니다.
3. $$E[\mathcal{L}](A)$$,$$E[\mathcal{L}](B)....$$ 를 계산합니다. 그리고 set $$\mathfrak{A}=\{x: E[\mathcal{L}](x)<\varepsilon\}$$ 을 정의합니다. 
4. 만약 $\mathfrak{A}$ 가 empty 면 다시 step 1 로 가서 계속 실험을 진행합니다. 비어있지 않으면 $\mathfrak{A}$ 에 있는 element 를 승자로 선언하고 종료합니다. 

- 하지만 이 경우에 이전에 2개의 Variants 에 대해서 사용했던 Computing algorithm 을 계산하기는 어렵습니다.
  - 그러므로 이를 계산하기 위해서 우리는 새로 loss 를 계산하는 Algorithm 을 만들어내야합니다.

> Computing alorithm

```
def loss(i, j, var):
	if var == ’A’:
		return max(j*0.01 - i*0.01, k*0.01-i*0.01, 0.0)
	if var == ’B’:
		return max(i*0.01 - j*0.01, k*0.01-j*0.01, 0.0)
	if var == ’C’:
		return max(i*0.01 - k*0.01, j*0.01-k*0.01, 0.0)
lossFunction = 0.0
	for i in range(100):
		for j in range(100):
			for k in range(100):
				lossFunction += joint_posterior[i,j,k] * loss(i,j,k,’A’)
```

- 위의 경우는 2개의 variants 에서 실행했던 '적분의 근사를 리만적분합 으로 근사' 하는 방법을 쓴 것입니다. 
- 하지만 위와 같이 계산하는것은 총 100^3 의 총 100만번의 연산을 요구합니다. 
  - 이렇게 계산량이 늘어난 이유는, 우리가 격자 근사(리만합)를 통하여 적분을 계산하였기 떄문입니다.
    - 그러므로 Variants 가 5개까지 늘어나게 된다면 100억번이 넘을것이고 이는 Bayes Framework의 속도를 느리게 할 것입니다 .
- 그러므로 우리는 Monte Carlo method 를 이용하여 이러한 Integral 을 쉽게 하려 합니다.
  - Monte carlo method 란 확률 분포를 이용해 근사하는 방법으로 제 블로그 Statistic 카테고리에 올려두었으므로 참고해주세요

# [Other Calculation](#link){: .btn .btn--primary}{: .align-center}

> ## Chance to beat Control , Chance to beat All

- Posterior 를 본격적으로 고려하기 전에 우리는 두가지 유용한 Quantities 들에 대해서 알아봅시다. 

> Chance to beat control 

- given variation (say B) 이 control 보다 더 높은 conversion rate 를 가질 확률입니다.

$$\mathcal{C T B C}(B)=\int \ldots \int_{\lambda_{B}>\lambda_{A}} P\left(\lambda_{A}, \lambda_{B}, \ldots, \lambda_{k}\right) d \lambda_{A} d \lambda_{B} \ldots d \lambda_{k}$$

> Chance to beat everyone 

- 우리는 또한 given variation (say B) 가 '다른 모든 것보다 좋을 확률' 을 다음과 같이 정의할 수 있습니다. 

$$\mathcal{C T B} \mathcal{A}(B)=\int \ldots \int_{\left(\lambda_{B}>\lambda_{A}\right) \wedge\left(\lambda_{B}>\lambda_{C}\right) \wedge \ldots} P\left(\lambda_{A}, \lambda_{B}, \ldots, \lambda_{k}\right) d \lambda_{A} d \lambda_{B} \ldots d \lambda_{k}$$

> ## Monte Carlo - how to compute the integrals

- 우리는 위에서도 언급했지만 '적분을 근사하는데' 격자방법을 계속 사용하다가는 계산량에 깔려 죽게됩니다. 
- 그러므로 우리는 이러한 값을 근사하기 위하여 Montecarlo 근사를 이용하여 아래와 같이 계산되어질 수 있습니다.

$$\frac{1}{N} \sum_{i=1}^{N} \mathcal{L}(\lambda_A^i , \lambda_B^i ,\lambda_C^i,A) \approx E[\mathcal{L}](A)$$

- $(\lambda_A^i , \lambda_B^i,\lambda_C^i ....)$ 는 각 posterior 에서 Sampling 된 i 번째 sample 입니다. 
- 이제 중요한 질문이 남았는데요, '위와 같이 계산하게 되는 Montecarlo Approx' 는 얼마나 정확할까요? 

> ## Monte Carlo - how accurate? 

> Theorem

- $\delta$ 가 이미 정해진 값이라고 합시다. 

$$P\left(\left|\frac{1}{N} \sum_{i=1}^{N} \mathcal{L}\left(\lambda_{A}{ }^{i}, \lambda_{B}^{i}, \ldots, A\right)-E[\mathcal{L}](A)\right|>\epsilon\right)<\delta$$

- 그러면 위를 만족하기 위해서는 N 은 최소한 $-ln(\delta)/(2\epsilon^2)$ 만큼의 Sample 이 필요하게 됩니다. 
- 증명은 Hoeffding's inequality 를 이용하게 됩니다. 여기에서는 생략하겠습니다.

> Note

-  $\epsilon$ 이 작을수록 매우 큰 Sample size 가 필요하게 됩니다. (inverse square scale) 
  - $\epsilon$ 를 설정한다는것은 이것보다 큰 차이의 Approximation 은 허용하기 싫다는 의미입니다. 
- $\delta$ 가 작아질수록 필요한  N 은 Logarithm scale 로 증가하게 됩니다.
  - $\delta$ 가 작다는것은 $\epsilon$ 이상의 차이를 보이는 Approximation 이 나타날 확률이 작게 Bounded 된다는 것입니다. 
  - 즉 $\epsilon$ 이상의 error 가 나오는 확률을 bounded 시키는 값이라 할 수 있겠습니다.
- 즉 $\epsilon$ 은 작게 , $\delta$ 도 작게 유지하는 N 의 값을 설정해야 좋은 Approximation 을 보장할  수 있습니다. 
  - WVO 에서는 $\delta = 10^{-10}$ 을 사용한다고 합니다. 

> ## Monte Carlo - how accurate 2 

> Theorem

$$\frac{1}{N} \sum_{i=1}^{N} \mathcal{L}\left(\lambda_{A}{ }^{i}, \lambda_{B}{ }^{i}, \ldots, A\right)-E[\mathcal{L}](A) \rightarrow N\left(0, S^{2} / N\right)$$

- Here $S^{2}$ satisfies the bound:

$$S^{2} \leq V A R\left[\lambda_{B}-\lambda_{A}\right]+V A R\left[\lambda_{C}-\lambda_{A}\right]+\ldots=V A R\left[\lambda_{B}\right]+V A R\left[\lambda_{C}\right]+\ldots+M\cdot V A R\left[\lambda_{A}\right]$$

- M 은 number of variants 입니다.

> Note

- 위의 Thm을 이용하여, 우리는 Monte Carlo Approximation 의 에러가 $\epsilon $ 보다 작아질 확률이 $\tau$ 가 되게 조절하기 위한 샘플 수 N 을 계산할 수 있습니다.
  - Normal Approximation 을 이용해 계산한다면 N 의 값은 아래와 같이 계산됩니다. 

$$N = [(S/\epsilon)cdf^{-1}(\tau/2)]^2$$

- 이떄 cdf 는 Normal distribution 에 대한 cdf 입니다. 

> Remark

- $\lambda_A$ 가 Beta distribution $B(a,b)$ 를 따른다고 가정합시다. 그렇다면 우리는 아래를 알 수 있습니다. 

$$VAR[\lambda_A] = \frac{ab}{(a+b)^2 (a+b+1)}$$ 

- 그러므로 만약, beta 를 prior 로 사용하게 된다면 이를 이용하여 $S^2$ 을 정확하게 계산해낼 수 있습니다.  
  - 먼저 모든 variation 은 fixed prior $(\alpha , \beta)$ 를 가진다고 가정합시다. 

$$\begin{array}{r}
S \leq \sum_{x=B, C, \ldots} \frac{\left(\alpha+c_{x}\right)\left(\beta+n_{x}-c_{x}\right)}{\left(\alpha+\beta+n_{x}\right)^{2}\left(\alpha+\beta+n_{x}+1\right)} \\
\quad+M\left(\frac{\left(\alpha+c_{A}\right)\left(\beta+n_{A}-c_{A}\right)}{\left(\alpha+\beta+n_{A}\right)^{2}\left(\alpha+\beta+n_{A}+1\right)}\right)
\end{array}$$

- 그러면 계산은 위와 같이 이루어 집니다. 이떄 눈여겨 봐야할점은 바로 Time Complexity 의 관점입니다.
  - 이때, 모든 variants 는 $n_A \approx n_B \approx n$ 으로 같은 trial 의 수를 지닙니다. 이를 적용하면, 아래와 같은 식이 나옵니다.

$$S\le O(\frac{M}{n^2})$$

- 그러므로 이를 이용하여 다시 이전 식에 대입한다면 아래와 같은 결과를 얻을 수 있습니다 .

$$N = O([(M/n^2\epsilon)cdf^{-1}(\tau/2)]^2)$$

- 그러므로 $\epsilon$ 가 작아질수록 $1/\epsilon^2$ 만큼 필요한 Sample 의 수가 증가합니다. 
- VWO 에서는 다음과 같은 설정을 따른다고 합니다. 
  - $\tau = 10^{-5}$ , $\epsilon = 0.0001$ 으로 설정합니다. 그러면 N 은 대게 1~50 million 사이에 위치하게 됩니다. 

# [Approximate worst case for Bernoulli](#link){: .btn .btn--primary}{: .align-center}

> ## Two Variants

- 이제 우리는 다음과 같은 궁금증이 생길 수 있습니다. 
  - Bernoulli test 가 끝나기 위해서 최악의 시나리오는 어떤것일까요? 
- 이러한 test 가 끝나기 위해서는 아래와 같은 조건을 만족해야합니다.
  - 특정한 Variants(say A) 가 $$E[\mathcal{L}](A)\le \epsilon$$ 를 만족할때 즉 
    - $$E[\mathcal{L}](A) = \int\int max(\lambda_A - \lambda_B , 0 ) P(\lambda_A , \lambda_B)d\lambda_A , d\lambda_B\le\epsilon$$
- 이떄 worst case 는 both variants 가 identically same 인 경우입니다. 
  - 이러한 bounded 를 계산하기 위하여 우선 아래와 같은 식을 참고합시다.

$$\int\int max(\lambda_A - \lambda_B , 0 ) P(\lambda_A , \lambda_B)d\lambda_A , d\lambda_B\le\int\int\mid\lambda_A - \lambda_B \mid P(\lambda_A , \lambda_B)d\lambda_A d\lambda_B$$

- 두번쨰로 Beta distribution 은 large  $a=N\zeta$ , $b = N\zeta$ 에 대해서 beta 는 normal 로 근사하게 됩니다. 
  - 이를 이용하면 위의 식은 다음과 같이 계산됩니다.   

$$\approx \iint\left|\lambda_{A}-\lambda_{B}\right| C \exp \left(-\frac{\left(\lambda_{A}-\zeta\right)^{2}+\left(\lambda_{B}-\zeta\right)^{2}}{2 \sigma^{2}}\right) d \lambda_{A} d \lambda_{B}$$

- 이제 위 식에 대해서, 계산을 하다 보면 (자세한 증명은 reference 참고) 아래와 같은 식이 나오게 됩니다. 

$$\approx 2\sqrt{\frac{\zeta(1-\zeta)}{\pi N}}$$

> Worst Case 일떄에 승자가 나올떄까지 얼마나 기달려야 하나요? 

$$2\sqrt{\frac{\zeta(1-\zeta)}{\pi N}} \le \epsilon$$ 

- 또는 동일하게  아래의 조건을 만족할떄까지는 기다려야 합니다.

$$N \ge 4 \frac{\zeta(1-\zeta)}{\pi \epsilon ^2}$$

- 이떄에 위의 N 값은 beta 가 normal 로 zppeoximation 하고 있다는 가정 하에서 만들어진 것인데요, 이러한 가정을 만족하려면 $$0\le p \pm 3\sqrt{\zeta(1-\zeta)/N)}\le 1$$ 가 되어야 합니다. 
- 정리하자면  $$0\le p \pm 3\sqrt{\zeta(1-\zeta)/N)}\le 1$$  를 만족한다면  $$N \ge 4 \frac{\zeta(1-\zeta)}{\pi \epsilon ^2}$$ 일때까지 실험을 진행해야 합니다.

> Remark

- 위의 계산은, 'A,B' 가 같다고 할 때에 Expected loss 가 $\epsilon$ 보다 작아지는 Sample 수 N 을 찾아서 그 N 을 제시하는 방법입니다. (대충 보면 이거인것 같습니다. 수식 더 뜯어보는건 시간 생기면 그떄 더 리뷰하겠습니다.)
- '최악' 의 시나리오에서 , 어느정도의 Sample 수가 필요한지를 간략하게 제시한것이라 보면 됩니다.
  - 왜 '같을떄' 가 최악의 시나리오냐면 A,B 둘중 하나가 좋으면 Expected loss 가 빠르게 낮아지기 떄문입니다. 
  - 하지만 둘다 엇비슷하면, Expected loss 가 느리게 낮아집니다. 

> ## Many Variants 

- Variants 가 많을때는 어떻게 할까요?  이 계산도 위와 같은 로직을 따라갑니다만 , 그 계산이 너무 복잡하여 여기에서는 그 공식만 제시하겠습니다. 

$$N \ge \zeta(1-\zeta)\frac{1}{\epsilon^2}(\frac{(K-1)\Gamma(K/2)}{\Gamma((K+1)/2)})^2$$

# [Modeling Revenue](#link){: .btn .btn--primary}{: .align-center}

> ## Modeling Idea

- revenue 를 모델링하기 위해서는 어떻게 할까요? 
  - 우리는 아래와 같이 두개의 Distribution 을 이용하여 'revenue' 를 나타내게 됩니다

$$Ber(\gamma)\to \alpha_i $$

$$Exp(\theta) \to r_i$$

$$\alpha_i \cdot r _i \to v_i$$

- 위의 모델에서 $\alpha_i \in \{0,1\}$ 이고, 이는 유저가 물건을 샀는지 , 안샀는지를 의미합니다. 
- 위의 모델에서 $r_i \in [0,inf]$ 을 의미하고 이는 유저가 물건을 샀다면 얼마나 샀는지를 의미합니다. 
- 위의 모델에서 $v_i$ 는 visistor i 에 의해 발생한 수익을 나타냅니다. 

> Parameters

- 이때에! 잘 보셔야 할것은 average avenue per sale 은 $\theta^{-1}$ 로 주어집니다. 
- 그리고 average revenue per visiroe 은 $\lambda\theta^{-1}$ 이 됩니다.
- 우리는 데이터를 이용하여 $c_i , r_i , v_i$ 에 대한 posterior 형성을 하고 싶습니다. 

> ## Notation

- $n_A$ 는 Variant A 에 대한 number of visitor 를 나타냅니다. 
- $c_A$ 는 Variant A 에 대한 number of sales 를 나타냅니다. 
- $s_A$ 는 sales 에 대한 revenue 를 나타냅니다. 
- $s_A^k$ 는 k-th customer 의 sale in variation A 입니다 즉 $$s_A = \frac{1}{c_A}\sum_{k=1} ^{C_A} s_A^k$$ 가 됩니다. 
- 만일 single variable 을 논의할떄에는 (ex : posterior 계산) subscript 를 떼고 본다고 합시다. 

> ## Computing posterior on sale size 

- $\Gamma(k,\theta)$ 는 gamma distribution 으로 다음과 같은 pdf 를 가집니다. 
- $r(x ; k,\theta) = \frac{1}{\Gamma(k)\theta^k}x^{k-1}e^{-x/\theta}$
- exponential with  rate $\theta$ 를 likelihood 라 할때에 prior 를 $\Gamma(k,\Theta)$ 라 하면 posterior 는 아래와 같이 계산됩니다.
  - 이 계산의 경우 exponential 의 모수를 rate 로 할지 , scale 로 할지, gamma 의 $\theta$ 모수를 rate 로 할지 scale 로 할지에 따라 그 posterior 의 형태는 약간씩 달라지나 모두 같은 의미이기 떄문에 혼란스러워 하지 마시길 바랍니다.

$$P(\theta \mid s )\sim \Gamma(k+c, \frac{\Theta}{1+\Theta c s})$$

> ## Total posterior 

- 위의 결과를 바탕으로 우리는 posterior on $(\lambda , \theta)$ 를 jointly 하게 구할 수 있습니다. 

  - $f(\lambda ; a,b)$ 를 $\lambda$ 에 대한 prior 라 합시다.

  - $r(k,\Theta,\theta)$ 를 $\theta$ 에 대한 prior 라 합시다. 

- 이 distribution 에 대해 다음과 같은 공식이 성립합니다. 

$$P(\lambda,\theta \mid n,c,s) = f(\lambda ;  a+c , b +n-c)r(k+c , \frac{\Theta}{1+\Theta c s} ,\theta)$$

> ## Chance to Beat all Revenue

- $\lambda_A , \theta_A,\lambda_B,\theta_B$ 4개에 대해서 각 posterior 를 계산하고 이를 곱하면 4개 hyperparameter 에 대한 posterior 가 계산됩니다. (independent 하다고 가정함)
  - 그러므로 이를 이용하여 아래의 공식을 계산할 수 있습니다. 

$$\begin{aligned}
&P\left(\lambda_{B} / \theta_{B}>\lambda_{A} / \theta_{A}\right) \\
&=\iiint \int \mathcal{H}\left(\lambda_{B} / \theta_{B}-\lambda_{A} / \theta_{A}\right) \\
&\cdot f\left(\lambda ; a+c_{A}, b+n_{A}-c_{A}\right) \gamma\left(k+c_{A}, \frac{\Theta}{1+\Theta c_{A} s_{A}}, \theta_{A}\right) \\
&\qquad \cdot f\left(\lambda_{B} ; a+c_{B}, b+n_{B}-c_{B}\right) \gamma\left(k+c_{B}, \frac{\Theta}{1+\Theta c_{B} s_{B}}, \theta_{B}\right) d \lambda_{A} d \lambda_{B} d \theta_{A} d \theta_{B}
\end{aligned}$$

- 이떄에 $\mathcal{H}$ 는 heaviside step function 으로 $\mathcal{H}(x) = 1\ if \  x \ge 0  $ ,   $\mathcal{H}(x) = 0\ if \  x < 0  $  입니다. 
  - 4변수의 끔찍한 함수 형태이기 떄문에 역시나 MonteCarlo sampling 을 이용할수밖에 없습니다. 

1. 즉 $$\lambda_A^i,\lambda_B^i,\theta_A^i,\theta_B^i$$ 를 각 posterior 에서 뽑아낸 i 번째 샘플이라고 합시다. 
2. 그 이후에 $\lambda_B^i/\theta_B^i > \lambda_A^i/\theta_A^i$  를 계산한 뒤에 M 으로 나눕니다.

> ## making decision based on Revenue 

- 이 경우에도 우리는 loss function 을 계산해야 합니다 
  - 이러한 계산은 다음과 같이 이루어집니다. 

$$\mathcal{L}(\lambda_A,\lambda_B,\theta_A,\theta_B,A) = max(\lambda_B / \theta_B - \lambda_A / \theta_A , 0)$$

$$\mathcal{L}(\lambda_A,\lambda_B,\theta_A,\theta_B,B) = max(\lambda_A / \theta_A - \lambda_B / \theta_B , 0)$$

- 이때에 더 많은 variants 가 있다면, 이전과 같이 정의가 됩니다. 

$$\mathcal{L}(\lambda_A,\lambda_B,\lambda_C,\theta_A,\theta_B,\theta_C,A) = max(\frac{\lambda_B}{\theta_B} - \frac{\lambda_A} {\theta_A} ,\frac{\lambda_C}{\theta_C} - \frac{\lambda_A} {\theta_A},  0)$$

$$\mathcal{L}(\lambda_A,\lambda_B,\lambda_C,\theta_A,\theta_B,\theta_C,B) = max(\frac{\lambda_A}{\theta_A} - \frac{\lambda_B} {\theta_B} ,\frac{\lambda_C}{\theta_C} - \frac{\lambda_B} {\theta_B},  0)$$

- 이로부터 우리는 Expected loss 를 다음과 같이 계산할 수 있습니다. 

$$E[\mathcal{L}](A) = E[\mathcal{L}(\lambda_A,\lambda_B,\lambda_C,\theta_A,\theta_B,\theta_C,A)]$$

$$E[\mathcal{L}](B) = E[\mathcal{L}(\lambda_A,\lambda_B,\lambda_C,\theta_A,\theta_B,\theta_C,B)]$$

- 그 이후 아래와 같은 조건을 만족하는 variant 를 만나게 되면 실험을 중지합니다.

$$\{X \in \{A,B,...\} : E[\mathcal{L}(X)]\le \epsilon\}$$ 

> ## Montecarlo SImulation

- 위 경우에 대해서 montecarlo simulation 을 생각해 봅시다. 
  - 우리는 몇개의 Sample 을 이용하여 Simulation 할지를 생각해 봐야 합니다. 
- 우리는 $M = (- ln\delta) / \epsilon^2$ 을 이용합니다.
  - $\delta$ 는 원하는 probability of error 입니다. 우리는 주로 $10^{-10}$ 을 사용합니다. 
  - $\epsilon$ 은 원하는 error 의 magnitue 입니다. 우리는 주로 $10^{-3}$ 을 사용합니다. 
- 이러한 error bound 는 정확하지는 않지만 참조할만 합니다. 

# [Experiments](#link){: .btn .btn--primary}{: .align-center}

> ## 1. A/A Test

- 우리는 다음과 같이 실험세팅을 해 보았습니다.
  - conversion rate 가 5%
  - revenue / sale 이 25달러 
- 이 경우 standard deviation of data 는 5.6 달러였습니다. 
  - revenue / visitor 의 데이터 평균은 1.25 달러라는것을 기억하면 꽤 심하게 분산이 큰 데이터입니다.
- 이 경우 t-test sample size calculator 에 의하면 test 는 20% 의 lift 를 잡아내기 위해서라면 4250 명의 data point 가 필요합니다. 
- 하지만 SImulation 에서 Bayesian Test 는 평균적으로 3292 개의 data points 를 요구하였습니다. 

![png](/assets/images/Stat/84_5.png)

- 위 그림을 보면 A/B Test 의 termination time 을 볼 수 있습니다. 

> ## 2. Varying conversion rates 

- 우리는 다음과 같은 실험세팅을해 보았습니다. 
  - conversion rate 가 5%(A) , 6%(B) 
  - revenue / sale 이 25달러
- 이 경우에 대해서 400 개의 A/B Simulations 을 실행해볼 수 있었습니다. 
  - Threshold of caring $\epsilon$ 은 mean visitor value 1.25 달러의 2% , 즉 0.025 = $\epsilon$ 로 설정하였습니다.

![png](/assets/images/Stat/84_6.png)

- 이러한 A/B Testing 에서 우리는 Bayesian Test 가 평균적으로 3000개의 data points 를 요구한다는것을 알았습니다.
- 400개가 넘는 SImulations 에서 95.75% 의 실험이 맞는 결과를 내보냈습니다. 

> ## 3. Varying average sale price

- 우리는 다음과 같이 실험세팅을 해 보았습니다. 
  - conversion rate 5%
  - revenue / sale 이 20달러 (A) , 30달러 (B)

![png](/assets/images/Stat/84_7.png)

- 이 실험의 결과는 비슷하였습니다. 
  - error 는 전체 실험의 6% 만 발생하였습니다. 

> ## 4. revenue not from an exponential distribution

- 우리는 다음과 같이 실험 세팅을 해 보았습니다. 
  - Converion rate 5% (A) , 6% (B)
  - sale price 는 unifomrly from [49,129,259] 에서 추출 
- 이번에 A/B Test 는 81% 의 정확성을 보였습니다. 

![png](/assets/images/Stat/84_8.png)

- 위와 같이 평균적으로 3290 개의 data points 를 요구하였습니다. 
  - 19% 의 실험은 8000개의 Sample 을 얻을떄까지 Convergence 가 이루어지지 않았습니다. 
  - 그래서 이런 경우에는 Variation A 를 선택하게 되었습니다. 그래서 Accuracy 가 81%인 것입니다.

> ## 5. Why does Bayesian testing require fewer sample

- 우리는 표본의 수가 급격하게 줄어든것은 확률 분포의 정확한 모델링을 통해 이룬 결과로 보입니다. 
  - CLT 를 단순 이용하게 되면 너무 정보량을 조금 사용하게 됩니다. 또한 CLT 를 사용하게 되면 negative revenue 에 대한 probability 를 허용하게 됩니다. 
  - 그냥 CLT 를 적용하게 되면 '평균은 Normal' 이라는 가정을 하는데, Normal 은 Negative 한  값에도 Support 가 존재하기 떄문입니다.
- 또한 데이터의 형태도 CLT 를 적용하기에 적합하지 않습니다.
  - 우리 데이터의 standard deviation 이 5.6 달러이고, 평균은 1.25 달러라는 것을 기억합시다. 즉 CLT 를 적용하기에 힘겨운 데이터 형태입니다.

**reference**

- <http://ls00012.mah.se/bitstream/handle/2043/28349/Olle%20Caspersson.pdf?sequence=1&isAllowed=y>

 베이즈 AB Test 에 대한 VWO 의 논문입니다. 마지막 Experiment 부분이 약간 부실한게 마음에 안들긴 하는데 (Revenue 가 만일 좀 더 Skewed 가 심한 모양이라던가..) 전체적으로는 적당한 난이도로 잘 서술되어있어서 좋게 읽었습니다. 하지만 실험한 Metric 이 모두 Conversion 기반 (revenue 도 결국 conversion 과 결합된 형태) 이여서 약간 아쉽네요. 클릭수와 같은 완벽한 Continuous data 형태일 경우에는 어떻게 적용되는지에 대한 Paper 도 있으면 좋겠네요.!.
{: .notice--success}

