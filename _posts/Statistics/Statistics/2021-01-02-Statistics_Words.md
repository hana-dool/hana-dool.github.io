---
title:  "통계 용어정리"
excerpt: "통계 용어들"
categories:
  - Stat
tags:
  - 3
last_modified_at: 2021-07-29

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: false

use_math : true
---

# intro 

- 용어 모음입니다.

# 표준편차와 표준오차

표준 편차는 '데이터가 얼마나 퍼져있는지' 를 나타내는 것이다.

표준 오차는 '데이터의 함수인 통계량이 얼마나 퍼져있는지' 를 나타내는 것이다. 

# QQ-plot

- Q-Q plot은 두 확률 분포를 그것들의 quantiles를 그려넣음으로써 비교 하는 것이다. 첫 째로, quantiles의 간격이 선택 된다. Q-Q plot의 첫 번째 한 점 (x, y)는 첫 번째 분포의 첫 번째 quantile이 x값이 되고, 두 번째 분포의 첫 번째 quatile이 y값이 된다. 즉, 100-quantiles로 선택했다고 치면, 두 분포에서 1%에 해당하는 샘플을 각각 x, y값으로 넣어서 점을 찍는 것이다

- QQ plot의 목적은 두 데이터 셋이 같은 분포로부터 왔는지를 보이는 것이다. 실용적으로 많은 데이터 셋이 가우시안 분포와 비교된다고 하는데, **보통은 두 개의 분포가 없이 그냥 한 분포를 R에서 qqnorm 함수를 사용해서 그 분포가 얼마나 가우시안 분포와 비슷한지를 알 수 있다. 하지만, 기본적으로 Q-Q plot은 가우시안 뿐만 아니라, 어떤 분포든 두 분포의 유사성을 보는 것으로, 두 분포가 포아송 분포라면 이것 역시 선으로 나타난다.**



# VIF

- 설명에 앞서 먼저 입력 데이터의 구성을 아래와 같이 약속하자.
  분석에 사용될 데이터가 입력변수 n개와 종속변수 1개로 구성된다고 하자. 총 변수는 n+1 이다.
  이 데이터의 변수들은 모두 수치형(양적) 변수이어야 한다.

그럼, *VIFk* 는 (여기서, 1<= k <= n 의 관계)
변수 k를 종속변수로 지정하고, 나머지 n-1 개의 입력변수를 입력변수로 지정하여 회귀분석을 수행한다.
즉, 이 회귀분석에서 종속변수 Y는 제외시킨다. 왜냐하면, 다중공선성은 입력변수들 간의 상관관계를 측정하는 것이기 때분이다.

위 수행된 회귀분석에서의 결정계수 *Rj*2 을 구한 후 아래의 수식으로 *VIFk* 를 구한다.

*VIFk* = 1 / (1 - *Rj*2)

중요한건 이게 범주형 변수에도 쓰일 수 있다는 것이다. one hot vector 처리를 한 데이터에서 이런것을 쓸 수 있다! 호호호

# sampling distribution

- 위 용어는 'Sampe 을 R.V. 취급하는 Freq 에서 쓰이는 말입니다. (베이즈의 경우에는 데이터는 'Fixed' 라고 생각합니다.)

- 빈도론자의 입장에서는, 미지의 세계인 모수를 들여다 보기 위해서는  Sampling distribution 을 구하는것이 필수입니다. 
- 하지만 이를 구하는것은 매우 고역 입니다. $\bar{X}$ 같은 값은 어느정도 쉽겠지만 (CLT) 우리가 궁금한게 $\bar{X}$ 뿐만이 아니라 모수, 복잡한 통계량 등일 떄가 많은데, 이럴때에 Sampling distribution 을 구하는게 매우 힘들다.

- exactly 한 Sampling distribution 을 구하는것은 매우 힘들다. 그래서 Limiting distribution 을 이용하기도 한다. 예시로 CLT 를 이용하면 $\bar{X}$ 의 극한분포를 구할 수 있고, 이를 이용해 Estimation, Testing 이 가능해진다.

- 하지만 Limiting distribution 을 구하는것도 마냥 쉽지는 않다. 학회지에 나오는 논문들을 보면, 새로운 분포를 만든 후 제일 시간이 오래 걸리는 작업이 Sampling distribution 을 해석학적으로 어떠한 분포를 Exactly 또는 Assymptotic 하게 따르는지 증명해내는 작업이라고 한다.
- 이러한 Assymptotic Disribution 을 구할 수 없을때에 울며 겨자먹기로 하는게 바로 Bootstrap 이라고 합니다...

# Best Critical Region

![png](/assets/images/Stat/0_1.png)

- 위와 같이, 같은 유의수준을 가지는 기각역들과 비교했을때 , Power 가 제일 쎈 기각역을 BCR 이라 합니다.



