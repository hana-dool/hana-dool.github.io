---
title:  "Partial Dependence Plot (PDP)"
excerpt: "변수를 움직이며 평균영향을 측정하기"
categories:
  - Interpretable_ML
tags:
  - 1
last_modified_at: 2021-09-01

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# PDP

![jpg](/assets/images/ML/1_14.jpg)

- 문제 상황이 나이 , 피임약 복용 기간으로 자궁암 (1,0) 을 분류하고 싶다고 하자. 
  - 왼쪽 그림과 같이 나이 / 복용 기간을 살짝씩 변화시키면서 자궁암 양성의 확률 예측을 살펴볼 수 있습니다.
  - 또는 오른쪽 그림과 같이, 두 값을 모두 변화시키면서 그 예측의 추이를 살펴볼 수 있습니다.

![jpg](/assets/images/ML/1_15.jpg)

- 현제 저희는 , 관심대상 ($X_s$) 이 변함에 따라서 모델이 어떻게 예측하는지를 보고 싶습니다.
  - 위의 1번 식처럼, 모델의 $X_s$ 에 대한 예측값은 나머지 관심없는 변수 $X_c$ 들의 Marginal 한 평균으로 계산이 됩니다. 
- 즉 Marginalize 하여서 하나의 변수에 대한 target 의 영향을 어느정도 알 수 있습니다.
- 하지만 $P(X_c)$ 를 알 수 없기떄문에 몬테카를로 방식으로 샘플링을 하여서 대체하게 됩니다. 
  - 즉, 변수의 갯수가 많아진다면 엄청나게 많은 샘플링을 해야된다는것을 알 수 있습니다.

# 장단점

![jpg](/assets/images/ML/1_16.jpg)

- 해석이 매우매우 쉽고 , 구현이 쉽습니다. 
- $X_c$ 에 대해서 몬테카를로 방법으로 $P(X_c)$ 를 구하기 떄문에 계산량이 매우 많습니다.
- 고정된 $X_s$ 에대해서 Marginalize 를 한다는것 자체가, $X_c$ 와  $X_s$ 간의 분포를 무시하는 일입니다.
  - 예를 들어서 , 키(해석하고자하는 $X_s$) vs 연봉(Target) 이라 합시다.
  - 이 경우 pdp 를 생성하기 위해 키 = 200cm 로 고정 후 MArginal 효과를 구하기 위해 $X_c$(몸무게) 를 추정한다고 합시다. 
  - 이 경우에 $X_c$ 를 20kg , 50kg .. 등을 생성하였는데, 키가 200cm 인 경우 20kg 의 몸무게는 불가능합니다. (분포 무시)

<br>

# 주의점

## **feature distribution**에 대해선 고려를 하지 않았다. 

-  PDP는 독립성 가정이 제일 큰 문제입니다. 
- 부분의존성이 계산되는 특성값은 다른 특성값과 상관관계가 없다고 가정합니다. 
- 예를 들어, 사람의 몸무게와 키를 고려할 때, 사람이 얼마나 빨리 걷는지 예측하고 싶다고 가정해봅니다. 
  - PDP 를 계산할때에 키를 고정해두고, 몸무게를 변화시키며 그 평균을 통해서 키에대한 Marginal 예측을 형성하게 됩니다.
  - 즉 이러한 경우 200cm 의 장신에 대해서 예측할떄에, 몸무게의 한계 분포를 평균하는데, 이는 2미터의 사람에게 비현실적인 50 kg 미만의 중량을 포함할 수 있습니다. 
- 즉 특성값이 상관있을때 실제 확률이 매우 낮은/ 불가능한 특성값 분포 영역에서 새로운 데이터 지점을 생성하게 됩니다. (예를 들어 키가 2m이지만 몸무게가 20kg 인 데이터를 생성)
- 이 문제에 대한 한 가지 해결책은 한계 분포 대신 조건부로 작동하는 누적지역효과도(Accumulated Local Effect plots) 또는 짧은 ALE이라 합니다.

## Mean 만을 표기하여 다른 효과는 드러나지 않을 수 있다.

- 이는 pdp보다는 mean(평균)의 문제이기도 한데, mean으로 인해 미처 보지못하는 효과가 있을 수도 있다.
  - 예를 들어 데이터의 상위 50%는 positive한값, 하위 50%는 negative한 값이 나오면, 평균으로 나오는 f(Xs)f(Xs)는 0에 가깝게 나와 효과가 없는것으로 보인다. 
  - 이처럼 ‘통합’으로 인해 생기는 문제를 보완하기 위한것이 [individual conditional expectation curves](https://christophm.github.io/interpretable-ml-book/ice.html#ice) 입니다.

# Refer

- http://dmqa.korea.ac.kr/activity/seminar/297
- https://godongyoung.github.io/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D/2019/04/13/Partial-Depedence-Plot.html
- https://eair.tistory.com/20?category=883307
