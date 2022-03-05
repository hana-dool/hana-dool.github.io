---
title: "Setting Up Conversion Funnels for A/B Test Metrics"
excerpt: "Funnel Analysis 를 통하여 Metric 설계"
categories:
  - AB_Article
last_modified_at: 2021-10-13

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 메트릭의 Construction 을 위하여 어떻게 하면 Conversion Funnel 을 이용할 수 있는지에 대해서 알아봅시다. Artice from Apptimize CEO Nanc Hua 
{: .notice--warning}

# [Conversion Funnels for A/B Testing](#link){: .btn .btn--primary}{: .align-center}

>## Introduction

- 만약 우리가 앱을 잘 최적화 하고 싶다면, 단지 개별적인 이벤트를 추적하는것만으로는 충분하지 않습니다.
- 이벤트를 Funnel 깔떼기로 묶어, 사용자가 앱에서 어떠것을 하는지 실제로 잘 구성해야 합니다. 
- Conversion Funnel 은 사용자가 어느 위치에서 이탈하는지에 대해서 흐름을 나타냅니다.
  - 이는 다양한 이벤트를 추적 가능하게 하여 문제를 정확히 파악 가능하게 해 줍니다.
- 이렇게 하면 우리가 시급히 해결해야 할 지점이 어디인지를 알 수 있고, 사용자에 대한 이해도를 높힐 수 있습니다. 
- 앱에서 이러한 drop off(사용자의 이탈 지점) 을 파악한 후에 treatment 를 통해 이 부분을 개선해볼 수 있습니다. 
- A/B Testing 과 Conversion Funnel 은 같이 사용하게 되면 매우 효과적입니다. 
  - user flow 의 흐름을 살펴본다면 이러한 흐름 과정에서 사용자에게 실제로 어떠한 영향을 미쳤는지를 파악할 수 있습니다.

> ## Example

![png](/assets/images/Stat/82_1.png)

- 우리는 유저가 앱에서 signup 을 많이 할 수 있도록 하고싶다고 합시다. 
  - 그러므로 우리는 '가입' 을 위한 Conversion Funnel 을 개선하려 하고 있습니다.
- 사용자는 앱을 열면 바로 Sign up 화면으로 이동합니다. 
- 위 그림에서 X 표시가 되어있는 아이콘을 클릭하면 Sign up 과정을 skip 하고 메인화면으로 나가게 됩니다.

![png](/assets/images/Stat/82_2.png)

![png](/assets/images/Stat/82_3.png)

- 위 과정을 Funnel 로 나타내면 위의 그림과 같습니다. 
  - 사람들은 대부분 건너뛰기 버튼을 많이 사용하고 있음을 알 수 있습니다.
- 이때에 홈페이지 로드 수를 추적해봅시다. 그러면 오로지 75% 만이 프로세스를 완료하고 있다는것을 볼 수 있습니다. (즉 1/4 의 사람은 처음에 저러한 Sign up 화면을 만나서, 그냥 불쾌해서 나가버림...)
- 우리는 홈페이지 로드 수를 늘리고 싶습니다. 그러면 어떻게 해야할까요? 다음과 같은 4가지를 고려해 보았습니다.
  - 튜토리얼 추가
  - 건너뛰기 단추를 두드러지게 만들기
  - User sign up 을 아예 제거하기
  - 사용성을 높히기 위하여 비밀번호 박스 만들기

> A/B Testing

![png](/assets/images/Stat/82_4.png)

- 그 결과 건너뛰기 (Skip) 버튼을 바꾸는 A/B Testing 을 기획하였습니다.
  - 우리는 이 경우 건너뛰기 버튼을 좀 더 눈에 띄게 만들었습니다.
  - 오른쪽 상단 버튼을 X 로 표기하는게 아니라 등록버튼 아래로 옮기고 추가적인 버튼도 만들었습니다. 

![png](/assets/images/Stat/82_5.png)

- 그 결과는 위와 같습니다. 
  - 전반적으로 앱의 홈 스크린에 접속하는 사람 수가 18% 증가했음을 알 수 있습니다.
  - 하지만 가입자 수는 어느정도 감소하고 있는것을 볼 수 있습니다.
  - Variant 에 대해서 SIgn up here 을 누른 사람 (1399명) 에 대해서 상당수의 사람이 sign up 을 다 마치지 않은것을 볼 수 있습니다. 이는 Skip 을 누르려다가 잘못 누른것이라 생각해볼 수 있습니다.
- 즉 Conversion Funnel 을 쓰지 않았다면 '홈 스크린 전환' 이 증가했다는 사실만 알게 될 것이고, Treatment 를 바로 적용할 것입니다.
- 하지만 Conversion Funnel 을 구성하여 유저의 흐름을 지켜보면 Signup Conversion 은 감소했다는것을 볼 수 있습니다. 
  - 'Skip' 을 잘 보이게 하는것은 사용자가 홈페이지로 전환하는것을 도와주지만 , 동시에 'Sign up 하기보다 바로 Skip 하는것을 더 선호' 하게 된다는 단점이 있습니다.
  - 또한 Sign up here 과 skip 의 위치를 헷갈려 선택한 사람이 많다는것도 주목할만한 포인트입니다. 

> Implication

- A/B Testing 과 User Funnel을 통하여 Skip 버튼이 미치는 효과를 자세하게 알아볼 수 있었습니다. 
  - 'Skip 버튼은 오히려 Sign up 활동을 저해함' 
  - 'Skip 버튼과 Sign up 버튼을 헷갈려 하는 사람이 존재' 
  - 'Skip 버튼은 홈페이지 전환율을 상승시킴'  

> ## Pitfall : Not Tracking down the Entire Funnel 

- 이러한 Funnel 분석을 할 때에 한가지 함정은 Conversion Funnel 을 너무 짧게 만드는 것입니다.
  -  즉 COnversion Funnel 을 수익 또는 주요 key metric 에 연관시키지 않는 경우입니다. 
- 홈페이지에 접속하는 사용자 수를 늘리는데에만 초점을 맞추지 말고, 우리 앱에서 '수익과 직결' 되는 premeium conversion 을 나타내 봅시다.
  - 즉 core KPI 가 연결되도록 Conversion Funnel 을 늘려서 실험해 봅시다.

![png](/assets/images/Stat/82_6.png)

- 위의 데이터를 보면 skip 버튼을 잘 보이게 만든것은 우리 수익과 직결되는 KPI 인 premium conversion rate 를 오히려 감소하고 있음을 볼 수 있습니다.
  - 즉 Treatment 는 오히려 안좋았다고 볼 수 있습니다.
- Conversion Funnel 을 자세히 추적하지 않았으면, 우리가 개선하고자 했던 '홈 스크린이 보이게 하자!' 를 달성했으므로 Skip button 을 잘 보이게 그냥 선택했을 것입니다. (즉 Treatment 선택) 
- Conversion Funnel 을 자세히 추적함으로서 '사용자 흐름에 Treatment 가 어떠한 영향을 끼치는지' 에 대하여 깊이 알 수 있었습니다.

**reference**

- <https://www.microsoft.com/en-us/research/group/experimentation-platform-exp/articles/patterns-of-trustworthy-experimentation-pre-experiment-stage/>

 A/B Testing 을 기획할떄에 위와 같이 우리가 주로 보고자 하는것에 대해서, 유저가 그것을 이루기 까지 '어떠한 행동을 하는지' 를 분석하고 각 단계를 Conversion 으로 나누어 분석한다면 그 결과해석이 더 정확해지고 큰 도움이 될 것입니다. 
{: .notice--success}

