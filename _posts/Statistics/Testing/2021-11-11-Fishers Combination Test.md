---
title:  " Global Testing (Fisher combination and Bonfferoni method)"
excerpt: "Fisher 의 Multivariate Testing 에서 Global null 을 검정하는 방법"
categories:
  - Stat_Testing
last_modified_at: 2021-11-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 Null Hypothesis 가 맞다면 p-value 가 Uniform 을 따르는것은 알 수 있습니다. 그렇다면 이렇게 'Null 이 맞을때의 분포' 를 알고있는데 테스트를 안하는것은 너무 억울하지 않나요? 이를 이용한 방법이 바로 Fister 의 Combinations Testing 입니다. 
{: .notice--warning}

# [Global test](#link){: .btn .btn--primary}{: .align-center}

- Multiple Testing 에서 우리는 다수의 Hypothesis 를 동시에 검정하고자 합니다.
  - 강한 사람과 전립선암에 걸린 사람들 사이에 각 유전자의 발현 수준에 대한 n개의 유전자와 데이터가 있다고 합시다.
  - 즉 우리는 전립선암과 특정 유전자와 어떠한 관련이 있는지에 대해서 알고 싶습니다. 

![png](/assets/images/Stat/100_1.png)

- 우리는 i th null hypotheiss 를 $H_{0,i}$ 라고 정의하겠습니다. 
  - 이는 유전자의 발현 수준이 두 그룹의 환자에서 동일했다는것을 나타냅니다.

> ## Global Testing

$$H_{0}=\bigcap_{i=1}^{n} H_{0, i}$$

- 위와 같은 Null Hypothesis 를 검정하는것을 Global Testing 이라고 합니다.
  - 위의 Null hypothesis 는 모든 Individual 한 Hypothesis 가 True 일 떄에만 성리반다는것을 기억합시다.
- 각각의 individual 한 Null Hypothesis 가 True 라고 합시다. 
  - 그렇다면 우리는 각각의 Testing 에 대해서 p - value , 즉 $p_1 ... p_n $ 을 알고 있을것입니다. 
  - 그리고 null 이 맞다면 각 p value 는 $p_i \sim U[0,1]$ 이라고 할 수 있습니다. 
  - 즉 이러한 분포를 가지고 Global Hypotheiss 를 테스팅 할 수 있을것입니다.

> ## Bonfferoni Method

- 본페로니 방법은 우리가 이전에 Multiple Testing 에서도 알아보았지만 매우 Global 하게 적용 가능한 방법론입니다. 
  - 첫눈에는 그냥 Naive 한것같지만 은근 학계에서도 많이 쓰이는 표준같은 정리입니다.

> Procedure

- Desired level $\alpha$ 에 대하여 Bonfferoni global test 는 rejects the global null whenever

$$min_i p_i \le \alpha / n$$

> Proof

- 하지만 위와 같이 Decision Rule 을 정한다면 우리가 원하는 level 인 $\alpha$ 로 False positive 를 제한할 수 있을까요? 

$$\begin{aligned}
\mathbb{P}_{H_{0}}(\text { Type I Error }) &=\mathbb{P}_{H_{0}}\left(\bigcup_{i=1}^{n} p_{i} \leq \alpha / n\right) \\
&=\sum_{i=1}^{n} \mathbb{P}_{H_{0}}\left(p_{i} \leq \alpha / n\right) \\
&=\sum_{i=1}^{n} \alpha / n \\
&=\alpha .
\end{aligned}$$

- 위와 같은 부등식이 성립합니다! 그러므로 우리의 테스팅은 유효합니다.

> but... Conservative.. Right? 

- 본페로니 방법론에 대한 오해중 하나가, 너무 Conservative 하게 테스팅을 진행한다는 것입니다. 
  - 즉 우리가 원하는 수준보다 훨씬 빡쎄게 (즉 0.05 의 false positive level 을 원하는데 0.045 가 되는식) 검정한다는 오해가 있죠

$$\begin{aligned}
\mathbb{P}_{H_{0}}(\text { Type I Error }) &=1-\mathbb{P}_{H_{0}}\left(\bigcup_{i=1}^{n} p_{i} \geq \alpha / n\right) \\
&=1-\left(1-\frac{\alpha}{n}\right)^{n} \\
& \stackrel{n \rightarrow \infty}{\longrightarrow} 1-\exp (-\alpha)=: q(\alpha)
\end{aligned}$$



- 하지만 위를 보면 그렇지가 않습니다. 유의수준 $\alpha$ 에 어느정도 잘 맞게 테스트를 진행하고 있음을 알 수 있습니다 ! 
  - 그러므로 n 을 아무리 증가시킨다 하여도, 실질적인 $\alpha$ 값은 우려처럼 낮아지지 않을것입니다.
- 한 예시로 $\alpha = 0.05$ 일때에 n 이 무한대로 간다 하더라도 그 수준은 $1- exp(-\alpha) = 0.0488$ 입니다. 

> Intuition 

![png](/assets/images/Stat/100_1.png)

- 위의 본페로니 방법론은 p-value 를 Sorting 한 이후에 그중에서 제일 작은 p-value 를 보는 바법론입니다.
  - 위의 그림에서 P-value 는 Uniform 한 분포를 따르므로 일반적으로는 X=Y 직선 위에 점이 분포하겠죠? 
- 위의 그림에서 만일 $\alpha/n$ 보다 작은 값이 존재한다면 Global Null hypothesis 를 기각하게 됩니다! 
- 하지만 위처럼 우리는 '작은 p-value 를 가지는 소수' 에만 집중하게 됩니다. 
  - 즉  bonferroni 방법은 소수의 집단이 크게 다를때에 더 효과적인 방법론이라고 할 수 있습니다! 

> ## Fisher's Combination Test

- 위에서 살펴본 Bonferroni 방법과 완전히 다른 방법은 바로 Fiser 의 Combination Testing 입니다.
  - Fisher 의 Combination Testing 아래의 Statsitic 이 큰 값을 가질떄에 Null 을 기각하게됩니다.

> Procedure 

- $T = - \sum _ {i=1}^n 2log p_i > \chi^2_{2n}(1-\alpha)$ 

> Proof 

- 하지만 우리는 위와 같은 통계량이 어떤 분포를 따르는지를 정확하게 알아야 합니다. 
  - 어떠한 분포를 따르는지 알기 위해서는 모든 Test 가 Independent 하다는 가정이 있어야 함을 기억합시다.

Suppose $p_1, . . . p_n$ are independent. Then under the null hypothesis, $T \sim χ^2_{2n}$

- 위를 증명하기 위해서는 , 몇가지 Probability Theory 에 대해서 알아두면 됩니다. 
  - $p_{i} \sim U[0,1] \Longrightarrow-\log p_{i} \sim \operatorname{Exp}(1)$
  - $E \sim \operatorname{Exp}(1) \Longrightarrow 2 E \sim \chi_{2}^{2}$.
- 그러므로 모든 $p_i$ 가 independent 면, $T \sim \chi^2_{2n}$ 이 됩니다.

> Intuition 

- 이떄 위의 Fisher Combination 의 통계량은 '모든 p-value' 에 대해서 고려하고 있다는것을 기억합시다. 
- Thus, Bonferroni’s method works better for detecting a few larger changes in the individual tests, while Fisher’s test works better for detecting many subtle changes
  - 즉 Fisher Test 은 '전체적으로 subtle 한 change' 를 검정하는데에 효과적이라면, Bonferroni Testing 은 특정한 individual 이 크게 변하는것을 검정할떄에 효과적이라고 할 수 있겠네요

   **Reference**

- <https://statweb.stanford.edu/~candes/teaching/stats300c/Lectures/Lecture01.pdf>

