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

> ## Metric Sample Ratio Mismatch

- 가설: 링크를 새로운 탭에서 띄우는 것은 홈페이지 로드 타임을 증가시킬 것이다. (Opening links in a new tab increased home page load time.) 로 설정했다고 합시다.
  - Treatment :  MSN 홈페이지에서 클릭된 어느 링크든, 새로운 탭으로 페이지가 뜬다.
  - Control : MSN 홈페이지에서 클릭된 어느 링크든, 오픈되어 있는 탭에서 링크로 이동된다.
- 결과 : 실험군에서 PLT (Page Load TIme) 이 8,32% 증가  (이는 너무 지나친 증가)

$$PLT(variant) = \frac{\sum_{homepage \ loads \ p}PLT(p)}{\sum _{hompage \ loads }1}$$

- 이는 사실 SRM 으로 일어난 결과였습니다.
  - Treatment에서의 페이지 로드 수: 8.4M
  - Control에서의 페이지 로드 수:  9.2M
- 이를 피하기 위해서는 Metric SRM 을 탐지하는 Test 를 실행해야 할 것입니다. 
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



**reference**

- <https://medium.com/bondata/a-b-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EA%B2%B0%EA%B3%BC-%ED%95%B4%EC%84%9D%EC%97%90%EC%84%9C-%EC%9E%90%EC%A3%BC-%EB%B0%9C%EC%83%9D%ED%95%98%EB%8A%94-12%EA%B0%80%EC%A7%80-%ED%95%A8%EC%A0%95%EB%93%A4-2fe273b76a2d>

 정리정리..
{: .notice--success}

