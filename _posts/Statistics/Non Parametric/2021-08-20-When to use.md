---
title:  "When To Use Nonparametric Test?"
excerpt: "언제 비모수 테스트를 써야하나"
categories:
  - Stat_Non_Parametric
tags:
  - 1
last_modified_at: 2021-08-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

- https://blog.minitab.com/ko/adventures-in-statistics-2/choosing-between-a-nonparametric-test-and-a-parametric-test

# Intro

- 통계 방법론을 사용하는 대부분은 모수 Test 를 사용합니다. 
- 모수 방법론은 , 데이터에 대한 Distribution 을 가정해야되는 등 가정사항이 많이 필요합니다.
- 그에 비해서 비모수 방법론은 데이터에 대한 Distribution 가정이 필요 없습니다.
- 이렇게만 생각하면 비모수 방법론이 더 좋지 않을까요?  왜 비모수 ㅂㅇ법론을 사용하지 않을까요?
- 이러한 주제에 대해서 아래에서 생각해 봅시다. 

![png](/assets/images/Stat/44_1.png)

<br>

# Parametric Test

## 1.모수 검정은 비대칭 / 비 정규 분포에 적합

![png](/assets/images/Stat/44_2.png)

- 위와 같은 가이드라인을 만족하는 경우, 모수 검정을 사용하는게 더 좋다고 합니다. 
- 위 가이드라인은 Minitab 의 통계학자가 시뮬레이션 한 결과라고 합니다 

## 2. 모수 검정은 각 집단의 분포가 다른경우 적합

- 집단을 비교하는 비모수 검정은 모든 집단의 데이터 산포가 동일해야 한다고 가정합니다.
- 즉 집단별로 분포가 다르면 모수 방법론이 좀 더 적합합니다.

## 3. 통계적 검정력

- 보통 모수 검정이 더 통계적 Power 가 큽니다.
- 그러므로 차이에 대해서 좀 더 정밀하게 탐지가 가능합니다.

<br>

# Non-parametric Test

## 1. 중위수가 적절한 Metric 인 경우가 있다.

![png](/assets/images/Stat/44_3.png)

- 예를 들어서 소득에 대한 인구분포를 검정할 경우, 평균은 별로 좋은 지표가 아닙니다.
  - 그 이유는 Outlier 때문입니다. 
- 그러므로 중위수를 테스트 가능한 비모수 방법론을 쓸 수 있습니다.

## 2. 표본의 크기가 매우 작을떄

- 표본의 크기가 작아 어떤 분포를 따르는지 알 수 없을때에 비모수 검정을 사용할 수 있습니다.
- 하지만 이떄에도 조심해야하는것이, 표본의 크기가 극단적으로 작을때 (10개) 에는 비모수 방법론도 사용하기 힘듭니다.
  - 실험의 가정은 만족하지만 , Power 가 형편없어 그 결과를 믿기 힘들어지기 떄문입니다.

## 3. Ordinal 데이터, 특이치에 Robust 하고싶을떄

- 전형적인 모수 검정 방법른은 대부분 Continuous 한 데이터의 경우에만 테스트가 가능합니다.
  - continuous 한 데이터는 특이치에 대해서 큰 영향을 받게됩니다.
  - 또한 Ordinal 한 경우의 처리는 잘 알려진바가 없습니다.
- 하지만 비모수 검정의 경우 Ordinal 의 경우에도 테스트가 가능하며, 특이치에 민감합니다.

<br>

# Refer

- https://blog.minitab.com/ko/adventures-in-statistics-2/choosing-between-a-nonparametric-test-and-a-parametric-test

