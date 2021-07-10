---
title:  "Limiting 분포"
excerpt: "Large N 일떄의 극한분포"
categories:
  - Stat
tags:
  - 1
last_modified_at: 2021-07-08

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# Binomial -> Normal

아래와 같이 CLT 로 인해서 Binomial 과 Normal 의 관계가 성립하게 된다. (n 이 충분히 크기만 하면 된다!)

![png](/assets/images/Stat/15_1.png)

<br>

# Binomial -> Poisson

$B(n,p) \to Pois(np)$ when $ n \to \inf , p \to 0 $ (가이드는 없지만 $ 100 \le n , p \le 0.01$ 이라고 한다..)

아래 식에서 since , and 부분의 식을 볼때에 n->inf / p->0 의 식이 필요함을 볼 수 있다.

![png](/assets/images/Stat/15_2.png)

아래와 같이 poisson 분포는 lambda 가 커질수록 Normal 에 가까워진다는것을 볼 수 있다.

![png](/assets/images/Stat/15_3.png)

<br>

# Poisson -> Normal

$\lambda$ 가 충분히 크다면 $pois(\lambda) \sim N(\lambda , \lambda)$  가 성립한다. 이 이유는 아래와 같다.

![png](/assets/images/Stat/15_4.png)

<br>

# hypergeometric -> Normal

![png](/assets/images/Stat/15_5.png)

<br>

# beta -> Normal

![png](/assets/images/Stat/15_6.png)

<br>

# ChiSquared -> Normal

![png](/assets/images/Stat/15_7.png)

<br>

# Gamma -> Normal

- $X_1 \sim \Gamma(a_1,b)$ , $X_2 \sim \Gamma(a_2,b)$  에 대해서,  두 r.v. 가 서로 독립이면 $X_1 + X_2 \sim \Gamma(a_1 + a_2 , b)$ 입니다. 
- 즉 CLT 에 의해서 a 가 크면 ( Shape ) Normal 에 가까워진다고 할 수 있습니다. 

![png](/assets/images/Stat/15_8.png)

> Q. 아니 그러면 모든 Gamma 는 Normal 아닌가요? 왜냐하면 Gamma(1,1) 도 결국에는 $\Gamma(0.01,1)+\Gamma(0.01,1) .....$ 아닌가요?

- 아닙이다. 위와 같은 로직이라면 모든 Additive 성질이 있는 Distribution 은 Normal 이겠죠.
- 물론 $\Gamma(0.01,1)$ 을 무한에 가깝게 더하게되면, $X = \sum X_i$ 는 Normal Approximation 이됩니다.
- 하지만 위 예시는 100개뿐이죠. 게다가 각각의 $\Gamma(0.01,1)$ 은 분산이 매우 크다는 점에서 Normal 로 근사하기까지는 매우 큰 표본이 필요합니다. 

![png](/assets/images/Stat/15_10.png)

- 위와 같은 그래프가 Normal 이 되려면 Sample 수가 적어도 10000개는 필요할 것입니다. 
  - 즉 쪼개놓은 각각의 그래프는 Normal 근사가 쉽지 않아서 CLT 가 성립하지 않는것입니다.

 <br>

# T distribution -> Normal

![png](/assets/images/Stat/15_9.png)

##Ref

- https://modelassist.epixanalytics.com/display/EA/Normal+approximation+to+the+Gamma+distribution

