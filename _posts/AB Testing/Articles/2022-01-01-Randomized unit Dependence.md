---
title: "Randomization unit Dependency Problem"
excerpt: "무작위 단위가 독립적이지 않아서 발생하는 문제"
categories:
  - AB_Article
last_modified_at: 2022-01-01

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

Outlier 와 A/B Testing
{: .notice--warning}

# [randomization unit in online A/B tests](#link){: .btn .btn--primary}{: .align-center}

- Treatment 의 진정한 효과를 측정하기 위한 방법론으로는 A/B 테스트가 일반적으로 간주되고 있습니다.
- 이 A/B 테스트라는게 쉬울라면 쉬운데, 점점 알아갈수록 매우 어려워지고 고려해야 될점도 많아집니다. 여기에서는 Randomization Unit 을 어떻게 선택하느냐에 따라 달라지는 차이에 대해서 알아봅시다.

> ## Background

- AB 테스트는 한마디로 하자면, 아래에서 Control/Treatment 를 아래와 같이 50/50 로 분할한 뒤에 Treatment 의 차이를 측정하게 됩니다.
- 하지만 이때 아래에서 50% 로 그룹을 나눈다고 하는데, 어떻게 50% 로 나눌 수 있을까요?

![jpg](/assets/images/Stat/142_1.jpg)

- 주로 Web Application 에서 이를 수행하는 3가지 방법은 아래와 같습니다.

> Example of Randomization Unit

- **Page Views** : page view 는 단일 페이지 뷰 를 의미합니다.
  - 렌더링되는 각 페이지(사람에게 표시됨)에 대해서, 특정 페이지가 버전 A 또는 버전 B가 보여집니다.
- **Session** : 세션은 일반적으로 특정 기간으로 묶인 동일한 사람이 만든 페이지 페이지 뷰들의 집합입니다. (세션이 얼마나 유지되는지는 웹사이트에 따라 다릅니다.). 
  - 세션 수준 무작위화에서는 주어진 세션의 모든 page view 에 대해서 사이트의 version A 또는 Version B 가 보여집니다.
- **Users:** 사용자는 사용자 또는 사용자를 식별하는 식별자를 의미합니다. 
  - 사용자가 애플리케이션에 로그인해야 하는 경우 계정 ID와 같은 것으로 쉽게 식별할 수 있습니다. 
  - 대부분의 웹사이트에서는 로그인할 필요가 없으므로 대신 [쿠키를](https://en.wikipedia.org/wiki/HTTP_cookie) 사용하여 사용자를 식별[합니다](https://en.wikipedia.org/wiki/HTTP_cookie) . 
  - 한 사람이 자신의 쿠키를 지우거나 다른 장치나 브라우저를 사용하여 새 쿠키를 할당받을 수 있기 때문에 이는 대략적인 수치일 뿐입니다. 
  - 사용자 수준 무작위화에서는 모든 세션 및 페이지 보기에서 특정 "사용자"에게 버전 A 또는 버전 B를 표시할지 여부를 임의로 선택할 수 있습니다.

> Note

- 위와 같은것들은 모두 Randomization unit 의 한 예시들입니다.
  - Randomization unit 은 각 그룹에 무작위로 할당되는것을 의미합니다. 
  - 이런 무작위화 딴위의 선택은 여러가지의 영향을 받게 됩니다
- 기술적 한계
  - 세션 및 사용자를 식별할 수 있는 식별자를 심을 수 있을까? 
- Treatment 의 유형
  - 웹페이지의 배경색을 바꾸는 Treatment 의 경우 페이지 뷰,또는 세션별로 계속 바뀐다면, 유저는 혼란스러운 경험을 하게 됩니다. 
- 계산하려는 Treatment 의 효과 크기 및 사용 가능한 표본
  - 일반적으로 세션 또는 페이지뷰가 user 에 비해 훨씬 많은 샘플 수를 얻을 수있습니다.
  - 그러므로 유저가 알아채기 힘들만한 차이 (추천 알고리즘 등) 인 경우에, 좀 더 작은 Randomization Unit 을 사용하여 Sensitivity 를 높힐 수있습니다. 
- Randomization 의 독립성
  - 우리 포스팅에서는 이러한 독립성에 대해서 초점을 맞추려고 합니다. 
  - 이에 대해서는 뒤에서 차근차근 알아보도록 합죠

> ## Indepdence of Randomization Unit

![jpg](/assets/images/Stat/142_2.jpg)

- Jerry 라는 사용자가 사이트를 방문함다고 합시다. 세션이 시작되고 나서, Control (그룹 A) 에 무작위 할당됩니다. 
  - 해당 세션동안 jerry 는 버젼 A 를 경험하게 됩니다. 
- Terry 라는 다른 사용자가 사이트를 방문했습니다. Terry 는 Treatment (그룹 B) 에 할당되었습니다. 
  - Terry 는 다른날 들어와서 새 새션을 생성하게 됩니다. 이번에는 해당 세션이 버젼 A 의 환경에 할당됩니다. 
- 위처럼 각 유저가 다른 세션에 따라서 다른 Version 을 경험하고 있습니다. 이런 상황이 괜찮을까요?

> Problem

![jpg](/assets/images/Stat/142_3.jpg)

- 위와 같이 온라인 쇼핑에서는 사용자가 구매를 하기 전에 사이트를 여러번 방문하게 되는것은 흔한 일입니다.
- 우리가 이전에 테리는 각 세션마다 다른 Version 의 영향을 받았던것을 기억 하시나요? A 는 비교상품을 노출할때 가격이 상대적으로 비싼것만 노출하는 version, B 는 썸네일이 영상으로 나간 경우 라고 합시다. 
- Terry 는 다음과 같이 신발을 사기까지가 진행되었다고 합시다. 
  - 1번쨰 방문 (B) : 스토어에 방문했더니 신발의 썸네일이 영상으로 나와서 클릭해보았다. 와! 상품이 생각보다 좋네... 일단 사는건 무리같고.. 잠이나 자자.
  - 2번째 방문 (A) : 아... 어제 봤던 신발이 자꾸 아른거리네. 다시 들어가보자! 오 다른 신발과의 가격을 보니까 상당히 싼데? ... 음... 일단 다른 홈쇼핑도 보고오자
  - 3번째 방문 (B) : 역시 이사이트가 제일 좋았어! 오 신발 움직이는거봐 너무 멋있어! 이거 사야지! (구매)
- 위와 같이 "구매" 는 Version B 에서 진행되었지만 이렇게 구매까지 이끈것은 B 와 A 의 효과 덕분이였습니다. (어쩌면 A 의 효과가 더 컸을수도 있네요.) 
  - 이는 바로 유저 A 의 '기억' 이 영향을 끼쳤다고 할 수 있죠. 
- 그러므로 우리가 각 세션에서의 구매의 경우 iid 하지 않다는것을 알 수 있습니다.
  - 왜냐하면 위 예시에서 처럼 A 와 B 의 효과가 서로 뒤섞일 수 있기 때문입니다.

> ##  Session level randomization with nonindependence

![jpg](/assets/images/Stat/142_4.jpg)

- 위가 제가 이전에 말한 "이월효과" 의 그림입니다. Treatment B 의 효과가 Treatment A 로 이월(Carry over) 되고 있습니다.
- 이러한 Carry over effect 는 우리가 실제 실험의 효과를 과소 평가하게 되고, Treatment 의 영향을 덜 감지하게 됩니다.
  - 왜냐하면 Treatment 가 매우 좋았다고 하더라도, Control 에서 이 효과를 뺏어가기 때문입니다.

> ## User Level Randomization

- 세션 대신에 사용자를 무작위화한다면 이러한 독립적이지 않은 세션을 처리하는것에 도움을 줍니다.
- 이떄 세션 수준 무작위화에서의 Depedency 를 피하기 위해서, 사용자는 다른 사람들과 독립적이라고 가정해야합니다.
  - 물론 Network Effect 라고 해서, 친구가 나에게 영향을 미치는 경우도 있을 수 있는데요 이러한 경우, 여기에서는 우선 생략하도록 하겠습니다.
- 이와 같은 유저 수준의 독립에서는 아래와 같이 Randomization 이 진행됩니다.

![jpg](/assets/images/Stat/142_5.jpg)

- 위처럼 각 사용자는 동일한 경험에 일관되게 할당되었음을 볼 수 있습니다.

> ## Experiment

- 우선 아래와 같은 세팅을 기본적으로 생각해보겠습니다.
  - Control 의 경우 전환율은 10%
  - Treatment 의 경우 전환율은 12%
  - 10000명의 사용자
- 베이지안 방법론을 통해서 구현 / 수백번 시뮬레이션 후에 다음과 같은 결과를 얻을 수있었습니다.

> 세션이 완전히 독립적일때 (즉 세션간의 간섭이 없다고 가정)

- A/B 테스트는 100.0% of the time 에대해서 긍정적인 효과를 정확하게 감지합니다(95% 신뢰수준에서).
- A/B 테스트는 평균 203bps(~2%)의 효과 크기를 감지

> 세션이 독립이 아닐때 (즉 세션간의 간섭이 있다고 가정)

- 동일한 사용자가 Treatment 그룹에서 세션을 경험하게 되면, 세션 전환율이 영구적으로 증가한다고 가정 
  - 즉 예시로 사용자가 Treatment 를 한번 경험하고 나면, 그 이후에 세션들은 Treatment 던지 Control 이던지 세션 전환율이 12%
- The A/B test correctly detects a positive effect 90.0% of the time (at a 95% “confidence” level)
- A/B 테스트는 평균 137bps(~1.4%)의 효과 크기를 감지.

> 사용자 수준 무작위화를 수행할때 (즉 세션간의 간섭이 있다고 가정)

- A/B 테스트는 100.0%의 시간 동안 긍정적인 효과를 정확하게 감지합니다(95% "신뢰" 수준에서).
- A/B 테스트는 평균 199bps(~2%)의 효과 크기를 감지

> Note

- 위의 결과로부터 알 수 있는것은, 간섭이 심할때에는 세션이 훨씬 샘플수가 많음을 보장하지만 , Randomization 을 잘 수행하는게 테스트의 품질에 더 큰 영향을 미친다는 것입니다. 

---

**reference**

- https://ianwhitestone.work/choosing-randomization-unit/




