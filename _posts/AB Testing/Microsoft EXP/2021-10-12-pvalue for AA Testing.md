---
title: "p-Values for Your p-Values &#58; Validating Metric Trustworthiness by Simulated A/A Tests"
excerpt: "A/A 테스팅을 통하여 Metric 의 Truthworthy 를 강화하는법"
categories:
  - AB_Microsoft
last_modified_at: 2021-10-12

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 A/A 테스팅과 이를 어떻게 Metric 과 연관지어서 생각할 수 있는지 알아봅시다.
{: .notice--warning}

# [p-value and A/A Testing](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

- Microsoft 팀은 매달 수천건의 A/B Testing 을 수행하고 있습니다.
- 이러한 팀은 A/B 테스트를 사용하여 Microsoft 제품 전반에 걸쳐서 고객환경을 개선하려 합니다.
- 이러한 테스트 각각에 대해 A/B 에 대하여 수십 , 수천개의 metric 에 대해서 두 A,B 를 비교하게 됩니다. 
- 또한 우리는 브라우저, 나라, 앱 버젼, 언어와 같은 피벗에 따라 segment 를 나누어 비교분석도 수행합니다. 
- 이러한 A/B comparison 의 최종 결정은 p-value 로 귀결됩니다. 
  - p-value 는 A/B Testing 의 핵심입니다. 
- 2020년 7월에만 우리의 A/B Testing platform 은 150억개의 p-value 를 계산하였습니다. 
- 이렇게 많은 p-value 값이 계산되고 그에 따라 매우 중요한 business decision 이 결정되기 때문에 이러한 결과의 신뢰도를 검증하는 작업은 중요합니다.
- 여기에서는 Exp 에서 신뢰성을 검증하기 위해 사용하는 여러 방법중 하나를 설명하려 합니다. 
- 통계 교과서를 보면 p-value 는 "귀무 가설이 맞다는 가정하에, 지금 얻은 데이터 이상으로 극단적일 확률" 으로 정의합니다.
- Microsoft 내부에서, 통계학자가 아닌 사람들에게 p-value 를 설명할떄에는 다음과 같은 설명을 즐겨 합니다. 
  - "만일 A/A Test 였다면 이러한 결과는 얼마나 비정상적인 값이였는가?"

> ## Testing your testig system with more test

- A/A 테스트는 A 와 B 가 동일한 테스트입닝다. 
- A/A 테스트는 A/B Test 플랫폼을 테스트하기 위한 가장 강력한 도구중 하나입니다. 
  - 시스템이 A 및 B 그룹에 불균형하게 할당하는 경우 등과 같은 에러를 잡아낼 수 있습니다.
- A/A Test 는 한가지 기가 막힌 특성을 가지고있는데, '귀무가설이 참이라고 가정하지 않아도 된다.' 라는 것입니다. '가정이 아니라 사실' 이기 떄문입니다.
- p-value 가 significant 하다고 여겨지는 흔한 기준은 p<0.05 입니다. 우리는 null hypothesis 가 true 일 경우에 p < 0.05 가 관측될 확률은 5% 라는것을 알고 있습니다. 
  - 실험이 잘 구성되었다면 p-value 는 0과 1사이 값을 균일하게 분포해야 합니다. 
- 이것을 확인하기 위해 엄청나게 많은 A/A Testing 을 할 수 있지만, 이는 시스템적으로 부담스러운 문제입니다. 
  - 대신에 이러한 A/A Testing 결과를 시스템 외부에서 Simulation 할 수 있으면 어떨까요? 

# [Offline A/A Testing](#link){: .btn .btn--primary}{: .align-center}

> ## Simulating A/A Tests offline

- 우리의 A/B 테스트 플랫폼은 고유 ID 에 해시 함수를 적용하여 사용자를 A 또는 B 에 할당합니다. 
  - ID 는 쿠키에 저장된 사용자 ID 거나 , Device Id 등이 가능합니다. 
- 우리는 이 해시 함수의 시드를 변경함으로서 많은 테스트를 동시에 실행합니다. 
- 매번 seed 를 변경하여 A/A Test 에서 어떤 일이 일어나는지에 대해서 시뮬레이션 할 수 있습니다.
  - A/A Test 에서 각 A/B Test 의 metric 에 대한 p-value 를 계산할 수 있습니다.
- 메트릭중 하나에 대해서 몇백개의 A/A Test 를 시뮬레이션 해보겠습니다. 
  - 이 경우 시뮬레이션을 200번 실행하고 p-value 를 히스토그램으로 만들었습니다.

> ## Healthy metric

- 문제가 없는 정산 메트릭일 경우에는 다음과 같이 표시가 됩니다.

![png](/assets/images/Stat/79_1.png)

- 위와 같이 정상적인 metric 은 Uniform 한 분포를 따르게 됩니다. 
- 왼쪽의 히스토그램만으로는 약간 감이 잘 안올 수 있으므로 오른쪽의 Expected p-value 분포를 보는것을 추천드립니다. 
  - 오른쪽의 Expected 되는 p-value 의 분포 (Uniform) 와 CDF 가 대게 일치하는것을 볼 수 있습니다.
- 물론 metric 하나마다 이렇게 지루한 시각화 확인 작업을 하기 어려우시다면 Anderson-Darling 통계 검정을 사용하는것도 좋은 방법입니다. 
  - 이떄에 metric 이 잘못되어있다고 잘못 판단하면 안되므로, 유의수준을 매우 낮은 수준으로 고정할 수 있습니다.

> ## One Extreme Outlier

- 위와 같은 과정을 다른 메트릭에 적용해봤더니 아래와 같은 분포를 따랏다고 합시다.

![png](/assets/images/Stat/79_2.png)

- 위와 같은 경우는 대부분의 p-value 가 0.32 에 몰려있는것을 볼 수 있습니다.
- 이는 메트릭이 '하나의 큰 Outlier' 에 의해 영향을 받을떄에 나타나는 현상입니다. 
  - 이 경우에는실수로 클릭 이벤트가 여러번 중복된 경우입니다. 
  - 대부분의 사용자가 링크를 1~10번 클릭하는 동안 한 사용자는 클릭을 100만번 하였습니다. 
- 그래서 Simulation 된 A/A 테스트를 할 때에, 모집단을 두 그룹으로 나누게 되는데 이때, 이러한 Outlier 사용자는 늘 어느 한쪽으로 할당되게 됩니다. 
  - 이러한 특이치는 메트릭에 대한 평균과 분산을 증가시키고, 또한 모든 A/A Test 의 검정에서 t-statsitics 는 1에 근접하게됩니다. 
  - 이렇게 T-statistic 이 1 에 근접할 경우 , p-value 는 0.32 가 나오게 됩니다. 

> ## Two Extreme Outlier

- 우리는 이전에서, 오프라인 로그에서 A/A Testing 을 통하여, metric 중 하나가 Outlier 에 대한 문제를 가지고 있다는것을 캐치했습니다. 
  - 우리는 'Outlier' 를 찾으려한게 아니라 그저 A/A Testing 을 통하여 이러한 문제를 잡아냈다는것에 주목합시다. 
- 위와 같이 하나의 Outlier 떄문이 아니라, 다른 문제의 경우에는 p-value 의 distribution 이 어떠한 모양을 띨까요? 

![png](/assets/images/Stat/79_3.png)

- 이 경우의 그림을 봅시다. Uniform 과는 약간 다른 모습을 볼 수 있습니다. 
- 이런 모습을 띤 원인은, 하나의 Outlier 가 아니라 2개의 매우 큰 outlier 가 있을떄에 발생하는 그림입니다. 
- 두개의 큰 특이치가 어느쪽에 분배되는지에 따라서 p-value 가 달라집니다.
  - 한쪽에 두개의 특이치가 몰리게 되면 , p-value 는 특정한 값을 띠게 됩니다. 
- 즉, p-value 는 특이치에 심하게 좌우되며 이는 multimodal 형태의 p-value 그래프를 형성하게 됩니다. 
- 이러한 Outlier 가 매우 많아지면 , 소수의 특이치가 t-statistic 값을 좌우하지는 않으므로 다시 Uniform 한 모습을 띠는것을 볼 수 있을것입니다. 
  - 이러한 특이치가 30개 이상일때에 어느정도 평평한 모습을 띨 것이라고 예측합니다. (그저 경험적인 CLT 의 표본 수 관점에서)
- 사실 위처럼 특이치가 t-statistic 에 매우 큰 영향을 줄 경우 A/B Testing 팀은 메트릭 분포를 잘라낼(capping) 것을 권장합니다. 
  - 사용자가 100만번 클릭한것은 A/B Testing 의 결과로 인해 일어난것을 아닐것입니다. 
- 적절히 클릭 횟수에 따른 상한(ex 50) 을 설정하고 , 이를 넘으면 이 값으로 바꿀 수 있습니다. 
  - 이러한 capping 은 metric 의 variance 를 낮추ㅜ어 Sensitivity 를 상승시킵니다. 

> ## Very rare event

![png](/assets/images/Stat/79_4.png)

- 위와 같은 경우는 오로지 8개의 다른 p-value 값을 나타내고 있습니다. 
- 이는 metric 이 매우 드문 사건의 발생을 측정할떄의 경우입니다. 
- 이 metric 이 측정하는 동안, 이 메트릭이 측정하려는 작업을 수행한 사용자는 겨우 15명 이였습니다. 
- 15명을 두 그룹으로 나누는 방법은 15/0 , 14/1 ... 8/7 으로 8개밖에 되지 않기 떄문에 8개의 p-value 값을 얻은것입니다. 
- 이러한 경우, metric 의 값이 너무나 적기때문에 결과를 신뢰할 수 없을것입니다. 
  - metric 의 값이 충분해야 의미있는 결과를 얻을 수 있습니다. 

> ## only 1 

- 위 경우 말고, p-value 가 늘 하나의 값만 나타내는 경우가 있습니다. 
- 이는 메트릭이 모든 사용자에 대해서 1 또는 항상 0 의 값만 가지는 경우입니다. (또는 일정한 상수값)
  - 이는 '사용자가 불가능한 작업 수' 를 센다던지, '로그 진입 자체' 를 센다던지 같은 경우에 얻게 됩니다. 
- 이런 metric 에는 p-value 는 항상 1 의 값을 가지게 됩니다. (A/A 를 어떻게 나누든 늘 동일한 값을 가지기 떄문입니다.)

# [Conclusion](#link){: .btn .btn--primary}{: .align-center}

- 우리는 12개의 Microsoft 제품의 모든 A/B Testing 의 메트릭을 검사해본 결과 일반적인 metric 의 10~15% 가 이러한 uniformity under hypothesis 테스트를 실패하였습니다. 
- 일부의 경우 failure rate 는 30% 까지 높았습니다. 
- 이러한 점검을 정기적으로 실시하는것이 좋습니다. 
  - 이번주 테스트를 통과했다고 해서 , 다음주 데이터의 특이치에 대해서 영향을 안받는게 아니기 떄문입니다. 
- 이러한 결과를 바탕으로 이러한 테스트를 자동화 하고, metric 에 문제가 있을때 이를 알리는 방법을 연구하고 있습니다. 
- EXP 팀에서는 신뢰할 수 있는 분석이 , 우리 platform 의 핵심 가치중 하나입니다. 
  - A/B 테스트 분석시에는 p-value 보다 근본적인것은 없으며 이 분석은 실험의 신뢰성을 확보하기 위한 여러가지 방법 중 하나입니다.
- 다른 게시물에서는 'metric 의 truthworthy' 를 보장하는 다른 방법에 대해서 알아보도록 하겠습니다.

**reference**

- <https://www.microsoft.com/en-us/research/group/experimentation-platform-exp/articles/p-values-for-your-p-values-validating-metric-trustworthiness-by-simulated-a-a-tests/>

 A/A 테스트입니다. 딱히 언급할만한 내용은 없고, 10~15% 의 메트릭이 p-value 그래프가 Uniform 이 아니였다는게 좀 충격이네요. 실험의 Sample size 를 내 생각보다 작게 잡고있는건가? 싶기도 하고, Outlier 가 그렇게 심한 Issue 인가... 싶기도하고...
{: .notice--success}

