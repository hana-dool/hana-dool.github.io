---
title:  "Inference in Linear regression"
excerpt: "OLS 에서 Inference 는 어떻게 이루어질까"
categories:
  - Regression
tags:
  - 1
last_modified_at: 2021-09-01

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true

---

# 1.개별 값에 대한 Inference 

## 1.1 $beta$ 추정하기

- 우선 $\beta$ 를 어떻게 추정할 수 있을지 Simple Linear regression 에서 알아봅시다.
- LSE 방법론을 적용한다면, Error^2 을 최소화 하는 방법으로 추정하려 합니다.
- 그에 따라서 '최소값' 을 찾는 문제로 바뀌고, 아래 그림과 같이 $\beta$ 가 추정됩니다. 

![png](/assets/images/Stat/50_1.png)

![png](/assets/images/Stat/50_2.png)

- 위와 같은 방법론에 의해 추정이 됩니다. 
- 참고로 이러한 추정량은 , Normal Error 모델에서의 MLE 추정량과 같습니다. 

![png](/assets/images/Stat/50_3.png)

## 1.2 Inference

- 우리는 위처럼 그 값을 추정할 수 있으며 , 이에따라 그 평균 , 분산등을 추정할 수 있습니다.
- 먼저 $b_1$ 에 대한 분산 , 평균 추정은 아래와 같습니다. 

![png](/assets/images/Stat/50_4.png)

- 위에 대한 추정을 하기 전에 먼저 아래의 사실을 먼저 알고갑시다.

![png](/assets/images/Stat/50_6.png)

- 위 사실로부터 우리는 아래와 같이 추정해낼 수 있습니다.

![png](/assets/images/Stat/50_5.png)

## 1.3 Multiple ? 

- Multiple Regression 일때에도 위와 같은 로직을 따르게 됩니다. 

![png](/assets/images/Stat/50_7.png)

<br>

# 2. 전체적인 계수에 대한 Inference

## 2.1 Anova Table

![png](/assets/images/Stat/50_8.png)

- 먼저 위와 같이 SSTO 를 SSR, SSE 로 분해합니다.

![png](/assets/images/Stat/50_9.png)

- 그 해석은 위와 같습니다.
  - SSTO : 전체적인 변동량
  - SSR : 회귀선이 설명하는 변동략
  - SSE : 회귀선이 설명하지 못하는 변동량

##2.2 F-Test 

![png](/assets/images/Stat/50_10.png)

![png](/assets/images/Stat/50_11.png)

- 위와 같이 MSR / MSE 를 통해서 $\beta = 0 $ 의 검정을 하게 됩니다. 

## 2.3 Multiple ? 

![png](/assets/images/Stat/50_12.png)

- Multiple 의 경우에도 위와 비슷한 로직을 따라가게 됩니다.

# Refer 

- 연세대학교 회귀분석 강의자료
