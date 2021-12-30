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
---

우리는 A/B Testing 을 진행할때에 샘플 사이즈를 먼저 계산하는것을 원칙으로 합니다. 하지만 이때 샘플 사이즈를 잘 맞추지 못해서, Testing 의 Power 가 너무 낮으면 어떤 일이 일어날까요? 
{: .notice--warning}

# [Lower Power Test](#link){: .btn .btn--primary}{: .align-center}

> ## 샘플 사이즈가 너무 작으면 어떤일이 일어나는가? 

- 통계적 검정력은 [모집단에](https://statisticsbyjim.com/glossary/population/) 존재하는 효과를 탐지하는 [가설 검정](https://statisticsbyjim.com/glossary/hypothesis-tests/) 의 능력입니다 . 분명히, 고성능 연구는 이러한 효과를 식별할 수 있다는 점에서 좋은 것입니다. 저전력은 실제 결과를 발견할 기회를 줄입니다. 그러나 많은 분석가는 낮은 검정력이 효과 크기도 부풀린다는 사실을 인식하지 못합니다.
- 이 게시물에서 나는 권력과 과장된 효과 크기 사이의 예상치 못한 관계가 어떻게 존재하는지 보여줍니다. 나는 또한 저널에 발표된 효과의 편향과 통계적 힘에 대한 기타 문제와 같은 다른 문제와 연결하겠습니다. 이번 포스팅은 많은 생각을 하게 하는 글이 될 것 같아요! 늘 그렇듯이 방정식보다는 그래프를 많이 사용하겠습니다.

> ## 연구 Simulation

- 이 효과 크기 팽창이 작동하는 방식을 설명하기 위해 연구를 시뮬레이션하고 세 가지 검정력 수준에서 여러 번 수행하겠습니다.
- 우리가 당신의 지능(IQ)을 증가시킨다고 약속하는 가상의 약물을 연구하고 있다고 상상해 보십시오. 우리의 실험에는 두 그룹이 있습니다. 즉, 피임약을 복용하지 않는 대조군과 복용하는 치료 그룹입니다. 그런 다음 각 그룹은 동일한 IQ 테스트를 수행하고 결과를 비교합니다. 효과 크기는 그룹 평균 간의 차이입니다.
- 우리는 이러한 연구를 시뮬레이션하고 있기 때문에 효과 크기와 모집단의 기타 속성을 제어할 수 있습니다. 효과 크기를 10 IQ 포인트로 설정하고 두 모집단을 다음과 같이 정의합니다.
  - **대조군** : 평균이 100이고 표준편차가 15인 정규분포.
  - **치료군** : 평균이 110이고 표준편차가 15인 정규분포.
- 0.3, 0.55, 0.8의 [통계적 검정력을 생성하는 데 필요한 표본 크기를](https://statisticsbyjim.com/hypothesis-testing/sample-size-power-analysis/) 계산했습니다 . 처음 두 값은 저전력 연구를 나타내고 세 번째 값은 표준 목표 값입니다. 아래 출력은 전력 분석 결과를 보여줍니다.

![jpg](/assets/images/Stat/139_1.jpg)

- 이제 통계 소프트웨어를 사용 하여 검정력 분석의 각 [표본](https://statisticsbyjim.com/glossary/sample/) 크기에 대해 위의 모집단에서 50개의 무작위 표본을 추출하겠습니다 . 마지막으로 모든 데이터 세트에 대해 2-표본 t-검정을 수행합니다. [유의 수준](https://statisticsbyjim.com/glossary/significance-level/) 이 0.05 인 양측 검정을 사용합니다 . 다음 논의에서는 3가지 검정력 수준 각각에 대한 50개의 2-표본 t-검정 결과를 설명합니다.

> ## 초저전력(0.3)에 대한 결과 및 예상 효과 크기

- 우리는 이러한 분석에 대한 올바른 효과 크기가 10이라는 것을 알고 있습니다. 2-표본 [가설 검정](https://statisticsbyjim.com/glossary/hypothesis-tests/) 이 0.3의 거듭제곱을 갖는 50개 데이터 세트에 대해 무엇을 나타내는지 봅시다 . 이 검정력이 주어지면 30%의 시간 동안 효과를 감지할 것으로 예상합니다. 테스트를 무한한 횟수로 수행하면 그 비율을 예상할 수 있습니다. 그러나 우리는 그것을 50번만 수행했기 때문에 유의미한 연구의 비율에 약간의 오차가 있습니다.
- 통계적 검정력이 가장 낮은 50개 검정 중 13개(26%)가 통계적으로 유의합니다. 평균 효과 크기는 17.05 IQ 포인트이고 범위는 12.01에서 21.45까지 확장됩니다. 평균 효과가 너무 높을 뿐만 아니라 전체 효과 범위가 실제 효과보다 큽니다. 아래 그래프는 통계적으로 유의한 결과의 분포를 실제 효과에 대한 참조선과 함께 표시합니다(10).

![jpg](/assets/images/Stat/139_2.jpg)

- 이제 다른 두 수준의 통계적 검정력에 대한 결과를 살펴보겠습니다.

> ## 전력 = 0.55

- 50개 테스트 중 34개(68%)가 통계적으로 유의합니다. 평균 효과 크기는 13.50이고 범위는 7.71에서 19.04로 확장됩니다. 대부분의 효과는 10보다 큽니다.

![jpg](/assets/images/Stat/139_3.jpg)

> ## 전력 = 0.8

- 50개 테스트 중 41개(82%)가 통계적으로 유의합니다. 평균 효과 크기는 11.92이고 범위는 6.30에서 19.43으로 확장됩니다. 실제 효과 크기는 분포의 중심에 더 가깝게 이동하고 있습니다.

![jpg](/assets/images/Stat/139_4.jpg)

> ## 통계적 검정력과 효과크기의 관계

- 검정력 수준이 높을수록 탐지 비율이 증가하고 효과 크기의 과장이 감소합니다. 
- 둘 다 좋은 일이고 공통된 원인이 있습니다. 아래 그래프는 과장된 요인(평균 유의미한 영향/실제 영향)을 검정력별로 표시한 것입니다. 1의 값에서 과장이 발생하지 않습니다.

![jpg](/assets/images/Stat/139_5.jpg)

- 통계적으로 유의미한 연구에서 효과가 모두 긍정적인 편향을 가짐을 확인했습니다. 일반적으로 귀하가 연구를 수행할 때 귀하, 다른 연구자 및 동료 평가 저널은 통계적으로 유의미한 결과에만 주의를 기울입니다. 결국, 유의하지 않은 결과는 표본이 모집단에 효과가 존재한다는 결론을 내리기에 불충분한 증거를 제공한다는 것을 나타냅니다. 그러나 세 가지 검정력 수준에 대해 유의미하거나 중요하지 않은 모든 결과를 살펴보겠습니다.

> ## 분석

- 세 가지 검정력 수준 각각에 대해 50개의 모든 검정은 정확한 값 10 근처에 평균 효과가 있습니다. 또한 효과는 대략 10 주위에 대칭적으로 분포됩니다.

![jpg](/assets/images/Stat/139_6.jpg)

![jpg](/assets/images/Stat/139_7.jpg)

![jpg](/assets/images/Stat/139_8.jpg)

> Note 

- **단서** : 유의미한 연구와 중요하지 않은 연구를 함께 평가할 때 추정된 효과는 실제 인구 효과 의 [편향되지 않은 추정치](https://statisticsbyjim.com/glossary/estimator/) 입니다. 그러나 통계적으로 유의한 효과만 평가할 때 추정된 효과는 [편향된 추정량](https://statisticsbyjim.com/glossary/estimator/) 입니다.
- 이 단서를 탐색하기 위해 유의미한 분포와 중요하지 않은 분포를 그래프로 그려봅시다.

![jpg](/assets/images/Stat/139_9.jpg)

![jpg](/assets/images/Stat/139_10.jpg)

![jpg](/assets/images/Stat/139_11.jpg)

- 이 그래프는 가설 검정이 가장 극단적인 효과 크기를 통계적으로 유의한 것으로 분류함을 보여줍니다. 검정력 수준이 증가함에 따라 효과 크기가 덜 극단적이어야 유의미합니다. 이것이 바로 가설 테스트가 작동하는 방식입니다!

> ## 낮은 통계력이 추정치를 편향시키는 방법

- 유의미한 검정 결과와 중요하지 않은 검정 결과의 전체 분포가 대략 올바른 효과 크기에 중심을 두고 있음을 확인했습니다. 그러나 유의미한 결과에 대한 편향된 [추정](https://statisticsbyjim.com/glossary/estimator/) 에서는 그렇지 않았습니다 .
- 값이 대칭 분포의 평균이 되려면 위와 아래에 대략 같은 수의 값이 있어야 합니다. 이 경우, 우리는 정확한 효과 크기가 10이라는 것을 알고 있습니다. 그러나 통계적 검정력은 검정이 통계적으로 유의한 것으로 분류하기 위해 추정된 효과 크기가 얼마나 극단적이어야 하는지에 영향을 미칩니다. 중요하지 않은 결과는 체계적으로 분포의 하한에 있습니다. 결과를 통계적 유의성으로 필터링하여 평균을 계산할 때 이러한 작은 효과를 제외하고 평균을 위로 편향시킵니다.
- 0.3의 통계적 검정력에 대해 주어진 실험 조건에서 검정은 13.39 IQ 포인트 이상인 경우에만 효과 크기를 탐지할 수 있습니다. 임계 t-값을 사용하여 이 값을 계산하고 여기에 평균 차이의 표준 오차(2.093 * 6.396)를 곱했습니다. 13.39는 올바른 효과 크기인 10보다 큽니다. 이 값만으로도 상당한 효과가 위쪽으로 편향된다는 것을 알 수 있습니다. 통계적 유의성을 얻으려면 비정상적으로 높은 표본 효과가 필요합니다. 이 높은 임계값은 결과의 전체 분포를 심각하게 자르므로 평균을 올바른 값으로 낮추는 더 낮은 추정값(즉, < 10)을 제거합니다. 또한 모든 유의미한 표본 추정치가 10보다 큰 이유도 설명합니다. 결과적으로 너무 높게 편향되어 있습니다.
- 0.55와 0.8의 거듭제곱에 대해 감지할 수 있는 최소 효과 크기는 각각 9.14와 6.95입니다. 이러한 고성능 테스트는 덜 극단적인 효과 크기를 탐지할 수 있습니다. 그러나 여전히 분포의 하단을 자르므로 효과가 위쪽으로 치우칩니다. 편향을 피하는 유일한 방법은 모든 테스트 결과를 포함하는 100%의 통계적 검정력을 갖는 것입니다. 그러나 가설 검정은 100% 검정력을 얻지 못합니다. 다행스럽게도 전력이 80%에 가까워지면 바이어스가 상대적으로 작습니다.

> ## 확률 분포도를 사용한 그래픽 표현

- 아래 차트 는 0.3과 0.8의 거듭제곱에 대한 [확률 분포](https://statisticsbyjim.com/basics/probability-distributions/) 플롯을 사용하여 이것이 어떻게 작동하는지 보여줍니다 . 왼쪽의 빨간색 분포 는 2-표본 t-검정이 주어진 설계에서 통계적 유의성을 결정하는 데 사용하는 t- [분포](https://statisticsbyjim.com/hypothesis-testing/t-tests-t-values-t-distributions-probabilities/) 입니다. 상단의 빨간색 숫자는 t-분포에 해당합니다. [귀무 가설](https://statisticsbyjim.com/glossary/null-hypothesis/) 값(차이 = 0)과 [양측 검정에](https://statisticsbyjim.com/hypothesis-testing/one-tailed-two-tailed-hypothesis-tests/) 대한 임계 상한 값(CV)을 정확히 찾아냅니다 . 낮은 임계값을 표시하지 않습니다. 편의를 위해 일반적으로 t-분포에서 볼 수 있는 t-값을 실제 데이터 단위로 변환했습니다.
- 오른쪽의 파란색 분포는 두 모집단의 특성이 주어진 평균 간의 차이의 예상 분포입니다. 파란색 숫자는 파란색 곡선의 정점에서 발생하는 올바른 효과(10)와 관련된 평균 IQ 차이를 나타냅니다.

![jpg](/assets/images/Stat/139_12.jpg)

![jpg](/assets/images/Stat/139_13.jpg)

다음은 주의해야 할 몇 가지 필수 측면입니다.

임계값 선이 파란색 곡선의 차이 분포를 자르는 방법에 주목하십시오. 빨간색 점선 CV 선 왼쪽에 있는 파란색 곡선의 모든 차이는 중요하지 않습니다. 파란색 곡선의 이 부분은 [통계학자가 ](https://statisticsbyjim.com/glossary/statistics/)[제2종 오류](https://statisticsbyjim.com/hypothesis-testing/types-errors-hypothesis-testing/) 라고 하는 거짓 음성을 나타냅니다 . 결과적으로 이러한 더 작은 효과 크기는 유의한 효과 크기의 평균 계산에 포함되지 않습니다. 평균 효과는 임계값보다 높아야 합니다. 전력이 0.3에서 0.8로 증가하면 잘림이 감소합니다. 잘림의 양은 통계적으로 유의한 결과 중에서 추정된 효과의 편향 정도를 결정합니다.

CV 라인의 오른쪽에 있는 파란색 곡선 아래 영역은 이러한 차이가 중요하기 때문에 검정력을 나타냅니다. 0.3 통계 검정력의 경우 파란색 곡선 아래 영역의 30%는 CV 선의 오른쪽에 있습니다. 0.8 거듭제곱의 경우 80%는 CV 라인의 오른쪽에 있습니다.

CV 선의 오른쪽에 있는 파란색 곡선의 비율이 높을수록 유의미한 효과에 편향이 덜 존재하고 통계적 검정력이 커집니다.

> ## Conclusion

이 삽화가 눈을 뜨게 했으면 좋겠습니다. 저전력 연구가 효과 크기를 부풀린다는 사실이 과소 평가되고 있다고 생각합니다. 일반적으로 분석가는 저전력 연구의 가장 큰 위험이 실제 가능성이 있는 효과를 놓치는 것이라고 생각합니다. 그러나 분석가가 낮은 검정력으로 유의미한 결과를 얻으면 안도하지만 효과 크기가 부풀린다는 사실을 깨닫지 못합니다!

특정 분야는 표본 크기가 작고 검정력이 낮은 연구를 수행하는 경향이 있습니다. 예를 들어, 심리학 연구는 일상적으로 작은 표본을 사용합니다. 당연히 심리학은 과장된 효과 크기에 문제가 있습니다. 또는 연구자들은 소규모 파일럿 연구를 시작하여 부풀려진 효과 크기를 생성할 수 있습니다.

편집자가 중요한 연구만 발표하기 때문에 저널 기사의 효과 크기가 편향되어 있다는 말을 들어보셨을 것입니다. 저널의 기사가 모두 동일한 힘을 가지지는 않지만 동일한 원칙이 적용됩니다. [p-값으로](https://statisticsbyjim.com/hypothesis-testing/interpreting-p-values/) 출판을 제한함으로써 저널은 더 작은 추정치를 제외합니다. 주제 영역을 조사하고 특정 효과에 대해 출판된 모든 기사를 찾았다고 상상해 보십시오. 이들을 함께 평균화하면 합리적인 [추정치를](https://statisticsbyjim.com/glossary/estimator/) 얻을 수 있다고 생각할 수도 있습니다 . 반드시 그런 것은 아닙니다! 중요한 결과만 표시한 첫 번째 그래프 집합을 다시 생각해 보십시오. 그것들은 편향적이었습니다. 평균 효과가 실제 효과에 가까웠던 것은 더 작고 중요하지 않은 효과를 모두 추가할 때까지였습니다.

마지막으로 이 시뮬레이션의 검정력 계산은 검정력 계산에 입력할 올바른 값을 알고 있었기 때문에 쉬웠습니다. 그러나 현실 세계에서 연구하는 것은 어려울 수 있습니다. 결과적으로, 자신이 낮은 검정력 연구를 가지고 있다는 사실을 항상 깨닫지 못할 수도 있습니다. 또한 이러한 시뮬레이션에서 가장 작은 연구에는 0.3의 통계적 검정력이 생성된 두 그룹으로 나누어진 22명의 피험자가 있었습니다. 이것이 실제 연구라면 연구원들은 그것이 그렇게 낮은 전력을 가지고 있다는 것을 깨닫지 못할 것입니다. 확실하지 않은 경우 더 큰 표본 크기에 오류가 있습니다. 그리고, 전력 계산으로 현실감있게 최선을 다하십시오!

---

**reference**

- <https://statisticsbyjim.com/hypothesis-testing/low-power-studies/>


