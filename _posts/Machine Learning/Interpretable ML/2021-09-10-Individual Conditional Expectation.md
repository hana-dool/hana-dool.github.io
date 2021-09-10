---
title:  "Individual Conditional Expectation (ICE)"
excerpt: "PDP 에서 하나하나 떼서 살펴보기"
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

# ICE

![jpg](/assets/images/ML/1_17.jpg)

- 이전에, PDP 는 모든 데이터에 대해서 예측값을 평균 내서 관심 변수의 영향력을 근사했습니다.
- 하지만 이러한 통합에서 오는 문제 (Correlation 되어있다거나, Skewed 된 경우 평균은 왜곡됨)를 보완하기 위하여 ICE 가 고안되었습니다.

![jpg](/assets/images/ML/2_2.png)

- 즉 관심없는 변수 $X_c$ 를 유지한 상태에서 관심변수 $X_s$ 를 조금씩 움직이며 모든 Train 데이터에 대해 그 예측이 어떻게 변하는지를 보여준 것입니다. 
- 이때 PDP 는 ICE 의 각 라인을 평균낸 것입니다.

![jpg](/assets/images/ML/2_1.png)

- 위의 예시를 봅시다. 우리는 나이에 따른 유방암 유무 의 효과를 보고싶습니다. 
  - 그래서 Age 를 X 축으로 (관심변수) 변화시키면서 각 선 (각 선은 여기에서 하나의 데이터를 나타냅니다.) 의 예측 발병률을 살펴봅니다. 
  - 이 경우 대부분의 예측이 0~0.1 에 몰려있고 소수의 값이 0.3을 넘는것을 볼 수 있습니다. 
  - 즉 이를 Mean (PDP) 해서 보게 된다면 극단값에 의해 의미가 왜곡될 수 있습니다. 
  - 그러므로 PDP 에서 볼 수 없는 상세한 관계를 볼 수 있게됩니다.

<br>

# 주의점

- 앞에서 살펴보았던 PDP 와 같이 실제 데이터의 분포를 유의해야합니다. (Corr 되어있는경우가 문제될 수 있습니다.)
  - ex) 나이와 몸무게는 연관되어있습니다. 10살의 경우 100kg 일 수는 없을것입니다. 하지만 ICE 에서는 이런 관계를 무시하고 독립이라 하고 진행합니다.
- 데이터의 갯수가 많으면 선이 너무 많아집니다. '

<br>

# Centered ICE Plot

- ICE 는 선들이 너무 난잡하여 $X_s$ 에 대한 효과의 트랜드를 정확히 파악하기가 어렵습니다. 

![jpg](/assets/images/ML/2_1.png)

- 위 그림을 다시 보면 나이가 20살~25살인 경우에는 대체 상승의 트랜드인지, 감소의 트랜드인지 알기가 어렵습니다. 
- 그러므로 모든 ICE 의 선을 0,0 에서 시작하게 만들어 Trend 를 살펴보는것이 C-ICE plot 입니다. 

![jpg](/assets/images/ML/2_3.png)

- 위와 같이, 특정 지점 (대부분 0,0 을 선택합니다.) 을 중심에 놓고 차이만 표시하게 됩니다. 
- 위의 경우, 나이가 10살즈음이 되면, 나이에 따른 그 영향이 매우 다이나믹 (긍/부정이 섞여있음) 함을 알 수 있습니다. 
- 또한 45살 즈음엔 매우 확실하게 나이가 많을수록 암 발병률이 높다고 생각할 수 있을것입니다.



# Refer

- http://dmqa.korea.ac.kr/activity/seminar/297
- https://godongyoung.github.io/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D/2019/04/13/Partial-Depedence-Plot.html
- https://eair.tistory.com/
