---
title: "Online Experimentation Diagnosis and Troubleshooting Beyond AA Validation"
excerpt: "실험의 Truthworthy 를 위한 다양한방법"
categories:
  - AB_Paper
last_modified_at: 2022-01-13

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 Metric 을 분석할때 Randomization Unit 과 Analysis Unit 이 다를때에는 어떻게 해야 될까
{: .notice--warning}

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## Abstract 

> Online Experiemnt 의 문제점

- Online Experiment 는 현재 다양한 온라인 회사에서 이용되는 다양한 방법입니다.
  - 게다가 Online Experiment 에 대한 설계는 이론적으로는 매우 간단합니다.

- 그러면 이떄 Oneline Experiment 은 무적일까? 
  - 하지만 실제로 적용해볼떄에는, 결과의 해석을 복잡하게 하고 ,User Experience 에 대한 Conclusion 을 무의미하게 만드는 다양한 문제가 존재합니다. 
  - 이러한 문제들 중 대다수는 발견하기 어렵습니다. 


> 해결책?

- 우리가 먼저 이러한 문제를 인식하고 사전에 진단할 수 있다면, 실험자가 근본적으로 결함이 있는 데이터를 기반으로 Decision 을 내리는 것을 방지할 수 있을것입니다! 
- 온라인 실험을 수행할 때에 제일 먼저 보장되어야 할 것은 데이터 품질 보장입니다.
  - Treatment 를 도입하기 전에 AA a검사를 통해 일부 문제를 발견할 수 있지만, AA 기간에는 많은 문제가 발생하지 않고 AB 기간에만 나타나는 문제가 있습니다.
  - 다른 연구에서는 AB 기간 동안의 문제 해결에 대해 다루지 않았었습니다.
- 이 논문에서 우리는 야후의 다양한 인터넷 소비자 제품에 대한 실험에서 얻은 교훈과 Diagnotic ,절차 , 그리고 문제가 발견되었을떄에 치료 절차에 대해서 알아보겠습니다. 
- 여기에 제시된 대부분의 트러블슈팅 절차는 다른 회사의 문제와도 일치합니다. 예를 들면 트래픽 분할문제, 이상치 문제와 같은 경우는 다른 연구에서도 활발히 논의되었스빈다
  - 하지만 다른것들은 이전의 문헌들에서 기술되지 않았습니다.

> ## Introduction

- AB Test 라고 알려져있는 Online Controlled Experiments 는 Control(A)과 그 변형 버전인 Treatment(B) 에 대한 Randomization Experiment 를 일컫습니다.
- 이때 A 가 더 좋은지 B 가 더 좋은지를 결정하기 위해 실험완료 (또는 실험 도중) 에 다양한 행동 및 성능 메트릭을 분석하게 됩니다.
  - AB 테스트는 구글, 페이스북, 링크드인, 마이크로소프트, 야후, 아마존, 이베이, 넷플릭스, 징가, 우버, 에어비앤비, 핀터레스트 및 기타 많은 인터넷 기업에서 제품 향상과 개발에 널리 사용되고 있습니다.
- 하지만 이떄 변경사항 ( Treatment ) 가 사용자의 경험에 예기치 않게 안좋은 영향을 미칠 수 있으므로, 안전하게 실험을 하기 전에는 변경사항이 User 에게 영향을 끼치는지 아닌지와 관계 없이 Production 을 한번 테스트 해야합니다. 
  - ex : 네이버에서 웹툰의 UI 를 개편했다고 합시다. 이론적으로는 웹툰 개편은 네이버 메인에 노출되지 않으므로, 네이버 메인에 진입되는 유저에 대해서는 아무 영향이 없어야 할 것이지만, 이러한 개편이 코드상의 어떤 영향으로 메인의 Latency 를 변화시킬수도 있으므로 꼭 확인해 봐야 할 것입니다.
- 일반적으로 AB Test 의 주제로는 다음과 같은 예시가 있습니다.
  - Front - end 의 유저 인터페이스 개선 
  - Recommendation System 에 대한 백앤드 개선
  - 온라인 광고....
- 이러힌 Controlled Experiments 의 핵심 목표는 Treatment 와 측정가능한 유저의 행동 사이의 인과관계를 밝혀내는 것입니다.
- 이 인과 관계는 교란 요인이 무작위화에 의해 잘 제어되고 테스트와 대조군 그룹 사이에서 균형을 이룬다는 전제하에 성립하게 됩니다.
- 이러한 사용자 행동의 변화 외에도 온라인 환경에서 시험과 통제 사이의 관찰된 차이점에 기여할 수 있는 많은 교란 요인이 있다. 관찰된 효과가 교란 요인 중 하나가 아닌 사용자의 행동 차이로 인한 것임을 보장하기 위해 데이터 품질 보증 절차를 따라야 한다.

> A/A Testing

- Null 테스트라고도 알려진 AA 테스트는 Online Controlled Experiment 에서 동일한. identical variants 인 A 와 A 끼리 비교하여서  AB 시험이 시작되기 전에 Control과 Variants군 사이에 존재하는 차이를 없애기 위해서 실행하게 됩니다.
  - ex : AA 실험을 해 보았는데, 예상 외로 차이가 크게 나게 되면, 버킷에 대해서 Random 할당이 잘못되었다는것을 나타낼 것입니다.
- 이떄 많은 기업들이 AA 테스트를 자주 수행하거나, 또는 적극적으로 추천하고 있습니다. 
- AA 테스트 절차를 실험하게 된다면 아래와 같은 절차를 따르게 됩니다. 
  - AA 테스트에서 테스트 그룹과 대조군 그룹 사이에 유의미한 차이가 나타나지 않는 경우 Treatment 를 적용할 수 있습니다.  
- 또는 A/A 테스트의 대안으로서, retroactive AA Test 를 수행하여서 
- 대안으로, 소급 AA 시험을 수행하여 테스트와 제어 사이의 차이를 확립하거나 트래픽이 재랜덤화(재순열)된 후에 모든 실험을 시작할 수 있다. 

> A/A Test 가 만능일까? 

- AA 검사를 통하여 우리는 실험시작 전에 Control Population 과 Treatment Population 이 적절하게 balanced 되어 있는지를 알아볼 수 있습니다.
  - ex : AA 테스트를 해 보았더니 mac 유저와 window 유저가 균일하게 배분되어있지 않았다고 합시다. 그러면 현재 우리가 진행한 Randomization 이 올바르지 않았다는것을 의미합니다. 이럴떄는 Randomization 을 다시 수행할 수 있습니다.
  - ex : AA 테스트를 해 보았더니, 인당 구매금액 차이가 크게 난다고 합시다. 그러면 Randomization 이 잘못되어 한쪽 버킷에 큰손이 몰려있음을 의미합니다. 이럴떄에도 Randomization 을 다시 수행하는게 좋습니다. 
- 하지만 위처럼 A/A 테스트는 도움을 주긴 하지만 일부 불균형이 AB 테스트 기간동안에 발생하는 경우, 즉 불균형을 초래할수도 있는 Confounding Factor 를 피하는데에는 별 도움을 주지 못합니다.
- 따라서 AA 테스트를 수행하는 기간을 넘어서, 실험에 사용하는 Experiment data 에 대해서 데이터의 품질을 점검하고, Control 과 Variant 간 균형에 대한 상세한 검정이 필요합니다. 
- 이 논문의 매우 특징중 하나는 "AB 기간 동안 검증 테스트를 추가하기 위해 구현한 절차"에 대한 설명입니다. 이런 특별한 주제는 이전 논문에서 자세히 논의되지 않았습니다.

> root cause of experiment imbalance 

- 이러한 imbalanced 를 일으키는 근본 원인을 찾기 위해서는 experimental platform 의 근본 작동 방식을 살펴보고, engineering code base 레벨 수준에서 살펴보는 작업이 필요합니다.
  - 증상을 세심히 살펴보고, 어떤 부분이 imbalane 의 원인이 되는지 살펴보고 고치는 작업은 매우 중요합니다. 

- 이전 논문은 온라인 실험의 설계 및 분석에서 얻은 중요한 교훈을 문서화하였다 [27], [29], [31]. 관련 분야에서는 고객 정서 조사를 위한 실질적인 어려움과 해결책도 논의되었다[40]. 이 논문의 한 가지 특징은 실험 품질 검증 테스트, 증상, 근본 원인 및 치료법을 연결하는 실제 데이터의 예를 제공하는 것이다. 이러한 교훈을 통해 실무자는 검증 테스트를 활용하여 실험 품질을 평가할 뿐만 아니라 동인이 무엇이고 실제로 문제를 해결하는 방법을 이해할 수 있다.
- 우리는 야후의 온라인 실험에 대해서 몇가지 challenge 에 직면했습니다. 
  - Yahoo’s infrastructure 는 원래 Experiment 를 염두하고 설계된것이 아닙니다. 그래서 실험은 대부분 기존의 ecosystem 을 어느정도 개조하여서 실험한 것입니다.
  - 야후는 다양한 사이트들을 보유하고 있으며, 다양한 device type 에 대해서 다른 version 의 view 를 보여주고 있습니다.
  - user experience 를 개선하기 위해서 급진적인 구조 개선이 자주 이루어집니다.

- 이러한 분산된 구조때문에 setting up experimental infrastructure 의 책임은 다양한 부서로 분산됩니다. 
- 물론 중앙 집중식 실험플랫폼을 이용하여서 트래픽 분할(샘플링) 알고리즘과 실험 관리 및 보고 시스템을 공유합니다.
  - 하지만 product team 별로 experimentation code 나, meta information 등은 다르게 가져갈 수 밖에 없기 때문에, 중앙 관리가 다소 힘든점이 있습니다.

- 즉 일일히 product team 마다 찾아가서 문제점을 진단해줄 수 없기떄문에 일반적인 diagnotic solution 의 필요성이 대두되었습니다.

> ## Paper 에서 다루는것 개요

> Paper 에서 다루는것

- 본 논문은 AB 기간 동안의 불균형 검출 및 이에 대한 remedy 에 대한 우리의 접근방식을 제시합니다.
- 섹션 II
  - AB 기간 동안 실험이 균형을 이루는지 여부를 검증하기 위해 통계 테스트를 도입합니다. 
  - AB 기간 동안 편향되지 않은 선택과 샘플 균형의 검증은 어렵지만 이전 문헌에서는 거의 논의되지 않았었습니다. 
  - 도입된 테스트는 이론적으로는 간단하지만 매우 실용적입니다. 
  - 이 테스트는  이후 섹션에서 다양한 문제로 인한 불균형을 감지하고 진단하기 위해서 사용됩니다.
- 섹션 III 
  - 불균형 원인과 해결책은 대게 아래와 같은 세가지 범주로 논의됩니다
    - 트래픽 분할 및 테스트 ID 스탬프
    - instrumentation 및 logging 
    - 이상치 제거 
  - 이러한 주제 중 일부는 개념적 차원에서 여러 논문에서 논의되었다
  - 본 논문은 무엇이 일어날 수 있는지, 무엇을 관찰할 것인지, 어떻게 감지하고 진단할 수 있는지, 그리고 치료법이 무엇인지 보여주는 구체적인 예를 제시함으로써 논의를 진전시켰습니다. 
- 섹션 VI
  - 실험 진단 및 trouble shooting 에대한 추가 주제에 대해 논의한다.

> Traffic Split 에 대한 문제

- Traffic Split 을 진행할때에, 적절하지 않은 해싱 함수를 사용해서 발생하는 문제는 [30] (아래 reference)에 설명되었지만 트래픽 분할 구현에 관한 문제는 언급되지 않았었습니다.
- 이 주제에 대한 많은 Reference 들에도 불구하고,  실험이 수년 동안 존재해 온 야후에서도 트래픽 분할과 관련된 여러 가지 문제들이 몇 년 전까지만 해도 관찰되어 왔습니다. 
- 우리는 이러한 상황이 특별하지 않으며, 많은 기업들이 이러한 문제가 존재한다는 것을 인지하지 못한 채 이러한 문제를 계속 겪고 있다고 생각하고 있습니다.

> logging 과 instrumentation 

- 계측 및 로깅과 관련된 문제는 kohavi[30]와 tang[44]에서 언급되긴 했지만, 우리가 마주친 문제는 일반적이지만 이전에는 문헌에 기술되지 않았었습니다.

> Outlier

- 마지막으로, 데이터 분석에서 특이치의 잠재적 위험은 잘 알려져 있지만, 이상치가 AB 테스트 결과에 미치는 영향은 이전에는 자세히 논의되지 않았습니다.

# [2.EXPERIMENT BALANCE VALIDATION IN AB PERIOD](#link){: .btn .btn--primary}{: .align-center}

> ## Intro

- AB Test 를 시작하기 전에, AA Test 를 실행하여서, sample size ratio between test and control 이 우리가 원하는대로 (50:50) 잘 분배되었는지를 테스트 할 수 있습니다.
- control 그룹과 test 그룹간 key metrics 차이가 있었는지를 확인해 볼 수 있습니다.
- 이러한 AA Testing 에 대한 중요성은 다양한 reference(  [9], [31], [32], [30], [38], [44]. ) 에서 언급되어 왔습니다.
- 이떄 추가적인 기법으로 AB 테스트의 Sensitivity 를 높히기 위하여 A/A Test 기간동안의 데이터를 이용하는것도 검토해볼 수 있습니다.
- 그러나 AA-Validation 이 유저 그룹간이 균형잡혀있다고 말할지라도, AB 기간동안에 imbalance 가 발생할 수 있습니다.
  - 이는 경험상 거의 절반이나 되는 실험에서 발생했었습니다. 

- 사실, 우리는 특정 교란 요인과 데이터 문제가 AB 기간 동안에만 발생할 가능성이 높다는 것을 발견했습니다. 
- 여기에서는 AA 테스트가 통과되었다고 가정하여 AB 기간에, 사용자간 균형을 이루기 위해서 어떻게 할 것인지에 대해서 논의하고자 합니다.

> ## 메트릭의 균형

- AB Test 기간동안의 Metric balance 는 AA 기간동안에서보다 평가하기 어렵습니다.
- 왜냐하면 metric 의 차이는 Treatment 로 인해서 일어나는 차이와 Congounding Factor 로 일어나는 차이가 혼재되어 있기 때문입니다.

![jpg](/assets/images/Stat/156_2.jpg)

- 즉 confounding factor 의 영향을 제대로 측정하기 위해서는 treatment 의 영향을 받지 않는 validation metric 을 설정하는것이 필요할 것입니다. 
  - 또한 추가적으로 control 과 test 에 대해서 systematic bias 의 영향을 크게 받는 metric 을 설정하는것이 좋습니다.

![jpg](/assets/images/Stat/156_3.jpg)



- 즉 정리하면 따라서 치료 효과에 의해 영향을 받을 것으로 예상되지 않지만 테스트와 대조군 사이에 체계적인 편향을 일으킬 수 있는 문제에 민감한 검증 지표가 필요하게 됩니다. 
- 이러한 측정 기준 중 하나는 AB 기간 동안의 누적 표본 크기이입니다. 누적 표본 크기는 Treatment 효과와 독립적이며 Control 과 Treatment 사이에 대해서 균형이 1:1 가 될 것으로 예상됩니다. 

![jpg](/assets/images/Stat/156_4.jpg)

- 다음과 같은 2가지 이윯 누적 AB 표본 Sample Size 는 1:1 일 것입니다.
  - 트래픽 분할 패키지가 사용자를 구성된 비율에 따라 실험 그룹으로 무작위로 분할합니다.
  - 사용자가 "첫 방문" 하기 전까지는 Treatment 와 control 에 대한 정보가 없습니다. 또한 누적 표본은 첫 방문한 시점부터 유저를 카운트 하기 때문에, 이러한 비율은 1:1 일 것입니다.

> ## cumulative count validating balance test

- 이러한 Valdiation Test 를 하기 위해서라면 AB period 시작때부터 cumulative count metric 을 측정하기 시작해야 합니다.
- 만약 cumulative count period 이 중간 기간부터 집계를 시작했다고 합시다. 그렇다면 이러한 count 는 Treatment 의 영향을 받게 됩니다.
  - Ex. 만일 Treatment 가 너무 좋아서 유저의 retension 이 높다고 합시다. 그러면 이런 경우에는 Treatment 의 효과 떄문에, Treatment 에 속한 유저의 count 가 더 높게 나올 것입니다.

> How to? 

- 우선 control group 에 대해서 $p_1$ 비율의 유저가 할당될 것이 예상된다고 합시다.
  - 그리고 Treatment group 에 대해서 $p_2$ 비율의 유저가 할당될것이 예상된다고 합시다.
  - A/B Test 시작하자마자 cumulative period counting 을 시작한다면, sample size 의 ratio 는 $\frac{p_1}{p_2}$ 로 예상될 것입니다. 
- 그리고 $N_1$ 은 control group 에 할당되는 샘플 사이즈라고 합시다.
- 그리고 $N_2$ 는 test group 에 할당된 샘플 사이즈라고 합시다.
- 그렇다면 우리는 아래와 같은 Hypothesis 를 테스트 할 수 있습니다.

$$\mathrm{H} 0: N_{1} \mid\left(N_{1}+N_{2}\right) \sim \operatorname{Binomial}\left(N_{1}+N_{2}, \frac{p_{1}}{p_{1}+p_{2}}\right)$$

- 이때 $$N_{1} \mid\left(N_{1}+N_{2}\right) $$ 는 conditional random variable 입니다.
- 위의 분포를 따르는지를 테스트하기 위해서 Chi - Square Goodness of fit 테스트를 수행할 수 있습니다. 그에 따라서 test statistic 은 아래와 같이 정의됩니다. 

$$\sum_{i=1}^{2} \frac{\left(N_{i}-\left(N_{1}+N_{2}\right) q_{i}\right)^{2}}{\left(N_{1}+N_{2}\right) q_{i}}$$

- where $q_{i}=\frac{p_{i}}{p_{1}+p_{2}}$ for $i=1,2$ , 그리고 statistic 은 follow chi square distribution - ($\chi_1$) 을 따릅니다.

> Multiple Test 일떄에는? 

- 이러한 테스트는 multiple treatment group 일때에도 쉽게 generalize 가 가능합니다.
- 각 $Treatment_i$ 에 대해서, 할당될것이 예상되는 비율을 $p_i$ 라고 정의한 뒤에 Multinomial Test 를 적용하면 됩니다.

> 좀 더 정확한 방식 ( ?? 나중에 보강 필요 ! )

- 좀 더 Complete 한 approach for testing experiment 는 empirical proportion $p_1$ 과 expected proportion $p_2$ 를 테스트 하는 것입니다.
- 우리가 experiment filter 를 적용한 이후에 qualified user 의 수를 $N$ 으로 알고 있다고 합시다. 
  - 그러면 우리는 $N_1 / N \approx p_1$ , $N_2/N \approx p_2$ 를 기대합니다. 
- 하지만 이러한 approch 는 filters 를 적용한 뒤에, qualified user 수를 정확하게 측정해야 하고 이러한 작업은 매우 expensive 한 작업입니다. 
  - ex : count(distinct) 쿼리는 다른 프로그래밍 언어들의 경우 대부분 근사값을 사용하고 있음 
- 그럼에도 이 방식이 권장되는 이유는 좀 더 많은것을 테스트 할 수 있기 떄문입니다.
- 이전의 $$N_{1} \mid\left(N_{1}+N_{2}\right) \sim \operatorname{Binomial}\left(N_{1}+N_{2}, \frac{p_{1}}{p_{1}+p_{2}}\right)$$ 가 보장되면 실험이 internally valid 함을 의미합니다.
  - 즉 test 와 control 의 유저 비율이 우리가 의도했던 비율대로 나누어졌으므로 internally valid 하다는 의미입니다. 
- 이에 더해서,  $N_1 / N \approx p_1$ , $N_2/N \approx p_2$ 가 보장되면 실험이 externally valid 함을 의미합니다. 
  - 즉 test 와 control 이 각각 우리가 의도한 비율대로 유저 비율이 나누어지므로 externally valid 하다는 의미입니다. 

![jpg](/assets/images/Stat/156_5.jpg)

- 위 예시는 balanced traffic allocation 에 대해서 테스트해본 예시를 보여주고 있습니다.
- daily unique user counts (실선) 은 날이 갈수록 차이가 나는것을 볼 수 있습니다.
  - 이는 Treatment 효과로 인하여 User Retention 이 증가했기 때문이라고 볼 수 있습니다.
- 하지만 7일동안의 Cumulative User Count 는 A 와 B 가 동일한것을 볼 수 있습니다.
  - 그리고 Chi - Square Test 를 통과 하였습니다. 
- 이러한 테스트를 통하여 우리는 overall experiment group balance 가 이루어졌다고 결론 내릴 수 있습니다. 
  - 만일 balance 가 이루어지지 않고 anomaly 가 감지된다면 우리는 experiment pipeline 을 다시 점검하고 sub - dimension 별로 다시 점검해야 합니다. 
  - 즉 운영체제별로 살펴본다던지, 나라별로 살펴봐야 한다는 것입니다. 
- 다음 섹션에서는 Experiment Pipeine 이 잘못되었을때 일어나는 현상들에 대해서 같이 살펴보도록 하겠습니다. 

> ## Traffic Splitting and Test Id Stamping 

- 만일 Experiment Imbalance 가 감지되었을때, experimentation system 이 어떤 부분에서 이러한 에러가 감지되었는지를 확인해야 합니다.

![jpg](/assets/images/Stat/156_6.jpg)

- 위 그림은 Yahoo 에서 사용하는 Traffic Splitting 을 보여줍니다. 
- Experiment platform back end 는 experiment configuration 과 meta 정보를 가지고 있습니다. 
  - 이러한 정보들을 ATS (Apache Traffic Servers) 로 주기적으로 전달합니다.
- Traffic Splitter Package는 Sampling Function 을 통해서 User Selection 의 Randomization 을 보장합니다. 
- ATS 는 사용자를 특정 프런트 엔드 서버로 라우팅하고 테스트 ID 정보를 전달합니다. 
  - 사용자 요청과 테스트 ID를 받으면 프런트 엔드 서버는 최종 사용자에게 해당 Treatment Experimence 를 제공하게 됩니다.
- Splitting Problem 은 Experiment 기간중 언제나 일어날 수 있습니다. 
  - 이러한 문제는 AA Test 중에 일어날수도 있습니다.
  - 또한 AA Test 를 문제없이 통과하더라도, AB TEst 중에 일어날수도 있습니다. 
- 이 섹션에서 우리는 위의 Experimental Platform 의 key feature 중 일부 결함이 있을때 우리가 마주쳤던 몇 가지 문제들을 설명하려고 합니다.

> ## A. Sampling Function 

> Experimentation Randomization Unit

- 트래픽을 Randomly Split 해서 Experiment Group 에 할당하는것은 Experimental Platform 의 기본중의 기본입니다.
- 이러한 Experimentation Randomization unit 은 다양한것들이 가능합니다.
  - Web : Browser Cookie ID
  - App : Device ID 
  - refister user ID 
  - Session ID 
  - Page view ID 
  - ad ID ........
- 위 중에서 어떤것을 Randomization Unit 으로 가져갈지는 목적에 따라 달라질 수 있습니다. 
- W.L.O.G. 우리는 User ID 를 Randomization Unit 으로 설정했다고 합시다.

> Hash Funtion

- 일반적으로는 이러한 User ID 를 그대로 사용하지는 않고, Hash FUnction 을 적용한 뒤에, 변황되는 값을 이용하여서 random seed 로 사용하게 됩니다.
- 이러한 Hash id 는 random seed 를 고정하고 적용되기 때문에 input 이 일정하면 output 도 일정합니다. 즉 유저마다 User ID 가 동일하다는 보장만 있다면 , Output 또한 일정하게 됩니다. 
  - 이는 유저들이 일관되게 Treatment 또는 Control 로 할당됨을 보장합니다. 

![jpg](/assets/images/Stat/156_7.jpg)

- 우리가 Treatment Group 을 설정하게 되면 각 그룹에 고유한 해시 값 집합이 할당됩니다.
- 예시로 해시 함수를 거치게 되면 User Id 는 0~1000 의 값을 가지게 됩니다. 즉 {0,1,...999} 의 값을 가지게 됩니다.
  - 만일 Treatment Group 에 1% 의 Traffic 을 할당하고자 한다면 10개의 hash value 를 Treatment Group 에 할당하면 됩니다. 
- 이러한 traffic split function 이 가져야 될 필요사항은 추가 문헌 (Practical guide to controlled experiments on the web: listen to your customers not to the hippo) 을 참고하면 좋습니다.

> Hash function 이 어떤 문제가 있나? 

- 모든 hash function 이 desired 되는 randomization properties 를 가지는것은 아닙니다. 
- 그리고 안좋은 해시 함수는 platform 의 전반적인 experiment 에 대해서 악영향을 끼치게 됩니다.
- 야후가 single-layer experimentation platform 을 multi-layer platform 으로 전환할떄에, best hash function 을 찾기 위해서 다양한 연구를 진행했습니다. 
- 만일 모든 실험 layers 에 대해서 같은 hash function 을 사용합니다. 다만 각 계층에는 고유한 시드가 있으므로 사용자 ID와 해시 값 간의 매핑 로직이 다소 변경됩니다.
- 다중 계층 실험 플랫폼은 해시 함수가 단일 계층 실험을 지원하기 위해 필요한 요구사항 보다 더 많은것들을 충족해야 합니다.

> ## 다중 실험 플랫폼이 가져야 할 두가지 mandatory properties

> Unifomity (within layer)

- 각 Layer 의 해시 범위에 걸쳐서 Traffic 이 균일하게 분산되어야 합니다. 
- 즉 임의로 선택한 사용자 ID를 각 해시 값에 할당할 확률은 같아야 합니다.
  - ex : 해시값이 {1,2,...100} 이고, 사용자가 100만명이면 각 해시값에 1만명 정도 분배되어야 합니다.

> Representation (Cross Layer)

![jpg](/assets/images/Stat/156_9.jpg)

- 동일한 해시 값을 갖는 클러스터된 사용자의 경우 다른 계층의 해시 값이 균등하게 분포되어야 합니다. 
  - 즉 위 그림처럼 Layer 1 에서 동일한 해시값 (1) 을 지니는 사용자들의 경우 Layer 2 에서는 균등 분포된 (1~3) 해시값을 가져야 한다는 것입니다.
- 이 속성은 사용자가 여러 실험에 동시에 참여하는 경우 Balanced 되고 orthogonal experiment design 한 실험 설계를 보장하게 됩니다.
- 위 예시처럼 Layer 1에서는 는 Heading 에 대해서 실험을 진행하고, Layer 2 에서는 본문에서 실험을 진행한다고 합시다. 
  - Orthogonal Design 을 위해서라면 위처럼 "균등" 한 분배를 보장해야 각 Layer 의 효과가 어느정도 희석되게 됩니다. 파,빨,초 색깔 변화 실험을 보면 heading 의 명암 차이가 영향을 주긴 하지만, "각 파 , 빨 ,초 에 밝은 heading, 어두운 heading 이 균일하게 분포하므로" 그 영향이 적다고 할 수 있습니다.

> Speed (추가사항)

- 또한, 속도는 다층 플랫폼에서 특히 중요한 고려 사항입니다. 
- 각 사용자 ID는 여러 번 해시되므로 이렇게 추가된 latency 시간은 User Experience 에 대해서 부정적인 영향을 미칠 수 있습니다 [41]. 

> ## Real Example : FNV Hash Function

- 야후의 이전 Single Layer 플랫폼에 사용된 해시 함수는 FNV (Fowler-Noll-Vo)였습니다. 
- 이전에, 다중 플랫폼이 가져야 할 두가지 mandatory property 에 대해서 이야기했었죠? 이  두 가지 속성의 성능을 평가하기 위해 야후에서는 수천만 개의 사용자 ID(브라우저 쿠키)로 구성된 데이터 세트를 사용해서 검정해 보았습니다.
- 10개의 실험 레이어에 대해서 각각 fix 된 무작위 시드로 해시 함수를 시뮬레이션했습니다. 이때 각 사용자 ID에 대해 Layer 당 하나씩 총 10개의 해시 값을 생성했습니다. 

> uniformity Property

- 균일성 특성은 각 layer 에 대해서 개별적으로 테스트되었습니다. 
- 카이-제곱 적합도 검정 (귀무 가설 하에서 균등 분포를 가정) 을 이용해서 해시 범위에 대한 사용자 카운트 분포가 과연 Uniform 인지? 를 검정하였습니다.

> representation property

- 동일한 해시 값을 갖는 클러스터된 사용자의 경우 다른 계층의 해시 값이 균등하게 분포되어야 하는 특성은 각각의 layer 쌍에 대해 테스트되었습니다. 
- 이떄 카이제곱 독립성 테스트를 통하여, 두 개의 서로 Layer 에서 사용자 ID의 분포가 통계적으로 독립적인지 여부를 확인해 보았습니다.
- 결과는 FNV 해시 함수가 균일성(uniformity Property) 테스트는 통과했지만, 계층 간 통계적 독립성에 대한 표현 테스트에는 실패했습니다.
- 이것은 FNV가 단층 실험 플랫폼에는 허용될 수 있지만 다층 플랫폼에는 좋지 않은 선택임을 나타내게 됩니다.

> ## Experiment

- 그러므로 우리는 잘못된 해시 함수를 고치기 위하여 몇가지 다른 해시함수들을 테스트 해 보았습니다.
- 이들 후보 중 Bob Jenkins (lookup3)와 Murmur3 가 균일성 검사와 통계적 독립성 검사 모두에서 좋은 성적을 거둬 최종 2개 후보 함수가 되었습니다.
- Bob Jenkins (lookup3)와 Murmur3 의 속도는 5백만 개의 구별되는 사용자 ID(브라우저 쿠키)의 데이터 세트를 사용하여 생산 과정에서 추가로 평가되었다
- 선택한 두 해시 함수의 속도는 함수 호출당 나노초 수준이었지만 테스트 환경에서 밥 젠킨스(62 ns/call)가 Murmur3(102 ns/call)보다 빨랐다. 
- 우리는 이런 우수한 성능 때문에 우리의 다층 실험 플랫폼에서 트래픽 분할을 위한 것으로Bob Jenkins를 선택하게 되었습니다.

> ## B. Test ID Stamping

- 우리는 테스트 ID 스탬핑 개념을 사용합니다. 
- 플랫폼에서 실험을 설정할 때 traffic split 패키지는 일관된 사용자 경험을 제공하고 사용자 행동에 대한 장기적인 영향을 측정하기 위해 사용자 ID를 동일한 실험 그룹에 일관되게 할당합니다. 
- 일관된 할당은 [30]에서 언급한 기준 중 하나였으며 신뢰할 수 있는 실험에 필요했다. 
- 실험에서 주어진 사용자 ID에 대해, 테스트 또는 제어 그룹의 일부이든 간에, 실험 기간 동안 기록된 모든 이벤트는 일관된 테스트 ID로 라벨이 지정되어야 합니다. 우리는 이 과정을 테스트 ID 스탬핑이라고 부릅니다.
- 그러나 실제로 기록된 이벤트에 테스트 ID를 스탬핑할 때 (1) 테스트 ID 누락 및 (2) 잘못된 테스트 ID라는 두 가지 주요 문제가 발생할 수 있습니다.
- 한 예에서, 우리는 사용자가 기록한 페이지 뷰 이벤트의 96%가 올바른 테스트 ID가 찍힌 반면 페이지 뷰 이벤트의 4%는 테스트 ID가 찍혀 있지 않다는 것을 발견했다. 비록 그 비율이 크지 않아 보일 수 있지만, 실험 분석과 사용자 경험 모두에 영향을 미쳤다. 첫째, 실험 메트릭은 일반적으로 테스트 ID가 있는 이벤트만 계산하기 때문에 보고된 메트릭과 사용자 수가 과소 평가되었다. 둘째, 그리고 더 중요한 것은 이 누락된 테스트 ID 문제는 테스트 그룹의 사용자에게 일관되지 않은 치료 경험을 나타냅니다. 해당 그룹의 사용자는 치료 그룹에 있을 때(테스트 ID 포함) 페이지의 테스트 버전을 본 시간이 96%인 반면, 실험에서 벗어난 경우(테스트 ID 없음) 페이지의 기본 버전을 본 시간은 4%에 달했다. 일관성 없는 경험에 대한 증거로, 테스트 그룹의 사용자가 제어(기본값) 페이지에만 있는 일부 모듈을 클릭한 것을 기록한 데이터에서 발견했습니다. 테스트 ID 손실이 테스트와 제어에 미치는 영향은 동일하지 않습니다. 이 테스트 ID 손실 문제는 제어 그룹의 사용자 환경에 영향을 미치지 않았습니다. 테스트 ID 스탬핑에 관계없이 제어 페이지가 이 실험의 기본 페이지와 같으므로 동일한 버전의 페이지를 볼 수 있습니다. 그러나 테스트 그룹에서 테스트 ID가 누락되었다는 것은 사용자가 일관되지 않은 경험을 했다는 것을 의미합니다. ATS 서버는 테스트 ID를 생성하므로 각 ATS 서버를 통해 레이블링된 실험 트래픽의 양을 검사한 결과 일부 특정 ATS 서버에서 테스트 ID를 생성하지 못했습니다. 사용자가 이러한 ATS 서버를 통해 페이지를 방문할 때 테스트 ID가 할당되지 않았습니다. 근본 원인을 파악한 후 이러한 ATS 서버의 버그를 수정하여 문제를 해결했습니다. 이 문제를 방지하려면 앞으로 테스트 ID를 생성하지 못한 ATS 서버에 플래그를 지정하는 모니터링 도구를 구현해야 합니다.

> ## outlier

- 온라인 실험 분석의 또 다른 과제는 데이터 특이치이다[17].
- 특이치는 실제 사용자 행동을 합리적으로 반영하지 않는 극단값을 갖는 데이터 점이며 실험 결과에 영향을 미칠 수 있다. 온라인 실험에서 이상값의 주요 원천은 로봇[29]으로, 짧은 시간 동안 엄청난 수의 기록된 이벤트를 생성할 수 있다. 
- 예를 들어, 한 실험에서 우리는 크롬 브라우저 하나가 78분 동안 10만 번의 클릭을 생성하는 것을 보았다. 
- 데이터가 분석 데이터 파이프라인으로 흐르기 전에 대부분의 로봇 이벤트를 제거하도록 세심하게 설계된 트래픽 보호 기능이 있지만, 로봇 생성자와 운영자는 탐지를 피하기 위한 새로운 방법을 끊임없이 찾고 있다. 
- 특이치는 신뢰할 수 없는 데이터 출처에서 발생할 수도 있습니다. 예를 들어, 소요된 시간 메트릭은 사용자 이벤트와 관련된 타임스탬프에서 파생됩니다. 
- 컴퓨터나 전화기의 내부 시계를 기준으로 클라이언트측 타임스탬프를 사용할 경우 클럭 동기화가 되지 않아 시계가 과거 또는 미래 시간으로 설정돼 데이터 측정 시점이 잘못될 수 있다. 이는 장치의 라디오가 꺼져 있거나 신호가 없는 모바일 앱의 경우 특히 어려우며, 이는 외부 클럭과 동기화할 방법이 없음을 의미한다.

- 특이치는 실험 분석에 부정확한 측정과 메트릭 분산의 팽창이라는 두 가지 영향을 미치며, 그 중 후자는 치료 효과를 탐지할 수 있는 통계적 검정력을 감소시킨다. 다음의 예에서 한 가지 실험이 야후 디지털 콘텐츠 사이트 중 하나에서 수행되었다. 제품팀은 페이지 디자인에 약간의 변화를 주었고 사이트 기술 스택도 개선했습니다. 이 특정 실험의 핵심 메트릭 중 하나는 이 페이지의 링크 A를 클릭하는 것이었습니다. 그러나 데이터는 그림 5a와 같이 대조군에 비해 테스트 그룹의 클릭 수가 예상외로 크게 증가했음을 보여주었다. 사용자당 주당 클릭 수는 거의 두 배로 증가했습니다. A 링크에 더 많은 클릭을 유도할 수 있도록 설계된 기능 변경이 없었기 때문에 데이터 문제가 있는 것으로 의심됩니다. 테스트 그룹에서는 여러 사용자가 매일 링크 A를 수천 번 클릭하는 반면 대조 그룹에서는 이렇게 큰 값이 관찰되지 않았다. 링크 A를 클릭하는 사용자 비율이 상대적으로 적다는 점을 고려할 때, 수천 번의 클릭을 하는 사용자 수는 전체 그룹 평균을 상당히 높일 것이다.
- 특이치를 탐지하고 제거하기 위해 다양한 통계 및 기계 학습 방법이 개발되었다 [49], [7], [1], [34]. 예를 들어, 관심 있는 사용자 참여 메트릭이 주어지면 관찰된 메트릭 값의 발생을 모델링하기 위해 적절한 통계적 분포를 제안할 수 있다. 특이치는 분포 가정 하에서 확률이 매우 낮은 영역에 속하는 경우 탐지될 수 있습니다. 정규분포를 따르는 지표에 대해서는 3가지 규칙을 적용할 수 있습니다. 클릭과 같이 음수가 아닌 정수 값만 취하는 메트릭의 경우 정규 분포는 기본 참 분포를 모델링하지 못하므로 보다 적절한 분포를 제안해야 한다. 그러나 이상치 감지 방법에 대한 자세한 설명은 이 논문의 초점이 아니다. 이 경우, 우리는 내부 특이치 탐지 방법 4를 적용했다. 이 특이치 모델은 이 실험에서 총 샘플 사용자의 약 0.01%를 걸러냈다. 
- 추가 이상값 필터가 구현되면서 우리는 그림 5b와 같이 제어와 비교하여 테스트에서 클릭이 감소했다는 다른 사실을 알게 되었습니다. 링크 A와 경쟁해야 하는 테스트 경험에 추가 모듈이 추가되었기 때문에 이러한 감소는 합리적입니다. 이 이야기는 이상치에 더 영향을 받지 않는 것으로 간주되는 또 다른 메트릭, 즉 링크 A를 클릭한 사용자의 비율을 사용하여 확인되었다. 특이치를 걸러내기 전에 링크 A를 클릭한 사용자 비율은 감소(제어 대비 17.65%)했지만 사용자당 클릭 수는 반직관적으로 증가했다. 이상치를 제외한 후 클릭 사용자 비율의 감소는 -17.65%(이상치 비율은 무시할 수 있음)로 유지되었고, 감소는 사용자당 클릭 수 감소와 일치했다.

---

**reference**

- https://alexdeng.github.io/public/files/jsm2011-deng.pdf

