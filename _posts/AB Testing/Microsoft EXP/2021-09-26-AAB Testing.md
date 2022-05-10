---
title:  "A/A’/B Testing &#58; Evaluating Microsoft Teams across Build Releases"
excerpt: "Microsoft Teams 에서 사용한 A/A'/B Test Frame Work"
categories:
  - AB_Microsoft
last_modified_at: 2021-09-26

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 마이크로소프트 Teams 가 마주친 이상한 상황에서 어떻게 문제를 해결하였는지 살펴봅시다. 이 실험의 교훈도 있는편이여서 읽어보시면 좋을것같아요~
{: .notice--warning}

# [Microsoft Teams A/B Testing](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

- Microsocft Team 은 커뮤니케이션 플랫폼입니다. 이 플랫폼은 Meet, Chat , Call 등을 하나로 모은 플랫폼입니다. 
- 이 Application 은 한달에도 여러번 새로운 Feature 를 업데이트합니다. 
  - 이러한 여러번의 Updating 을 통해서 현재 존재하는 Feature 들을 업데이트 합니다. 
- User Experience의 만족도를 높히기 위하여 팀은 이러한 Feature update 를 비교하고, 좋은 Feature 를 업데이트 하고 싶었습니다.
  - AB Testing 은 이러한 Feature 의 Variants 비교에 적합하였습니다.
- 그래서 Microsoft Team 은 100개 이상의 A/B Testing 을 진행합니다. 

- 하지만 A/B Test는 한번에 하나의 특징 또는 몇개의 조합만을 테스트 할 수 있습니다.
  - 왜냐하면 A/B Test 는 단위 테스트 도구이기 때문입니다. 

![png](/assets/images/Stat/69_1.png)

- A/B Testing 은 여러 기능을 한번에 비교하는 경우에는 사용되지 않습니다.
  - A version 과 B version 을 비교했을때 B 버젼이 좋다고 하여도 어떠한 기능 변화 덕분에 더 좋아졌는지를 파악하기 어렵기 때문입니다. 

- 여기에서는 통계적 Analysis 도중에 Bias 를 발생시키는 두가지 요인을 소개하겠습니다. 
  - 이러한 요인에 대해서 알아보고 Microsoft Teams 에서 사용하는 A/A'/B Testing 에 대해서 알아보겠습니다.

> ## Why is comparing builds through A/B testing insufficient?

- 우리는 A/B Test 프레임 워크를 통하여 A/A Test 를 실행하기 시작하였습니다. 
  - 이러한 A/A Test 는 Sanity check 로 쓰이는 검사입니다.
- Control 에 속하는 유저는 계속 Current Build 를 사용합니다.
  - Treatment 에 속하는 유저는 다음 Build 로 업데이트 하곘냐는 요청을 받습니다.
    - 이러한 updae 는 version number 만 다를뿐, Current Build 와 같습니다. 
    - 즉 이 업데이트를 한 유저는 Control 과 같은 경험을 할 것입니다. (버전이 같으므로)
- 이러한 A/A Test 의 결과로 우리는 통계적으로 변하지 않음을 기대했습니다.
  - 하지만 통계적으로 metric 이 차이가 있다는 결론이 나왔습니다. 
  - 이러한 결과는 왜 나타났을까요? 
  - 이러한 결과의 두가지 요인 penetration difference (침투 효과) 와 update effect (재설치 효과) 에 있었습니다.

> ## Penentration difference 

- 다음 Build 가 사용자에게 침투하는데에는 시간이걸립니다. 

![png](/assets/images/Stat/69_2.png)

- 위에서 v 는 current build version 즉 A 에 할당된 version 이라고 합시다. 
  - 그리고 v+1 은 다음 build version 즉 B 에 할당된 version 이라고 합시다. 
- day 0 의 경우는 100% 의 사람이 A 에 속해 있습니다. 
  - 1일째, B 에 속하는 유저는 두개의 part 로 나뉩니다.
    - build v 를 이용하는 유저와 build v+1 을 이용하는 유저입니다. 
- v+1 version 은 시간이 갈수록 test 기간이 길어질수록 많아집니다. 
  - 결국에는 B 실험에 속하는 사람은 100% 모두 v+1 을 이용하게 될 것입니다.
  - 하지만 이렇게 100% 에 도달하는 시간은 사용자에게 침투하는 기간에 따라 달라집니다. 
  - 몇주 , 몇달이 될 수 있습니다.
- 이러한 '침투' 에 시간이 걸리는것은 분석에 문제를 끼칠 수 있었습니다. 이에 대해서는 아래에서 깊게 다뤄봅시다.

> ## Impact on analysis

- 위와 같은 경우 비교를 수행할 수 있는 두가지 옵션이 있습니다.
  - Filtered Analysis , Standard Analysis 입니다.
- Filtered Analysis 는 user 가 업데이트 했는지 안했는지를 필터링 한 후에 비교합니다.
  - 즉 이 떄에는 A의 파란 상자와 B 의 회색 부분을 비교하게 됩니다.
- Standard Analysis 는 두 변형 모두를 포함하게 됩니다. (업데이트 유무는 상관 X)
  - 즉 이때에는 A 의 파란상자 VS B 의 회색 + 파란색 부분을 비교하게 됩니다.

> Filter Analysis

- Filtered Analysis 는 build 의 차이를 직접적으로 비교하게 됩니다.
  - 하지만 A 의 유저와 다음 build 를 사용하는 유저간에 Selection biased 가 존재합니다. 
    - 예를 들어 daily user 는 24시간 인에 업데이트 할 가능성이 높습니다.
    - 하지만 weekly user 는 업데이트 하는데에 최대 일주일이 걸릴 수 있습니다. 
  - 그러므로 이러한 유저 둘을 직접적으로 비교해서는 안됩니다.
- Filter analysis 를 계속 진해아면 build 끼리의 차이를 측정하는게 아니라 더 많이 참여하는 사용자와 덜 참여하는 사용자의 특성에 따라 그 차이가 dominated 될 수 있습니다.
  - Day 1 에 비교할 경우, B 의 회색 유저는 대부분 부지런한 Daily 사용하는 유저입니다. 즉 이러한 유저의 특성에 의해 AB Test 결과가 왜곡될 수 있다는 의미입니다.

> Standard Analysis

- 하지만 A 와 B 를 단순히 비교하는 경우에는 어떨까요? 
- 이러한 분석은 사용자를 Filtering 하지 않으므로 Selection biased 에 대한 걱정은 하지 않아도 됩니다.
- 하지만 B 에도 이전 version 이 섞여있므으로 Treatment 의 효과가 희석되는 단점이 있습니다.

> Conclusion

- 결과적으로 Filtering Analysis 는 Selection biased 를 유발할 수 있습니다.
- 그에 비해서 Standard Analysis 는 그렇지 않습니다. 
  - 하지만 이런 Standard Analysis 의 경우에도 뒤에 살펴볼 Update Effect 떄문에 완벽하지 못합니다.

> ## Update effect

- 새로운 버젼으로 업데이트 하기 위해서는 Microsoft teams 의 어플리케이션을 다시 설치하고 다시 시작해야 했습니다. 
  - Control 실험자의 경우 다시 설치 하지 않는다면 업데이트된 새로운 Feature 떄문에(물론 적용은 아직 되지 않은) 메모리 사용량이 누적됩니다. 
    - 하지만 Control 유저는 업데이트 하라는 메시지를 받지 않으므로(당연히 업데이트 될 feature 가 없으므로) 다시 설치하지 않을것입니다.
  - Treatment 실험자의 경우 새로운 Feature 를 적용하기위해 다시 시작하면 메모리 사용량이 비교적 크게 줄어듭니다.
- 이러한 차이떄문에 Application 에 대한 성능 차이가 날 수 있습니다.
  - 그러므로 build 간 비교는 이러한 재설치 및 재시작의 영향도 받게 되는 것입니다.
- 즉 build 간 비교를 온전히 할 수 없는 상황인 것입니다.
- 이전에 A/A Test 에서도 Metric 의 Movements 를 관찰했다고 했었습니다.
  - 이 Movements 는 결국 update effect 가 주요한 원인이였던것입니다. 

# [Methods Considered](#link){: .btn .btn--primary}{: .align-center}

- 이러한 침투 효과및 업데이트 영향을 해결하기 위하여 몇가지 방법을 제안하였습니다.

> ## Triggered Analysis

- 트리거 분석은 업데이트의 수신 여부에 상관 없이 앱을 다시 시작한 유저의 활동을 드릴다운하는 것입니다.
  - 즉 앱을 다시 시작(설치)한 유저에 대해서만 분석하겠다는 것입니다.
- 이렇게 하게되면 업데이트 효과의 영향이 완화됩니다만 , 재설치에 대한 영향은 무시할 수 있게됩니다.
  - 이렇게 할 경우 A/B Test 의 프레임워크를 수정할 필요는 없지만 여전히 편향 문제가 있습니다.
  - Treatment 가 유저에게 업데이트 요청을 사전에 전송하게 됩니다. 그러면  Treatment 에서 앱을 다시 시작할 확률이 높게 되는것입니다. ( Selection biased )

> ## Forced update in control variant

- 이에 대한 대안으로 Control 유저에 대해서 재설치를 유도할 수 있습니다. 
- 이러한 경우 Control 유저도 Treatment 와 똑같은 process 를 겪게 됩니다.
- 하지만 이러한 방법의 경우 이런 '가짜 업데이트' 를 추적해야할 필요성이 생깁니다.
  - 그렇지 않으면 특정한 유저는 무한 업데이트 루프에 빠질 수 있기 때문입니다.

> ## Forced update in additional control variant (A/A’/B testing)

- 우리는 Custom Control 의 변형을 도입하였습니다.
  - 이는 기존의 A/B Testing 이 아니라 A/A'/B 테스트를 실행하게 됩니다.

![png](/assets/images/Stat/69_3.png)

- 위 그림과 같이 A 는 일반적으로 change 가 없는 Control 그룹입니다.
- A' 는 빌드버젼이 v' 로 업데이트 된다는 요청을 하는것 외에는 A 와 완벽히 동일합니다. 
  - 빌드가 업데이트 되고 나서도 사실 이전 버젼 (v) 와 동일합니다.
- B 는 빌드 버젼이 v+1 로 업데이트 됩니다.
- Treatment effect 를 희석시키지 않기 위해서 우리는 filterting analysis 를 시행하였습니다. 
  - 그러므로 우리는 v' 버전과 v+1 버전을 driling 하여 비교하였습니다. 

![png](/assets/images/Stat/69_4.png)

> Sanity Check

- Sanity Check 를 위하여 A 와 A' 를 비교하였습니다. 
- 물론 완벽한 A/A Test 가 아니기 떄문에 주로 , 업데이트 요청을 보낸 효과가 얼마나였는지를 측정하게 될 것입니다.
- 비교시에는 Penentration difference 를 피하기 위해서 A 와 A' 를 비교한다는것에 유의하세요! 
  - (즉 색깔별로 비교하는게 아니란것입니다.)

> Decision making

- 이 경우에는 A' 와 B 를 비교하게 됩니다. 
- 이 두 비교시에는 Update effect 또한 없고 (A' 와 B 가 같은 업데이트 요청을 받으므로) 또한 침투 효과도 없습니다. (색깔별 비교가 아니라 A' 와 B 를 비교하므로)

# [We selected A/A’/B testing](#link){: .btn .btn--primary}{: .align-center}

- 구현 및 분석이 간단한 A/A'/B 테스트를 선택하였습니다.
- 위와 같이 제안된 프레임워크를 이용해 테스트를 시행하였습니다. 
- A 와 A' 의 비교중에 Selection biased 를 제거하기 위하여 Standard Analysis 를 수행하였습니다.
  - 그 결과 30% 의 메트릭이 통계적으로 유의한 움직임을 보였습니다.
  - 이때 테스트의 유의수준은 0.001 로 설정하였습니다. (기존의 0.05 보다 훨씬 낮은 수준)
  - 그러므로 이러한 metric 의 Movement 는 높은 확률로 True 라 예측할 수 있습니다. 
- 위와 같은 결론은 바로 Update Effect 에 의한 차이일 것입니다.
- A' 와 B 의 비교시에는 Metric 의 Movement 는 False positive rate 와 비슷하였습니다. (significant level)
- 이러한 Test 를 통하여 build 간의 비교를 정확하게 할 수 있었습니다.

> ## Deploy

- 우리는 Production 을 배포할떄에는 A' 와 B 만 유지하여 변경하였습니다. 
- 이 이유는 A 와 A' 의 비교에서는 별로 큰 이득을 보지 못하기 때문입니다.
  - 이미 Update 에 의한 차이는 잘 알았기 때문입니다. 
- 이 이후에는 A'/B 테스트를 시행하게되고, 트래픽을 모두 여기에 투입할 수 있게 되어서 메트릭의 Sensitivity 를 최대한으로 올릴 수 있게 되었습니다.

---

**Reference**

- <https://www.microsoft.com/en-us/research/group/experimentation-platform-exp/articles/a-a-b-testing-evaluating-microsoft-teams-across-build-releases/>

처음 봤을떄는 엄청 흥미로운 주제일것 같았는데 (A/A/B 테스트의 변형?) , A/B/C 테스트였던것 같네요. 개발자가 아니라 그런지 중간중간 이해 못하는 (업데이트시 메모리 누적?) 부분이 있었지만 그래도 읽을만 했던것 같습니다. 문제점을 밝혀내기 위하여 (A / A' / B) 테스트를 시행한것은 다른 부분에도 적용할 수 있을것같아요. 이를 더 확장하여, 업데이트문제만이 아니라 다양한 문제가 얽혀있을것 같을때에는 각각의 문제를 하나하나씩 떼어보아서 (A / A' / A'' / A''' / B) 테스트도 가능하겠네요! 
{: .notice--success}

