---
title: "Google HEART Framework to Measure User Experience"
excerpt: "UX(User Experience) 를 제대로 측정하기 위한 HEART의 Metric 설계과정"
categories:
  - AB_Article
last_modified_at: 2021-10-10
date : 2021-10-10 11:00:00 +0900

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 이전의 논문에서 우리는 HEART 방법론이 어떤것인지 알아보았습니다. 여기에서는 HEART 에 대해서 논문리뷰가 아니라 실제적인 관점에서 간단히 알아보고, 그러한 Frame work 에 따라 Metric 을 가상으로 구축해보려 합니다.
{: .notice--warning}

# [HEART Frame work](#link){: .btn .btn--primary}{: .align-center}

> ## Summary

- Heart 프레임 워크란, User Experience 를 제대로 측정하고자 하는 목표로, 구글에서 만든 Metric 생성 프레임 워크입니다.

> Metric 의 5가지 범주

- Happiness : 만족도 및 사용 용이성과 같은 사용자의 주관적 측면 
  - 주로 survey / app rating / review 등으로 측정할 수 있습니다. 
- Engagement : 사용자가 제품과 얼마나 깊게 집중하였는지의 측면입니다. 
  - 방문자 수 , 좋아요 수 , 앱에 얼마나 시간을 보냈는지, 
- Adoption  : 얼마나 많은 신규 유저가 제품을 사용하였는지
  - 신규 유저의 수, 앱 다운 수  등
- Retention : 얼마나 많은 유저가 '남아'서 제품을 사용하는지 
  - 가입자 이탈율(Chrun) 등 
- Task Success : 유저가 얼마나 그들의 목표(goal) 를 제품을 이용해 빠르고 효과적으로 달성했는지
  - 오류율 , 작업 완료 시간 , 작업 완료 수

> Frame work 사용법

- 목표 설정 
  - 목표를 미리 설정하여 모든 구성원이 공통의 목적을 설정하도록 합니다. 
- 신호 정의
  - 우리가 정한 목표에는 관련된 사용자의 신호가 있을것입니다. 
  - 이러한 관련된 사용자의 신호를 찾고 정의합니다. 
- metric 선택
  - 위에서 정한 신호를 잘 proxy 하는 metric 을 설정합니다. 

> ## Detail

> Happiness

![png](/assets/images/Stat/75_2.png)

- Happiness 는 위와 같이 사용자가 제품에 대해 생각하게 되는 주관적 측면입니다.
- Goal 
  - 이를 위해 Goal 은 위와 같이 '유저가 앱이재밋고 행복하고 다루기 쉽다고 느끼게 하는것' 으로 설정할 수 있습니다. 
- Signal
  - 위와 같은 Goal 을 이룬다면, 사용자는 좋은 피드백과, 앱을 추천하게 될 것입니다. 
- Metric
  - 위의 시드널을 매져하기 위한 metric 은 앱 평점 , 긍정적인 서베이의 결과 등이 될 수 있습니다. 

> Engagement 

![png](/assets/images/Stat/75_3.png)

- Engagement 는 사용자가 제품과 얼마나 깊게 집중하였는지 입니다. 
- Goal 
  - 유저가 앱과 지속적으로 소통하고, 관련되기를 원합니다. 
- Signal 
  - 위와 같은 goal 을 이룬다면 앱에 시간을 많이 쓰고, newsletter 메일을 더 많이 읽을 것입니다. 
- Metric
  - 위와 같은 Signal 을 매져하기 위한 metric 은 세션길이 , 뉴스래터를 여는 비율 등이 될 수 있습니다. 

> Adoption

![png](/assets/images/Stat/75_4.png)

- Adoption 은 얼마나 많은 신규 유저가 제품을 사용하였는지를 나타냅니다. 
- Goal
  - 새로운 유저가 제품의 가치를 알아주기를 원합니다. 
- Signal 
  - 위와 같은 goal 을 이룬다면 앱 다운 수 / paid account 수 등이 늘 것입니다. 
- Metric
  - 위와 같은 signal 을 매져하기 위한 metric 은 다운 수 , 등록 수 등이 있습니다. 

> Retention

![png](/assets/images/Stat/75_5.png)

- Retention 는 유저들의 지속적이고 반복적인 참여를 나타냅니다. 
- Goal
  - 유저가 계속 남아서 우리 제품을 사용해주기를 원함
- Signal 
  - 앱에활성화 된 채로 남기 / 구독 연장 / 유저의 충실도 
- Metric 
  - 이탈율 / 구독 갱신율 / 재방문 유저 수 

> Task Success

![png](/assets/images/Stat/75_6.png)

- Task Success 는 유저가 제품의 워크 flow 에 따라 작업을 완료하는 효율성 , 오류율을 나타냅니다. 
- Goal 
  - 유저가 그들의 GOal 을 빠르고 쉽게 완수하게 하기
- Signal 
  - 완료된 task 수가 많아진다. / 일이 효율적이 된다. / 에러 수가 적어진다. 
- Metric 
  - 완료된 Task 수 비율 / Task 완료에 걸리는 시간 / Error rate 

> ## Tables

![png](/assets/images/Stat/75_1.png)

- 일반적으로 위와 같이 표로 작성하여 메트릭을 구성하는것이 일반적입니다. 

**Reference**

- <https://uxdesign.cc/googles-heart-framework-choosing-the-right-metrics-for-your-product-112bd7300d55>
- ,<https://brunch.co.kr/@blackindigo-red/14>
- <https://clevertap.com/blog/google-heart-framework/>
- <https://medium.muz.li/how-to-use-google-s-heart-framework-to-measure-ux-metrics-e4bab590aa58>

논문은 좀 장황해서 뭔소리인지 헷갈렸는데 직접 적용하는걸 보니까 어렵지 않네요. User Funnel 로 Metric 구성하는것도 좋지만 이렇게 바라보는것도 좋네요 
{: .notice--success}

