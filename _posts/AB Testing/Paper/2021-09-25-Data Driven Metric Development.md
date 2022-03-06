---
title: "Data-Driven Metric Development for Online Controlled
Experiments  &#58; Seven Lessons Learned"
excerpt: "Microsoft Bing 의 AB Testing Metric 에 관한 논문"
categories:
  - AB_Paper
last_modified_at: 2021-09-25

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 A/B 테스트라고 불리는 Online Controlled experiment 는 많은 웹 기업에서 데이터 중심 의사 결정을 위한 방법론으로 많이 쓰이고 있습니다. 이에 대한 연구로는 많은 설계 기법이나 다양한 문제에 대해 초점을 맞춘 연구가 있었습니다. 하지만 메트릭 자체를 중심적으로 연구한것은 거의 없었습니다. 이 논문에서는 온라인 서비스에서 유용한 메트릭을 개발하는 방법에 초점을 맞춥니다. 
{: .notice--warning}

- 용어 정리
  - Overall Evaluation Criteria (OEC) (also known as goal metrics or key metrics

![png](/assets/images/Stat/68_14.png)

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

- Kevin 은 '측정할 수 없으면 개선할 수 없다.' 라는 말을 하였습니다. 
  - 이는 온라인 서비스에도 해당되는 말입니다. 다양한 서비스에서는 측정 기준을 사용해 사용자가 얼마나 잘 서비스를 사용하고 있는지를 알 수 있습니다.
- 이러한 측정 기준은 '메트릭' 으로 정량화되어 측정될 수 있습니다. 
- 대부분의 온라인 서비스는 두가지의 측정 지표가 있습니다.
  - 오프라인 측정 치표 : 오프라인 데이터 셋 기반 지표 
  - 온라인 측정 지표 : 수백만개의 데이터 로그 기반 
- 업계에서는 온라인 메트릭을 주로 사용합니다.
  -  이러한 온라인 메트릭을 모니터링 / 비교하는 가장 보편적 방법은 AB Testing 입니다.

![png](/assets/images/Stat/68_1.png)

- 위 그림은 서비스와 온라인 메트릭간의 관계를 나타냅니다. 
  - 메트릭을 통해서 서비스가 얼마나 잘 운영되는지 알 수 있으며 이를 통해서 어디를 추가적으로 개선해야될지를 알 수 있습니다.
- 오늘날에는 아마존, 이베이, 페이스북, 링크드인, 넷플릭스 , 야후 등을 포함하는 많은 온라인 서비스 회사들이 제품을 개선하기 위해 Online metric 을 사용하고 있습니다. 
  - 회사의 목표를 달성하기 위한 OEC 를 설정하고 이를 궁극적인 개선 목적으로 삼고 실험을 진행하게 됩니다.
- 이전의 많은 실험들이 실험 플랫폼 / 통계적 추론 등에 집중한 반면 우리의 paper 에서는 메트릭 중심으로 연구를 소개하려 합니다.

# [Preliminaries](#link){: .btn .btn--primary}{: .align-center}

> ## Offline metric vs Online metric

- 업계에서 시스템의 성능을 측정하는 가장 일반적 방법은 AUC(AUROC) , RMSE, NDCG(정규화된 누적 이득) 같은 오프라인 메트릭이 있습니다.
- 이러한 오프라인 메트릭은 Dataset 이 매우 작고, 대상이 실제 유저가 아니였던 학계에서 차용된 것입니다. 
  - 그러므로 실제 사용자가 Sample 인 Online Experimental 에서는 잘 맞지 않는 경향이 있다고 합니다.
  - 또한 온라인 서비스의 궁극적인 목표는 학계와 다르게 비즈니스의 성공이라는 점에서 위 Offline metric 은 잘 맞지 않습니다.
- 물론 Offline metric 이 완전 쓸모없지는 않습니다. 이러한 메트릭은 서비스 초기에 큰 가치가 있습니다.
  - 예시로 빙은 검색 엔진의 초기 단계에서 오랬동안 오프라인 매트릭 NDCG 를 사용하였습니다. 
- 하지만 이러한 NDCG 는 온라인 메트릭이 보여주는 방향과 일치하지 않을때가 많았습니다.
  - 실제로 많은 경우 Offline metric 은 Online metric 과 낮은 상관관계를 가진다고 합니다.
  - 이러한 이유는 2가지일 수 있습니다. 
    - AUC,NDCG 과 같은 오프라인 지표는 인적 요인을 무시합니다. 그러므로 Personalized 된 서비스의 품질을 정확히 측정할 수 없습니다.
    - Offline metric 은 불완전하고, 편향된 Offline data set 을 기반으로 하기 떄문에, Offline metric 이 large scale real user 를 기반으로 하는 Online metric 과는 다를 수 밖에 없습니다. 
  - 아직까지는 Offline metric 과 Online metric 의 상관관계에 대해서는 미해결 과제라고 합니다. 

> ## Types of online metrics

- 여기에서는 Online metric 은 어떤 종류가 있는지에 대해서 알아보겠습니다.

> Business report driven metrics

- 온라인 서비스의 장기적인 목표를 기반으로 정의되는 Metric 입니다. 
  - 일반적으로 인당 수익률, 인당 쿼리, 인당 방문 수  와 같이 비즈니스의 성공과 직접적으로 연결되는 메트릭입니다. 
- 이 메트릭은 온라인 서비스와 직접적 관련이 있으므로 임원, 사업주 등에게 보고하는 용도로 많이 사용됩니다. 
  - 이떄에 주의할점은 , 메트릭의 단기적 움직임은 장기적 영향과 다를 수 있다는 것입니다. 
    - 예시로 빙의 경우 서비스의 성공을 위해서는 사용자당 장기 수익이 중요합니다. 
    - 하지만 대부분의 실험은 단기적(예 : 2주) 으로 이루어지기 떄문에 이러한 장기 수익율은 측정하기가 매우 어렵습니다. 
- 그래서 장기적인 영향을 측정하려면 필연적으로 장기간 실험을 진행해야 하고, 이는 민첩한 대응이 핵심인 온라인 실험에서는 매우 어려운 일입니다. 
  - 이러한 장기적 효과를 측정할 수 있는 방법론도 있는데 여기에서 다루지는 않겠습니다.

> SImple heuristic based metric

- 단순한 휴리스틱 메트릭도 있습니다.
- 이러한 메트릭은 단순한 사용자와 온라인 서비스의 상호 작용에 기초합니다.  
  - 페이지당 클릭율(CTR) , 사용자당 작업 수 등등이 예시가 될 수 있습니다. 
- 이러한 metric은 대부분의 서비스에서 쉽게 적용이 가능합니다. 
  - 예를 들어 특정기간 내 사용자당 작업 수는 , 사용자가 서비스에서 활동하는 빈도를 나타냅니다.
- 하지만 이러한 metric 은 단순한 사용자의 행동만을 나타내기 떄문에 명확한 해석이 어렵고, 우리의 OEC 와 연결시키기가 어렵습니다. 
  - 체류시간이 늘어난다고 좋은것일까요? 단순히 사이트가 느려졌기 때문에 체류시간이 늘어났을 수 있습니다.
  - 또한 체류시간이 늘어났다도 해서 우리의 OEC 인 '매출상승' 과 관련이 있을까요? 
- 우리가 여태 살펴본 Business 기반 매트릭과 Heuristic metric 은 온라인 메트릭의 첫 세대입니다. 
  - 이것들은 단순하고 분명하며 우리의 상식과 일치합니다. 
  - 일반적으로 온라인서비스의 초기 단계에서는 사용자가 충분하지 않고 아직 직관이 부족하기 때문에 이 두가지 메트릭을 적극적으로 이용할 수 있습니다. 
- 하지만 시간이 갈수록 많은 사용자를 확보하고, 서비스가 안정적이 될 경우 이러한 측정 기준은  다음과 같은 단점을 지닙니다.
  - 소규모의 기능 개선에 둔감함. (특히 수익 기반 측정기준)
  - 유저 경험(Experiment) 의 실제 개선과 일치하지 않는 경우가 있다. 
    - 유저는 검색엔진에 만족하지만, 실제로 유저당 쿼리수는 감소할 수 있습니다. (만족하고 더 검색을 안하기 때문)
- 그래서 우리는 세번쨰 온라인 메트릭인 사용자 기반 메트릭이 중요하게 됩니다. 

> User-behavior-driven metrics

- 이러한 메트릭은 사용자 행동을 기반으로 만들어집니다.
  - 잘 설계된 유저 행동 메트릭은 사용자 경험을 직접 측정할 수 있고, 서비스의 장기적 성공과 높은 상관관계를 가져야 합니다. 
- 이 매트릭을 정의하기 위해서는 사용자의 만족과 관련한 측정 모델이 필요합니다.
  - 클릭률 자체가 '사용자의 만족' 을 나타낸다고 볼 수 없는것처럼 , 이러한 측정 모델은 정의하기가 까다롭십니다. 
  - 사용자의 동작을 자세히 분석하며 '만족'(또는 불만 등) 이 어떤것과 관련되는지 모델을 만들어야 합니다.
- 이 메트릭을 설계하는것은 뒤에서 자세히 알아보도록 합시다.

# [Seven Lessons of Online Metric Development](#link){: .btn .btn--primary}{: .align-center}

> ## Lesson 1: Define metrics for metrics

- 우리는 AB Testing 을 수행할때에 , metric 을 사용하게 됩니다.
- 하지만 이러한 metric 을 개발할떄에 이 metric 을 정량적으로 평가할 수 있는 기준이 있을까요? 
  - 수백 수천개의 metric 중에서 어떠한 메트릭이 좋은지 비교하고 선택해야 할 것입니다.
  - 일반적으로 이러한 metric 을 선택할떄에 고려해야하는 두가지 필수 Property 가 있습니다
    - 방향성과 민감성입니다. 
- metric 의 방향성과 민감성은 벡터의 방향과 크기 라고 생각하면 됩니다. 

![png](/assets/images/Stat/68_2.png)

- 이러한 특성은 효과적인 AB Testing 을 위한 OEC Metric 설정에 필수적이라 할 수 있습니다. 

> Directionality (방향성)

- 좋은 metric 은 사용자 경험과 일치하는 명확한 방향이 있어야 합니다. 
  - 즉 사용자 경험에 좋은 영향을 미친다면 늘 일관된 방향을 가르켜야 합니다. 
  - 사용자 경험에 안좋은 영향을 미친다면 늘 일관된 방향을 가르켜야 합니다. 
- 만일 좋은 영향을 미쳤는데 방향이 마구잡이라면 이는 좋은 메트릭이 아니게 됩니다.
- 이러한 사용자 Experiment 를 표시하는데에 있어 방향이 애매한 Metric 을 보는것은 드문일이 아닙니다.
  - 예시로 사용자당 고유 쿼리 메트릭이 있습니다.
  - 검색 결과를 잘 보여준  경우에도 두가지의 방향이 나올 수 있습니다.
    - 검색 결과를 잘 보여줬기 떄문에 오히려 단기적으로는 검색 수가 감소 (추가적인 검색을 안하므로)
    - 또는 이 사이트가 검색 결과를 잘 보여주었으므로 이 사이트에서 검색을 더 많이해 더 해서 metric 이 증가
- 위와 같은 Metric 자체가 모호한 방향성을 가지고 있어 Metric 이 증가하더라도 이게 사용자 Experiment 가 개선되어서 증가한것인지, 아니면 Experiment 가 악화되어서 증가한것인지 결정하기가 힘들 수 있습니다. 
  - 즉 이런 매트릭은 방향성이 좋지 못하므로 OEC 로는 쓸 수 없는 메트릭입니다.

> Sensitivity (민감성)

- 좋은 metric 은 사용자 경험 개선에 대해서 민감하게 반응해야 합니다.
  - 민감한 목표 측정을 통해서 , 팀은 신속하게 의사결정을 할 수 있을것입니다. 
  - 사용자의 경험을 개선했음에도 맨날 같은 값을 가지는 메트릭이 있다면 이러한 메트릭은 쓸모가 없을것입니다.
- 일반적으로 수익기반 측정 Metric 은 긴 실험 시간과 많은 Sample 수를 요구합니다. 
  - 예를 들어서 인당 세션 수는 검색 엔진의 시장 점유율과 만족도와 관련이 있는것으로 나타납니다. 
  - 하지만 이것보다 검색 관련성에 관한 실험일 경우 인당 세션수보다 검색 성공률 metric 이 훨씬 더 즉각적으로 변화하는 MEtric 이라고 합니다. 
  - 즉 유저당 세션 수보다는 유저당 성공 세션 수가 훨씬 더 민감하게 반응하고 선호된다고 합니다. 

> Evaluation

- 이러한 두가지 품질을 측정하고 좋은 메트릭을 고를 수 있게 한다면 실험 개선에 큰 도움을 줄 것입니다.
  - bing 에서는 MEtricLab 이라는 평가 프레임워크가 있다고 합니다.
  - Metric lab 에서는 메트릭의 품질을 비교하고 , 좋은 측정 지표를 추천해줍니다.

> ## Lesson 2: Understand roles of metrics

- 이전에 우리는 온라인 서비스의 목표 메트릭스(OEC) 가 가져야 될 두가지 필수 품질 (Sensitivity , Direction) 에 대해서 알아보았습니다. 
- 하지만 Metric 의 역할이 OEC 처럼 '서비스가 목표에 다다르는지' 를 측정하는 Metric 만 있는것이 아닙니다. 

> Guardrail Metric

- 가드레일 메트릭은, goal metric 을 적용할 수 없는 경우에 대안 / 보충 으로 사용될 수 있는 기능을 합니다. 
- 일반적으로 두가지 시나리오에 대해서 사용됩니다. 
  - 목표 지표가 적용되지 않아 이를 대체할때
    - 예시로 목표 지표를 클릭당 체류시간으로 정했다고 합시다. 
    - 하지만 클릭을 아예 하지 않고 사용자에게 올바른 정보를 제공하는것을 목표로 하는 집단에서는 이러한 OEC 가 무용지물입니다.
      - ex) 날씨 알리미 , 뉴스 헤드라인 
    - 그러므로 이런 집단에서는 OEC 말고 다른 지표(Guardrail) 를 사용할 수 있습니다.
  - 목표 지표가 측정할 수 없는 다른 차원의 사용자 경험 측정
    - 목표 지표는, Metric 하나이기 떄문에 사용자의 단면밖에 보지 못합니다.
    - 그러므로 다양한 Guardrail 지표를 설정하여 다양한 측면에서 사용자를 바라보아야 합니다.
    - 예를 들어 게임 환경에서 사용자의 과금액수를 OEC 로 정하였다고 합시다. Guarail metric 은 사용자의 수를 정할 수 있습니다.
    - 만일 지나친 과금정책으로 OEC 는 증가하나, Guardrail metric 은 감소할 수 있습니다. 이러한 경우 Treatment 를 다시 고려해야할 것입니다.
- 우와  같은 두가지 측면에서 Guardrail metric 이 중요합니다. 그래서 일반적으로 Testing 을 할 때에는 OEC 를 제외하고도 Guardrail metric 을 추가로 정의합니다.

> Denugging metric 

- 디버깅 메트릭은 중요한 메트릭이 이동하거나, 이동하지 않는 경우에 대한 해석을 도와줍니다.
- 일반적으로 Goal metic 은 다양한 사용자의 Behavior signal 을 합쳐놓은 metric 입니다.
  - 그러므로 gaol metric 이 상승했다고 한다면, 어떠한 이유로 상승했는지에 대해서 궁금해 할 것입니다. 
  - 디버그 매트릭은 이러한 해석을 도와주는 매트릭입니다.
- 자세한것은 나중에 더 알아보겠습니다.

> ## Lesson 3: Evaluate metric qualities

- Lesson 1 에서, 우리는 Metric 이 가져야 할 2가지 Qualities 에 대해서 알아보았습니다. 
  - 바로 Sensitivity 와 directionality 입니다. 
- 메트릭의 성능을 알 수 있다면 실험 계획에 큰 도움이 될 것입니다. 
- 이러한 성능을 알아보기 위하여 어떤 방법을 쓸 수 있는지에 대해서 알아봅시다.

> Validation Corpus Methods

- Supervised Learning 에 모티브를 얻어 우리는 실험에 대해 validation dataset 을 구성하였습니다.
  - 즉 이는 AB Tesing 에서 실제 이 기능이 사용자에게 실제로 좋았는지 안좋았는지를 알고 있는 실험들로 구성되어 있는 , Label 이 명확한 실험 Set 입니다.
  - 즉 , 각 실험은 '사용자에게 좋은 실험' / '사용자에게 나쁜 실험' 두가지 라벨을 가지게 되고, 이에 대해서 Metric 을 시험하는 형태로 (Supervised learning) 메트릭의 품질을 확인할 수 있습니다.
- 즉 이러한 Labeled 된 실험들에 대해 많은 메트릭을 실험하면서, 메트릭이 일관된 방향성으로 움직이는지 , 또는 Sensitive 한지에 대해 실험할 수 있다는 것입니다. 
- MetricLab 에서는 메트릭에 대해서 평가했고, 3가지 경우로 구분하였습니다.

1. Metric 이 일관된 방향으로 , 통계적으로 유의한 움직임을 나타내는 경우
2. Metric 이 모호한 방향으로 , 통계적으로 유의한 움직임을 나타내는 경우
3. Metric 이 통계적으로 무의미한 움직임을 나타내는 경우

- 위와 같이 '유의한 움직임' 을 측정할때에는 t-통계량 으로 측정할 수 있습니다. (자세한 내용은 뒤에서 더 알아보겠습니다.)

> degradation Experiment 

- 하지만 위에서 설명했던 Validation Corpus method 는 우리가 새로운 실험을 설계할때에 적용할 수 없다는 것입니다. 
  - 새로운 메트릭을 실험하거나, 새로운 서비스를 시작할떄에 이러한 Validation Set 이 존재하지 않습니다. 
- 이를 해결한 Idea 는 바로 '사용자 경험에 좋은 Featrue 를 고안하는것은 어렵지만 망치기는 쉽다.' 라는 경험에서 시작됩니다.
  - 즉 긍정적인 Label 을 가지는 Experiment 는 찾기 어렵지만 부정적인 Label ('사용자에게 나쁜 실험') 을 가진 사례는 많다는 것입니다.
  - 즉 이러한 실험을 기반으로 우리는 Metric 의 성능을 측정할 수 있습니다. (Control 이 상대적으로 더 좋은실험이 될 것입니다.)
- 아예 실험이 없다면, 웹 페이지 지연 (Latency 증가) , 안좋은 서비스로 Downgrade 와 같이 의도적으로 사용자의 경험을 저하시킬 수 있습니다.
  - 물론 이러한 의도적 실험에 대해서 반감을 가질 수 있습니다. 하지만 이러한 실험은 오로지 단기적으로 실험되고 그 이후에는 복구되므로, 사용자의 경험에 큰 영향을 끼치지 않습니다.
- 하지만 빙에서는 이러한 실험으로 얻은 지식이, 장기적으로 사용자의 단기적인 Experience 손실보다 더 큰 가치를 지닌다고 생각합니다.
  - 빙에서는 의도적으로 페이지의 result page 를 띄우는것을 250ms 지연시켰고, 장기적인 사용자의 experience 손실은 보지 못했다고 합니다. 
  - 또한 검색 관련성 저하 실험도 수행하였으나, 사용자 기반에 미치는 영향은 적었다고 합니다.
- 이러한 의도적 실험은 측정 기준의 방향을 검증하고, Metric 을 검증하고 목표를 정하는데에 큰 도움을 주었습니다. 

> ##  Lesson 4: Decompose metric sensitivity

- 어떠한 metric 이 goal metric 으로 사용될만큼 민감하지 않은게 있다고 합니다.
  - 하지만 우리는 이것을 포기하기 전에 이 '민감도' 에 대해서 잘 알 필요가 있습니다.
- 메트릭의 민감도는 두가지 구성요소로 구분됩니다. 

1. Statistical Power : Treatment 가 실제로 차이가 있다고 가정할때 metric 이 얼마나 잘 detect 하는가? 
2. Movement Probability : Treatment 를 적용할때에 metric 이 실제로 얼마나 잘 움직이는지? 

- 위 두가지 구성요소를 분리해 생각하면 , 매트릭의 민감도를 좀 더 자세하게 살펴볼 수 있습니다. 
- 예시로 유저당 세션 수는 일반적으로 Sensitivity 하지 않은 Metric 으로 보고되고 있습니다.
  - 하지만 이 이유는 통계적 Power 가 부족해서가 아닙니다. 
  - 인당 세션수의 변동 계수 (표준편차를 평균으로 나눈 값) 는 크지 않습니다. 그 말은 표준편차가 평균 대비 작다는 의미이고 이는, 변동성이 작다는 의미이며 , power 는 어느정도 크다고 생각할 수있습니다.
  - sensitivity 가 안좋은 경우는 일일당 유저의 검색수는 제한될 수밖에 없으며 그에 따라 사용자가 Treatment 에 대한 Change 에 잘 녹아들기 까지는 큰 시간이 걸리기 떄문입니다. 
  - 즉 Sensitivity 가 안좋은 이유는 Movement Probability 가 낮았기 떄문입니다.
- 즉 위와 같은 유저당 세션수 메트릭의 경우, Reduction variance 와 같은 Sensitivity 를 높히기 위한 방편을 써도 의미가 없을것이라는것을 예측 가능합니다.
  - 왜냐하면 '통계적으로 power 가 낮아서 그런것이 아니라, 이 메트릭(유저당 세션 수) 은 Treatment 에 대해서 잘 움직이기가 힘든 구조이기 떄문입니다.'
- 만일 문제가 통계적 Power 가 낮아서 문제였다면 Reduction variable 과 같은 방법론에 초점을 맞출 수 있습니다. 
  - skewness 가 큰 메트릭의 경우, power 가 낮아질 수 있기 떄문에 특정한 지점 이상은 평균으로 처리한다던가, binary metiric 으로 대체하는 등의 변환 방법이 가능할 것입니다.

> How to measure? 

- 이러한 민감도의 두가지 특성을 측정하기 위해서 우리는 몇가지 가정이 필요합니다.

![png](/assets/images/Stat/68_3.png)

- 위와 같이 가정을 합니다. 

![png](/assets/images/Stat/68_4.png)

- 그 뒤에는 위와 같이 Two Sample Z-Test 의 통계량을 정할 수 있습니다. 
  - 이는 , Online Experimental 환경이 Large sample 이기 때문에 가능합니다. 
- 그 뒤에 통계량이 Notation 을 살짝 바꾸어서, pooled variance 와 effect size 로 나타내면 위 (1) 과 같이 식이 바뀝니다.

![png](/assets/images/Stat/68_5.png)

- 위와 같이 $\sigma$ 를 Constanct 취급을 하게됨다면 $\mu $ 를 위와 같이 정의하게 된다면, 정규화를 시킨 꼴이므로 Scale 이 없는 Treatment effect 가 될 수 있습니다.

![png](/assets/images/Stat/68_6.png)

- $H_0$ 는Treatment effect 가 0이라는 가정을 합니다.  
- $H_1$ 에 대해서는 일반적인 Power analysis 에서는 특정한 값을 가지는것을 가정하고 이루어지지만 , 여기에서는 $\mu$ 가 특정한 distribution g 를 따른다고 가정합니다. 

![png](/assets/images/Stat/68_7.png)

- 위와 같이 Treatment 가 실제로 효과가 있었고($P(H_1)$), 이를 탐지할 능력은 $P(H_1)\cdot P(\mid Z\mid > 1.96 \mid H_1) $ 로 정의됩니다.

![png](/assets/images/Stat/68_8.png)

- 결국에 Statistical Power 를 계산하기 위해서는 $H_1$ 하에서 $\delta$ 의 분포를 알아내야만 합니다. 
  - effect size 가 $\delta = \Delta/\sigma$ 으로 정의되었음을 기억합시다. 
  - 일반적인 Power analysis 에서는 이러한 차이에 대해서 Constant 값을 가정하고 시작합니다만 이 paper 에서는 Random Variable 취급을 하게됩니다.
  - 즉, 'Control 과 Treatment 의 차이' 를 R.V 으로 바라본다는 이야기입니다. (마치 베이즈같네요.) 
- 이러한 $\delta$ 의 분포를 이끌어내기 위해서 $H_1$  하에서 $\mu \sim N(0,V^2)$   라고 정의하게 됩니다.
  - $\mu$ 가 앞에서 $(\tau_T - \tau_C) /\sigma $ 으로 정의되었음을 기억합시다. 
  - 이러한 $V$ 파라미터가 크다면 , Control 과 Treatment 간의 차이가 크게 변동한다는것을 의미합니다. 즉 Movement 를 더 detect 하기 쉬울것입니다. 
- 위와 같이 정의를 하게된다면 $\delta \sim N(0,(1/N_E + V^2))$ 이 됩니다. (이에 대한 자세한 계산 과정은 별도 논문을 참조하세요)
  - <https://alexdeng.github.io/public/files/BayesianAB.pdf>
- 그에 따서, 위와 같이 Sensitivity 는 (4)번 식과 같이 계산되어 질 수 있습니다.

![png](/assets/images/Stat/68_9.png)

- (4) 식을 참고하면 어떠한 effective sample size 에 대해서도 , V 가 크다면 위의 확률이 커짐을 알 수 있습니다. 
- 전통적인 방법에서는 가정된 effect size 에 대한 sample size 가 궁금했지만 이 방법에서는 sample size 가 필요 없습니다.
  - 대신에 우리는 어떠한 given gample size 에 대해, 기대되는 statistical power 가 궁금한 거입니다. 

![png](/assets/images/Stat/68_10.png)

- 위와 같은 추정을 하기 위해서는 결국 $P(H_1) $ 과 $V$ 를 추정해야 합니다.
  - 이를 추정하기 위해서는 우리는 Validation corpus 방법을 사용해야 합니다. 
- 하지만 이러한 corpus 는 전문가의 labeling 이 되어야하기 때문에 매우 어려운 방법입니다. 
  - 우리는 대신에 unlabeled historical data 를 이용한 방법을 쓸 수 있습니다. 
    - <https://alexdeng.github.io/public/files/BayesianAB.pdf> 를 참조해주세요
- 이렇게 V 와 $P(H_1)$ 을 추정하고 나면 우리는 두개의 metric 을 비교할 수 있게 됩니다. 

![png](/assets/images/Stat/68_11.png)

- 위의 표는 Sensitivity 를 분해한 결과를 나타냅니다. 위의 결과를 통해 우리는 몇가지를 말할 수 있습니다.
  - metric A 에 대해서 whole page 를 보는거보다 subpages 를 보는게 더 효과가 있습니다
    - subregion 을 볼때에가 $P(H_1)$ 도 높은걸로 봐서 '실제로 움직이는 비율' 이 높으며 또한 $V^2/(1/N_E)$ 을 볼때에도 Statistical power 도 더 높습니다.
    - 이 둘을 종합한 P(Detect the Movement) 의 비율 또한 subregion 이 좋습니다. 
  - metric B 를 보면 weight 를 세부조절한것이 , Sensitivity 에 도움을 줍니다.
  - metric C 를 보면 Variance Reduction 방법은 $\sigma^2$ 을 크게 낮춥니다. 즉 $V$ 를 증가시키게 됩니다. 
    - VR(Variance Reduction) 방법을 하면 실제 metric 이 움직이는 비율(P(True movement)) 는 당연히 거의 그대로이지만 , Statistical Power 를 높여 P(Detect True movement) 를 높히게 됩니다. 
  - metric D 의 경우는 skewed metric 에서 capping을 통해 sensitivity 를 높힌 경우입니다.
    - 이러한 경우를 볼 떄에 capping 은 통계적 Sensitivity 를 크게 높힌것을 볼 수 있습니다.

> Unlabeled Corpus methods

- 이떄에 나이브하지만 Sensitivity 를 잴 수 있는 방법을 소개하고자 합니다. 
  - 그 방법은 바로 Unlabeled history data 를 이용한 방법입니다. 
  - 이 방법론은 (3) 에서 제시한 $P(H_1) \cdot P(\mid Z \mid>1.96\mid H_1)$ 과 같은 정교한 방법론을 사용할수는 없습니다.
- Metric 이 움직이지 않았다고 가정합시다. 그렇다면 $P(H_1) = 0$ 이 됩니다. 
  - 그렇다면 Type 1 error 때문에 이러한 naive approach 는 5% 의 에러를 가지게 됩니다. 
    - 즉 naive approach 는 $P(H_0) \cdot 5\% \le 5\%$ 의 에러를 가지게 됩니다. 
    - '효과가 없을때에' 효과가 있다고 말할 에러는 5% 로 bounded 된다는 의미입니다. 
  - 그럼에도 이러한 biased 는 5%로 bounded 되어있기 떄문에 빠르게 Sensitivity 를 비교할 수 있는 수단이 됩니다. 
    - 즉 , 실험의 결과만을 가지고도 우리는 어느정도 Sensitivity 를 비교할 수 잇다는 의미입니다.
- 즉 Metric A 를 이용하였을때 Sensitivity score 가 B 보다 5% 이상 차이가 난다면 우리는 A 가 B 보다 더 Sensitive 하다고 할 수 있을것입니다. 
  - 이러한 방법은 A,B 에 대한 Metric 의 estimation error 를 배재하고 고려한 방법론입니다. 
  - 이러한 estimation error 는 data set 이 크면 작아지므로 , unlabel 방법론은 sample 이 클때에 적절한 방법론임을 알 수 있습니다. 
    - 다시말하면, unlabed 방법론은 애초에 실험 결과만을 이용해 Sensitivity 를 측정하는 방법론이고 , 이를 위해서는 실험이 정확해야 하므로 Large sample 을 요구한다고도 볼 수 있습니다.

> ## Lesson 5: Learn from offline data

- 이전에 언급했듯이 시스템이 안정됨에 따라 사용자 행동성 메트릭이 중요해지고 있습니다. 
  - 이러한 사용자 행동 중심의 메트릭은 유저가 시스템에 대해서 좌절 ,만족등을 예측하고 측정할 수 있는 모델에 기반합니다. 
- 즉 잘 설계된 user behavior 메트릭은 사용자 경험과 매우 밀접하므로 높은 Sensitivity 를 보장하며 우리의 목표와 일맥상통하게 됩니다.
- 하지만 사용자들은 온라인 플랫폼을 이용할때에 직접적인 피드백을 제공하지 않습니다. 
  - 그러므로 어떠한 유저의 로그 신호가 , 직접적으로 만족과 연결되는지 알기가 힘들것입니다. 
- 그러므로 우리는 오프라인 라벨링 데이터를 이용하여 사용자의 행동 신호(활동 로그) 를 이용하는 방법을 제안합니다.

> User behavior driven metric 개발단계

1. Step1 : 관찰을 통하여 User experience 에 대한 몇가지 가정을 세웁니다. 
2. Step 2 : User study Experiment 를 디자인하고, Labeled 된 dataset 을 모읍니다. 
   - Step 1 에서 세운 모델을 labeled 된 dataset 에 대하여 실험해봅니다. 
3. Step 3 : Step 2 에서 실험한 결과에 대해서 ONline Metric 을 만들어봅니다. 
   - Labeld Corpus 에 기반하여 우리가 만족할만한 수준까지 도달하도록 MEtric 을 설계합니다. 

- 위와 같은 개발단계에서 유의해야할 것들이 있습니다.

> 1단계에서 시작하는 가설은 사용자의 주요한 '집단 행동 패턴'을 포착해야 합니다. 

- 집단 행동 패턴이란 '대부분의 사용자로부터 관찰될 수 있는 행동 패턴을 의미합니다.'
- 즉 '소수' 에 집중하는것이 아니라 대부분, 일반적인 행동 패턴에 주의를 기울여야한다는 의미입니다.

> 라벨이 붙은 Offline 데이터를 수집하고 Step 2 에서 모델을 학습할때 라벨 데이터에 대해 주의할점이 있습니다.

- 가능하다면 라벨이 붙은 데이터를 여러 다른 방법으로 수집해야합니다.
  - 이는 데이터를 수집할때에는 필연적으로 편향되어 수집되기 떄문입니다.
- 라벨을 붙인 데이터를 수집하기 위해서는 두가지 방법이가능합니다.
  - 하나는 lab study 로서 사용자로부터 설문조사를 하는 방법입니다.
    - 이 방법은 사용자가 스스로 Experiment 에 대한 label 을 형성해주기떄문에 정확합니다
    - 하지만 가격이 비싼 단점이 있습니다.
  - 또 다른 방법은 제 3자가 로그 데이터에 대해 정보를 모아서 라벨을 붙이는 방법입니다. 
    - 그러나 이 방법론은 제 3자에게 실제 접근권을 준다는것은, 데이터 Security 입장에서 매우 민감한 셜정입니다.
    - 그리고 정확하지가 않다는 단점이 있습니다.
  - Bing 에서는 위 두가지 방법을 결합한 방법을 수행한다고 합니다. 

> 모델을 블랙박스 모델로 만들면 안됩니다.

- 이전에 우리는 OEC 에 대해 디버깅 메트릭을 정의하는것이 중요하다고 하였습니다.
- 이러한 디버깅 가능한 메트릭을 얻기 위해서는 메트릭이 추적 가능하고, 분해가 쉬워야 합니다.

![png](/assets/images/Stat/68_12.png)

- 예를 들어서 위와 같이 OEC 를 사용자당 성공 쿼리를 설정하는 경우에, 위와 같이 
  - 사용자당 쿼리 
  - 사용자당 재구성 쿼리 (검색어를 다시 고쳐서 검색하는것)
  - 사용자당 Longdwell time Click (오랜 시간이 지난 후 클릭하는것)
  - 를 디버깅 메트릭으로 사용하여  OEC 메트릭에 대해 이해할 수 있습니다.

> 모델에 대한 Feature 를 선택할때에는 외부 기능만 사용 가능한지 고려하세요

- 외부 기능은 사용자의 클릭 동작 , 검색 패턴 처럼 사용자 측면에서의 동작입니다.
- 그에 반해서 내생적 기능은 웹 페이지에 표시되는 정보와 같이 서비스 측면에서의 동작입니다.
- 이러한 내생적 특성이 metric 에 포함되는 경우 Optimization 팀은 이러한 메트릭에 개입할 수 있게 됩니다. 
  - 의도적이든 , 의도적이지 않든 메트릭은 공정성으로서의 품질을 잃게 됩니다. 

> ## Lesson 6: Choose the right rate metrics

- Rate metric 은 정의에 분자와 분모 두개가 같이 있는 메트릭입니다. (이때에 분모는 사용자 수가 아닙니다.)
  - 분모가 사용자 수가 된다면 여기에서 논의되는것은 유효하지 않습니다. 왜냐하면 단순히 Randomized unit 으로 나눈것에 불과하기 떄문입니다. 
  - 쿼리당 성공 쿼리 수, 클릭 속도 등이 있습니다.
- 이러한 Rate 메트릭은 널리 사용되며 OEC 의 좋은 후보주에 하나입니다.
- 이러한 속도 메트릭은 치우침이 적고, Upper / lower bound 를 지니기 떄문에 상대적으로 Sensitivity 가 더 좋기 때문입니다. 
- 하지만 이런 rate metric 을 설정할때에 주의해야할 기준이 있습니다.

> rate metric 이 증가하는 경우 많은 경우의 수가 있다.

- Rate metric 이 증가한다고 합시다. 그렇다면 몇가지 경우의 수가 있습니다.
  - (a) 분자증가, 분모는 그대로
  - (b) 분자증가, 분모 감소
  - (c) 분자증가, 분모 증가
  - (d) 분자그대로 분모 감소
  - (e) 분자감소 분모 감소 
- 처음 경우 (분자 증가, 분모 그대로) 를 제외하고는 다른 경우가 좋다고 말하기는 애매합니다. 
- 이러한 예시를 들어봅시다. 분모는 총 춰리의 수, 분자는 성공 쿼리 수라고 합시다. 
  - 사례 (a) 의 경우 사용자의 총 쿼리수는 그대로 유지되는 상태에서 성공 쿼리가 늘어나므로 좋은 징조라할 수 있습니다.
  - 그러나 분모가 안정적이지 않은 경우에는 b~e 까지의 시나리오가 긍정 / 부정을 결정하는것은 매우 어렵습니다. 
- 그러므로 Rate metric 을 다룰때에는 다음과 같은 2가지의 규칙을 지켜야합니다. 

1.We should always keep the denominator and the numerator as debugging metrics (discussed in Section 3.2) for a rate metric;<br>
2.When we choose a rate metric to be a goal metric, we should choose the one whose denominator is relatively more stable in most cases.
{: .notice}

1. 즉 분모는 유지한채로 분자는 debugging metric 작용을 하게 따로 빼 놓아야 합니다. 
2. 그리고 rate metric 을 goal metric 으로 정의할때에는 denominator 가 최대한 안정적인 경우로 설정합니다.

- 예로 만약 Goal mtric 을 쿼리당 성공쿼리수(QSR) , 세션당 성공세션수(SSR) 두가지에 대해서 살펴봅시다. 
  - 이러한 경우 bing 은 이전에 살펴본것처럼 metric 의 direction , sensitivity 에 대해서 살펴보았고 또한 분모의 안정성에 대해서 살펴보았습니다. 
  - 이 결과 SSR 의 분모 (유저당 세션수) 가 유저당 쿼리수 보다 훨씬 안정적이였습니다. 
  - 실제로 QSR 에서 통계적으로 유의한 10% 의 경우는, 분모가 함께 움직인 경우였습니다. 
    - 즉 이러한 QSR 에서는 metric 의 해석이 어려울수밖에 없습니다. 
  - QSR 이 좀 더 Sensitive 하였지만 SSR 이 이러한 안정성 덕분에 채택되었습니다.
    - 대신 이러한 QSR 은 버리지 않고 debuggin metric 으로 활용하였습니다.

> rate metric 을 계산하는 방식은 두가지가 있다. 

- Rate metric 을 계산하는 방식은 두가지가 있습니다.
  - Average of ratio	
  - Ratio of Average
- 예시로 Click Through rate (CTR) 은 아래와 같이 2가지로 정의가 될 수 있습니다.
  - 유저당 평균 CTR (즉 Average of ratio)
  - 유저의 모든 클릭 수 / 모든 유저 수  (ratio of Average)
- 두개의 definition 모두 실제에서 자주 쓰입니다. 
  - 하지만 어떤 경우에서는 위 두가지 경우를 혼용하면서 쓰는 경우도 있었습니다.
  - 그러므로 이러한 정의를 제대로 알아두어야 할 것입니다.
- 각각의 정의는 사용자에 대한 가중치가 다릅니다.
  - Average of ratio (비율의 평균) 은 각 사용자는 단일 비율값을 가지기 떄문에 최종 메트릭에 대한 가중치가 동일합니다.
    - 각 유저당 세션당 성공 세션의 비율이 0.2 , 0.9 , 0.1 이라 합시다. 이 경우 비율의 평균은 0.4 입니다. (동일 가중치)
  - Ratio of Average (평균비율) 은 각 사용자가 가지는 값에 대해서 가중치가 상이합니다.
    - 각 유저당 세션,성공세션의 수가 (10,2) , (100,90) , (10,1) 이라 합시다. 이 경우 평균의 비율은 93/120 입니다. 즉 각 유저의 영향력이 Weighted mean 으로 들어가게 됩니다. 
- 우리의 경험에 따르면 두가지의 Ratio 메트릭은 대부분 실험에서 동일한 방향으로 움직입니다. 
  - 그렇지 않을 경우, 많은 log 를 일으키는 유저가 어떠한 왜곡을 발생시킨것이라는데 이러한 경우 추가 조사가 필요할 것입니다.
  - 일반적으로 비율의 평균이 평균비율 보다  Treatment 가 모든 사용자에게 동일할 경우 더 민감한 경향이 있습니다. 
    - 그 이유는 평균비율은 많은 log 를 가지는 사용자에 대해서 큰 영향을 받기 떄문입니다. 그래서 이러한 영향이 큰 유저가 어디에 속하는지가 매우 중요해지게 됩니다. 
      - 이는 Effective Sample size 가 곧 heavy user 의 수와 비슷하다는 의미가 됩니다. (이러한 유저의 영향을 크게 받으므로)
      - 그러므로 Statiticaly 유효한 heavy user 의 수를 확보하기 위하여 매우 큰 Sample size 를 요구하게 됩니다.
    - 그에 비해 비율의 평균은 모든 사용자에게 동등한 가중치를 주게 됩니다. 그 의미는 Effective sample size 는 모든 유저가 되고 , 평균비율을 계산할때보다 훨씬 적은 샘플이 필요하게 됩니다. 
- 또한 계산시에도 조심해야 합니다.
  - 평균비율 에 대한 분산은 유저가 무작위 단위로 사용되는 경우, Delta 방법을 이용해야 합니다.
    - 이는 Randomized unit 과 분모가 다를 경우에 해당되는 이야기입니다.
  - 그에 반해 비율의 평균일 경우에는 '유저의비율' 에 대한 평균이기 떄문에 분산을 계산할때 일반적으로 수행하면 됩니다.

> ##  Lesson 7: Use combo metrics as surrogate for OEC

- 위에서 설명한 많은 방법론들에도 불구하고, 좋은 goal metric 을 찾는것은 여전히 어려운 일일 수 있습니다. 
- 우리의 목표에 맞는 단일 OEC 를 찾기가 힘든 경우 한가지 방법은 바로 성공적이였던 metric 들의 set 을 사용하는 방법입니다.
  - 이러한 메트릭들을 모두 살펴봄으로서 실험 결과에대해 나은 평가를 할 수 있습니다.
- 이러한 전략이 성공하기 위해서는 모든 성공 측정 기준을 포괄적으로 이해해야 합니다.
  - 각 메트릭에 대해 의도된 방향 해석과 보다 중요한 시나리오를 알아야 합니다.
  - 또한 메트릭이 명확한 방향을 제시하지 못해 의사 결정 과정에서 폐기되거나 다른 메트릭으로 대체될 수 있어야합니다.
- 개별 측정 기준 집합은 알려진 모든 시나리오를 포함해야 한다
  - 하나의 메트릭이 명확한 방향을 제공하지 못할 경우 공백을 메울 수 있는 다른 메트릭이 하나 이상 있어야 합니다. 
- 마지막으로 가장 애매한 상황은 두 메트릭이 서로 다른 방향을 나타내는 경우이다. 
  - 즉, 하나는 사용자 경험이 개선되고 다른 하나는 저하를 암시한다. 
  - 이러한 경우 신호 강도와 신호 값이라는 두 가지를 신중하게 교환하기 위해 전문가의 의견이 종종 필요합니다.

> How to? 

- 위에서 설명한것을 수행하기 위해서 콤보 메트릭이 설계되어씁니다.
- 이 메트릭은 성공 기준 메트릭들로 구성된 파생 메트릭입니다.
- set of metric $X_i, i = 1,2,...$ 에 대하여 Combo metric 은 다음과 같은 Form 을 지닙니다.

$$f(\Delta \%(X_i) , ... ,\Delta\%(X_k))$$

- $\Delta\%(X_i)$ 는 $X_i$ 의 퍼센티지 변화도를 나타내며 $(X_i^T - X_i^C)/X_i^C \cdot 100\%$ 를 나타냅니다. 
  - $X_i^T$ 와 $X_i^C$ 는 각각 Treatment 와 Control 의 $X_i$ 메트릭에 대한 값입니다. 
- 이때에 우리는 f 를 정의해야 합니다. 
  - 이러한 f 를 정의할떄에 미분 가능하고 1차 미분값이 continuous 한것을 추천드립니다.
- 왜냐하면 콤보 매트릭에 대해서 통계적 테스트를 수행해야하는데, 연속성이 있어야 쉽게 테스트가 가능하기 떄문입니다.
  - 미분가능하지 않으면 메트릭 분석을 용이하게 하는 Assymptotic normal distribution 이 없을 수 있습니다. 
  -  f is differentiable with continuous partial derivatives. 일떄에 Assymptotic normality 가 존재합니다.
    - 자세한 증명 과정은 생략하겠습니다. 
- 가장 Simplest way 는 combo metric 을 linear combination 으로 정의하는것입니다.

$$\sum w_i \Delta \% (X_i)$$ 

- $w_i$ 는 각 메트릭에 대한 weight 가 됩니다. 
  - vaildation corpus 가 가능하다면 위 메트릭에 대한 sensitivity 와 direction 을 테스트 할 수 있습니다. 
  - 그러므로 다양한 weight 를 비요하면서 가장 좋은 performance 를 가지는 metric 을 선택할 수 있을것입니다. 
  - validation corpus 가 불가능할때에는 degradation experimant 를 통해서 분석할수도 있을것입니다. 

# [Conclusion](#link){: .btn .btn--primary}{: .align-center}

- 이 논문에서 우리는 수년간 배운 교훈들을 보여줌으로서 메트릭을 설계하는 그 과정 또한 데이터 중심이 될 수 있다고 제시하였습니다. 
- Goal Metric(OEC) 이 만족해야할 방향성과 민감성을 제시하고 이러한 품질을 체계적으로 측정하기 위한 방법들을 제시하였습니다. 
- 또한 통계 기법들을 활용하여 가장 적절한 Metric 을 선택하는 방법도 보여주었습니다. 
- 이러한 방법론을 통해서 다양한 Online Service 에서 online metric 을 성공적으로 사용하는데에 도움이 되었으면 합니다. 

---

**Reference**

- <https://www.kdd.org/kdd2016/papers/files/adf0853-dengA.pdf>

토요일 내내 봤던 논문이네요.. 중간에 베이즈 얘기가 나오는 부분에서 시간을 많이 뻇기고(이 내용은 아직 완전하게 이해를 못했네요.. ), 또 bing 에서 나온 논문이라 그런지 seach 환경에 대한 용어가 자꾸 나와서(쿼리,.... 등) 이해하는데에 시간이 오래걸렸네요... 그래도 읽어보았을때에 얻는게 많았던 논문이라 재밌었습니다! 
{: .notice--success}

