---
title: "A Dirty Dozen &#58; Twelve Common Metric Interpretation Pitfalls in Online Controlled Experiments"
excerpt: "Microsoft 에서 실험에서 만나게 되는 12가지 Pitfall"
categories:
  - AB_Paper
last_modified_at: 2021-11-06

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Microsoft Data Analysis & Experimentation team Data Scientist **Somit Gupta** 가 **KDD2017**에서 발표한  논문입니다. <https://medium.com/bondata> 님의 서술과 논문을 참고하였습니다.
{: .notice--warning}

- <https://hyperconnect.github.io/2021/02/26/auto-stats-test.html>

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## Metric Taxonomy

- Microsoft 에서는 메트릭 해석시에 , 수백개의 측정 기준을 계산하여 실험 결과를 분석합니다.
- 이떄에 '몇개' 만 주요한 승자 예측시에 사용되고 나머지는 올바른 결정을 내리는지 살펴보는 보조적인 지표입니다. 
- 이때 메트릭의 설계와 분류 프로세스에 대해서 설명하려 합니다. 

> Data Quality Metrics 

- 우리가 실험을 믿을 수 있도록 사용한 '데이터' 가 올바른지? 에 대해서 입니다. 
  - 이러한것을 측정하는 지표는 Control , Treatment 의 샘플이 1 대 1 로 잘 나뉘었는지? 등이 됩니다.

> OEC metric

- 최우선 목표가 되는 메트릭스입니다.
- 비록 짧은 기간에 측정되는 메트릭이긴 하지만, 장기적인 효과와 사용자의 만족도를 측정하려는 메트릭이 이상적입니다. 
  - 이는 몇가지 다른 메트릭이 조합될 수 있습니다.
- (이러한 metric 의 Construction 에 대해서는 다양한 논문이 있습니다.)

> Guardrail metric

- 우리는 실험의 Treatment 의 성공을 바랍니다만, 해를 끼치기를 원하지 않는 메트릭이 있을것입니다.
  - 로드 타임 등이 있을 것입니다. 
- 큰 저하를 원하지 않는 메트릭입니다.

> Local Feature and Diagnostic Metrics

- 지표들이 왜 변하였는지를 알 아보기 위한 메트릭
- OEC 의 이동이 어떠한 이유로 일어났는지 등을 이해하기 위하여 설정됩니다.
  - 웹 페이지에서 전체적인 CTR 이 OEC 였다면, 개별적인 Feature 에 대한 CTR 을 설정할 수 있습니다. 즉 구체적으로 왜 웹 페이지의 CTR 상승이 이루어졌는지를 알 수 있는 메트릭들을 알 수 있는것입니다. 
- 또는 특정 유저에 대해서 구매전환율을 CTR 로 삼았다고 합시다.
  - 이때에 구매까지 이르는 퍼널은 전면 화면에서 카테고리 클릭 -> 아이템 클릭 -> 스크롤 -> 결제 와 같이 구성될 수 있습니다. 
  - 각각의 경로에 대해서 메트릭을 추가적으로 살펴본다면 우리는 OEC 가 왜 변한것인지에 대해서 잘 알수 있게 됩니다.

# [METRIC INTERPRETATION PITFALLS](#link){: .btn .btn--primary}{: .align-center}

> ## 1,Metric Sample Ratio Mismatch

![jpg](/assets/images/Stat/138_1.jpg)

- 가설: 링크를 새로운 탭에서 띄우는 것은 홈페이지 로드 타임을 증가시킬 것이다. (Opening links in a new tab increased home page load time.) 로 설정했다고 합시다.
  - Treatment :  MSN 홈페이지에서 클릭된 어느 링크든, 새로운 탭으로 페이지가 뜬다.
  - Control : MSN 홈페이지에서 클릭된 어느 링크든, 오픈되어 있는 탭에서 링크로 이동된다.
- 결과 : 실험군에서 PLT (Page Load TIme) 이 8,32% 증가  (이는 너무 지나친 증가)

$$PLT(variant) = \frac{\sum_{homepage \ loads \ p}PLT(p)}{\sum _{hompage \ loads }1}$$

- 이는 사실 SRM 으로 일어난 결과였습니다.
  - Treatment에서의 페이지 로드 수: 8.4M
  - Control에서의 페이지 로드 수:  9.2M

> Remedy

- Metric SRM 을 탐지하는 Test 를 자동으로 감지하고 경고합니다.
- Data Quality metric 을 선정합니다.
- 비율 지표를 분해하여 메트릭의 어느 부분에서 차이가 발생하는지 이해합니다. 
  - 이러한 mismatch 에 영향받지 않는 subset 을 찾아서 신뢰 가능한 실험을 하는게 좋습니다.
  - 아래는 그러한 Metric Breakdown 의 예시입니다.

```
Homepage PLT (페이지 로드 타임) can be decomposed into:
1. Average homepage PLT per user 
  a. Average homepage PLT per user with 1 homepage visit
  b. Average homepage PLT per user with 2+homepage visits
2. Number of homepage loads per user
  a. Number of back-button loads
  b. Number of non-back-button loads
    i. PLT for non-back-button loads
```

> ## 2.Misinterpretation of Ratio Metrics

![jpg](/assets/images/Stat/138_2.jpg)

- MSN 메인 페이지에는 엔터테인먼트, 스포츠와 같은 토픽으로 구분된 다양한 module이 있습니다. 이런 모듈의 위치는 유저 경험 최적화를 위해서 종종 실험의 대상이 되는데요. 어떤 한 실험에서는 스크롤의 맨 밑에 있던 모듈을 최상단으로 옮겼습니다. 여기서, 평균 CTR이 40% 상승했습니다.
  - 가설: 모듈의 위치를 상단으로 옮기면 CTR이 상승할 것이다.
  - 결과: 실험군에서의 CTR이 40% 감소

> About the Pitfall

- 이떄에  users in treatment and control 에 대해서 검정한 결과, SRM 이슈는 발생하지 않았습니다. 

$$\text { Avg CTR/User }=\frac{\sum_{\text {users }}\left(\frac{\sharp \text { clicks on the module }}{\sharp \text { impressions of the module }}\right)}{\sum_{\text {users }} 1}$$

- 위의 비율 지표를 분해해 보았습니다. 이때 분해 결과는 아래와 같았습니다.
  - 분모(impression(노출) user count)의 Control 대비 증가율 200%
  - 분자(whole CTR)의 Control 대비 증가율 74%
- 즉 impression(노출) 의 증가가 Control 보다 훨씬 많았고, 이로 인하여 Treatment 의 평균 CTR 이 더 작아진 상황입니다.
  - 즉 비율 지표를 비교할때에는, 분모의 지표도 잘 살펴봐야 한다는것을 기억해야합니다.
- 예시로 아래와 같은 상황을 봅시다.
  - Control : 1/2, 1/2 ,1/2 
  - Treatment :  2/6, 2/6 ,2/6 
  - 위 경우 control 이 더 좋아보이죠. (1/2) 하지만 우리는 , Treatment 가 더 좋다고 생각할수도 있습니다. (단순히 분자의 합으로만 보면 Treatment 가 더 좋은것이죠)

> 비율 지표 계산법 2가지

1. 비율의 평균(위 Avg CTR/User 케이스): AVG(SUM/SUM)
2. 평균의 비율: AVG/AVG

- 이때 (2) 보다 (1) 이 더 좋다고 합니다. 그 이유는 아래와 같습니다.

> Why (1) is better then (2) ?

- 각 유저마다 끼칠수 있는 영향력이 일정하므로 Outlier 에 강건함, 그에 따라서 test 시에 더 높은 power 를 가짐
  - 예시로 5명의 유저 데이터가 1/3 , 1/3, 1/3, 1/3, 20/88 인 경우, 첫번쨰 셈법에 의하면 평균은 1/3 에 가깝지만 (대부분 유저의 영향력을 반영), 두번째 셈법에 의하면 23/100 으로, outlier 인 다섯번쨰 유저의 영향력을 크게 받게 되는 것입니다.
- Randomized Unit 과 Analysis Unit 이 같기때문에 분석이 용이합니다.
  - 1번의 경우 '유저' 가 평균을 내게 되는 단위이고, Randomized Unit 이므로 indepent 가 보장되여 t-test 를 수행할때 정상적으로 가능합니다.
  - 2번의 경우, 전체 클릭수 / 전체 노출수 인 경우에, 분산 계산은 Analysis Unit 이 노출로 가정하고 계산하게 되는데요, 이때 Randomized Unit 인 유저와 같지 않아서 Delta method 를 써야하는 등, 귀찮은 작업이 필요합니다.
- Randomized Unit 을 분석에 바로 사용하여서 통제를 보장한다.
  - 우리는 일반적으로 User 를 Randomized Unit 으로 쓰게 되는데요, 그러므로 보장된 Random 방법론으로 Control 과 Treatment 에 User 등이 잘 분배되도록 심혈을 기울입니다.
  - 그러므로 (1) 번 방법론을 쓰게 될때, Analysis Unit 이 되는 각각의 값들에 대해서 Control 과 Treatment 가 같은 비율로 잘 나뉘었다고 생각할 수 있죠.
  - 하지만 (2) 번 방법론을 쓰게 될떄, Analysis Unit 이 Randomize Unit 과 다를 수 있기떄문에 Control 과 Treatment 에 같은 비율로 데이터가 들어가지 못할 수 있습니다. (유저가 반반으로 나눠진다고 해고, 페이지뷰같은 경우는 경우는 반반이지 못할 수 있기 떄문이죠)

> Remedy

- 그러므로 비율 지표를 사용할때에는 꼭 분자와 분모도 반드시 명시하고, 같이 살펴보는것을 권장합니다.

> ## 3. Telemetry Loss Bias

> Experiment

- Telemetry = 무선 및 유선으로 디지털 신호 데이터를 측정, 변환, 전송 + 축적, 분석하는 기술을 의미

![jpg](/assets/images/Stat/138_3.jpg)

- 가설: iPhone Skype notification에 사용하는 protocol을 바꾸었을 때, 통화 품질 지표(call quality metrics)를 변화시킬 것이다.
  - Treatment: VolP protocol 사용
  - Control: 다른 protocol 사용

> 결과

- 시도한 통화의 비율과 같이, 통화관련 메트릭에서 중요한 변화를 보였습니다.
  - 하지만 이 경우, 전형적인 Improvement 나 Degradation 과 같은 패턴을 보이지 않았습니다. 
  - 일부 지표는 매우 강하게 움직이는 반면, 일부 지표는 그대로였습니다. (이는 매우 드문경우입니다.)
- 일부 통화 관련 지표에서 예상치 못한 강한 변동이 있었다. 다른 지표들은 변화가 없었다.
- 가드레일 메트릭, 로컬 메트릭을 통해서 강한 변동을 빠르게 파악하고 대응이 가능했다.

> About the pitfall

- 실험군에서 사용한 protocol의 경우. 푸시를 받고 데이터를 batch 형태로 모아서 보내기까지 몇 초 더 대기합니다. 기술적인 이슈가 실험의 결과를 해석하는 데에 편향을 줍니다.
- 즉 이 경우, 샘플이 매우 편향되어있으므로  클라이언트 event based, click based metric은 전부 믿을 수 없게 됩니다.

> How to avoid

1. 클라이언트에서의 call event 수, 서버에서의 call event 수를 비교하고 loss rate를 Data Quality Metric으로 포함합니다.
2. 클라이언트에서 할당하는 이벤트의 sequence number 사이에 빈틈이 있는지 파악합니다.
3. 메트릭들은 가능하다면 클라 사이드 이벤트보다 서버 사이드의 이벤트 기반으로 카운트 되어야 합니다. less lossy, more uniform합니다.

> ## 4. Assuming Underpowered Metrics had no Change

> Experiments

- MSN 홈페이지에서 일어나는 실험들 중에서, total number of page views per user 은 중요한 OEC metric입니다. 특정 실험에서 대조군 대비 실험군에서 0.5%의 metric 향상이 있었다고 합시다.
  - 하지만 대부분 P-value가 통계적으로 유의하지 않다고 나옵니다.
- MSN과 같은 대규모 온라인 비즈니스에서는 0.5%의 향상도 비즈니스에서 매우 큰 임팩트로 해석되곤 합니다.
  - 즉 비즈니스적으로는 의미가 있으나 통계적으로는 의미가 없는것이죠.

> About the Pitfall

- 이 케이스에서 우리는 power = 80% 를 설정했을때에는 대조군과 실험군이 7.8% 이상의 차이가 나야 p-value가 통계적으로 유의하다고 나오게 됩니다. 
  - 하지만 성숙한 비즈니스에서 7.8% 이상의 차이를 내기는 쉽지 않습니다. 즉 우리가 시행하는 테스트의 탐지 수준이 너무 안좋아서 
- 이런 작은 샘플 사이즈를 설정하게 되면 몇가지 안좋은 효과가 일어나게 됩니다.
  - underpowered metric 에 대해서  Statistically Significant 하다고 밝혀진 경우, 이러한 결과는 사실 실제 change 에 비해 과정된 결과일 가능성이 더 높습니다.

> How to avoid

- Priori power analysis을 진행하여, OEC와 가드레일 메트릭에서 비즈니스에서 충분히 크다고 판단되는 임팩트(%)를 감지할 수 있을 샘플 사이즈를 미리 정합니다. 
- 이러한 선행 전력 분석의 권장사항은 주어진 제품에 대한 일반적인 실험 시나리오에 대해 단순화할 수 있습니다. 
  - 예를 들어 미국에서 실행되는 Bing 실험의 경우 테스트 중인 기능이 대부분의 사용자에게 영향을 미칠 경우 최소 10%의 사용자에 대해서 1주일동안 실험하는게 좋습니다.
- 떄로는 탐지하고자 MDE 와 Power 를 기반으로 Sample Size 를 계산해 보았더니, 권장하는 샘플 수가, 서비스에서 가용할 수 있는 모든 트래픽 이상일수도 있습니다
- 이러한 경우에도, 실험자들이, 현재 모든 트래픽을 사용했을떄에 우리가 얻을 수 있는 MDE 가 어느정도 수준인지 파악하는것도 중요합니다. 
- 이때 Power 의 수준은 결과를 적절하게 평가하기 위해 OEC 와 가드레일 메트릭의 작은 변화를 탐지할 수 있는 최소 80%의 Power 로 설정하는게 좋습니다.

> ## 5. Claiming Success with a Borderline P-value

> Experiment

- 마이크로소프트의 또다른 웹 페이지 [Bing.com](http://bing.com/) 에서 실험 A를 진행했습니다. 실험군, 대조군 간의 OEC metric 증분을 검정한 결과 0.029의 p-value가 나왔습니다.
  - 이 OEC metric은 유저의 만족도 지표고, 유저의 잔존에 직결되는 leading indicator입니다. 
  - 하지만 대부분의 실험이 이 metric을 개선하는 데에 성공하지 못했습니다.
- 하지만 이때 P-value로 실험 A의 성공을 확신하지 않고, 검증용으로 동일한 실험을 독립적으로 시행했습니다. 
  - 실험군, 대조군 트래픽을 2배로 늘려서 실험을 시행한 결과, 동일한 OEC metric 증분을 검정했지만 통계적으로 유의하지 않았습니다.

> About the pitfall

- P-value가 0.05에 가까운 boundary에 있을 때, 다른 추가 근거를 고려하지 않고 귀무가설을 단순하게 기각하는 경우 발생합니다. 
  - Borderline p-value(0.05의 경계에 가까운 값)을 보일 때, 1종 오류(False Positive)의 경고일 수 있습니다.

> How to avoid

- P-value가 0.05의 경계에 가깝지 않은 OEC metric에 더 중점을 두고 실험을 평가합니다.
- 또는 Control / Treatment 에 대해서 유저 수 트래픽을 키워서 동일한 실험을 새로운 유저들에게 시행해 봅니다.
- 두 가지 방법이 다 불가능하거나 2번을 시행해도 여전히 borderline p-value가 나온다면 [Fisher’s Method](https://en.wikipedia.org/wiki/Fisher's_method)를 활용합니다. 
  - 위 방법은 샘플 수가 적거나, 카테고리가 많고 범주형 자료일 때 사용하는 검정법입니다.

> ## 6. Continuous Monitoring and Early Stopping

![jpg](/assets/images/Stat/138_4.jpg)
$$
\begin{array}{|c|l|l|}
\hline & {\text { EXP-01 }} &{\text { EXP-02 }} \\
\hline \text { 기간 } & 2 \text { weeks } & 2 \text { weeks } \\
\hline \text { 처치 } & \text { A new ranking algorithm in Bing.com } & \begin{array}{l}
\text { Gave teaching tips for Xbox suspended } \\
\text { users(due to bad behavior) }
\end{array} \\
\hline \text { 목적 } & \begin{array}{l}
\text { Launch better ranking algorithm in } \\
\text { Bing.com }
\end{array} & \begin{array}{l}
\text { Decrease customer support service calls } \\
\text { about suspensions }
\end{array} \\
\hline \text { 결과 } & \begin{array}{l}
\text { 1 week가 지났는데, OEC metric이 통계적으로 } \\
\text { 유의한 향상을 보였다. 그러면 이 실험은 success } \\
\text { 인가? 그만해도 될까? }
\end{array} & \begin{array}{l}
\text { 2 weeks가 지나도, OEC metric(nums of CS calls) } \\
\text { 가 통계적으로 유의한 차이를 보이지 않았다. 그러면 } \\
\text { 실험 기간을 늘려야 할까? }
\end{array} \\
\hline
\end{array}
$$

- EXP-01, EXP-02 두 상황에 대한 대답은 모두 안된다! 입니다.
  -  [KDD2015에서 A/B 테스트를 12년간 운영한 Microsoft의 다른 엔지니어가 위와 같은 상황에서 early stopping, extending을 해도 괜찮다](https://exp-platform.com/kdd2015keynotekohavi/)고 발표한 바가 있을 정도로 , 매우 민감하고 미묘한 문제입니다. 
- 이러한 실수는 일부 A/B 테스트 책자의 권장 사례로도 사용될 정도로 미묘합니다
  - 물론 대부분의 실험 기획자들은 통계적으로 일찍 중단하게 되면 Type 1 error 가 늘어나기 떄문에 하면 안되는 짓이라는것을 명심하고 있습니다만 왜 이런 실수를 할까요? 
- 그것은 바로 AB 테스트에서 , 사용자에게 큰 저하가 예상될 경우 Shutdown 하는 기능이 필수로 구현되야 하기 때문입니다.
  - 이런 기능하에서 우리는 다음과 같은 생각을 하기 쉽습니다. "어? Sutdown 자체가 Early Stopping 인데, 모든 메트릭에 대해서 수행하도 되는거 아닌가?"
- 이러한  "establishing the guidelines that require making ship decision only at the pre-defined time point" . 즉 정해진 시간에만 Stopping 을 할 수 있게 하는 등의 조치가 필요합니다. 

> About the pitfall

- 지속적으로 결과를 체크하고, 통계적 유의성을 확보한 순간 실험을 종료하는 것은 1종 오류(False Positive)의 발생 가능성이 높아집니다. 
  - 1종 오류가 발생한 채 의사 결정을 내릴 경우, 실제로 지표를 개선시키지 못하는 기능을 출시하게 됩니다.

> How to Avoid

1. 실험 소유자들(experiment owners)가 이러한 Pitfall 에 대해 인지하게 하고, 특정 시점에만 의사 결정을 하도록 가이드라인을 확립합니다.
2. [Sequential Hypothesis Testing](https://arxiv.org/pdf/1512.04922.pdf)을 통해 p-value를 조정합니다.
3. [Bayesian testing](https://arxiv.org/abs/1602.05549)을 진행하면, 자연적으로 지속적인 모니터링 기반의 optional stopping이 가능하다고 합니다.

> ## 7. Assuming the Metric Movement is Homogeneous

> Experiment 

- 많은 선행연구에서 사용자에게 품질이 안좋은 광고를 많이 보여주는것은 UX (user experience) 를 크게 감소시키는것으로 알려져 있습니다. 
- 그러므로 Bing 에서는 새로운 광고 경매 및 배치 알고리즘을 통해 ,광고의 수를 동일하게 유지하면서 매출을 상승시키려고 하였습니다. 
- 그 결과 매출을 2.3% 상승시키면서, 페이지별 표시되는 광고의 개수가 0.6% 감소하게 되었습니다.
  - 이 결과만 보게 되면, 페이지당 광고의 수가 줄었으므로 UX 에게는 훨씬 더 적은 영향을 미치게 되겠죠. 
  - 또한 매출이 2.3% 매출이 상승했으므로 금상 첨화일 것입니다. 

> About the pitfall

- 이떄 광고가 뜨는 페이지를 세그먼트내보았을 때, 결과가 달라집니다.
  - 첫 페이지(original page): # of ads per page 0.3% 증가
  - 뒤로 가기한 페이지(dup page): # of ads per page 2.3% 감소
- 원인은, 뒤로 가기 할 경우, 첫 페이지에서 뜨는 광고와 다른 광고가 떠야 합니다. 아마 빠르게 다른 광고로 스위치하면서, 충분한 광고가 로딩 되지 않아서 감소하지 않았나 예상합니다.
- 따라서 original page 케이스가 전체 페이지 수에서 차지하는 비중은 컸지만, dup page 케이스에서의 드라마틱한 delta로 전체 결과에서 0.6% 감소로 이끌었습니다.
- 이렇게 페이지를 쪼개어서 확인해본 결과, 사실상 중요한 것은 첫 페이지(original page)이지만, 첫 페이지의 경우 OEC metric이 증가하지 않았기 때문에 실험은 성공하지 못했습니다.
- 즉, **이 함정은 ‘처치 효과가 모든 유저와 상황에서 동질할 것이라고 가정할 경우’를 의미합니다. 다양한 상황에서 처치 효과에 대한 OEC metric의 반응이 달라질 수 있습니다.**

> How to avoid

1. **하나의 기능을 ship하는 것은 전반적인 유저 경험을 향상시키지만, 대체로 특정 유저 그룹의 경험은 저해하게 됩니다.** 이 사실을 인지하고, 주요한 세그먼트는 쪼개어서 분석합니다.
2. 수백개의 metric을 다양한 세그먼트 별로 쪼개어 보면서 이질적인 처치 효과(heterogenous treatment effect)가 있는지 확인하는 것은 manual analysis로는 불가능합니다.
3. 따라서 automated tool이 필요합니다.

> ## 8. Segment Interpretation (Simpson’s Paradox, 심슨의 역설)

> Experiments

- 아래는 [Bing.com](http://bing.com/) 에서 seattle seahawks라는 키워드를 검색했을 때 ranking algorithm 기반으로 결과가 뜬 이미지입니다.

![jpg](/assets/images/Stat/138_5.jpg)

- 가설 
  - 가설: Bing에서 새로운 ranking algorithm을 런칭했을 때, Sessions per User가 상승할 것이다.
- 세그먼트 쪼개기
  - 일반적으로 세그먼트는 사용자의 국가 / 운영체제 / 앱 버전 / 장치 유형 등으로 쪼갤 수 있습니다.
  - 위의 이미지에서 News, Schedule, Centurylink Field, Videos 항목(deeplink 라고도 함)을 눌러서 본 여부에 따라 세그먼트를 나눴습니다.
    - 눌러서 본 유저 = U1
    - 눌러보지 않은 유저 = U2
    - 전체 유저 = U1 + U2
- 결과:
  - 실험군 U1가 대조군 U1에 대비하여 통계적으로 유의하게 Sessions per User 향상
  - 실험군 U2가 대조군 U2에 대비하여 통계적으로 유의하게 Sessions per User 향상
  - 실험군 전체가 대조군 전체에 대비하여 통계적으로 유의한 변화 없었음. ([심슨의 역설](https://namu.wiki/w/심슨의 역설))
- 이는 실험군에서의 U1의 비중이 대조군에서의 U1의 비중보다 컸기떄문 (실험군, 대조군 비율 불일치)

> About the Pitfall

- 실험의 결과는 사실 사용자당 세션 수 메트릭에 영향을 끼치지 않았습니다. 
  - 그러나 U1 의 사용자 비율(deeplink 를 본 사람) 의 경우는 Treatment 에서 감소했습니다.
- Segmentation은 디버깅에 효과적인 툴입니다.
  - 예를 들어, KPI가 감소했을 때 원인 진단을 위해서 세그먼트를 쪼개어서 두드러지게 감소하는 세그먼트를 찾습니다.
  -  또한 세그먼트로 쪼개어서 이질적인 효과를 발견할 수 있습니다.
- 하지만 세그먼트를 분류해서 통계적 유의성 검사를 할 때, Simpson’s paradox와 Sample Ratio Mismatch를 경계해야 합니다. 또한 실험 소유자들은 기대하는 효과, 즉 통계적 유의성을 확보할 수 있을 때까지 세그먼트를 쪼개어 분석하는 경향도 있습니다.
- 하지만 세그먼트를 쪼개면서 계속 분석하는것은 결국 Multiple Comparison 의 한 문제가 됩니다. 
  - 이는 결국 세그먼트를 나누면 나눌수록 False Positive 의 문제를 일으키게 될 것입니다. 

> How to avoid

1. 세그먼트 분류 기준이 실험의 처치에 영향을 받는 영역이 아니어야 합니다. → SRM 테스트를 통해 검증할 수 있습니다.
2. Multiple testing problem(다중 비교) → [Bonferroni correction](https://ko.wikipedia.org/wiki/본페로니_교정)으로 1종 오류를 보정하는 과정을 거칩니다.

> ## 9. Impact of Outliers 

> Experiment

![jpg](/assets/images/Stat/138_6.jpg)

- 동일하게 MSN 홈페이지 케이스입니다. 여성의 얼굴이 있는 곳을 Carousel 및 Infopane 이라고 합니다.
- 가설: Carousel에 더 많은 슬라이드를 보여줄수록 user engagement metric이 증가할 것이다.
  - Treatment: 16 slides in the carousel
  - Control: 12 slides in the carousel
- 결과 : 2가지 측면
  - user engagement metric이 실험군에서 통계적으로 유의한, 급격한 상승을 보였다.
  - 또한 실험은 SRM을 보유했다. (SRM test p value ~ 1e-6) 실험군 유저 수가 더 적었다.

> About the Pitfall

- 웹 페이지에서 Bot filtering 알고리즘이 있는데, 알고리즘에서 봇으로 판단하는 기준 중 하나가 # of distinct actions user takes 였습니다.
  - Carousel에서 슬라이드를 넘기는 행동을 과도하게 많이 한 일부 outlier 유저들이 봇으로 판단되어, 실험군 유저 수에서 자동으로 배제되었습니다.
  - Bot filtering 알고리즘을 수정하니 SRM도 사라졌습니다.
- **이처럼, 아웃라이어는 지표 값을 skew할 수 있고, 이 경우 지표의 분산이 커져 통계적으로 유의성을 내기에 더 어려워집니다.**

> How to avoid 

1. Trimming: 아웃라이어 제거하기
2. Capping: 아웃라이어를 특정 고정된 값으로 대체하기
3. Windsorizing: 아웃라이어를 특정 percentile 값으로 대체하기
4. Data Quality metric으로 위 bot filtering 과 같은 케이스 피하기
5. 지표의 평균이 아닌, 25, 50, 75, 95% 값을 보기
6. 로그를 취해 변환하기 (하지만 이 방법은 메트릭 값을 해석하기 어렵게 만들어서 추천하지는 않음,,)

> ## 10. Novelty and Primacy Effects 

![jpg](/assets/images/Stat/138_7.jpg)

- Edge 브라우저는 새로운 탭을 켰을 때 유저가 가장 많이 방문한 frequently visited TOP SITES 섹션이 있습니다. 쓰는 유저들은 잘 쓰지만 안 쓰는 유저들은 아예 안 써서, 사용을 유도하기 위해 coach mark를 추가했다고 합니다.
  - coach mark : 사용을 유도하기 위해 쓰는 하이라이트나 화살표 등
- 가설: Coach mark를 추가했을 때 top sites 페이지 클릭 수가 증가할 것이다.
  - 실험 진행 기간: 4주
- 결과:
  - 실험군 전체 페이지 클릭 수에서 0.96% 향상
  - 실험군 top sites 페이지 클릭 수에서 2.07% 향상
- 의문점
  - 이 효과가 얼마나 오래갈까? 
  - 이러한 효과가 장기적인 유저의 참여 증가로 이어질 수 있을까? 

> Pitfall

- 세그먼트를 나누어서 봅니다.

![jpg](/assets/images/Stat/138_8.jpg)

- 유저의 첫 coach mark 페이지 방문과 이후 방문을 나누어 보았습니다. 
  - 이후 방문에서는 페이지 클릭 수가 유의하게 상승하지 않는것을 볼 수 있습니다.
  - 따라서, Treatment Effect 는 첫 방문 이후로 지속되지 않았습니다
- 이러한 Novelty effect를 짚어냄으로써 프로덕트팀이 더 많은 coach mark를 만드는 데에 리소스를 쓰지 않게 되었고, 유저들은 distraction을 줄 수 있는 coach mark를 더 이상 보지 않아도 되었습니다. 

> Novelty Effect?

- 실험은 일반적으로 짧은 기간 동안 진행되지만, 우리는 Treatment 가 비즈니스와 사용자에게 미치는 장기적인 영향을 추정하려고 노력합니다. 
- 이때 장기적인 영향을 제대로 평가하기 위해서는 시간이 지남에 따라 치료 효과가 증가하는지 감소하는지 고려할 필요가 있습니다. 
  - 위의 예에서 단기적으로는 변화가 긍정적으로 보였으나 장기적으로는 변동이 없었습니다. 
- 이렇게 긍정적인 효과가 단기간에만 발생하고, 장기간으로는 flat한 효과를 보일 때 Novelty effect라고 합니다. 이러한 효과를 무시하게 된다면, 실험은 계속 안좋은 기능을 안고 갈 수 있습니다.

> About the pitfall: Primacy Effect

- Novelty Effect와 정반대로, **초반에는 유저가 반응하지 않다가 시간이 지날수록 user learning이 발생하여 처치에 더 잘 적응하고, 반응하는 현상**을 의미합니다. 아래와 같은 케이스들이 있습니다.
  - Ad blindness: 초반에는 유저가 광고를 무시하다가, 유저와 관련된 광고가 뜨기 시작하면서 user engagement가 상승합니다.
  - Content recommendation system: 유저의 정보 데이터가 쌓이면서, 더 양질의 콘텐츠를 추천해주며 user engagement가 상승합니다. 유저들도 익숙해집니다.

> How to avoid

실험들은 주로 짧은 기간안에 종료되지만, 비즈니스와 유저에게 장기적인 영향을 측정하고자 할 때가 많습니다.

1. Novelty Effect를 구분해서 보기 위해서는, A/B 테스트 각 그룹에서 신규 유저만 추출하여 A-신규/ B-신규를 구분해서 봅니다. 성공적인 A/B 테스트는 신규 유저를 대상으로 유의미한 효과를 보여야 합니다. 그렇지 않으면, 기존 유저들을 대상으로 최적화하여 로컬 옵티멈으로 수렴하며, 현재 주요 유저 베이스 밖에서의 기회를 놓치는 셈입니다.(참고: [노트북](https://productds.com/wp-content/uploads/Novelty_Effect.html))
2. 처치 효과를 실험의 다양한 일자 세그먼트별로 쪼개어서 봅니다. 또는 유저의 방문 회차 세그먼트로 쪼개어서 봅니다. 쪼개어 보며 장기에도 처치 효과가 유지되는지 봅니다.
3. 실험을 장기로 진행합니다.

> [참고] 프로덕트 소셜 bias(레퍼런스)

- Early Adopters Bias (프로덕트의 신규 버전을 사용하는 초기 유저들은 전체 유저 인구와 성격이 다릅니다.)
- Novelty Effect (신규 기능 및 기술이 출시되면, 실제 앱 학습과 성취에서의 개선때문이 아니라 신규 기능 및 기술에 대한 관심의 증가로 인해 performance가 초기에 개선되는 경향이 있습니다)
- Default Effect (변화에 대한 적응에 노력이 필요하기 때문에’change aversion’ 유저들은 기본 세팅을 계속해서 사용하려고 할 것입니다.)

→ Solution: Balancing KPIs (여러 관점에서의 KPI를 함께 보아야 편향을 피할 수 있습니다.)

> ## 11. Incomplete Funnel Metrics (퍼널 단계별 메트릭 부재)

- 가설: Xbox 제품 중에서 특정 프로모션 전략을 취했을 때, 매출이 상승할 것이다.

  결과:

  - 결제 페이지 CTR: 실험군에서 통계적으로 유의하게 증가
  - 매출: 변화가 통계적으로 유의하지 않음

> About the pitfall

- 위와 같은 결과는 작은 변화가 판매를 클릭하는 사용자 수에 큰 긍정적인 영향을 미친다는 것을 보여주었습니다. 
  - 하지만 매출의 변화를 보았을때에, 특정 위치에서 얻는 클릭 수를 늘리는 것은 쉽지만 수익 증대 목표와는 직접적인 관련이 없는것을 볼 수 있었습니다.
- 이러한 실험들이 power 가 부족해서였을까요? 그게 이유가 아니였습니다. 일부 실험의 경우 충분한 Power 를 가지고 있었음에도, 수익이 증가하지 않았습니다. 

> funnel Analysis

- 이떄에는 깔때기 프로세스로 사용자의 경험을 자세하게 모델링 할 수 있습니다. 
  - 이때 주로 측정되는 사용자 경험으로는 온라인 서비스 가입과, 온라인 쇼핑 결제가 있습니다.
- 이 과정에서 사용자는 최종 성공 목표 (가입 또는 구매)가 달성될 때까지 연속적으로 여러 프로세스를 경험하게 됩니다.
  - 실제의 경우 1% 미만의 최종 성공률(가입 또는 구매)이 흔하므로 이러한 프로세스를 이해하고 최적화하는 것이 매우 중요하다. 
- 깔때기 기반 시나리오의 경우 프로세스의 모든 부분을 측정하는 것이 중요합니다.
  - 이때에 깔때기의 모든 단계에서 단순 클릭이나 사용자 수가 아닌 성공률을 비교해야 합니다. 
- 또한 조건부 성공률 지표와 무조건적 성공률 지표 모두를 측정해야 합니다.
  - 조건부 성공률은 단계를 시작하려고 시도한 사용자 중에서 주어진 단계를 완료한 사용자의 비율로 정의됩니다.
  - 무조건 성공률은 깔때기 맨 위에서 시작한 모든 사용자를 고려하여 성공률을 계산한다. 
- 위에서 제시한 두가지 유형의 메트릭과 각 단계의 세부 분석을 같이 보는것이 졸습니다.
- 이때 또 하나 유의할점은 , 대규모의 사이트 (수백만명의 유저) 일지라고, 최종 단계까지 가는 유저가 수백명밖에 되지 않을 수 있습니다. 그러므로 최대한 각 step 에서 만족할만한 power 를 제공하는것도 중요합니다.

> ## 12. Failure to Apply Twyman’s Law (큰 수치 변화를 의심 없이 신뢰)

![jpg](/assets/images/Stat/138_9.jpg)

- 가설: MSN 홈페이지에 상단에 있는 기능 버튼을 mail 앱으로 변경할 경우 앱 클릭 수가 증가할 것이다.
  - Treatment: 위 이미지에서 빨간 네모에 mail 앱을 배치
  - Control: 위 이미지에서 빨간 네모가 outlook 앱

- 결과
  - 빨간 네모에 있는 앱 클릭수가 28% 증가
  - 빨간 네모 앱 근처 버튼 클릭 수가 27% 증가
  - 실험군에서 전반적인 페이지 클릭 수가 4.7% 증가

> About the pitfall

- 위와 같은 수치 변화는 Too good to be true라고 합니다. 
  - 여러 가지 metric을 함께 보았을 때, user retention & satisfaction 지표에는 변화가 없었다고 합니다. 
  - 또한 매일 앱 클릭수를 지켜보았는데 하루하루 급격히 감소했습니다.

![jpg](/assets/images/Stat/138_10.jpg)

- 즉, 실험군에서 유저들이 당연히 아웃룩이 있을 줄 알고 버튼을 클릭했는데 예상과 달리 메일 앱에 들어갔고, 그 안과 밖에서 헤매이며 탐색하느라 연관된 클릭 수가 증가했다는 결론입니다.
  - [**Twyman’s Law**](https://blog.amplitude.com/twymans-law)**: 흥미롭거나 달라보이는 수치는 대부분 잘못되었다는 법칙**
  - “the more unusual or interesting the data, the more likely they are to have been the result of an error of one kind or another”.

- 예상치 못한 지표 변화는 이슈가 있음을 의미하고, 긍정적인 지표 변화도 회의적으로 바라봐야 합니다.

> How to avoid

1. 포괄적이고 다양한 metric을 구비하고 함께 봅니다.
2. 다양한 세그먼트로 쪼개어 봅니다.
3. Microsoft에서는 예상치 못한 큰 범위의 metric movements가 발생할 경우, 긍정 부정 방향과 관계없이 경고 & 실험을 자동 종료하는 시스템이 있습니다.

> ## Wrap Up

- 실험 플랫폼은
  - 이와 같은 자주 발생하는 함정을 감지할 수 있어야 하고, 경고하는 시스템을 포함해야 합니다. 
  - 또한 풍성한 Data quality metric, Diagnostic metric을 갖춰야 합니다. 
  - Microsoft는 hundreds of those metrics을 함께 본다고 해요.

- 실험자들은
  - healthy skepticism을 통해서 데이터에서 결과를 재단해야 하며 OEC metric의 움직임을 Diagnostic metric을 기반으로 가설 형태로 설명할 수 있어야 하며 Twyman’s law를 적용하고 세그먼트로 drill down해서 볼 수 있어야 합니다.

---

**reference**

- <https://medium.com/bondata/a-b-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EA%B2%B0%EA%B3%BC-%ED%95%B4%EC%84%9D%EC%97%90%EC%84%9C-%EC%9E%90%EC%A3%BC-%EB%B0%9C%EC%83%9D%ED%95%98%EB%8A%94-12%EA%B0%80%EC%A7%80-%ED%95%A8%EC%A0%95%EB%93%A4-2fe273b76a2d>
- <https://exp-platform.com/Documents/2017-08%20KDDMetricInterpretationPitfalls.pdf>

