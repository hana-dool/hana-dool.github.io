---
title:  "Probit regression"
excerpt: "로지스틱의 친척 프로빗 모델"
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

![png](/assets/images/Stat/26_1.png)

- 확률 모델링을 위와 같이 Linear 하게 한다고 합시다.

![png](/assets/images/Stat/26_2.png)

- 그러면 위와 같이, 확률에 대한 추정이 Linear 하게 이루어지기 떄문에, 0~1 의 범위를 벗어나는 문제가 생깁니다.
- 즉 위와 같은 상황에서 y 의 범위를 적절하게 조절해줄 필요성이 생깁니다.

<br>

# 2. Probit Model?

![png](/assets/images/Stat/26_3.png)

- 위와 같이 오른쪽에 Normal 분포의 CDF 를 붙인다면, 그 범위를 0과 1로 제한시킬 수 있습니다. 
- 그 결과는 아래의 그래프와 같습니다.

![png](/assets/images/Stat/26_4.png)

<br>

# 3. Estimation? 

![png](/assets/images/Stat/26_5.png)

- 위와 같이 MLE 방법으로 추정이 됩니다. 
- Log Likelihood 함수가 베타에 대해서 ConCave 하기 떄문에, MLE 를 추정할 떄에, Unique 한 MLE 가 존재하고 추정도 쉽다고 합니다.
- 그리고 역시! MLE 이기 때문에 Assymptotic 한 분포가 Normal 로 알려져 있습니다. 
- 즉.. 추정치에 대한 '분포' 를 알 수 있기떄문에, 이를 이용해 Testing 도 가능합니다.

<br>

