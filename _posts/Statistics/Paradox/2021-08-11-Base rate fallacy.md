---
title:  "base rate 의 역설"
excerpt: "기본적인 비율을 무시함에서 오는 에러"
categories:
  - Stat_Paradox
tags:
  - 1
last_modified_at: 2021-08-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# base rate란?

- Base Rate 란, 어떤 요소가 통계적으로 전체에서 차지하는 기본 비율을 가르킵니다. 
- 어떠한 사건이 일어났을때, 그 사건의 기본 비율을 생각하지 못함에서 오는 에러를 Base Rate의 역설 이라고 합니다.

<br>

# Base Rate 의 역설

- 99% 의 정확도를 가지는 암 검사 장비가 있다고 합시다. 

![png](/assets/images/Stat/32_2.png)

- 위와 같은 장비를 이용해 검사를 받았는데 암 환자라는 결과를 얻었다고 합시다.
- 그러면 "아 나는 99% 확률로 암환자야.. ㅜㅜ 이번생은 빠빠이다" 라고 생각해야 할까요? 
- 실상은 그렇지 않습니다. 이러한 분류 문제에 대해서, 내가 1 로 분류되었을때 저희는 True Positive 와  False Positive 의 확률만 생각하지 , 실제 데이터의 수의 비율은 생각하지 못함에서 오는 에러입니다.

![png](/assets/images/Stat/32_1.png)

- 위와 같이 확률로만 비교한다면 TP 는 99% , FP 는 1% 로서, 내 양성(Positive) 결과는 마치 TP (진짜 암환자야) 일 확률이 높아보입니다. 
- 하지만 좀 더 자세히 살펴보면 다른 결과가 나옵니다. 
  - 실제 암 환자의 비율은 1/8000 이라고 합시다. ($p(D) = 1/8000$)
  - $P(D\mid detect D) = p(detect D\mid D)p(D)/[p(detect D\mid D)p(D)+p(detect D\mid notD)p(notD)]$
  - 그렇다면 위의 계산을 해보면, 내가 실제로 암이 걸렸을 확률은 약 1~2% 가 나옵니다.
- 즉 실제 데이터의 비율을 살펴보면 내가 암환자여서 암이라고 진단되었다기 보다는 , 암환자가 아님에도 오분류로 암이라고 분류될 확률이 높다는 것입니다.
- 이는 기본적으로 비율이 매우 Imbalanced 되어있는 경우에 일어나는 역설입니다.

