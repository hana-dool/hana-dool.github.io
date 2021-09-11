---
title:  "Confidence Interval"
excerpt: "내 추정의 정확성을 알려주는 구간"
categories:
  - Stat
tags:
  - 1
last_modified_at: 2021-08-05

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 신뢰구간

![png](/assets/images/Stat/29_1.png)

- 위에서와 같이, 신뢰구간은 구간 안에 '모수가 존재할 확률' 이 95% 라는 의미가 아닙니다. 
- '신뢰구간이' 모수를 포함할 확률이 95% 라는 의미입니다. 
- Random 성을 띠는 '주체' 는 데이터이고, 신뢰구간은 이러한 데이터의 함수이기 떄문입니다.  

![png](/assets/images/Stat/29_2.png)

- 위와 같이, 95% 신뢰구간이란, 100개중 95개의 신뢰구간이 모수를 포함한다는 의미일 뿐입니다.

<br>

# 어떻게 구함..?

- 이러한 Confidence Interval 을 구하기 위해서라면 Pivotal Qauntity 를 이용합니다.

![png](/assets/images/Stat/29_3.png)

- Pivotal Qauntatiy 란 위와 같이, $\theta$ 가 들어간 통계량 ~ $\theta$ 가 없는 분포 의 형식으로 나타낼 수 있다면, $\theta$ 를 혼자 분리시킬 수 있으므로 CI 를 구할 수 있게 된다는 의미입니다. 

![png](/assets/images/Stat/29_4.png)

- 위의 예시는 $\frac{\bar{X}-\mu}{\sigma/\sqrt{n}}\sim N(0,1^2)$ 을 따르는것을 이용한 것입니다. 
- 왼쪽의 통계량에는 $\mu$  가 존재하지만 오른쪽에는 존재하지 않기떄문에 분리할 수 있는것입니다.

<br>

# CI 는 여러개가 가능..?

![png](/assets/images/Stat/29_3.png)

- 위에서도 봤겠지만 , 사실 구간은 여러개가 가능합니다. 
- 당연히 '그 구간에 속할 확률이 $1-\alpha$ 이기만 하면 되니까, 다양한 Upper / Lower 구간이 가능합니다.
- 이러한 상황에서 General 한 방법은 '구간을 제일 짧게' 가지는 방법입니다.

![png](/assets/images/Stat/29_5.png)

- 위를 보면, 일반적인 T 분포를 따르는 검정을 할 때에 CI 가 왜  + - 형태로 나왔는지 이해할 수 있을것입니다.

<br>

# 다양한 CI

![png](/assets/images/Stat/29_6.png)

<br>

# Bootsrapping CI

- 사실 위처럼 '분포가정' 을 활용한다는 점 때문에 CI 를 구하기 어려울 수 있습니다. 
- 이런 경우 부트스트랩을 이용해 CI 를 구할 수 있습니다 .

- 부트스트랩은 확률 분포의 가정을 두지 않고 주어진 데이터를 원래의 모집단을 대표하는 독립 표본으로 가정하고 진행합니다.
- 그리고 중복을 허용한 무작위 재추출로(복원추출로) 각각에서 얻어진 통계량을 계산합니다.


> 1.데이터에서 복원추출 방식으로 크기 n 인 표본을 뽑는다.(재추출)
>
> 2.재표본된 표본에 대해서 원하는 통계량을 구하고 기록한다.
>
> 3.1~2 단계를 k 번 반복한다.
>
> 4.x% 신뢰구간을 구하기 위해 R개의 재표본 결과로부터 분포의 양쪽 끝에서 (100-x) / 2 % 만큼 잘라낸다.
>
> 5.절단이 끝난 뒤 나머지 점들의 분포는 x% 부트스트랩 신뢰구간의 양 끝점이 된다.
