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

---

**reference**

- <https://medium.com/bondata/a-b-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EA%B2%B0%EA%B3%BC-%ED%95%B4%EC%84%9D%EC%97%90%EC%84%9C-%EC%9E%90%EC%A3%BC-%EB%B0%9C%EC%83%9D%ED%95%98%EB%8A%94-12%EA%B0%80%EC%A7%80-%ED%95%A8%EC%A0%95%EB%93%A4-2fe273b76a2d>

 정리정리..
{: .notice--success}

