---
title: "Outlier And A/B Testing"
excerpt: "아웃라이어 처리에 대해서 알아보기"
categories:
  - AB_Article
last_modified_at: 2021-12-09

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

Outlier 와 A/B Testing
{: .notice--warning}

# [A/B Testing and Outlier](#link){: .btn .btn--primary}{: .align-center}

> ## What is Outlier

- 이상치는 모집단의 무작위 표본에 대해서, 다른 값과 비정상적인 거리에 있는 관측값이라 할 수 있습니다.
  - 물론 Outlier 에 대해서는 '비정상적인 거리' 라는 표현은 매우 모호한 기준이기때문에 이를 검정하는것은 매우 어려운 일입니다.
- 이러한 Outlier 는 왜 생겨날까요? 
  - 측정오류
  - 의도하지 않은 이상유저 (클릭수 일 경우 자동으로 클릭을 구현한 봇 등)
- 이때 이상치도 하나의 고객이기때문에 '포함 해야되느냐, 말아야 하느냐' 는 논란이 될 수밖에 없습니다.
  - 여기에서는 그러한 판단을 내리기보다는 어떤게 문제가 되고 어떻게 대처할 수 있는지에 대해서ㅈ 짧게 알아볻록 하겠습니다.

> ## What is Effect

- effect 는 다양하게 결과를 왜곡하는데, 그 영향은 다음과 같습니다.
  - Outlier 가 평균을 왜곡함
  - Outlier 가 분산을 왜곡함

$$t=\frac{\bar{X}_{1}-\bar{X}_{2}}{\sqrt{\frac{s_{1}^{2}}{N_{1}}+\frac{s_{2}^{2}}{N_{2}}}}$$

- 이러한 영향은 위의 통계량을 보더라도 예측할 수 있는것인데요 만일 Outlier 가 너무 큰 값이 들어오게 된다면
  -  $\bar{X_1} - \bar{X_2}$ 의 값이 변하고, 그에 따라서 통계량이 왜곡됩니다.
  - $\sqrt{\frac{s_{1}^{2}}{N_{1}}+\frac{s_{2}^{2}}{N_{2}}}$ 의 값이 변하고 (표본분산) 그에 따라서 통계량이 왜곡
- 즉 위의 영향때문에 Ourlier 는 통계적 검정에 영향을 끼치게 됩니다. 

> Experiment

- Treatment 가 실제로 차이($\delta$)를 가지는 실험에 대해서 하나의 Outlier 를 계속 추가하는 실험을 계획해 보겠습니다.

![jpg](/assets/images/Stat/121_1.jpg)

- 위의 각각의 점은 하나의 실험을 의미합니다. 
  - y 축 : T - Statistics 
  - x 축 : Outlier Size  (즉 Outlier 가 $\delta$ 의 몇배인지를 나타냄)
- 즉 Outlier 가 점점 커질수록 그에따라서 'Significant 한 실험' 이 UnSignificant 하게 변하는것을 볼 수 있습니다.
  - 이는 Outlier 때문에 평균의 차이도 왜곡시키지만 , 추가로 분산을 더욱 크게 왜곡하기때문에 그에 따라서 통계량을 왜곡시키게 됩니다.

> ## Outlier in revenue

- 평균 수익율과 같은 메트릭에서 자주 나타나는게 바로 이상치 문제입니다.

> https://www.brooksbell.com/resource/blog/dealing-with-outliers-part-1/#sthash.bmyQNmmP.dpuf

“In this particular situation, resellers were the culprit—customers who buy in bulk with the intention of reselling items later. Far from your typical customer, they place unusually large orders, paying little attention to the experience they’re in. It’s not just resellers who won’t be truly affected by your tests. Depending on your industry, it could be very loyal customers, in-store employees who order off the site, or another group that exhibits out-of-the-ordinary behavior."
{: .notice}

- Brooks Bell의 수석 최적화 분석가인 Taylor Wilson 는 위와 같이 나중에 품목을 재판매할 의도로 대량 구매하는 고객때문에 이상치가 발생했다고 합니다. 
- 이러한 고객들은 User Experience (즉 인터페이스가 어떻든간에) 에 별  상관 없이 많은 주문을 하게 되므로 우리 테스트에서 제외되어야 할 대상이 될 수 있습니다.
- 만약 샘플 데이터가 적다면 , 위와 같은 현상은 매우 큰 문제가 될 수 있을 것입니다.

# [Outlier Remedy](#link){: .btn .btn--primary}{: .align-center}

> ## Optimizely

> Three Sigma Rule

```
arithmetic mean + (3 * standard deviation)
```

- 위와 같이 평균 + Standard deviation *3 이상의 차이가 나게 될 경우 이상치로 처리하게 됩니다. 
- 이상치인 값은 평균으로 대체되게 됩니다.
- https://www.youtube.com/watch?v=raX9EoCOn9s 참조 
- https://support.optimizely.com/hc/en-us/articles/4410289414413 참조

> Daily Exclusion

- 이때, A/B Testing 을 실행하면서 Outlier 제거를 Sequential 하게 하는 방법을 알고리즘을 소개하는데 다음과 같습니다.
  - 첫 7일 전까지는 가능한 데이터를 모두 사용하여 평균, 표준오차를 계산한뒤 제거합니다. (이때 평균을 계산하는 방법은 Moving Everage 를 사용한다고 합니다.)
  - 7일 이후부터는 이전 7일 Window 계산으로 평균, 표준오차를 계산한 뒤에 제거합니다.

> Construction

![jpg](/assets/images/Stat/122_1.jpg)

- 위처럼 Metric 생성과정에서 Outlier Detection 기능을 넣을 수 있습니다. 

![jpg](/assets/images/Stat/122_2.jpg)

- 그리고 결과 화면에서도 Outlier 가 제거된 이후에 계산된 모습을 볼 수 있습니다.

> ## Dynamic Yeild

- <https://www.dynamicyield.com/lesson/outliers-detection/>

> 68–95–99.7 rule( sigma rule )

- 이 경우에도 위와 같이 Outlier 를 검정하기 위해서 3-시그마 규칙을 사용합니다. 
- 해당 값이 평균 + 표준편차*3 이상의 차이이면 이상치로 처리되게 됩니다.

![jpg](/assets/images/Stat/122_3.jpg)

> Construnction

![jpg](/assets/images/Stat/122_4.jpg)

- 위와 같이 Dynamic Yield)은 결과 화면에서 이상치를  포함할지 아니면 완전히 제외할지 여부를 선택할 수 있는 옵션을 제공하게 됩니다.

> ## Percentile 쳐내기

- https://cxl.com/blog/outliers/ 
- 위와 같이 Kvin Hilstrom [은 팟캐스트](http://minethatdata.com/)에서 1% 또는 5% 의 의 상위값을 trimming 한다고 합니다. 
  - 이때 대체될 이상치를 대체할때에 어떤 값으로 대체될 수 있을까요? 
- https://en.wikipedia.org/wiki/Winsorizing
  - 위와 같이 Winsorizing 방법을 사용할수도 있습니다.
- 이 방법론은 Outlier 로 제거되지 않은 값들 중에서 최대(또는 최소) 값으로 Replace 되는 방법입니다.
  - {92, 19, **101**, 58, **1053**, 91, 26, 78, 10, 13, **−40**, **101**, 86, 85, 15, 89, 89, 28, **−5**, 41}    (N = 20, mean = 101.5)
  - {92, 19, 101, 58, 101, 91, 26, 78, 10, 13, −5, 101, 86, 85, 15, 89, 89, 28, −5, 41}       (N = 20, mean = 55.65)

> ## 분포 고려하기

- [신뢰 구간](https://cxl.com/blog/confidence-intervals/) 을 계산하는 전통적인 방법 은 데이터가 [정규 분포](https://en.wikipedia.org/wiki/Normal_distribution) 를 따른다고 가정 하지만 방문자당 평균 수익같은 경우는 이러한 방법이 작동하지 않습니다. 

![jpg](/assets/images/Stat/122_5.jpg)

- Julia Engelmann의 블로그에에서 왼쪽 그림은 이론적인 정규 분포를 보여줍니다. 이떄 주문 수는 양의 평균 값을 중심으로 변동합니다. 이 예시에서 고객은 평균적으로 5번 주문합니다만, 주문의 수는 Normal 분포를 따르지 않습니다.
- 오른쪽의 그림은 이러한 Revenue 분포에 대한 현실을 보여줍니다. 대부분의 고객은 주문을 하지 않고, 한다고 하더라도 평균(5) 보다 훨씬 낮은 수의 주문을 하게 됩니다. 그리고 소수의 Outlier 가 위치하게 됩니다.

- 기본적으로 우리는 분포가 Normal이라고 가정한 상태에서 AB Test 를 진행하게 됩니자. 즉  아래와 같이 치우친 Revenue 와 같은 분포의 경우 , 우리의 테스트가 잘 작동하지 않죠...

![jpg](/assets/images/Stat/122_6.jpg)

- 그러므로 Assumption 을 제대로 지키고 있는지를 알아보기 위하여 [Shapiro-Wilk 테스트를](https://en.wikipedia.org/wiki/Shapiro–Wilk_test) 사용하여서 데이터의 정규 분포를 [테스트](https://en.wikipedia.org/wiki/Shapiro–Wilk_test) 하는것을 추천드립니다. 
  - 만일 Normality Test 가 작동하지 않는 경우 t-검정이 아닌 다른 방법을 사용하여 데이터를 살펴보는 것이 좋습니다. 

> ## 다른 테스트 방법론 사용

- **Mann-Whitney U-검정** . Mann-Whitney U-검정은 데이터가 정규 분포에서 크게 벗어날 때 , T - Test의 대안으로서 사용할 수 있습니다.

- **Robust statistics** :  [**Robust statistics**](https://www.rci.rutgers.edu/~dtyler/ShortCourse.pdf) 방법은 데이터가 정규 분포를 따르지 않거나 이상값에 의해 왜곡될 때 사용할 수 있습니다. 여기에서 평균값과 분산은 비정상적으로 높거나 낮은 값의 영향을 받지 않도록 계산됩니다. (Winsorizing 방법론에서 설명했음)

- **Bootstrapping** :   [Bootstrap](https://en.wikipedia.org/wiki/Bootstrapping_(statistics)) 이 방법론은 분포 가정과 독립적으로 작동합니다. 신뢰 수준 및 구간에 대한 신뢰할 수 있는 추정치를 제공하기 떄문에 매우 강력합니다. 이 방법론의 핵심은 무작위 샘플링 절차를 통해 관찰된 데이터(통계량)를 기반으로 변수 분포의 신뢰할 수 있는 추정치를 제공해 줍니다. 

> ## 이상치 가치를 고려하기

- 방문자당 수익의 분포를 보았듯이 메트릭의 분포는 대게 비정상적일떄가 많습니다.  
  - 소수의 갑부 구매자가 데이터 세트를 극단으로 치우치게 하는 상황은 매우 일반적인 상황입니다. 
  - 이런경우에 이상값 탐지는 매우 어렵게 됩니다.
- 데이터 분석에서 이상치를 버리지 말아야 할 필요도 있습니다.
  - 데이터들을 [세분화](https://cxl.com/blog/audience-segmentation/) 하고 더 깊이 분석해야 합니다. 
  - 어떤 인구 통계학적 특성, 행동 특성 또는 기업 통계학적 특성이 구매 행동과 관련이 있을까요? 
  - 그리고 거기에서 어떤 인과관계를 알아내기 위해 어떻게 실험을 실행할 수 있을까요?
- 위와 같은 질문들은 단순한 A/B 테스트보다 더 깊이 생각해야 되는 질문들입니다. 이러한 Segmentation 분석을 잘 하면, AB 테스트에 대해 더 깊은 이해를 할 수 있습니다.

# [Conclusion](#link){: .btn .btn--primary}{: .align-center}

> ## 어떤 일이라도 해라

- Dan Begley-Groth [는 Richrelevance 블로그에](https://www.richrelevance.com/blog/2014/02/25/tipping-point-outliers-ab-testing-dan-begley-roth/) 다음과 [같이 썼습니다](https://www.richrelevance.com/blog/2014/02/25/tipping-point-outliers-ab-testing-dan-begley-roth/) .

테스트가 통계적으로 유효하려면 테스트가 시작되기 전에 테스트에 대한 모든 규칙이 먼저 결정되어야 합니다. 그렇지 않다면, 테스트 진행 추이에 따라 우리 주관이 영향을 받을 수 있기 때문입니다. 그러므로 우리는 테스트 전에 이상치의 임계값을 결정하고 (RichRelevance 테스트의 경우 평균에서 3개의 표준 편차) 이를 제거하는 방법론을 설정해서, A/B 테스트 해석시에 무작위 노이즈와 주관성을 크게 감소시킬 수 있습니다. 
{: .notice}

- 이상치는 테스트의 품질을 떨어트리게 됩니다. 그러므로 우리는 늘 outlier 를 제거하려는 노력을 하는것이 중요합니다.

> ## Conclusion

- 이상치는 테스트에서, 결과에 영향을 미치는 중요한 요인입니다.
  - 작은 표본 크기에서 하나 또는 두 개의 높은 이상치는 우리의 Decision 을 완전히 왜곡시킬 수 있습니다.
- 대부분의 경우에, 데이터가 이러한 극단적인 경우의 영향을 받는 경우, 이상치를 제외하고 대표값으로 대체할 수 있습니다. (이러한 기준은 value 의 최대 / 최소값 등이 될 수 있습니다.)
- 또 다른 방법은 post-test data 를 가지고.각 메트릭 사례별로 이상값의 영향을 확인합니다. *그런 다음* 이상치 값을 제거, 변경 또는 유지할지 여부를 결정하는 방법이 있습니다.
- 데이터의 이상값을 처리하는 방법은 많이 있습니다. (구글에서는 이걸로 특허를냄...) 그러므로 이상치에 대해서는 항상 잘 제거하는 방법이 필요..

---

**reference**

- <https://cxl.com/blog/outliers/>

