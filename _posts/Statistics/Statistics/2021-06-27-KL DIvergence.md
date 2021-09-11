---
title:  "KL divergence"
excerpt: "분포의 차이"
categories:
  - Stat
tags:
  - 1
last_modified_at: 2021-06-27

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

- 정보이론에서 KL divergence 가 어떤 의미이고 어떻게 쓰일 수 있는지에 대해서 알아보겠습니다. 

# <center><font size="10">Intro</font></center>

![png](/assets/images/Stat/4_1.png)

- 위와 같이 KL - divergence 가 정의됩니다. 
- 이는 알려지지않은 분포 p 를 추정하기 위해 q 를 사용하였을때에 필요한 추가 정보량 이라는 의미를 가지고 있습니다. 
- '두 분포 사이의 거리' 라고 Mild 하게 해석할 수도 있지만, 엄밀히 말하면 '거리' 의 성질인 Symmetric 을 만족하지 못하여 틀린 말입니다. 
  - 하지만 여기에서는 편의상 '거리' 라고 말하겠습니다.

> - $D_{kl}(p \mid \mid q) \ge 0 $
>
> - $D_{kl}(p \mid \mid q) = 0  \leftrightarrow p =q$
>
> - $D_{kl}(p \mid \mid q) \not = D_{kl} (q\mid \mid p) $ 

- 위의 사실을 이용한다면 두 분포의 '거리' 를 KL - Divergence 로 추정할 수 있을것입니다. 

<br>

# <center><font size="10">MLE </font></center>

- 우리가 모델링하고자하는, 알려지지 않은 분포 p(x) 로 부터 데이터가 만들어지는 상황을 가정해보자. 
- 변경 가능한 매개변수 $\theta$ 로 표현되는 분포 $q(x\mid \theta)$ 를 이용해 $p(x)$ 를 추정하려 할 수 있다.
  - 통계학에서는 통상 $q(Data \mid \theta)$ 를 최대화 하는 $\theta ^*$ 를 추정한뒤, $q(x\mid \theta^*)$ 를 $p(x)$ 의 분포로 사용하려 하였다.
  - 하지만 여기에서는 $D_{kl}(p(x) \mid q(x\mid \theta))$ 를 최소화 하는 방법으로 q 를 추정한다고 합시다. 
- 먼저 $q(x\mid \theta)\in Q(\theta)$ 를 가정합시다.
  - q 함수를 parameter function space 로 제한을 둡니다. 
  - 이 경우 각 함수 q 는 parameter $\theta$ 에 의해 완전히 결정됩니다. 
  - 즉 function optimize problem 에서 parameter optimize problem 이 되어 좀 더 문제풀이가 쉬워집니다. 
- 그리고 $x_1 .... x_n$ 을 데이터들이라 가정합시다. 

![png](/assets/images/Stat/4_2.png)

- 위와 같이 KL divergence 을 최소화하는것은, 결국 $q(x\mid \theta)$ 를 최대화 하는 문제, 즉 MLE  문제와 같아집니다.

