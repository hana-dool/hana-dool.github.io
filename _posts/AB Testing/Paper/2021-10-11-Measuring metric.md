---
title: "Measuring metric"
excerpt: "Bing 의 Metric 평가 시스템과 평가 방법에 대한 논문"
categories:
  - AB_Paper
last_modified_at: 2021-10-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 우리가 측정하지 못하는것에 대해서는 알 수 없습니다. 즉 metric 은 조직의 goal 과 실험을 이어주는 아주 중요한 실험 구성 요소입니다. 많은 실험기획자들은 좋은 metric 을 사용하려 합니다. 그래서 sucess , delight , loyalty, engagement 와 같이 추상적인 개념을 이용하여 좋은 메트릭의 기준을 세우려 하였습니다. 하지만 어떻게 할 떄에 , 우리는 정량적으로 메트릭을 비교할 수 있을까요? 이 논문에서는 빙에서의 메트릭 평가 시스템에 대해서 설명하고자 합니다. 
{: .notice--warning}

- user value : 유저가 좋은 경험을 했는지에 대한 매져, 크면 좋은경험 
- 쿼리 : 사용자가 검색창에 검색하는것을 이렇게 표현 

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## 1. Introduction

- meric 은 조직에서 목표를 절정하고, 실험을 결정하고 샘플 사이즈를 설정하는것 등에 사용되는 강력한 도구입니다. 
- 올바르게 선택된 metric 은 팀의 장기적 관점에서 매우 이익이 됩니다.
  - 하지만 잘못 선택된 metric 은 역효과를 낼 수 있습니다. 
- 이렇게 중요한 메트릭을 어떻게 하면 잘 정의할 수 있을까요?

> 올바른 metric 을 정의하는것은 어렵다.

- metric 은 조직의 방향을 주도하지만 이러한 '올바른' meetric 을 정의하는것은 매우 어려운 문제입니다.
- 왜냐하면 metric 은 유저의 성공 / 기쁨 / 충성심 / 참여 와 같은 추상적인 개념을 포함하기 때문입니다.
  - 실제 조직 목표는 '유저에게 행복을 주자!' 처럼 정해지지만 이를 구체적으로 정의하는 metric 은 없습니다.
- 다음과 같은 example 을 봅시다. 
  - search engine 은 '유저가 원하는 정보를 찾는것' 을 'success' 의 기준으로 삼게 됩니다. 
  - 그래서 '클릭 이후에 지난 시간' 으로 다음과 success 를 정의할 수 있습니다.

$$success(q)=\begin{cases}
1,\text{if q had a click with dwell time > 30 seconds}\\
0, \text{otherwise} 
\end{cases}$$

- 위와 같이 성공을 클릭 이후에 시간이 30초 이상 머무른다면 이것을 성공으로 간주할 수 있습니다.
  - 왜냐하면, 좋은 결과를 내보내서, 유저가 그 결과를 살펴보면서 30초를 보내고 있다고 생각할 수 있기 떄문입니다.
- 이 정의는 많은 시나리오에 적합하다고 하지만, 여전히 많은 문제가 있습니다. 
  - 사용자가 아무것도 클릭하지 않고 단지 resut page 에서 쿼리에 대한 답을 직접 얻는 경우는 측정되지 않습니다. (즉 0 으로 측정되나 사실은 success) (이를 good - abandonment 라 합니다.)
  - 또한 사용자가 결과 페이지를 빠르게 탐색하는 경우(클릭 이후 30초 미만만 머무름) 에도 성공으로 측정하지 않습니다. 
- 즉 위처럼 단순한 메트릭을 조직의 목표로 삼게 된다면, 많은 경우, 많은 시나리오에서 에러가 날 것입니다.
  - 예시로 페이지의 결과 페이지에 좋은 정보를 많이 담으면 사용자의 경험은 좋아지지만 클릭이 발생하지 않아 오히려 메트릭은 감소합니다. 즉 이러한 잘못된 메트릭을 가지고 계속 평가를 하게 되면 , 사용자의 경험 개선이 잘 이루어지지 않습니다.

> 메트릭의 품질을 측정하는것은 중요하다.

- 그러므로 '좋은' 메트릭을 설계해야 되고, 이는 어려운 일이기 때문에 무언가 '기준' 이 될만한 것이 필요하고 그것이 바로 메트릭의 품질이 될 수 있습니다. 
- 우리는 이 논문에서 빙 검색 엔진의 맥락에서 메트릭을 평가하는데 사용했던 데이터 중심 접근 방식에 대해서 알아보겠습니다.

> 이 논문에서 다루게 되는것

- metric quality 를 다루는 system architecture
- 메트릭 평가 프레임워크 
- 이러한 프레임워크를 이용하여 메트릭 설계를 어떻게 할 수 있는지 
- 이러한 시스템이 미친 영향과 결론

> ## CONTROLLED EXPERIMENTS

- A/B Test 에서 유저는 Control (A) 또는 Treatment(B) 에 할당됩니다. 
- 실험이 잘 설계되었으면 A,B 간에 다른점은 Treatment 뿐이므로 이 기능의 영향에 대해서 올바르게 판단할 수 있습니다.
- 계절성 , 타 회사 영향 과 같은 영향은 A,B 모두에게 동일하게 미치게 되므로 크게 상관할 내용은 아닙니다. (물론 이 실험의 해석의 타당성에 대해서는 추가적인 조사가 필요하겠지만 단순히 'Treatment 로 인한 A 와 B 의 차이를 측정' 한다는 기준 내에서는 합리적입니다.) 
  - 즉 , 계절성이 존재하기 떄문에 여름에 실시한 실험의 결과가 겨울에도 똑같이 적용되리라는 보장은 없지만 (해석의 타당성은 보장 못하지만) , 현재 시점에서의 Treatment 에 대한 영향 자체는 올바르게 추정하고 있다고 볼 수 있습니다.

> ## RELATED WORK

- Related work 는3 개의 그룹으로 나누어 살펴볼 수 있습니다. 
  - 각 주석이 어떤것을 의미하는지는 맨 마지막 Reference 부분에 수록하였습니다.

> Controlled Experiments

- Research focused on scalability of experimentation systems [18, 26]
- new statistical methods to improve sensitivity [5]
- rules of thumbs and lessons learned from running controlled experiments in practical settings [19, 17]
- projections of results from short-term experiment to the long term [10]
- Applying new statistical methods, such as the variance reduction technique described in Deng et. al. [5]

> individual metric improvement

- NDCG [21]
- user satisfaction [8] in the area of learning to rank
- MAP or AUC in the area of collaborative filtering [27]

> principles of metric design

- It is articulated using statements such as “What gets measured, gets managed” [25]
- “What you measure is what you get” [13]
- and “You are what you measure” [9]
- A good survey of research can be found in Blackburn et. al. [2]
- The topic of finding good organizational metrics is also discussed in several books [1, 3, 6, 22]
- Recently, we shared several lessons on defining metrics for controlled experiments in [4]

# [Metric Evalutation Framework](#link){: .btn .btn--primary}{: .align-center}

> ## Metric Evaluation Framework

![png](/assets/images/Stat/78_1.png)

- 위 그림은 빙의 metric evalutation framework 를 나타냅니다. 
- 이 프레임워크에서 가장 중요한 component 는 Experiment Corpus 라 불리는  controlled experiment 의 historical dataset 입니다. 

> Dataset

- 빙에서는 다양한 corpuses 들을 가지고 있습니다. 
  - 최근 실험중 랜덤하게 고른 corpus 
  - 중요하고, 대표적인 실험을 다양한 전문가가 positive / negative 로 분류한 corpus 
  - 특정 feature 팀에 의하여 만들어진 small corpus (광고팀은 광고 선택 , 위치 조절 과 관련된 실험 corpus 를 가지고 있을 것입니다.)

> Metrics to evaluate

- 위 framework 에서 input 은 평가받고자 하는 metric 입니다. 
  - 일반적으로 이는 새롭게 생겨난 메트릭 또는 평가받기를 원하는 이미 존재한 메트릭이 될 수 있습니다. 

> Computation engine

- 메트릭스 랩의 역할은 experiment corpus 의 각 메트릭에 대한 통계를 계산하게 됩니다.
- 여기에서 문제는 로그를 검토하고, 데이터를 형성하며, metric 을 계산하는것이 Computationaly Expensive 하다는것입니다. 이에 대해서는 4.2 에서 알아보겠습니다. 

> Analysis and Reporting

- 각 메트릭에 대한 통계가 계산된다면, 몇가지 품질 기준에 따라 메트릭을 평가하고, 각 메트릭에 대한 성능에 대한 보고서를 형성합니다.

> ## Experiment Corpus

- 평가에 이용되는 Experiment Corpus 는 metric 평가 결과의  신뢰도에 매우 큰 영향을 미칩니다. 
  - 즉 Experiment corpus 에 대해 bias 가 있거나, 품질이 낮은 Experiment 를 이용하여 metric 의 평가를 하게 됨다면 안좋은 결론을 내릴 수 있습니다. 
- 우리는 수년에 걸쳐서 Experiment corpus 를 구성하는 방법을 개선하였고, 다른 유형의 평가를 위한 여러가지 Corpus 를 만들었습니다. 다음에는 이러한 corpus 에 대해서 알아보겠습니다.

> Randomly selected recent sample corpus

- 첫번쨰 Corpus 는 최근 현재 회사에서 실행중인 Experiment 를 무작위로 선택한 것입니다.
  - 이 corpus 에 대해 평가된 metric 의 결과는 모든 Experiment 에 대해 일반화 되게 됩니다. 
- 하지만 이 Experiemtn corpus 를 얻는것은 간단하지 않습니다. 
  - 시스템에서 단순휘 무작위하게 고르게 된다면, 잘못 구성되거나, power 가 부족한 실험이 많이 발생하게 됩니다.
  - 이러한 실험에 대해 metric 을 평가하게 되면 잘못된 결론을 내릴 수 있습니다.  
- 잘못된 실험 구성에 의하여, 실험들은 오류가 있을 수 있습니다. 
  - 예를 들어서 크롬에만 적용되는 Treatment 를 적용하였지만, control 에는 크롬유저와 사파리 유저 둘다 있을 수 있습니다. 
  - 이러한 실험을 우리의 evalutation corpus 에 포함하는것은 bias 를 증가시킵니다. 
  - 다행인 것은 이와 같은 실험은 예상되는 참여자와 실제 참여자의 비율을 조사하여 차이가 유의한 경우 실험을 거르는 형태로 찾아낼 수 있습니다. (크롬 유저만 받으면 10만인데 20만이 control 에 들어왔다고? 이건 말도안돼!) 
  - 하지만 이처럼 단순한 해결책이 통하지 않는 실험이 많이 존재합니다. (중복된 id ...)
- 그래서 이러한 경우를 걸러내기 위하여 합리적인 범위 내에 experiment metric 이 존재하는지를 검정합니다. 
  - 예를 들어 특정 실험이 수익을 두배로 증가시키면 '정해진 range 를 벗어낫으므로 이 실험은 제대로 구성되었을리가 없다' 라고 판단하게 됩니다.

- 또한 실험에서 적용되는 많은 feature 들은 아주 작은 영역에만 적용됩니다.
  - 예를 들어서 "4200/75" 와 같은 쿼리에 대해서 그 계산값을 어떻게 출력하는지에 대한 실험을 할 수 있습니다. 
  - 이러한 쿼리를 보내는 사용자가 거의 없기 떄문에, 이러한 메트릭의 movement 를 탐지하기 위해서는(즉 실험이 power 를 가지기 위해서) 는 엄청나게 많은 사용자가 필요하거나 또는 사용자를 '4200/75' 와 같은 쿼리를 보낸 사용자 로 제한하여야 합니다. 
  - 하지만 이런 조치 없이 그냥 모든 유저에게 적당한 샘플 수로 실험을 진행한 경우, 이 실험에 대해서 metric 은 유의한 움직임을 보이지 않을것이며, 이러한 metric 을 evalutation corpus 에 포함시키는것은 시간 낭비입니다.
- 이런 유형( 에러가 있거나 power 가 너무 약함) 의 무쓸모한 Experiment 를 감지하는 방법은, 통계적으로 유의한 메트릭의 비율이 우연으로 예상되는 비율보다 큰지 알아보는 것입니다.
  - p-value 로 인해 5% 가 '실험이 효과가 있는데도 없다고 함' 이므로, 5% 를 초과하여 metric 이 얼마나 움직였는지를 체크하여 위처럼 'power 가 부족한 실험' 을 걸러낼 수 있다는 의미입니다.

> Interesting Corpus

- 두번째 corpus 는 metric 평가를 위한 실험의 '흥미(Interesting)' 에 기초하여 수동으로 구성합니다.
- 이떄에 흥미로운 실험은 다음과 같은 예시가 있습니다. 
  -  다양한 feature 영역에 대해 수행되는 대표적인(representative) 실험
  - 유저의 행동을 이해하기 위해 실행되는 학습(learning) 실험
  - 사용자에게 부정적인 영향을 미친것이 확실한 버그를 발견했던 실험
  - current metric 이 잘 작동하지 않는 실험
- 예시를 하나 들겠습니다. 이전에 성공 지표를 '클릭 이후에 지난 시간' 으로 success 를 정의할 떄에, 클릭 이후에 아무것도 하지 않지만 result 페이지에서 답을 알고 돌아가는 경우는 성공으로 측정하지 못하는 에러가 있었습니다.
  - 즉 이러한 실험은 네번째 카테고리로서 Interesting Experiment corpus 에 포함될 가치가 있습니다.
- 우리는 각 실험에 대해서 positive 또는 negative 의 label 을 붙입니다.
  - 라벨을 붙일떄에 사용자가 더 좋은 경험을(positive) 했는지 아닌지에 대해서 어떻게 판단할 수 이을까요? 
  - 우리는 단순히 이 feature 가 production 으로 배포되었는지만 단순히 체크하려는 유혹을 받을 수 있습니다. (즉 배포가 되면 positive)
  - 하지만 이러한 방식은 신뢰될 수 없습니다. 왜냐하면 특정 실험은 단순히 사용자에 대한 행동을 이해하기 위해서 수행된다던지, 유저에게 영향이 없는 실험이라던지, 최종 버전의 Feature 를 내려는 실험이 아니라 좋은 feature 를 만들어내는 디딤돌과 같은 실험을 할 수 도 있는 등 다양한 실험이 있기 떄문입니다. (즉 posivitive / negative 를 붙이기 어려운 실험이 있다는것)
- 위와 같은 이유로 우리는 label 을 얻기 위하여 수동적인 process 를 사용합니다. 
  - 기준 metric 기준만으로 label 을 할당하게 된다면 이는 우리가 개선하려는 metric 에 유리하게 편향될 수 있습니다. 
    - 예시로 A metric을 평가려 하는데 A 가 큰 실험 : positive / A 가 작은 실험 : negative 로 정의한다면 A metric 을 평가시에 100% 의 정확성을 가지게 됩니다. 즉 'label' 을 매길때에는 평가하고자 하는 metric 을 너무 참고하면 안됩니다.
  - 정확한 label 을 매기기 위하여 전문가 패널과 함께 사용자 연구 / meric 에 대한 피드백 / 다른 실험들을 살폅기..... 등 다양한 부분으로 고려하여 Experiment 의 label 을 붙입니다.
  - 이는 비싼 process 이지만 고품질의 label 을 형성하게 됩니다.
- 이런 '흥미로운 corpus' 를 구성하는 과정은 본질적으로 편향되어있다는 점에 주의해야 합니다. 
  - corpus 의 결과를 모든 실험에 일반화 할떄에 주의해야합니다. 
  - 그러므로 우리는 이러한 corpus 에서 얻은 결과를 무작위로 샘플링된 corpus 에서도 테스트 하도록 권장됩니다.
- 왜 굳이 이런 interesting 한 corpus 를 구성하는것일까요 ? 그냥 처음부터 Randomly Selected 된 Experiment 에 대해서 평가를 수행하면 안될까요? 
-  이러한 '흥미로운' corpus 는 무작위로 샘플링된 corpus 보다 metric 간의 차이를 훨씬 더 잘 나타낸다는 것을 발견하였습니다.
  - ground truth label 은 단지 metric 의 sensitivity 만을 측정하는 것이 아니라, 유저의 true label 을 참고하여 더욱 자세하게 metric의 품질을 측정할 수 있습니다.
  - 흥미있는 experiment corpus 의 실험은 질적 분석을 통하여 특정 실험에서 측정 지표의 변화를 야기한 원인을 결정하고 , 측정 지표를 추가로 개선하는 방법에 대해 생각할 수 있게 합니다.
- 이러한 이점 떄문에 분석가들은 흥미로운 corpus 에 대해서 먼저 metric 의 평가를 실시한 이후, 여기에서도 잘 작동하는 metric 후보들은 무작위로 sampling 된 corpus 에서 다시 평가되게 됩니다.

> small corpus 

- 일부 feature 팀들은 기능별 개선을 위하여 기능과 관련된 small corpus 를 유지합니다. 
  - 예를 들어서 광고팀은 광고 선택 / 배치 등과 관련된 그들만의 small corpus 를 가지고 있습니다. 
- 이러한 corpus 는 기능별 metric 을 개선하기 위해 사용됩니다
  - 매우 특정한 기능 (help 메뉴에서의 클릭 동작) 의 경우에는 모든 corpus 에서 적용될 필요가 없을 수 있기 떄문입니다. (이렇게 특수한 feature 는, 이 영역을 바꾼 실험이 아닌한, 거의 영향을 안받아서 controll , treatment 모두 동일한 경우가 매우 많음)

> ## Metrics Lab

- 이전에 말한것처럼 Experiment corpus 에서 바로 metric 의 평가를 수행하는 일은 매우 큰 연산량을 요구합니다. 
  - 왜냐하면 Experiment corpus 데이터 자체가 어마어마하게 크기 때문입니다. 
  - 만일 2주간 수행한 실험이 100개 쌓였다고 합시다. 그렇다면 이 실험 데이터는 약 4년간의 길이를 가진 로그데이터가 됩니다. 

![png](/assets/images/Stat/78_2.png)

- Metric Lab 은 이러한 Computational problem 을 위와 같은 구조를 통하여 해결하였습니다. 
- 100개의 Experiment corpus 가 있으면 이 전체 로그 데이터로부터 Metric 의 평균을 비교하는 평가 작업을 처리하려면 100시간 정도의 시간이 필요합니다. 
  - 그러므로 이 전체 로그에서 추출된 실험 데이터 캐시는 오로지 실험에 필요한 대한 데이터만 사용하게 됩니다. 
  - 전체 로그 대신에 추출된 데이터에서 Metric 을 평가/분석하게 되면 최대 10시간정도의 시간만이 듭니다. 
- 대부분의 평가 작업에는 트리거된 사용자 모집단만 필요합니다. 이때에 트리거된 실험 데이터 (실험에 참가한 유저의 로그 데이터) 만 이용하게 되면 7시간 까지로 줄어듭니다.
- 그리고 이전에 미리 계산되었던 메트릭은 재사용하는방식으로 구현하게 되면 (precomputed Standard Metric) 시간을 5시간까지로 줄일 수 있습니다. 
  - 이 OEC 일 경우 몇개의 metric 이 같이 사용되는데, 이떄에 각각을 모두 계산하는게 아니라, 이전에 계산된 metric 을 이용하게 됩니다. 

![png](/assets/images/Stat/78_3.png)

- 위 그림은 metric evalution process 를 데이터 분석가의 입장에서 바라본 것입니다. 
  - 이 프로세스는 쉽고 간단하여 메트릭 아이디어를 평가하는데에 매우 쉽게 사용될 수 있습니다. 
  - 분석가는 평가할 측정 기준의 이름, experiment corpus 이름 등을 명시하여 내 작업에 대한 프로파일을 만드는것으로 시작합니다. 
  - 그 이후 SQL 과 같은 언어를 이용하여 새 메트릭에 대한 계산 로직을 정의합니다. 이를 메트릭스 랩에 전달하고 나면 메트릭스 랩은 보고서를 내놓습니다.

# [Metric Evalutation Process](#link){: .btn .btn--primary}{: .align-center}

> ## Metric Evaluation

- Hauser 과 Katz 는 좋은 측정 기준의 두가지 속성을 언급했습니다.

1. 측정 기준을 개선한다면 회사는 장기적으로 원하는 결과로 이동해야한다. 
2. 개별 팀은 metric 에 직접적으로 영향을 끼칠 수 있어야 합니다. 

- 위 두가지 특성은 중요합니다. 
  - 회사의 목표와 상관관계가 없는 지표는 자칫 잘못된 목표로 향하게 됩니다. 
  - 또한 팀이 직접적인 영향을 끼칠 수 없는 지표는 해당 팀의 작업의 방향을 정하는데에 적합하지 않습니다. (광고팀에서는 쿼리당 클릭률 같은 지표에 대해서는 아무런 작업을 할 수 없을것입니다. 즉 이 메트릭이 있어봤자 광고팀 입장에서는 아무런 도움이 안됨)
- 여기에서는 이러한 속성을 측정하는 몇가지 메타 메트릭스(다른 메트릭을 비교하기 위한 메트릭) 을 소개하려 합니다. 
  - 우리는 메타 메트릭을 단순하게 유지하려고 하였습니다. (쉽게 해석하고 디버그 할 수 있도록)

> ## Sensitivity

- Contolled Experiment 입장에서 메트릭의 Sensitivity 는 메트릭이 treatment 와 cntrol 의 차이가 delta 라고 할때에, 이 delta 만큼의 차이를 감지하기 위하여 필요한 샘플 데이터의 양을 나타낸다고 볼 수 있습니다.
- Sensitivity 가 크가면 이러한 작은 변화도 빨리 감지하여 실험에 필요한 Sample 데이터 수를 작게 합니다. 
- Sensitivity 는 실험 실해에 필요한 시간을 단축하고 의사결정을 빠르게 할 수 있어 민감도는 매우 중요한 성질중에 하나입니다. 
- Sensitivit 는 데이터의 양(사용자 수 , 쿼리 수, 세션수 ...) 와 메트릭의 분산 및 effect size(Treatment - contol 의 평균차) 에 의 세가지 요인에 따라 달라집니다. 
  - 이때에 데이터의 양과 메트릭의 분산은 메트릭의 속성이며, 실험 유형에 따라 크게 달라지지 않습니다. 
  - 하지만 마지막(effect size)  요인은 조직에서 어떤 종류의 실험을 수행하느냐에 따라 직접적으로 달라집니다. 
    - 즉 contol 과 별반 다를바가 없는 Treatment 를 적용할 경우 effect size 는 매우 작아질 수 있습니다. 
  - 위와 같이 effectsize 는 실험 유형에 따라 달라지므로 특정 실험에서 민감했던 metric 은 다른 실험에서 민감하지 않을 수 있습니다. 
    - 예를 들어 페이지 로드 시간은 페이지에 시각적 feature 를 얼마나 추가하는지에 대해서 민감한 지표일것입니다. (시각적 feature 은 로드하는데에 시간이 걸리기 떄문) 하지만 백앤드에서 순위 알고리즘을 변경하는 실험에 대해서는 둔감할 것입니다. 
  - 그러므로 조직에서 실행되는 실험들의 맥락에서 메트릭의 민감도를 평가하는것이 중요합니다. 
    - 우리에게 있어 이러한 맥락은 Expereiment corpus 에 의해서 정의됩니다.

> Sensitivity

- m 을 metric 이라 하고 $\{e_1,e_2...,e_N\}$ 을 experiments corpus 의 metric 이라고 합시다. m 에 대해서 실험 $e_i$ 에 대해서 수행한 statistical test statistics 를 $t_i$ 라 합시다. 그러면 우리는 Sensitivity 를 다음과 같이 정의할 수 있습니다 .

$$Sensitivity(m) = \sum_{i=1}^{N} abs(t_i) / N$$ 

- $abs(t_i)$ 가 큰 경우에는 매우 작은 p-value 를 나타냅니다. 즉 이는 더욱 Sensitive 한 메트릭을 나타내게 됩니다. 
- 모든 corpus 에 대해서 Large Sensitivity score 를 가진다는것은 , metric 이 다양한 타입의 실험들에 대해서 Sensitive 하다는것을 의미합니다. (또는 많은 팀이 수행하는 실험들은 이 metric 에 영향을 가하고 있다는것을 의미합니다. )
  - 둘중 어느쪽이던 우리가 원하는 좋은 메트릭입니다.

> Binary Sensitivity

- 우리는 또한 Binary Sensitivity 를 정의할 수 있습니다. 이는 전체 실험 corpus 중에서 statistically significant 하다고 결론 내리는 실험의 비율을 나타냅니다. Binary Sensitivity 는 위의 Sensitivity 보다는 훨씬 robust 하고 또한 해석도 용이합니다. 
- t 를 metric 이 Statistically SIgnificant 하다고 결론내릴 통계량이라고 합시다. (주로 p-value 0.05 기준으로 설정되고는 합니다.)
- 그리고 $I$ 는 indicator funtion 이라고 합시다. 그렇다면 다음과 같이 정의됩니다. 

$$Binary Sensitivity(m) = \sum_{i=1}^N I(abs(t_i)>t)/N$$

> Variance Reduction

![png](/assets/images/Stat/78_4.png)

- 위 그림은 Binary Sensivity 를 t=1.96 의 Threshold 에 맞추어 계산해 본 결과입니다. 
- 위와 같은 비교는 몇가지 흥미로운 점을 시사합니다. 먼저 위의 값들이 어떻게 정의되었는지 살펴봅시다.

![png](/assets/images/Stat/78_5.png)

- 단순히 user event 를 count 한것은 별로 Sensitive 하지 못합니다.
  - Queries per User , Session per User , Queries per Session 
- 더 Sensitive 한 metric 을 얻기 위해 우리는 count 를 normalize 해 보았습니다. 
  - Queries per Session 은 Queries per User 보다 훨씬 Sensitive 하였습니다. 
  - Overall Queries click rate 는 Queries with Clicks per User 보다 훨씬 Sensitive 하였습니다. 
- 이렇게 더욱 Sensitive 해진 이유는 바로 Variance reduction 덕분입니다. 
  - 쿼리의per user 수는 매우 큰 range 를 가집니다. 그에 반해 쿼리 per session 은 bounded 가 됩니다. (세션마다 쿼리이므로 많아봤자 10?) 
  - 비슷하게 Queries with Clicks per User 는 bounded 되지 않은 한편 click rate(queries with clicks / total queries) 는 0~1 사이로 bounded 된 값을 가집니다.
- 이러한 Variance reduction 을 정의를 다르게 해서 얻을 수도 있고 Capping 을 통해서 얻을수도 있습니다. 

>Specific metric

![png](/assets/images/Stat/78_4.png)

- 위 그림을 다시 봅시다. 위에서  Overall Query Click Rate 는 어느정도 큰 Sensitivie 를나타냅니다.

![png](/assets/images/Stat/78_6.png)

- 이때에 위와 같이  Overall Query Click Rate 의 한 부분인 Web Result Click Rate 의 Sensitivity 를 보면 더욱 큰 값을 나타내고 있음을 알 수 있습니다. 
- 이러한 결과는 'Experiment 는 특정한 일부분을 바꾸는것' 은 더 쉽지만 '전체적인 사용자 경험' 을 바꾸는것은 여럽게 떄문에 나타난 현상입니다. 
- 이러한 이유로 인해 Experiment corpus 에 Related Search Click Rate 와 연관된 실험이 별로 없었음에도, Related Search Click Rate 의 Sensitivity 가 큰 값을 나타낸 이유도 같습니다.  

> System level metric 

![png](/assets/images/Stat/78_4.png)

- 위에서 세번쨰 그룹 (Log Record Size , Page Load Time) 을 보면 이 그룹은 시스템 레벨의 metric 입니다. 
- 이러한 시스템 레벨의 메트릭은 유저의 행동을 매져한다기 보다는, 시스템 엔진의 operation 을 매져합니다. 
  - 이러한 메트릭은 보통 Sensitive 하지만 뒤에서 이러한 metric 이 왜 안좋은지에 대해서 알아보겠습니다.

> ## Alignment with User Values

- Bing 에서 우리는 customer 의 만족을 서치 엔진의 주요 long term objectives 로 삼았습니다. 
  - 만족한 유저는 더 많이 사용할 것이고, 더 큰 광고 매출로 이어질 것입니다. 
- 각각의 interesting corpus 에 있는 실험은 Positive 와 Negative label 이 붙어있었다는것을 기억합니다. 
  - 이러한 label 을 이용하여 user value 와 alignment 가 제대로 이루어지는지에 대해서 살펴보도록 합시다. 

> LabelAgreement(m)

- $N_a^+$ 는 metric m 이 통계적으로 유의하고, metric 이 label 과 방향이 일치하는지를 나타냅니다. 
  - treatment - control 평균 차이 값이 통계적으로 유의한 positive 이고 또한 label 도 positive 일떄
  - treatment - control 평균 차이 값이 통계적으로 유의한 negative 이고 또한 label 도 negative 일떄
- $N_a^-$ 는 metric m 이 통계적으로 유의하고 metric 이 label 과 방향이 반대일떄를 나타냅니다. 
- 우리는 여러 버전의 LabelAgreement 를 정의했고, 아래는 그 예시입니다. 

$$LabelAgreement(m) =\{ w_1 \cdot MAX(N_a^+ , N_a^-)-w_2\cdot MIN(N_a^+,N_a^-)\}/N$$

- 위의 $w_1$ 과 $w_2$ 는 non negative weight 로서 $w_1 + w_2=1$ 의 값을 가집니다.
- 이떄에 특정한 metric 은 '더 작아야' 좋기 떄문에 (page load time) MAX operator 를 통하여 agreement 를 측정하게 됩니다.
  - 반면에 MIN operator 는 disagreement 값을 측정하게 됩니다. 
  - 이렇게 정의한 위 값은 'label 이 positive , negative' 인지에 대해서 '일관된 행동' 을 나타내는지를 나타냅니다. 
  - 좋은 메트릭은 사용자 경험이 좋을때 일관적으로 metric 이 작아지는 패턴을 가지거나, 사용자 경험이 좋을떄 일관적으로 metric 이 커지는 패턴을 가집니다. 두 경우 모두 $LabelAgreement(m)$ 이 큰 값을 가지게 됩니다.
- 우리는 weight 값을 조절함으로서 metric 이 '맞게 측정한 경우' 에 더 큰 weight 를 줄지 또는 틀릴 경우에 더 큰 weight 를 줄지를 결정할 수 있습니다. 

> LabelAgreement(m) (None Disagreement)

- 우리는 evaluation 을 거듭할수록 사실 Disagreement 보다는 agreement 가 훨씬 중요하다는것을 꺠달았습니다. 
- 그래서 우리는 아래와 같은 Simple Version 을 사용하게 되었습니다. (즉 Disagreement 는 고려하지 않음)

$$LabelAgreement(m) = MAX(N_a^+,N_a^-)/N$$

- 위와 같은 경우도 이전과 비슷하게 '얼마나 많은 Experiment 에 대해 일관된 방향으로 유의하다고 결론 내렸는지' 를 매져하게 됩니다.
- LabelAgreement 는 이전에 살펴본 Sensitivity 와 user value(만족(positive)/ 불만족(negative)) 을 통합한 것이라는것을 명심합시다. 
- 그러므로 이 매져는 interesting corpus 를 평가하기 위한 evaluation 기준으로 사용될 수 있습니다. 

> Example of Label Agreement score

![png](/assets/images/Stat/78_7.png)

- 위와 같이 LabelAgreement score 를 위와 같이 살펴볼 수 있습니다. 
- 위의 값을 볼 떄에 Session per User 메트릭은 매우 낮은 agreement score 를 가지고 있습니다. 
  - 직관적으로는 이 메트릭은 user value 와 alignment 가 잘 이루어질것으로 예상됩니다. 왜냐하면 유저가 사이트에 자주 온다는것은 사이트가 좋다는것과 일맥 상통한다고 생각되기 떄문입니다.
  - 위와 같은 이유로 Session per User 는 key site metric 으로 흔히 채택되곤 합니다. (Site Visit 이라는 이름으로 metric 이 생성되기도 합니다.)
  - 하지만 실제로는, 이 metric 을 개선시키기란 매우 어렵습니다. 
    - 사용자의 일일 웹 검색량이 일정하다고 할때, 이 메트릭이 상승한다는것은 다른 검색엔진에서 검색 점유율을 뻇어서 얻는것과 같습니다.'
    - 즉 짧은 시간동안 유저에게 이러한 변화를 요구하는것은 매우 어렵습니다. 즉 이러한 유저별 event Count 메트릭은 공통적인 문제를 가지고 있습니다.
- Click rate metric 은 매우 좋은 Label Agreement 를 가지는것을 볼 수 있습니다. 그중에서 제일 높은 LabelAgreement 를 가지는 metric 은 web result click rate 였습니다. 
  - 이는 놀라운 일이 아닙니다. result 의 품질을 개선하게 되면 이 메트릭이 직접적으로 변하게 되기 때문입니다. 
- Web result click rate 보다 더 나은 메트릭이 있을까요? 있습니다. 
  - bing 에서 가장 labelagreement 가 높은 메트릭은 앞에서 정의한 success 개념을 활용합니다. (여기에서는 논의되지 않습니다.)
  - 그럼에도 Web result click rate 는 단순한 메트릭중 매우 좋은 성능을 보이는 메트릭이였습니다. 

> Label of Agreement Score

- 이전에 말했듯이, sysytem - level metric 은 꽤 높은 Sensitive 를 가지나, Label Agreement 는 매우 낮은것을 볼 수 있습니다.
- 또한 그림에서 (+) 또는 (-) 로 표시된 방향을 살펴보는것도 흥미롭습니다.
  - (+) 는 metric 의 값이 높아지면 user 의 경험이 positive 가 됩니다.
  - (-) 는 metric 의 값이 낮아지면 user 의 경험이 positive 가 됩니다.
- Ads lick rate 는 (-) 의 방향을 가집니다. 이는 광고와 사용자의 Engagement 를 증가시키면 user value 가 감소한다는 이야기입니다.
  - 또한 검색 결과의 품질을 떨어트리면 사용자가 광고에 더 많이 참여한다는것을 나타냅니다. 
- 또한 사용자당 쿼리와 세션당 쿼리는 부정적인 방향으로 Label 과 더 일치하고 있습니다.
  - 이는 일반적으로 검색결과의 품질을 향상시키면 사용자가 쿼리를 많이 재구성할 필요가 없어집니다. 즉 세션당 전체적으로 쿼리가 줄어들게 되는 것입니다. 
  - 반대로 검색 품질을 떨어트리게 되면 사용자가 원하는것을 찾지 못하고 더욱 많이 쿼리를 발행하게 됩니다.

> Analysis

- 분석가를 도와주기 위하여 메트릭스 랩은 이에서 보고한 모든 meta-metrics 를 포함한 자동화된 보고서를 만들게 됩니다. 
- 또한 분석가가 profile 에서 지정한 모든 메트릭 쌍에 대하여 쌍별 비교를 형성하여 두 메트릭이 일치하지 않는 특정 실험들을 나열합니다. 
  - 예시로 한 메트릭은 통계적으로 유의한 positive 이고 , 다른 메트릭은 통계적으로 유의한 negative 혹은 유의하지 않은 경우입니다.
- 이 떄에 실험에 자주 영향을 받는 다른 디버그 정보도 생성합니다.
  - 이러한 디버그 메트릭을 분석함으로서 메트릭 동작에 대한 많은 통찰을 얻을 수 있습니다. 
  - 이러한 분석에서 insight 를 얻는것 또한 향후 작업의 방향중 하나입니다.

# [Examples](#link){: .btn .btn--primary}{: .align-center}

- 이 섹션에서는 위와 같이 메트릭 평가 프레임워크를 적용하여 실제메트릭을 개선하는 몇가지 아이디어를 제시합니다. 
- 이 예제를 통하여 우리는 '결과를 상세하게 보고' 하는것을 얻는게 아니라, 메트릭 평가 프레임워크가 어떤것을 할 수 있고, 어떤것을 할 수 없는지에 대해서 알아보는 것입니다. 

> ## Dedup or not Dedup

- 중복 쿼리는 사용자가 같은 세션 내에서 연속으로 두번 실행한, 동일한 쿼리입니다. 
  - 이러한 쿼리는 검색 엔진 쿼리 로그 내에서 매우 일반적이며 , 거의 모든 쿼리의 10% 를 차지한다고 합니다. 
- 이러한 쿼리중에서 일부는 실제 사용자가 시작한 쿼리일 수 있고, 다른 쿼리중 일부는 브라우저 캐시 손실, 의도치 않은 두번 클릭 등으로 발생할 수 있는 에러입니다. 
- 이때 흥미로운 질문은 metric 계산에 대해서 '모든 쿼리를 사용하는것이 나은지' 또는 '중복 쿼리를' 통합하고 사용자 작업 (클릭, hover 등) 을 조합하여 사용하는게 좋을지 의 여부입니다.
- 직관적으로 생각하면 사용자의 중복 쿼리를 통합한다는것은 노이즈가 제거되므로 메트릭에 긍정적인 영향을 준다고 생각할 수 있습니다. 
  - 하지만 실제로는 중복 쿼리에서의 신호가 손실되어 피해를 입을 수 있습니다. 
  - 이 결정은 많은 메트릭인 '쿼리수' , '쿼리당 클릭 수' 등에 영향을 미치기 떄문에 매우 중요한 결정중에 하나입니다.
- 라벨링한 데이터 수집에 기초한 전통적인 접근 방식(실험을 두가지 )을 사용하면 이 질문에 답하는것은 매우 어렵습니다. 
  - 즉 데이터에 대해 추가적으로 즉 중복된 쿼리인지 아닌지에 대한 라벨을 형성하고, 중복된 쿼리를 발생한 유저에 대해서는 중복된 쿼리를 경우 통합해보면서 그 영향을 고려해야 합니다. 이는 엄청 힘든 작업입니다.
  - 또한 이렇게 하더라도 noise 가 감소하는것과(중복된것을 처리), 신호가 감소하는것(ㅈ중복되는것 처리하여 정보량 감소) 간의 Tradeoff 를 평가하는것은 어렵습니다.
- 하지만 이를 우리의 방법으로 평가한는것은 매우 직설적입니다. 
  - 우리는 3개의 key metric 에 대해서 각각 다른 방식의 metric 을 형성하였습니다. 즉 dedupping 과 dedpupping 을 하지 않은 metric 을 형성해 보았습니다.

![png](/assets/images/Stat/78_8.png)

- 그 결과는 위와 같습니다. 
  - Table 은 $\Delta$ 에 대한 Sensitivity , LabelAgreement , LabelDIsagreement 를 나타내고 있습니다. 
  - dedupped metric 이 좋은 경우는 초록색으로 표시됩니다. 
  - dedupped 되지 않은 metric 이 좋은 경우는 주황색으로 표시됩니다. 
- 우리는 dedupped 된 metric 이 더 나은 성능을 발휘한다는것을 볼 수 있었습니다. 
- 여기에서 유일한 빨간색인 실험에 대해서는 Deep dive(더 깊게 살펴봄) 를 해볼 수 있습니다.
  - 이전에 사용한 debug 방법을 사용하여 민감도의 차이는 두개의 실험이였지만 매트릭의 direction 이 다른 경우 9가지나 있었다는것을 알았습니다. 
  - 이러한 9가지 경우를 자세히 조사함으로서 dedup 된 쿼리를 적용하는게 더 낫다는것을 재차 확인할 수 있었습니다.

> ## Metric Sensitivity to Threshold Changes

- 많은 metric 은 주로 Threshold 에 의존하여 value 가 결정됩니다. 
- 예를 들어서 이전에 보았던 dwell time 에 대한 success 는 아래와 같이 정의되었었습니다.

$$success(q)=\begin{cases}
1,\text{if q had a click with dwell time > T seconds}\\
0, \text{otherwise} 
\end{cases}$$

- 위에서 시간 T 는 검색 결과가 사용자가 만족할만큼 좋은 정보를 제공했는지에 대해 판단 기준이 됩니다. 
- 이러한 Click Success 는 다른 query Success , session success 와 같은 성공 관련 메트릭의 기본 메트릭입니다. 
- 우리는 이러한 Treshold가 메트릭의 품질에 미치는 효과를 알아보려 한다고 합니다. 
  - 15초 ? 30초? 1분 ? 어떤것을 사용할떄에 메트릭이 개선될까요? 
- 이 질문에 답하기 위한 전통적인 접근 방식은 라벨이 붙은 로그 데이터를 수집하는 것입니다.
  - 이떄에 성공 / 실패에대한 주석을 사용자 자신 또는 전문가가 달 수 있습니다. 
  - 그 이후에 성공 label 을 판단하기 위한 서로 다른 cutoff 값과 비교하여 최상의 임계값을 결정할 수 있습니다. (cutoff 가 몇일떄에 최적의 정확성을 가지는지 비교)
- 하지만 이러한 Training data 를 얻는것은 비용이 많이 들고,label 판단 프로세스의 영향에 매우 민감합니다. 
  - 즉 biased 되기가 쉽다는 것입니다. 
- 또한 이러한 방식은 단순히 클릭성공의 Threshold 에 대한 정의의 정확성만을 평가하게 됩니다.
  - 이러한 정의를 기반으로 할때에 , 얼마나 좋은지 또는 얼마나 중요한지에 대해서는 알려주지 않습니다. 

![png](/assets/images/Stat/78_9.png)

- 위 그림과 같이 클릭 dwell Time 을 정의하는 다양한 임계값 (15, 30, 60) 을사용하여 수정된 버전을 구현하고, 평가 프레임워크를 실행하여 수정된 메트릭을 기존의 임계값(30초) 와 비교합니다. 
  - 이때에 우리는 5개의 메트릭 (M1 .. M5) 에 대해서 임계값을 비교하였습니다.
  - interesting corpus 와 비교하면 1~2일 이내로 결과를 얻을 수 있습니다. 
  - bar 가 없는 부분은 바꾸어 보아도, 아무 이익이 없는 (Delta = 0) 경우를 나타냅니다. (M4)
- 60-second 정의의 경우에는 오히려 안좋아지는것을 알 수 있습니다. 
- 15-second 의 정의는 두개에서는 좋았고 하나의 경우에는 안좋은 결과를 덩었습니다. 
  - 하지만 이떄에 우리는 100개 이상의 experiment corpus 에 대해서 평가가 진행되었다는것을 기억합니다. 
  - 그러므로 이러한 결과는 매우 적은 차이만을 보여주고 있다고 볼 수 있습니다.
- 즉 이러한 결과를 바탕으로 우리는 30 - second Threshold 를 그대로 유지하기로 하였습니다. 

> ## Measuring User Effort

- 사용자의 노력을 측정하기 위해 일반적으로 사용되는 방법중 하나는 클릭 시간입니다. 
- 이 메트릭은 사용자 세션 시작(첫번쨰 쿼리) 부터 첫번째 결과 클릭까지의 시간을 클릭합니다.
- 결과가 좋고 페이지가 명확하면 할수록 사용자가 클릭할위치를 더욱 빨리 정할것입니다.
- 이 사례 연구에서는 클릭시간을 다른 유사한 메트릭과 비됴합니다. 
  - TIme to Long Click : 사용자가 클릭 후 최소 30초동안 검색 엔진으로 돌아가지 않는것을 long 으로 정의합니다. 
  - 직관적으로 long click 은 그들이 더 좋은것을 찾았을떄에, 기존의 클릭 시간보다는 좋아보입니다. 

![png](/assets/images/Stat/78_10.png)

- 그 결과는 위와 같습니다. 긴 클릭류로 메트릭을 전환하면 메트릭 품질에 매우 큰 영향을 끼칩니다.
- Sensitivitiy 는 거의 두배 , Label Agreement 는 거의 3배 증가하였습니다. 
- 심층 분석의 결과, Time to Long Click 은 거의 모든 Feature 영역 (사용자 인터페이스 개선 , 광고, 웹결과 품질) 에서 winner 가 되는 metric 이였습니다. 
- 실험 도중 몇가지 Time to Long Click 과 CLick TIme 의 방향이 일치하지 않는 경우가 있었으나 두 경우 모두 Time to Long CLick 이 맞는 경우였고, Time to Click 은 잘못된 경우였습니다. 

# [Conclusion](#link){: .btn .btn--primary}{: .align-center}

> ## Impact

- 이 paper 에서 논의했던 Measurement Framework 는 지난 몇년동안 bing 에서 적용되고 있는 프레임 워크입니다. 
  - 이것은 수많은 데이터분석가, 개발자 등에 의해서 사용되었습니다. 
- 위에서 논의했던 case 말고도 다양한 부분에서 이 프레임워크가 적용되었습니다.
  - Experiment 에 대한 실험 지침 개발
  - 'success' 매트릭 개선 
  - 정확한 dwell 시간 계산을 위한 평가
  - revenue /relevance trade off metric 개발 
  - good abandonment 에 대한 metric 개발 
  - transfomation (로그 , 캐핑 등) 에 대한 영향
- data driven metric evalution 을 통하여 우리는 metric 의 성능을향상시키고, A/B Testing의 품질을 올릴 수 있었습니다 

> ## Conclusion

- 좋은 metric 은 조직에 있어서 매우 중요하지만, 이를 평가하기 위한 frame work 를 설계하는것은 매우 어려운 일입니다.
- 이 논문에서는 빙에서 좋은 메트릭을 설계하고, 시간이 갈수록 개선하는 메트릭 평가 프레임 워크를 소개하였습니다. 
- 좋은 메트릭의 특성을 정의하고 metric Sensitivity 와 user Alignment 를 평가하기 위한 meta metric 을 제안하였습니다.
- 우리는 전통적으로 수동으로 라벨링된 데이터를 기반으로하는 전통적인 평가 접근법 보다 여러 면에서 우수하다는것을 보여줍니다. 

**reference**

- <https://www.exp-platform.com/Documents/2016CIKM_MeasuringMetrics.pdf>

 메트릭 평가 프레임워크를 이렇게까지 자세하게 풀어낼줄은... 왜 마이크로소프트는 이렇게 좋은 정보를 다 풀어내주는지 모르겠네요. 대단대단 ... 왜 애플이나, 아마존같은 기업은 이런 좋은 Paper 를 안내는걸까요? 
{: .notice--success}

