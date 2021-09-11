---
title:  "왜 Logistic 을 더 선호하는가?(~ing..)"
excerpt: "Logistic,Probit,cloglog 모델의 비교"
categories:
  - Regression
tags:
  - 1
last_modified_at: 2021-08-02

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# 1. Linear model?

![png](/assets/images/Stat/27_1.png)

- 위와 같은 모델은, y 변수가 bounded 되어야하는 것입니다.
- 이러한 제한식이 걸리게되면 최적화도 어려우며, 추정이 잘 되지 않습니다. 
- 그러므로 y 변수를 좀 늘리고 떙겨서 범위를 -inf ~ inf 까지 늘려주고싶습니다. 

# 2. Link Function

- 링크 function 을 y 쪽 (정확하게 말하면, 추정하고자 하는 $E[X\mid y]$  에 붙여서 Linear 하게 추정하고자 하는것이 바로 링크함수의 역할입니다.) 에 붙여 추정해 봅시다.

![png](/assets/images/Stat/27_2.png)

- 이때 위처럼 Link Function 을 용할 수 있는데, 이 떄에 사용할 수 있는 Link 는 아래와 같이 3가지입니다.

![png](/assets/images/Stat/27_3.png)

- 이 경우 위의 3개 링크 Function 에서 제일 널리 쓰이는것은 바로 Logit Fnction 입니다. 
- 왜 Logistic regression 이 제일 널리 쓰이게 되었을까요? 

<br>

# First : 더 일반적임

![png](/assets/images/Stat/27_4.png)

- 우선 cloglog 모델은, 확률값에 대해 모양이 대칭적이지 않습니다. 
  - 이런 대칭을 가지는 모델은, 일반적으로 적용하기 힘들다고 합니다.
- 이에 반해 Logistic/probit 모델은 대칭이므로 훨씬 일반적이라고 합니다. 

# Second : 훨씬 해석이 쉬움

- Probit regerssion 이 감싸고 있는것이 cdf 임을 기억합시다.
- 즉 Logistic regression 에서는 1 단위 증가하면 로짓이 1늘어난다 같은 해석이 가능했지만 probit 은 cdf 함수를 넣어 설명하기 떄문에 설명하기가 어렵습니다.
- 즉 Logistic 이 훨씬 설명하기가 쉽다고 합니다.

<br>

# Refer

- <https://towardsdatascience.com/why-is-logistic-regression-the-spokesperson-of-binomial-regression-models-54a65a3f368e>

- https://aip.scitation.org/doi/pdf/10.1063/1.5139815
- http://www.columbia.edu/~so33/SusDev/Lecture_9.pdf
- https://igija.tistory.com/338
- http://www.stat.ualberta.ca/~kcarrier/STAT562/comp_log_log.pdf
