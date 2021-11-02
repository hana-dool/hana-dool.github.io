---
title:  "Bayes Factor"
excerpt: "베이즈 펙터를 이용하여 가설검정과 모델 Selection 을 해보자"
categories:
  - Bayes
last_modified_at: 2021-11-02

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Bayesian Statistics 를 쓴다고 해도, 특정 가설에 대해서 Testing 하고 싶은 니즈는 있을것입니다. 이러한 가설검정을 수행할 수 있는 방법을 소개하고자 합니다.
{: .notice--warning}

# [Hypothesis Testing](#link){: .btn .btn--primary}{: .align-center}

> ## Idea

- 베이지안 통계 분석이 매력적인것중에 하나는 '두개의 Hypothesis' 를 직접 비교 가능하다는 점입니다. 
- 기존 NHST 에서는 이러한 접근이 불가능 하였습니다. 
  - 가설 검정이 $H_0 \ vs \ H_1$ 로 이루어지는데, 이 때에 기준이 되는것은 '$H_0$ 가준으로 계산된 p-value' 라는 점입니다. 
  - p-value 의 정의가 '$H_0$ 을 가정할때 우리 데이터가 대립가설 방향으로 얼마나 이상한가?'  인 것을 고려하면 대립가설의 정보는 극히 미미하게 반영됩니다."
  - 게다가 대립가설을 명료한 형태로 기술하는 경우 자체도 드물었습니다. 
  - 이러한 차이로 인해서 Bayes 와 Freq 의 Testing 의 결과가 다른 경우도 생기는데요, Lindley's Paradox 를  참고하시면 좋을것 같습니다. (제 블로그에도 정리를 해 두었습니다.)
- 베이즈의 경우는 두개의 가설에 대해서 직접적인 비교가 가능합니다 ! 
  - 데이터가 $H_0$ 과 $H_1$ 중에서 어떤것을 더 지지하는지에 대해서 구체적으로 계산할 수 있습니다. 

> ## definition 

- 확률 법칙에 의하면 아래의 공식이 성립합니다. 

$$\frac{P(H_1 \mid D)}{P(H_0 \mid D)} = \frac{P(D \mid H_1)}{P(D \mid \H_0)} \cdot \frac{P(H_1)}{P(H_0)}$$

- 좌변은 데이터를 관측한 후의 Posterior 를 고려할떄에 $H_1$ 이 맞을 확률이 $H_0$ 이 맞을 확률보다 몇배인지를 계산하게 됩니다. 
  - 즉 두 가설의 Posterior 의 비에 해당되고, 이를 Posterior Odds 라고 부릅니다. 
- 이 떄에 좌변운 다시 우변의 두 항으로 계산되는데, 앞의 항 ($\frac{P(D \mid H_1)}{P(D \mid \H_0)}$) 을 Bayes Factor 라 하고 뒤의 항 $\frac{P(H_1)}{P(H_0)}$ 을 Prior odds 라 부릅니다. 
  - 다시 말해서 다음과 같이 계산된다고 할 수 있습니다. 

$$(Posterior \ Odds) = (Bayes Factor) \cdot (Prior \ Odds)$$

- 위의 식을 , 다시 표현하면 다음과 같습니다. 

$$Bayes Factor = \frac{Posterior \ Odds}{Prior Odds}$$

> Interpret 1 

- 위 공식을 볼때에 Bayes Factor 의 의미는 뭘까요? 
  - 데이터를 관측한 후에 Odds ratio 가 관측 전의 Odds ratio 의 몇배인지를 나타냅니다.
  - 즉 데이터 관측 후에 가설이 가설(대립가설) 이 참이라는 믿음이 몇배의 비율로 올라갔는지를 나타냅니다. 
- 만일 BF 의 값이 1 보다 크다면 $H_1$ 을 지지한다는 것이고, 0 보다 작다는것은 $H_0$ 을 지지한다는 의미일것입니다. 

> Interpret 2 

- Bayes Factor 의 공식을 바로 살펴보면 ($\frac{P(D \mid H_1)}{P(D \mid \H_0)}$) 입니다. 
- 분자는 $H_0$ 이 맞다는 가정 하에서 데이터를 관측할 확률 $P(D\mid H_1)$ 입니다. 
- 분모는 $H_1$ 이 맞다는 가정 하에서 데이터가 관측할 확률 $P(D \mid H_0)$ 입니다.
- 즉 정리하자면 각각의 가설이 데이터를 설명하는 비율 으로도 생각할 수 있습니다.

> ## Criterion 

- 위의 베이즈 펙터를 이용하여 가설검정ㄹ을 하게 된다면 결국 p-value 의 0.05 처럼 그 기준이 필요하게 됩니다.
- 아래의 기준은 Jeffrey 가 BF 가 $H_0$ 을 지지할때에 베이즈 인자($\frac{P(D \mid H_0)}{P(D \mid \H_1)}$)  값을 정리한 것입니다.

| $log(BF)$ | BF        | H0 의 지지도 정도    |
| --------- | --------- | -------------------- |
| 0 to 1/2  | 1 to 3.2  | 쉽게 판단하기 어려움 |
| 1/2 to 1  | 3.2 to 10 | 조건부적으로 지지    |
| 1 to 2    | 10 to 100 | 강하게 지지          |
| > 2       | > 100     | 결정적으로 지지      |

- 위와 같이 BF 를 정하는 기준이 매우 유연하다는 장점이 있습니다.
  - Freq 를 쓸때에 0.051 의 p-value 를 얻으면 분하지만 어쩔 수 없었던 경험이 있었을 것입니다.
  - 하지만 Bayes 를 써서 BF 를 구하면 충분하면 충분한대로 받아들이면 되고, 아니면 받아들이지 않으면 그만입니다.

> ## Example

- $Y \sim B(10,\theta)$ 일때에 $H_0 : \theta = \frac{1}{2} $ vs $$H_1 : \theta \not = \frac{1}{2}$$ 라 합시다. $H_0, H_1$ 의 사전확률이 동일하고 $H_1$ 하에서 $\theta \sim beta(1,1)$ 이며 관측값이 7 일때에 귀무가설을 지지하는 베이즈 인자($BF_{01} = $($\frac{P(D \mid H_0)}{P(D \mid \H_1)}$) 를 구해보고 판단하세요.

$$\begin{aligned}
B_{01} &=\frac{\alpha_{0} / \pi_{0}}{\alpha_{1} / \pi_{1}}=\frac{p\left(y \mid \theta_{0}\right)}{\int_{\Theta_{1}} p(y \mid \theta) g(\theta) d \theta}=\frac{p\left(Y=7 \mid \theta=\frac{1}{2}\right)}{\int_{\Theta_{1}} p(y \mid \theta) d \theta} \\
&=\frac{\left(\begin{array}{c}
10 \\
7
\end{array}\right)\left(\frac{1}{2}\right)^{7}\left(1-\frac{1}{2}\right)^{3}}{\int_{0}^{1}\left(\begin{array}{c}
10 \\
7
\end{array}\right) \theta^{7}(1-\theta)^{3} d \theta}=\frac{1}{2^{10}} \frac{1}{\int_{0}^{1} \theta^{8-1}(1-\theta)^{4-1} d \theta}=\frac{1}{2^{10}} \frac{\Gamma(8+4)}{\Gamma(8) \Gamma(4)} \\
&=\frac{1}{2^{10}} \frac{11 !}{7 ! \cdot 3 !}=\frac{1}{2^{10}} \frac{8 \cdot 9 \cdot 10 \cdot 11}{2 \cdot 3}=\frac{2^{4} \cdot 3^{2} \cdot 5 \cdot 11}{2^{11} \cdot 3}=\frac{165}{2^{7}}=1.2890625
\end{aligned}$$



- 위의 값을 보면 귀무가설을 좀 더 지지하고 있음을 알 수 있습니다.

# [Model Selection](#link){: .btn .btn--primary}{: .align-center}

> ## Idea

- 아이디어는 이전과 똑같습니다. 가설 ($H$) 을 그냥 모델 ($M$) 으로만 바꾸어 생각하면 됩니다. $\frac{P(D \mid M_1)}{P(D \mid M_0)}$
  - 이 경우, 모델을 고려할때에 데이터가 얼마나 지지하느냐 아니냐 를 통해서 Model 을 결정하게 됩니다.

> ## Example

- 데이터 $D$ 는 10개의 문항중에에서 9개를 맞았다고 합시다. 
  - 그리고 Likelihood 는 BInomial 로 처리하고, 맞을 확률은 $\theta$ 로 모델링 한다고 합시다.
- 이떄 prior 에 따라서 다른 모델이 만들어지는데요, 다음과 같이 만들어진다고 가정하겠습니다.
  - $M_1 :$  prior 를 $\theta$ = 0.5
  - $M_2 :$  prior 를 $\theta \sim Beta(1,1)$ 
- 위와 같은 모델에 대해서 , Bayes Factor 를 계산하기 위하여 $p(D \mid M)$ 을 계산해 봅시다.

$$P(D\mid M_1) = 0.00977$$ 

$$\begin{aligned}
P\left(D \mid M_{2}\right) &=\int_{0}^{1} P\left(D \mid \theta, M_{2}\right) d \theta \\
&=\int_{0}^{1}\left(\begin{array}{c}
10 \\
9
\end{array}\right) \theta^{9}(1-\theta)^{1} d \theta \\
&=\int_{0}^{1}\left(\begin{array}{c}
10 \\
9
\end{array}\right)\left(\theta^{9}-\theta^{10}\right) d \theta \\
&=10\left[\frac{\theta^{10}}{10}-\frac{\theta^{11}}{11}\right]_{0}^{1} \\
&=10 \times \frac{1}{110}=\frac{1}{11}
\end{aligned}$$

이 경우 Bayes Facor ()는 0.107 이며 , 

**reference**

- <https://en.wikipedia.org/wiki/Bayes_factor>
- <http://posterior.egloos.com/9637425>

위와  
{: .notice--success}

