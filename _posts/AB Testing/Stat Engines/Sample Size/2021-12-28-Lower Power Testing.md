---
title: "Low Power Tests Exaggerate Effect Sizes"
excerpt: "낮은 Power 의 테스트는 효과를 과장한다."
tags:
  - AB_Stat
last_modified_at: 2021-12-13
toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../../hana-dool.github.io
---

우리는 A/B Testing 을 진행할때에 샘플 사이즈를 먼저 계산하는것을 원칙으로 합니다. 하지만 이때 샘플 사이즈를 잘 맞추지 못해서, Testing 의 Power 가 너무 낮으면 어떤 일이 일어날까요? 
{: .notice--warning}

# [Lower Power Test](#link){: .btn .btn--primary}{: .align-center}

> ## 샘플 사이즈가 너무 작으면 어떤일이 일어나는가? 

- 통계적 검정력은 Population 에 존재하는 효과를 탐지하는 능력입니다 (Power)
- Power 가 높다는것은 이러한 효과를 탐지할 수 있다는 것입니다.
  - lower Power 실제 Effect 를 잘 탐지하지 못하게 합니다.

- 위처런 '작은 '그러나 많은 분석가는 낮은 검정력이 효과 크기도 부풀린다는 사실을 인식하지 못합니다.
- 이 게시물에서는 Power 와 과장된 효과 크키가 어떻게 관련되는지에 대해서 보여주려고 합니다.
  - 또한 저널에 발표된 효과의 편향과 Power 에 대한 문제들과 연관하도록 하겠습니다.


> ## Hypothetical Study Scenario

- 이러한 "검출되는 효과에 대한 과장" 현상을 알아보기 위해서 Simulation 해보도록 하겠습니다.
- 우리가 당신의 지능(IQ)을 증가시킨다고 주장하는 가상의 약물을 연구하고 있다고 상상해보세요. 
  - 우리의 실험에는 두 그룹이 있습니다. 즉, 약을 복용하지 않는 대조군과 복용하는 치료 그룹입니다. 
  - 그런 다음 각 그룹은 동일한 IQ 테스트를 수행하고 결과를 비교합니다. 
  - 이때 효과 크기(Effect Size )는 그룹 평균 간의 차이입니다.

- 이러한 Effect Size 를 아래와 같이 설정하도록 하겠습니다.
  - **대조군** : 평균이 100이고 표준편차가 15인 정규분포.
  - **치료군** : 평균이 110이고 표준편차가 15인 정규분포.
- 0.3, 0.55, 0.8의 [통계적 검정력을 생성하는 데 필요한 표본 크기를](https://statisticsbyjim.com/hypothesis-testing/sample-size-power-analysis/) 계산해 보았습니다.
  -  처음 두 값은 Lower Powered Research 를 나타냅니다.
  - 0.8 값은 Test 의 표준적인 값입니다. 아래의 output 은 Power Analysis 의 결과를 나타냅니다.


![jpg](/assets/images/Stat/139_1.jpg)

- 이제 각각 Power 수준에 맞추어 샘플링을 수행하고 (이때 Power 수준에 맞추어야 하므로 ) 모든 데이터 세트에 대해 2-표본 t-검정을 수행해 보았습니다. 
- [유의 수준](https://statisticsbyjim.com/glossary/significance-level/) 이 0.05 인 양측 검정을 사용합니다 . 
  - 아래에서는 3가지 검정력 수준 에 대해서 Two Sample T Test 결과를 알아보겠습니다.


> ## Findings and Estimated Effect Sizes for Very Low Power (0.3)

- 우리는 이러한 분석에 대한 올바른 효과 크기가 10이라는 것을 알고 있습니다. 2-표본 [가설 검정](https://statisticsbyjim.com/glossary/hypothesis-tests/) 이 0.3의 거듭제곱을 갖는 50개 데이터 세트에 대해 무엇을 나타내는지 봅시다 . 
  - 이 검정력이 주어지면 30% 의 테스트가 효과를 감지할것이라고 예상됩니다.
  - 테스트를 무한한 횟수로 수행하면 그 비율을 예상할 수 있습니다. 그러나 우리는 그것을 50번만 수행했기 때문에 유의미한 연구의 비율에 약간의 오차가 있음을 명심하세요


![jpg](/assets/images/Stat/139_2.jpg)

- 50개 검정 중 13개(26%)가 통계적으로 유의했습니다. 
  - 평균 효과 크기(즉 Control 과 Treatment 의 차이)는 17.05 IQ 포인트이고 범위는 12.01에서 21.45까지입니다. 
- 이때 우리가 검출하게 된 평균 효과는 실제 효과 (10) 보다 매우 큰것을 볼 수 있습니다. 
  - 위 그래프는 통계적으로 유의한 결과들을 모두 모아서, 각자의 Difference 를 히스토그램 형식으로 표현한것을 나타냅니다. 
  - 딱 봐도, 실제 Difference (10) 보다 모두 과대주청을 하고 있는것을 볼 수 있습니다. 

> Concusion

- True Difference 보다 검출된 Difference 가 훨씬 과정됨
- 검출력도 상당히 떨어짐 (26% )

> ## Power = 0.55

![jpg](/assets/images/Stat/139_3.jpg)

> Conclusion

- 50개 테스트 중 34개(68%)가 통계적으로 유의합니다.
- 평균 효과 크기는 13.50이고 범위는 7.71에서 19.04 의 범위를 지닙니다. 대부분의 효과는 10보다 큽니다.

> ## Power = 0.80

![jpg](/assets/images/Stat/139_4.jpg)

> Conclusion

- 50개 테스트 중 41개(82%)가 통계적으로 유의합니다. 
- 평균 효과(Difference ) 의 크기는 11.92이고 범위는 6.30에서 19.43의 범위를 지닙니다. 
- 실제 효과 크기는 분포의 중심에 더 가깝게 이동하고 있습니다.

> ## 통계적 검정력과 효과크기의 관계

- 검정력(Power) 의 수준이 높을수록 탐지 비율이 증가하고 Effect Size 의 과대추정이 줄어듭니다
- 아래 그래프는 과장된 요인(평균 유의미한 영향/실제 영향)을 검정력별로 표시한 것입니다. 
  - 1의 값에서 과장이 발생하지 않는가는것을 기억합시다.


![jpg](/assets/images/Stat/139_5.jpg)

- 위를 본다면, 통계적으로 유의미한 Experiment 들은 모두 Effect Size 를 약간 과장하는것을 보여줍니다.

> Note 

- 이는 일반적으로 우리가 연구를 수행하게 되면, 동료들(또는 평가 저널) 들은 유의미한 결과에만 주의를 기울이게 됩니다.
  - 왜냐하면 유의하지 않은 결과는 Treatment Effect 가 존재하지 않는다는것을 의미하기 때문입니다. 
- 그럼에 따라서, 우리 연구가 위처럼 Effect Size 를 과대하게 추정할 수 있음을 의미합니다. 

> ## Analysis Results 

- 세 가지 검정력 수준 각각에 대해 50개의 모든 검정에 대해서 살펴보겠습니다. 
  - 대부분의 실험은 모두 Effect Size 10 근처에서 실험들이 자리잡고 있습니다.


![jpg](/assets/images/Stat/139_6.jpg)

![jpg](/assets/images/Stat/139_7.jpg)

![jpg](/assets/images/Stat/139_8.jpg)

> Note 

- 위처럼 Insignificant 한 연구와 Significant 한 연구를 함께 평가할 때 추정된 효과(Effect Size)는 실제 효과에 대한 Unbiased Estimator 가 됩니다. 
  - 하지만 통계적으로 유의한 결과만 보게된다면, 그것은 "모든샘플을 고려하겠다" 가 아니라 "어느정도 차이가 있는 샘플만 고려하겠다." 가 되므로 통계적으로 유의한 효과만 평가하는것은 편향된 추정량이 됩니다. 
- 위의 주장에 대해서 좀 더 알아보기 위하여 아래와 같이 Significant 한 실험과 NonSignificant 한 실험으로 나누어서 그림을 그려보겠습니다.

![jpg](/assets/images/Stat/139_9.jpg)

![jpg](/assets/images/Stat/139_10.jpg)

![jpg](/assets/images/Stat/139_11.jpg)

- 위 그래프를 보면 가설 검정은 극단적인 Difference 를 가질때에만 유의하다고 결론을 내리는 것을 볼 수 있습니다. 즉 Effect Size 를 편향시키고 있는 것입니다. 
- 또한 Power 가 작을수록 작은 Effect Size 는 Insignificant 하다고 결론을 내리게 되므로, 결과를 더 많이 편향되게 하는것을 볼 수 있습니다. 
  - 이는 다르게 말하면 Power 가 작을수록 편향이 더욱 심해진다는것을 의미합니다.


> ## How Low Statistical Power Biases the Estimates

- 전체 샘플을 보게 되면 Effect Size 에 대해서 불편향 추정을 하고 있는것을 보고 있습니다..
  - 하지만 Significant 한 값만 보게된다면, 이는 '통계적으로 유의' 한 결과만 필터링해서 보겠다는 것이므로 결국에 효과를 좀 더 편향시키게 됩니다.


> Example

- 0.3의 Statistical Power 에 대해서13.39 IQ 포인트 이상인 경우에만 효과에 대한 차이를 갑지할 수 있습니다.  (13.39 는 critical t-value 값을 사용한하여 평균 차이의 표준 오차(2.093 * 6.396) 를 이용하여 추정) 
  - 13.39는 올바른 효과 크기인 10보다 큽니다. 
  - 이 값만으로도 상당한 효과가 위쪽으로 편향된다는 것을 알 수 있습니다. 
  - 통계적 유의성을 얻으려면, 기초적으로 높은 표본효과가 필요하게 됩니다. 이러한 Critical value 는 전체 분포를 심각하게 편향시키게 됩니다. 
- 0.55와 0.8의 powers 에 대해서 감지할 수 있는 최소 효과 크기는 각각 9.14와 6.95입니다. 
  - Test 의 Power 과 최소 효과에 대한 탐지 수준이 낮아서, 덜 편향시킵니다. 
  - 하지만 이도 역시나 편향을 피할수는 없습니다. 어쨋든 "Effect Size" 가 Threshold 이상으로 높게 형성되는 경우에만 Significant 하다고 결론내리게 되기 때문입니다. 
- 사실 Significant 한 결과에 대한 Effect Size 가 편향되지 않는 유일한 방법은 바로, 모든 테스트 결과에 대해서 Significant 하다고 결론을 내리는것 뿐입니다. 
  - 하지만 이는... 더이상 테스트라고 할 수 없죠. 
-  다행스런 일은 그나마 power 가 0.8 이면 biased 가 그나마 좀 적다는 것입니다.

> ## Graphical Representation Using Probability Distribution Plots

- 아래 차트 는 0.3과 0.8의 Power 에 대한 Probability Plot 을 활용하여 , 우리 Test 의 Procedure 를 요약한 그림입니다.
- 왼쪽의 빨간색 분포 는 2-표본 t-검정의 통계량이 Null Hypothesis 하에서 어떤 분포를 보이는지 나타냅니다. 
- CV 는 Critival Value 라는 의미로서 유의수준 0.05 하에서, Critival Value 값을 나타냅니다.
  - 오른쪽의 파란 분포는 주어진 Effect Size 값을 가질때에 가지는 분포를 나타냅니다. (True Treatment Distribution)
  - 파란색 숫자는 올바른 Effect Size(10) 를 나타내고 있습니다 


![jpg](/assets/images/Stat/139_12.jpg)

![jpg](/assets/images/Stat/139_13.jpg)

- 임계값 선이 파란색 곡선의 어느 부분을 자르게 되는지 주목합시다! 
  - 빨간색 점선 CV 선 왼쪽에 있는 파란색 곡선의 영역은 제 2종 오류라고 부르는 에러 영역입니다.
- 평균 효과는 임계값 (CV 라고 표시되어있는 부분) 보다 높아야 합니다. 
  - Power 가 0.3 에서 0.8 로 증가함에 따라 이러한 CV 가 낮아지는것을 확인할 수 있습니다. (즉 Error 가 줄고 높은 Power 의 Test 가 되는것을 볼 수 있는것이죠.)
- 어쩃든 CV 가 어디에 위치하던 결과가 편향된다는것은 쉽게 알 수 있죠!

> ## Conclusion

- 위와 같은 논의를통해서 Lower Power Test 가 Effect Size 를 부풀린다는 사실에 대해서 잘 알게 되었으면 좋겠습니다. 
- 일반적으로 분석가들은 Lower Power Experiment 가 단순히 낮은 Effect 를 가지는 실험을 제대록  감지하지 못할뿐이라고만 생각합니다. 
  - 하지만 Lower Power Test는 Effect Size 를 부풀리게 되는 효과도 있습니다!!!
- 특정 분야에서는 Small Sample Size 하에서 검정력이 낮은 연구를 수행하는 경우가 있습니다.
  - 예를 들어서 심리학 연구는 작은 표본을 사용할수밖에 없습니다. 
  - 즉 심리학과 같은 분야는 과장된 Effect Size 라는 문제가 존재한다는 것입니다. 
  - 더 심각한것은 일부로 적은 표본을 사용하여 부풀려진 Effect Size 를 생성할수도 있다는 것입니다...
- 항상 저자들은 중요한 연구(즉 Significant 한 연구) 만 발표하기 때문에 기사의 결과값들은 대부분 편향되어있습니다. 
  - 예를 들어서 설탕과 비만이 미치는 효과에 대해 조사한다고 합시다. 이에 대해서 자세하게 조사하기 위해서 여러 문헌들을 조사한다고 합시다. 
  - 하지만 이러한 문헌들의 특징은 모두 결과가 편향되어 있다는 것입니다. 이러한 문헌들을 가지고 평균 효과를 조사한다고 해봤자, 그 효과는 Biased 되어 있을 것입니다
- 위의 경우에는 당연히 우리가 Simulation 을 통해서 power 를 계산했으므로 정확한 ture Power 를 계산할 수 있엇습니다.
  - 하지만 일반적으로 True Effect size 를 알 수 없기때문에, 계산하기는 쉽지 않습니다. 
  - 그러므로 MDE 를 설정하든, 어느정도 어림을 잡던 등의 방법을 통해, 미리 실험 하기 전에 어느정도의 Power 를 가지는지에 대해서 미리 알아두는것이 필요합니다.

---

**reference**

- <https://statisticsbyjim.com/hypothesis-testing/low-power-studies/>



