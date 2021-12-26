---
title: "A Dirty Dozen &#58; Twelve Common Metric Interpretation Pitfalls in Online Controlled Experiments"
excerpt: "Microsoft 에서 실험에서 만나게 되는 12가지 Pitfall"
categories:
  - AB_Testing
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

- Telemetry = 무선 및 유선으로 디지털 신호 데이터를 측정, 변환, 전송 + 축적, 분석하는 기술을 의미

![jpg](/assets/images/Stat/138_3.jpg)

- 가설: iPhone Skype notification에 사용하는 protocol을 바꾸었을 때, 통화 품질 지표(call quality metrics)를 변화시킬 것이다.
  - Treatment: VolP protocol 사용
  - Control: 다른 protocol 사용
- 결과: 일부 통화 관련 지표에서 예상치 못한 강한 변동이 있었다. 다른 지표들은 변화가 없었다.
- 가드레일 메트릭, 로컬 메트릭을 통해서 강한 변동을 빠르게 파악하고 대응이 가능했다.

> About the pitfall

- 실험군에서 사용한 protocol의 경우. 푸시를 받고 데이터를 batch 형태로 모아서 보내기까지 몇 초 더 대기합니다. 기술적인 이슈가 실험의 결과를 해석하는 데에 편향을 줍니다.
- 이 케이스의 경우, 클라이언트 event based, click based metric은 전부 신뢰성을 잃게 됩니다.

> How to avoid

1. 클라이언트에서의 call event 수, 서버에서의 call event 수를 비교하고 loss rate를 Data Quality Metric으로 포함합니다.
2. 클라이언트에서 할당하는 이벤트의 sequence number 사이에 빈틈이 있는지 파악합니다.
3. 메트릭들은 가능하다면 클라 사이드 이벤트보다 서버 사이드의 이벤트 기반으로 카운트 되어야 합니다. less lossy, more uniform합니다.

> ## 4. Assuming Underpowered Metrics had no Change

- MSN 홈페이지에서 일어나는 실험들 중에서, total number of page views per user 은 중요한 OEC metric입니다. 특정 실험에서 대조군 대비 실험군에서 0.5%의 metric 향상이 있었다고 합시다.
  - 하지만 P-value가 통계적으로 유의하지 않았습니다.
- mature 단계에 있는 MSN과 같은 온라인 비즈니스에서는 **0.5%의 향상도 비즈니스에 큰 임팩트로 해석됩니다.**

> About the Pitfall

- 검정 과정을 살펴보니 신뢰 구간을 계산하는 데에 사용한 검정력(power)가 80%를 사용했습니다. 
- 이 케이스에서의 실험군, 대조군 샘플 수와 power = 80% 의 조건에서는, 대조군과 실험군이 7.8% 이상의 차이가 나야 p-value가 통계적으로 유의하다고 나옵니다. 
  - 하지만 성숙한 비즈니스에서 7.8% 이상의 차이를 내기는 쉽지 않습니다.
- 즉, 샘플 수를 power analysis를 통해 결정하지 않았기 때문에 발생한 문제입니다.

> How to avoid

- Priori power analysis을 진행하여, OEC와 가드레일 메트릭에서 비즈니스에서 충분히 크다고 판단되는 임팩트(%)를 감지할 수 있을 샘플 사이즈를 선정합니다.
- 이러한 선행 전력 분석의 권장사항은 주어진 제품에 대한 일반적인 실험 시나리오에 대해 단순화할 수 있습니다. 
  - 예를 들어 미국에서 실행되는 Bing 실험의 경우 테스트 중인 기능이 대부분의 사용자에게 영향을 미칠 경우 최소 10%의 사용자에 대해서 1주일동안 실험하는게 좋습니다.
- 떄로는 탐지하고자 MDE 와 Power 를 기반으로 Sample Size 를 계산해 보았더니, 권장하는 샘플 수가, 서비스에서 가용할 수 있는 모든 트래픽 이상일수도 있습니다
- 이러한 경우에도, 실험자들이, 현재 모든 트래픽을 사용했을떄에 우리가 얻을 수 있는 MDE 가 어느정도 수준인지 파악하는것도 중요합니다. 
- 이때 Power 의 수준은 결과를 적절하게 평가하기 위해 OEC 와 가드레일 메트릭의 작은 변화를 탐지할 수 있는 최소 80%의 Power 로 설정하는게 좋습니다.

> ## Claiming Success with a Borderline P-value

- 마이크로소프트의 또다른 웹 페이지 [Bing.com](http://bing.com/) 에서 실험 A를 진행했습니다. 실험군, 대조군 간의 OEC metric 증분을 검정한 결과 0.029의 p-value가 나왔습니다.
  - 이 OEC metric은 유저의 만족도 지표고, 유저의 잔존에 직결되는 leading indicator입니다. 대부분의 실험이 이 metric을 개선하는 데에 성공하지 못했습니다.
  - P-value로 실험 A의 성공을 확신하지 않고, 검증용으로 동일한 실험을 독립적으로 시행했습니다. 실험군, 대조군 트래픽을 2배로 늘려서 실험을 시행한 결과, 동일한 OEC metric 증분을 검정했지만 통계적으로 유의하지 않았습니다.

> About the pitfall

- P-value가 0.05에 가까운 boundary에 있을 때, 다른 추가 근거를 고려하지 않고 귀무가설을 단순하게 기각하는 경우 발생합니다. Borderline p-value(0.05의 경계에 가까운 값)을 보일 때, 1종 오류(False Positive)의 경고일 수 있습니다.
- P-value가 0.05의 경계에 가깝지 않은 OEC metric에 더 중점을 두고 실험을 평가합니다.
- 실험군, 대조군 유저 수 트래픽을 키워서 동일한 실험을 새로운 유저들에게 시행합니다.
- 두 가지 방법이 다 불가능하거나 2번을 시행해도 여전히 borderline p-value가 나온다면 [Fisher’s Method](https://en.wikipedia.org/wiki/Fisher's_method)를 활용합니다. (샘플 수가 적거나, 카테고리가 많고 범주형 자료일 때 사용하는 검정법)

---

**reference**

- <https://medium.com/bondata/a-b-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EA%B2%B0%EA%B3%BC-%ED%95%B4%EC%84%9D%EC%97%90%EC%84%9C-%EC%9E%90%EC%A3%BC-%EB%B0%9C%EC%83%9D%ED%95%98%EB%8A%94-12%EA%B0%80%EC%A7%80-%ED%95%A8%EC%A0%95%EB%93%A4-2fe273b76a2d>

 정리정리..
{: .notice--success}

