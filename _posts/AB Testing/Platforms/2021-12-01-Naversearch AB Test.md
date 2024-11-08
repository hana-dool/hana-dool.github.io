---
title: "Naver Search A/B Test (2021)"
excerpt: "네이버 서치의 A/B Testing"
categories:
  - AB_Platform
last_modified_at: 2021-12-01

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

네이버 서치에 대한 A/B Testing
{: .notice--warning}

# [Naver Search A/B Testing](#link){: .btn .btn--primary}{: .align-center}

> ## Contents

1. A/B 테스트가 보기보다 어려운 이유
2. 네이버 서치 $\mathrm{ABT}$ 프로젝트 소개
3. 네이버 서치 $\mathrm{ABT}$ 플랫폼 신뢰도 검증하기
4. 네이버 서치 $\mathrm{ABT}$ 실험 분석 방법론
5. 네이버 서치 $\mathrm{ABT}$ 향후 개발 계획

> ## A/B Testing

- A/B Testing 의 기본적인 개념은 단순함! 

1. 사용자를 무작위로 나누어 실험군(A/B)을 설정한다
2. 실험군 별로 다른 서비스를 제공하고 반응을 기록한다
3. 사용자의 반응을 서로 비교하여 결론을 도출한다

> ## A/B Testing 에 존재하는 다양한 함정

![jpg](/assets/images/Stat/117_1.jpg)

1. 사용자군 설정이 완전 무작위로 이루어지지 않음
2. 실험군에 따른 분기가 제대로 이루어지지 않음
3. 사용자 로깅이 일부 누락되거나 오류가 발생
4. 의사결정 기준 지표가 사전에 충분히 정의되지 않음
5. 분석 결과에 대한 유의성 검증이 제대로 되지 않음
6. 실험을 너무 일찍 중단하고 의사결정을 내림

> ## 현대적인 A/B Testing 플랫폼의 조건! 

1. (앞서 언급한) 실험의 오류가능성을 사전에 최소화
2. 여러 팀/프로젝트에서 동시에 간섭없이 실험을 진행
3. 개별 실험의 버전업을 통해 여러 차례 반복 개선을 지원
4. 사용자 지표에 악영향을 주는 실험을 자동 경고 \& 셧다운
5. 실험 결과에 대한 대시보드와 Custom Analysis 템플릿 지원

# [Naver Search A/B Testing 개발](#link){: .btn .btn--primary}{: .align-center}

> ## Motivation

- Motivation: 네이버 검색을 우한 현 대적인 $\mathrm{ABT}$
- AS-IS: 사실 이미 개별 팀에서 $\mathrm{ABT}$ 를 독자적으로 진행하고 있긴 했습니다.
  - 이렇게 개별 팀에서 지표를 각각 다르게 보기 떄문에 개별 파트에서의 영향은 알 수 있겠지만 전체적인 사용자 영향의 확인이 어려움 (메트릭이 달라서!)
  - 실험 결과의 검증 및 고급 분석의 어려움
- TO-BE: 네이버 검색 전체를 위한 현대적인 $\mathrm{ABT}$ 개발 (모두 통일된 플랫폼에서 실험이 가능하게 하기 위하여)
  - 실험 설계/수행/분석의 일원화 (Data \& Analytics팀)
  - 모든 팀이 같은 지표/프로세스를 통해 의사결정

> ##  네이버 검색 ABT 아키텍쳐

![jpg](/assets/images/Stat/117_2.jpg)

- 위와 같이 크게 3개로 이루어져 있습니다.

1. 실험 관리자가 등록/변경한 실험 설정 정보를 제공하는 OES 서버
2. 검색 서버에서 OES의 버킷 정보를 받아 서비스 분기 및 로깅
3. 검색 로그를 정제하여 실험 결과를 생성하는 파이프라인

> ## 실험 설정 UI

> 1.실험 세팅하기

![jpg](/assets/images/Stat/117_3.jpg)

- 위와 같이 실험 기간등을 설정

> 2.실험 파악

![jpg](/assets/images/Stat/117_4.jpg)

- 그 이후에는 위와 같이, 현재 돌아가고 있는 Active 한 실험을 개별 팀별로 보여주고 있습니다.

> 3.레이어별로 할당된 트래픽 파악

![jpg](/assets/images/Stat/117_6.jpg)

- 실험의 유형별로 레이어라는것을 정의
  - 레이어 안에서 트래픽 전체를 나눠서 정의할 수 있음
- 트래픽은 slot 이라는 단위로 구분됨

> ## Lifecycle

![jpg](/assets/images/Stat/117_7.jpg)

> 그림설명

- Study Creation : 실험이 생성됨
- Study is Deployed : 실제 황경에 적용됨
- No KPI Alert : 주요 KPI 에 영향을 끼치는지 아닌지를 검사
- Study is put on Hold : 주요 KPI 에 영향을 끼치는것이 확인되면 실험이 멈춤
- Discuss Study Results : 실험 결과에 대해서 토론
- Decision is made : 최종적인 실험에 대한 판단
- Update Study Version : 실험을 다시 업데이트하여 (feature 업데이트 등) 실험

> 플랫폼 구현시 고려한것

- 실험 버전업의 필요성
  - 대부분의 실험은 여러 iteration을 거치므로, 이를 지원해야함
- 그럼 실험 버전업은 어떤 경우에 해야할까? 
  - 예기치 못한 실험 결과가 나올때 , 한번 더 검증해보자! 
  - 실험군의 설정 혹은 구현이 바뀌는 경우 
  - 트래픽 재분배(re-shuffle)가 필요한 경우 
- 실험 버전업은 어떻게 결정할까? 
  - 보통 담당자들이 회의를 거쳐 의사결정

> ## 분석 파이프라인

![jpg](/assets/images/Stat/117_8.jpg)

> 1.사용자 로그 및 메타데이터가 수집되어 저장

- 실험에서 나온 사용자의 메타 데이터들이 하둡 서버에 저장됨

> 2.대용량 데이터 파이프라인에서 기본적인 정제 작업

- Raw 데이터를 해석하기 편리한 데이터 레벨로 높히는 작업
- 페이지 뷰 $\to$ Session $\to$ 사용자 $\to$ 사용자 cohort
  - 실험 로그를 위와 같은 레벨로 집계됨
  - 집계된 로그는 사용자 코호트별로 분류되어 보여주는 기능도 구현함

> 3.실험군별 지표가 계산되어 대시보드 및 노트북으로 결과 확인

- 대시보드를 통해 분석이 가능

> ## 실험 진행 프로세스

![jpg](/assets/images/Stat/117_9.jpg)

- 실험을 위해 서비스 담당자 및 실험 담당자가 협업
- 실험 요청 / 구현 / 테스트 / 배포 / 리포팅의 순서
- 주간 회의를 통해 계획/진행중인 실험에 대한 논의
- 런치 2 달만에 여러 파트너 팀과 두자리수 실험 진행
- 실험 준비에서 완료까지 보통 3-4주 가량 소요

# [플랫폼 신뢰도를 검정하기](#link){: .btn .btn--primary}{: .align-center}

> ## 신뢰도 검정

![jpg](/assets/images/Stat/117_10.jpg)

> 신회성 검정이 왜 필요할까? 

- 의사결정을 위해서 실험을 하는것이므로, 신뢰성 있는 실험이 필요
- 신뢰성 있는 실험이 되어야 더 많은 실험을 할 수 있음
- 이러한 더 많은 실험을 통해 더욱 신뢰성 있는 실험을 제공 (선순환!)

> 신뢰성 검정의 방법

- 여러 실험 집단을 레이어로 구분하여 실험중임. 이때 실험 레이어간 결과의 간섭은 없을까?
  - 실험 레이어 간 트래픽 배분 비율 검증 
- 개별 실험 내에서 트래픽은 제대로 분배되었을까?
  - 실험 내부의 트래픽 배분 비율 검증
- 실험 트래픽 배분은 무작위(random)로 되었을까? (비율이 맞더라도 편향이 있을 수 있으므로! )
  - Large-scale A/A 테스트 수행 결과
- 같은 실험은 반복하면 같은 결과가 나올까? (재현성에 대한 검정)
  - 재현(replication) 실험을 통한 검증

> ## 실험 레이어간 트래픽 교차 분배 검정

- 목표: 서로 다른 레이어의 실험은 트래픽 교차 배분을 통해 독립성 보장! 
- 방법 : 실험A (Layer1)와 실험B에 (Layer2) 할당된 사용자의 교차 배분 비율을 비교 Chi-Square Test의 p-value를 사용해 이상 여부를 검증

![jpg](/assets/images/Stat/117_11.jpg)

- 위와 같은 실험의 경우, 서로 독립적으로 잘 분배되는것을 볼 수 있음! 
- 한 사용자가 두가지 실험에 동시에 할당되더라도, 두 실험의 결과에는 영향을 끼치지 않는다는것을 보여주기 위함

> ## 실험군별 트래픽 분배 정합성 검증

- 목표: 실험군별 트래픽이 실험 설정에 맞게 분배되었는지 확인
  - 우리가 1:1 로 나뉘도록 설정했더라도, 이렇게 분배되지 않을 수 있음
- 날짜별/전체 기간 동안 실험군별 사용자 수의 비율을 비교 Chi-Square Test의 p-value를 사용해 이상 여부를 검증

![jpg](/assets/images/Stat/117_12.jpg)

- 위와 같이 A , B , A' 를 나눈 비율이 잘 맞는지를 p-value 통해서 검정이 가능

> ## Large scale A/A Test 를 통한 검정

- 목표: 서로 동일한 실험군에 대해서 실제로 지표 차이가 없는 것을 증명하자
  - 서로 동일 한 실험군 100 개를 (A01~A100) 갖는 실험을 생성
    - 대조군 (control) 끼리에 대한 실험
  - 주요 지표에 대해 실험군간에 유의미한 차이가 있는지를 검증
  - 결과: P-value 가 기준치 이하 로 나타난 실험군은 5% 미만이 되어야 정상임

![jpg](/assets/images/Stat/117_13.jpg)

- 위 실험을 볼때, 우리 예상대로 5% 이하의 p-value 를 가지는 실험이 매우 적으므로 , 실험이 잘 설계되었다고 생각할 수있음

> ## 재현 (replication) 실험을 통한 검증

> 목표: 결과의 재현성을 확인하여 $\mathrm{ABT}$ 플랫폼 및 실험의 신뢰성을 검증!

- 특정 실험에 대해 동일한 조건에서 서로 다른 시기에 2 회 반복 실시
- 1 회와 2 회 결과를 비교하여 큰 경향성이 거의 유사함을 확인
- P-value 가 유의성 임계치 (0.05) 근처에 있는 지표의 경우 결과가 재현되지 않음

![jpg](/assets/images/Stat/117_14.jpg)

- 같은 실험을 두번 진행하였음. 첫번째와 두번쨰에 대해서 결과를 비교하는데 , 특정한 메트릭은 첫번쨰 실험에 대해서 유의하지 않다고 하는데, 두번쨰 실험에서는 유의하다고 하고 있음! (재현되지 않는 경우도 있다..)

# [실험 분석 방법론](#link){: .btn .btn--primary}{: .align-center}

> ## 실험 분석 방법론 개요

![jpg](/assets/images/Stat/117_15.jpg)

> 실험 전체 지표

- 대조군과 실험군과의 지표값을 비교하여, 전체적으로 어떤 결과를 보이는지를 살펴봅니다.

> 일별 지표 트랜드

- 이 결과가 시간이 지나도 바뀌지 않을 Stable 한 변화인지 확인
  - 일별로 추이를 살펴봄! 

> 부문별 세부 지표로 원인 해석

- 이 결과의 원인을 어떻게 설명할 수 있을지를 알기 위하여 결과를 세세하게 살펴봄!
  - 사용자군별 (Cohort) 로 나누어서 확인
  - 다양한 지표 및 세부지표 확인

> ## 전체 지표 검증

![jpg](/assets/images/Stat/117_16.jpg)

> 살펴보는것

- 서로 다른 단위를 가지는 지표간의 비교를 위해 절대적인 차이를 상대적인 차이(%Delta)로 환산
  - 즉, 별건 아니고 A,B 의 메트릭 차이를 % 로 보겠다는것. (물론 위 그림에는 없지만 절대적인 차이도 봄)
- 이런 차이의 통계적인 유의성을 확인하기 위해 p-value를 계산

> 재현성 검증을 위하여 실험을 두번 하여서 검증함. (V1 and V2)

- V1 의 실험 결과와 V2 의 실험 결과를 짝지어서 비교함
  - 이때 한쪽에서는 p-value 가 낮고, 한쪽에서는 높게 나온다면 약간 의심해야할것

> 각 실험에 대해서 A,B,A' 을 설정하여 A/A 검증 (즉 대조군을 2개 설정)

- 즉 모든 실험에 대조군 2 개 $\left(\mathrm{A}\right.$ 와 $\left.\mathrm{A}^{\prime}\right)$ 를 설정하여 A/A'테스트를 수행
  - (Note : 이 경우 Control vs Control 실험을 통해서 A/A 검증을 하는듯함)

> ## Note : False Discovery Rate

- 일반적인 $\mathrm{AB}$ 테스 트 환경에 서는 수 백/수 천 개의 지표 에 대해 서 동시에 통계적 유의성을 테스트
- 이는 개별 결과에 대해 우연히 유의 성을 발견하게될확률 (False Positive Rate)을 높임! 
- 네이버서치 $\mathrm{ABT}$ 에서는 이런 잘못된 발견의 비율 (False Discovery Rate)을 통제하기 위해 $\mathrm{p}$-value를 오른쪽과 같이 보정 (Work in Progress)
- False Discovery Rate (FDR)

$$=E\left(\frac{ F \text { alsePositive }}{ \text { FalsePositive + TruePositive }}\right)$$

- 이러한 보정을 통해서 수백 수천개의 지표를 동시에 보더라도 False Discovery rate 가 5% 미만이 되게 조절!

> ## 일별 지표 트랜드 해석하기

- 통합검색 내 특정 영역의 일별 CTR 트렌드 (좌: CTR절대값/ 우: CTR차이)
- 일별 트렌드에서도 $\mathrm{A} / \mathrm{A}^{\prime}$ 의 차이가 거의 없음
- $\mathrm{A} / \mathrm{B}$ 군의 차이 역시 비교적 안정적으로 보임

![jpg](/assets/images/Stat/117_17.jpg)

- 실험의 결과 화면에서는 위와 같은 지표 모니터링을 보여줍니다.
  - 왼쪽은 절댓값 / 오른족은 상대값을 보여줍니다. 
- 절댓값에서는 일별로 달라질수밖에 없음 (사용자들이 주중과 주말에 따라서 행동 방식이 다르기 떄문)
- 상댓값을($\Delta A/B$) 볼때에는, 이러한 스케일을 보정하게 되므로 , 좀 더 안정적인 추이를 보여줍니다.
  - 근데 상댓값에 뭔가 일별 트랜드가 보인다면, 이는 실험 결과가 안정되어있다고 볼 수 없을것입니다.
  - 그러므로 상댓값의 일별 트랜드가 있으면 실험을 완료될 준비가 안되었다고 판단! 
- 위 그래프에서는 어느정도 안정된것처럼 보임

> ## Note : 일별 지표 트렌드의 원인

![jpg](/assets/images/Stat/117_18.jpg)

- 위와 같은 실험의 경우, 트랜드가 존재하는것을 볼 수 있음! 

> 원인

- Novelty / Learning Effect:
  - 새로운 UX피처에 대한 새로움/학습 효과
- User Mix Shift:
  - 날짜별로 서비스 방문 사용자 군의 차이
- Seasonal / Dow Effect:
  - 계절/요일별 사용패턴 차이
- Carryover Effect:
  - 예전 실험의 효과가 신규 실험에 전이

> ## 부분별 세부 지표 해석하기

![jpg](/assets/images/Stat/117_19.jpg)

- 개별 실험의 결과를 이해하기 위해 다양한 기준으로 결과를 나눠볼 수 있어야함!
  - 위 지표에 대해서는 다양한 기준 (A,B,C,D1,D2 질의에 대한 쿼리 랭킹) 에 대해서 위 그림은  질의군들에 따라 다른 경향
  - 아래 지표에 대해서는 질의군에 대해, 관계없이 거의 같은 경향을 보여줍니다. 
- 위 지표에 대해서 (First Click Rank) 질의군별로 다른 영향
- 아래 지표에 대해서는 (Time to First Click) 질의군에 관계 없이 거의 같은 영향
- 비슷한 Breakdown을 사용자군 / 검색 랭킹 및 검색 결과 유형별로도 제공

> ## Note : 부분별 세부 지표 해석시 유의사항

![jpg](/assets/images/Stat/117_20.jpg)

- 위와 같은 코호트 분석이 필요한 이유는 개별적인 효과와 전체적인 효과가 다를 수 있기 때문
- 우리는 전체 실험결과 (왼쪽) 를 보면 사용자군별로 (어린이, 어른, 여성, 남성...) 다른 사용자군별로 영향이 달라질 수 있음! (Breakdown)
- 즉 실험에 따라 부문별로 다른 영향을 가져올 수 있으며, Breakdown을 통해 이를 발견할 수 있음. 
- Note : 단 여기서도 여러 집단을 쪼개서 보는것(즉 실험의 갯수가 늘어나는것) 이므로 False Discovery 이슈를 고려해야

# [Summary](#link){: .btn .btn--primary}{: .align-center}

- 네이버 검색 전체를 위한 현대적인 $\mathrm{ABT}$ 개발
- 개별 팀의 독립적인 실험 수행 및 iteration을 지원
- 모든 팀이 같은 지표/프로세스를 통해 의사결정
- 런치 두달만에 네이버 서치 대부분의 팀과 실험 수행

> Next Steps

- 고급 지표 개발 (예: 사용자의 종합적인 만족/불만족을 지표화)
- 고급 질의군 및 사용자군 Cohort 개발 (대용량 클러스터링 기반)
- 더 많은 지표에 대해 실시간 이상 탐지 및 Shutdown 기능 제공 (지금은 부분적으로만 제공..)
- 더 자동화된 실험 결과 분석 및 편리한 Custom Analysis 지원
- 전통적인 실험이 어려운 경우에 대한 기법 연구 (Causal Inference)
- 평가를 넘어 온라인 환경에서의 파라메터 최적화를 지원 (Contextual Bandit)

---

**reference**

- <https://medium.com/criteo-engineering/why-your-ab-test-needs-confidence-intervals-bec9fe18db41>

  

