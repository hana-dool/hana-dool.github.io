---
title: "Hackle A/B Test (2021)"
excerpt: "핵클의 A/B Testing 웨비나"
categories:
  - AB_Platform
last_modified_at: 2021-12-01

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

핵클 웨비나에서의 A/B Testing
{: .notice--warning}

# [Hackle A/B Testing](#link){: .btn .btn--primary}{: .align-center}

> ## Agile 개발을 하는 이유 

![jpg](/assets/images/Stat/118_1.jpg)

> 일반적인 서비스 출시 과정

- 고객 요구 사항 반영까지 긴 시간 소요
- 계속해서 나타나는 새로운 고객 요구 사항 반영 불가
- 느린 서비스 개발 속도로 인한고격 신뢰 유실

> Agile한 서비스 출시 과정

- 고객 요구 사항 반영까지 짱은 시간 소요
- 계속해서 나타나는 새로운고객 요구 사항 반영 가능
- 빠른 서비스 개발 속도로 인한고객 신뢰 확보

> Summary

- 즉 에자일한 개발로 제품을 계속 만드는것이 매우 중요! 
- 1년에 1~2 번 기능을 출시하는 기업과 하루에도 수백번 기능을 출시하는 기업 성장속도는 차이가 날수밖에 없음! 

> ## 우리의 목적 : 좋은것만 드려요~

- 그러면 우리가 고객의 요구사항을 서비스에 제대로 반영하려면 어떻게 해야할까요? 
  - 즉 빠르게 성장하는 서비스를 만드려면 어떻게 해야할까요?

![jpg](/assets/images/Stat/118_2.jpg)

> 빠르게 성장하는 서비스 만들기

- 위 그림과 같이 그 방법은 두가지가 될 수 있습니다.
  - 유저에게 좋은 영향을 주는것들을 적용하기
  - 유저에게 나쁜 영향을 주는것들은 적용하지 않기

> ## 유저에게 영향을 어떻게 알 수 있을까? 

> 유저의 영향 파악하기

- 위에서 우리는 유저에게 좋은것들만 제공하고 싶을텐데요, 이때에 유저에게 좋은것들은 어떻게 알 수 있을까요? 
  - 이때에 많이 사용되는 방법이 바로 A/B Test 입니다. (다른말로는 통제실험이라고도 합니다.)
- 이러한 통제실험이 어떻게 유저의 영향을 측정할 수 있다는것인지, 그리고 어떻게 적용할 수 있을까요?

# [온라인 통제실험](#link){: .btn .btn--primary}{: .align-center}

> ## 1.통제실험이란?

![jpg](/assets/images/Stat/118_3.jpg)

- 강낭콩을 더 잘 키우기 위해서 강낭콩이 원하는 요소를 어떻게 찾을 수 있을지 알고싶다고 합니다.
- 이떄에 다양한 요소 (토양 , 수분, 햇빛, 영양분 ..) 가 많은데, 이때 햇빛의 영향도의 영향도를 파악하고 싶을 것입니다 .

> 가설

- 즉 우리는 가설을 다음과 같이 설정하게 됩니다. 

$$\text{빛의 양이 많으면 강낭콩이 더욱 잘 성장할 것이다}$$

- 위 가설을 확인하기 위해서 창가에 둔 강낭콩과 그늘에 둔 강낭콩을 비교한다고 합시다.

![jpg](/assets/images/Stat/118_4.jpg)

> 실험 세팅

- 이때 빛의 양을 제외한 나머지 조건은 동일하게 합니다.
  - 빛의 양 : 영향도를 확인하고 싶은 변수
  - 나머지 조건 : 영향도를 확인하기 위해 통제되는 변수

> 실험 결과

- 빛의 양을 제외한 나머지 조건은 모두 일치시킴으로서, '빛의 양이 강낭콩의 빠른 성장에 영향을 끼치는지' 를 실험을 통해 확인하게 됩니다.
  - 즉 적절한 통제를 통해서 우리의 가설을 '정확하게' 검증할 수 있습니다!

> ## 2.통제 실험의 필요성

![jpg](/assets/images/Stat/118_5.jpg)

- 위와 같이 배달의 민족과 같은 예시를 들어봅시다. 
- 우리는 UX 변화에 대해서 그 영향도가 얼마나 되는지 궁금하다고 합니다.

![jpg](/assets/images/Stat/118_6.jpg)

- 하지만 위처럼 외부요인이 너무 많아서, UX 요인의 효과를 분석하기가 어렵습니다. 
  - 이러한 외부 요인을 고려하지 않으면 오판할 수 있기 떄문에 잘못된 의사결정을 할 수 있습니다.

> Example : 외부요인을 고려하지 않아서 오판하는 경우

![jpg](/assets/images/Stat/118_7.jpg)

- 위처럼 Buy 버튼을 바꾸었을때 신규 버젼이 훨씬 더 좋아보이는것처럼 보입니다.
  - 하지만 이는 외부요인 (마케팅) 덕분에 구매전환율이 높아진것입니다.
  - 즉, 버튼의 크기가 커진것은 오히려 구매전환률을 감소 (-12%) 시키지만, 우리는 마케팅 효과 (+37%) 때문에, 전체적인 향상도 (25%) 만 보고, 버튼이 고객에게 좋은 영향을 끼쳤다고 착각할 수 있습니다.

> 즉 외부요인을 통제해야 한다! 

- 이전의 강낭콩 실험에서 햇빛 이외의 요소를 통제했듯이, UX 이외의 다른 요인들을 통제해야 합니다.

![jpg](/assets/images/Stat/118_8.jpg)

> ## 3.정확한 인과관계 확인이 필요한 이유?

- 우리는 위에서 통제실험을 하게되면 인과관계를 더 명확히 알 수 있다는 것을 알았습니다.
  - 하지만 왜 이렇게 정확한 인과 관계 확인이 필요할까요? 

> 1.유저를 불편하게 만드는 업데이트는 비즈니스를 악화시킨다.

- 변경사항이 유저에게 악영을 끼치는것이라면 비즈니스를 악화시킵니다.
- 그러므로 정확하게 변경사항의 영향력(인과관계)를 확인하고 출시해야 할 것입니다!

> 2.정확한 인과관계를 확인하고, 좋지않은 영향을 준다면 보완해서 출시하자! 

![jpg](/assets/images/Stat/118_9.jpg)

- 위처럼 글로벌 대기업이라고 할 지어도, 새로 출시하는 기능의 성공 확률은 매우 낮습니다.
  - 그러므로 아무리 사전에 확인했던 기능을 출시한다 하더라도 실제 인과관계에서는 유저에게 좋지 않은 영향을 줄 수 있고, 이는 정확한 인과관계 확인이 필요하다는것을 알 수 있습니다.

> ## 4.많은 A/B Testing 이 필요합니다.

![jpg](/assets/images/Stat/118_10.jpg)

- 위와 같이 글로벌 기업들은 매년 엄청난 A/B Test 를 수행하며 유저의 반응을 숫자로 확인합니다.
- 가설을 세우고, 유저에게 실험하고, 다시 피드백을 가지는 과정을 반복하게 됩니다.

> Example : Bing 

![jpg](/assets/images/Stat/118_11.jpg)

- 위처럼 Bing 은 매주 수백개의 A/B Testing 을 하고있습니다.

> ## 5.통제실험은 어떻게 해야할까요? 

- 온라인 통제실험의 경우, 유저는 2개의 화면중 하나를 보게됩니다. 

![jpg](/assets/images/Stat/118_12.jpg)

- 이 경우 외부요인 (코로나 확진자 수, 배민에 입점한 상점 수, 버거킹 할인 행사...) 등은 양쪽 유저에 대해서 동등하게 영향을 끼치게 됩니다. 즉 통제가 된다고 할 수 있습니다!
  - 유저가 보는 화면에만 차이가 있습니다! 그러므로 우리는 적절한 통제실험을 간단하게 진행할 수 있는 것입니다.
- Control 과 Treatment 에 대해서 원하는 지표에 대한 영향력을 각각 측정하면 됩니다. 

# [AB Testing 해보기](#link){: .btn .btn--primary}{: .align-center}

> ## 어떤것을 실험해야 할까?

- 맥도날드에서 밀크쉐이크를 더 많이 팔고싶어서, 바나나향도 넣어보고, 딸기맛도 넣어보는 등 실험을 했는데 별다른 변화가 없었다고 합니다.
- 이떄 밀크쉐이크를 먹는 사람을 분석해본 결과 아래 그림과 같은 이유로 밀크 쉐이크를 구매한다는것을 알 수 있었습니다.

![jpg](/assets/images/Stat/118_13.jpg)

- 즉, 위 사례에서 고객들이 어떠한 불편함을 해소하기 위해 우리 서비스를 사용하는지 에 대한 근본적인 질문을 해야할 것입니다. 

> Four Customer Questions

- 우리 서비스에 대해서 다음 4가지의 질문을 생각할 수 있습니다.
  - Who is the immediate Customer? (우리 서비스의 고객은 누구인가?)
  - What is the Customer job? (유저가 원하는것은? 서비스에서 이루고자 하는것은?)
  - What must we do 10x better? (어떻게 하면 10 배 더 잘할 수 있을까?)
  - What are our measures of success? (성공 측정 기준이 무엇인지?)
- 위의 질문을 고려하먼서 고객을 만족시키기 위해서 어떤것을 할 수 있을지를 생각할 수 있습니다.

> Example : 고객 불편한점 찾기

- 배달의 민족에서 고객들이 원하는것 , 불편한것을 찾아보려고 한다고 합시다. 
  - 목적을 "배가 고픈 고객이 빠르게 결제할 수 있도록 해야 한다! " 라고 정했다고 합시다.

![jpg](/assets/images/Stat/118_14.jpg)

- 위처럼 고객 입장에서 불편한점이 어디에 있는지를 먼저 찾을 수 있습니다. 

![jpg](/assets/images/Stat/118_15.jpg)

- 그리고 위와 같이 각 단계에서 전환율, 카드 등록율을 살펴보면서 (퍼널분석) 개선할 부분을 찾아볼 수 있습니다.

> ## 어떤 지표를 봐야할까?

- 이제 실험에서 어떤 부분을 고칠지 , 어떤 가설을 만들어야 할지에 대해서 어느정도 알았습니다.
  - 이를 '실험' 하기 위해서 이제 지표를 설정해야 하는데요, 이때 어떻게 하면 지표를 설계할 수 있을까요?

![jpg](/assets/images/Stat/118_16.jpg)

- 지표를 유형에 따라서 분류할 필요가 있습니다. 핵클에서는 위와 같이 3개의 지표로 설정해야 합니다. 
  - 성공지표 : 실험의 승자를 결정할때에 영향을 주는 지표
  - 가드레일 지표 : 개선의 목표가 되지는 않지만, 현재 수준은 지켜야되는것
  - 보조지표 : 실험의 다양한 측면을 보기 위하여 설정하게 되는 지표

![jpg](/assets/images/Stat/118_17.jpg)

- 사실 위와 같이 각자의 목적에 맞게 분류하는 내부적인 기준이 있습니다.
- 어떠한 지표를 우선순위로 둘지는 각 서비스가 결정해야 할 것입니다!

# [통제 실험에서 주의할것](#link){: .btn .btn--primary}{: .align-center}

> ## 1. 충분한 실험기간

![jpg](/assets/images/Stat/118_18.jpg)

- 위처럼 각 서비스마다 차이가 있습니다. (자체 기술 블로그 참조)
- 통상적으로 대부분 서비스의 경우 서비스 진입부터 구매에 이르기까지 길지 않기 때문에 1주 ~ 2주의 기간을 권장하고 있음
- 요일별 편차가 있기 때문에 (주말과 평일..) 1주일 단위의 실험을 권장함!

> Example : 왜 Airbnb 는 4주일까? 

![jpg](/assets/images/Stat/118_19.jpg)

- 위 그래프에서
  - 파란색 그래프는 예약 전환율에 대한 차이($\Delta$) 입니다.
  - 빨간색 그래프는 p-value 입니다.
- 1주~2주의 실험을 했을때에는 가끔씩 실험이 유의하다고 나온 구간이 있었습니다.
  - 하지만 1개월까지 한 결과, 아무런 영향이 없었다고 결론이 나오게 되었습니다.
- 즉 이 실험을 했을때 1~2 주의 기간만 실험을 했다면 틀린 결정을 했겠죠. 

![jpg](/assets/images/Stat/118_20.jpg)

- 그 이유는 위 그림과 같이 숙소를 예약하기 위해서는 호스트와 컨텍하고, 예약에 이르기까지 상당한 기간이 소요되었습니다. (약 4주)
  - 그러므로 Airbnb 서비스의 경우 4주를 권장하게 된 것입니다.
  - Note : 물론 일반적인 커머스의 경우에서는 즉각적인 효과가 바로 나타나기 때문에 큰 기간을 설정하지는 않아도 됩니다! 

> ## 2.평균의 함정에서 벗어나기

- 이전 Airbnb 의 실험을 다시 가져와 봅시다.

![jpg](/assets/images/Stat/118_21.jpg)

- 평균만 비교했을때에는 A 와 B 는 차이가 없었습니다. 	
  - 하지만 세부 분석을 실시하였을때에는 IE 브라우저에서 새 디자인이 클릭이 안되는 이슈가 있었음을 알 수 있습니다.
- 즉 IE 문제를 수정하고 다시 실험을 했을때에는 통계적으로 좋은 실험이였다! 라는 맞는 결론을 내릴 수 있었습니다. 
  - 세그먼트 단위로 분석하여, '평균' 의 함정에서 벗어날 수 있었습니다.

> Example : Neflix 

- https://hbr.org/2020/03/avoid-the-pitfalls-of-a-b-testing
- 평균 시간이 늘어나는 배포가 좋은것인가? 를 생각해 볼때, 평균은 Heavy 유저가 평균에 큰 영향을 줄 것입니다.
- Heavy 유저의 시청시간만 늘리고, 넷플릭스에 engaged 가 적은 유저들의 시청시간의 개선은 없을때, 넷플릭스는 구독 모델이기 때문에, 이러한 경우는 별로 원하는 상황이 아닙니다.
- 즉 전체적인 평균 시간을 보는것보다, 아직 넷플릭스에 정착하지 못한 유저들의 시청 시간 , 스트리밍 갯수 등 늘리는것이 중요할 것입니다.

> Example : Linked in

- Well-connected 유저와(친구가 몇백명 ) Sparsely-connected 유저로 그룹화하여 분석을 진행!
  - 전체 유저를 한 통으로 보는게 아니라 Heavy 유저와 Light 유저를 분리해서 살펴봅니다.
- 상위 $1 \%$ 유저들이 주요 지표에 얼마나 기여도를 가지는지 추적

# [Summary And Q&A](#link){: .btn .btn--primary}{: .align-center}

> ## Conclusion

![jpg](/assets/images/Stat/118_22.jpg)

- 위와 같이, 실험문화의 조직이 중요하다는것을 말하고 끝마치도록 하겠습니다.

> ## Q & A

> 테스트 후 결과의 유의미성을 판단하기 위해서 수치가 어느정도 차이가 나야 하는지, 목표를 어떻게 잡아야 하는지 판단 기준이 궁금합니다! 

- 지표의 유의미성은 p-value 와 같은 값으로 확인할 수 있습니다.
  - 수치의 차이가 큰것보다 p-value 와 같은 통계적인 유의미성을 볼 수 있는 값을 함께 보아야합니다.

> 하나의 실험이 끝난 후, 이후 액션 아이템은 어떻게 가져가야 하는지 등에 대한 실험 이후 과정에 대한 내용도 궁금하다!

![jpg](/assets/images/Stat/118_23.jpg)

- 위와 같이 그룹 A, 그룹 B 의 결과가 각각 검색 전환율, 구매 전환율의 우위가 다르다고 합시다.
  - 물론 이때, OEC를 구매 전환율으로  선택했으므로, 그룹 A 를 선택하게 될 것입니다. 
- 하지만 위의 경우 추가적으로 '왜 그룹 A 가 검색 전환율은 낮은데 구매 전환율은 높았을까?' 를 분석해볼 수 있습니다.
  - 검색 이후에 어떤 과정을 거치면서 유저가 이탈했는지를 추가적으로 분석해볼 수 있고, 더 발전시킬 수 있다는 것입니다.
- 즉 이 실험에서는 결론을 내는것 외에도, 실험을 통해서 다음과 같은 learning 을 배울 수 있습니다.
  - 더 좋은 실험을 위한 개선점
  - 유저들에 대한 더 깊은 이해
- 그러므로 다양한 지표를 보면, 실험 이후에 랩업하고, 그 이후 어떤 결정을 하는지에 더 도움이 많이 될 수 있습니다.

> $\mathrm{A} / \mathrm{B}$ 테스트 진행/미진행 여부에 따라 성과가 어떻게 달라지는지, 기존 미진행했을 때보다 진행하고나서 대체로 어떤 점들이 개선되었는지가 궁금합니다

- A/B 테스트를 통해 어떤 learning을 얻는지가 중요함.
  - 부정적인 결과를 보인 지표들을 알게 되어, 이를 개선시킬 방향을 찾을 수 있음!
  - 어떤 요소들이 유저들에게 긍정적으로 반응하는지를 알 수 있음! 
- A/B 테스트를 안하면 위와 같은것들을 놓치게 됩니다. 
  - 오랜 시간이 지나고 나면 A/B 테스트를 한것과 하지 않은것은 유저의 만족도에 대해서 매우 큰 차이가 나게 될 것입니다.

> A/B 테스트에서 실전에서 저지르기 쉬운 실수, 오류들 리스트가 궁금해요!

1.서로가 생각한 $\mathrm{A} / \mathrm{B}$ 테스트 시작 지점이 다른 경우 

- A/B 테스트의 시작 지점이 서로 다를수가 있어서 이 경우 의도한 표본이 아니여서 분석이 약간 어려워질 수 있습니다.

2.서로가 생각한 $\mathrm{A} / \mathrm{B}$ 테스트 대상자 조건이 다른 경우 $\rightarrow$ 다시 해야됨

- 예를 들어 첫 구매 이력이 없는 유저를 대상으로 A/B 테스트를 하려 했는데, 그게 되지 않은경우입니다.... 그 경우 다시 해야됩니다! ㅜㅜ

3.A/B 테스트를 한지 1주일이 됐는데.. 로그가 안 심어져 있네요.. $\rightarrow$ 다시 해야됨

- 즉. 서비스가 로그를 잘 심었는지를 잘 점검해야 합니다.

4.$\mathrm{p}$-value가 하루만에 $0.05$ 미만이 되어 기쁘게 $\mathrm{A} / \mathrm{B}$ 테스트를 종료하는 경우 $\rightarrow$ 맞는 결과인지 의심하게 됨

- Peeking p-value 문제입니다! 참을성을 가지고 살펴봐야 합니다.

> 앱 초기에 모수가 별로 없어서 $\mathrm{A} / \mathrm{B}$ 테스트 유의미한 모수를 만들기 어려울 때는 어떻게 하면 좋을가요?

- 어떤 상황에서든 꼭 $\mathrm{A} / \mathrm{B}$ 테스트를 해야 하는 것은 아닙니다! 통계적인 유의미성을 파악할 수 있는 모수가 있는 경우에 A/B 테스트가 효과적입니다.
- 모수가 적은 경우, 통계적인 유의미성을 확보하기 쉽지 않기 때문에 서비스를 이용한 고객들과 잠재 고객들의 피드백을 많이 듣고(인터뷰 등...) 이를 서비스에 반영하는 것이 적합한 선택일 수 있습니다.
  - 혹은 마케팅을 통해 서비스에 많은 유입이 발생되도록 하고 실험을 진행할 수 있습니다.

> A/B/C 를 비교할때 B 와 C 비교도 가능한가?

- B 와 C 비교도 가능하고 그거보다 더 많은 비교도 가능합니다! 

> 트래픽이 매우 적은 초창기 서비스의 경우, 빠르고, 다양한, 다수의 실험(ABTest)을 할 수 있는 방법은 어떤게 있나요?

- 모수가 적기때문에 유저를 나누어서 A/B 테스트를 하기 힘든 환경! 그럼에도 여러개의 피쳐를 한꺼번에 런칭하면서 각각의 영향도를 측정할 수 있을까?
  - 매우 어렵다! 이러한 상황에 놓였을때는 각각을 A/B 테스트를 하는것보다는 그때그떄 유저의 요구를 반영하는게 훨씬 더 좋다고 생각됨 
  - 고객에게 직접적인 피드백을 받는게 좋을것

> A/B 테스트가 유의미할 수 있는 최소한의 모수는 어느정도일까? 

- 핵클에서 보는 최소한의 모수는 1000단위 이상의 유저들이 쌓이는 경우에 유의미한 분석을 하기에 적합하다! 라고 생각중
  - 홈 화면에서 A/B 테스트를 한다고 할때, 실험 기간 내에 실험에 참여한 실험자 수가 1000명 이상인지를 살펴보게 됩니다.

> Airbnb의 사례 에서 1~2 주 동안의 실험에서는 유의하다고 나왔는데, 이는 화면이 바뀐게 유저에게 어쩃든 긍정적인 효과를 미친게 아닌가요?

![jpg](/assets/images/Stat/118_19.jpg)

- 질문자님이 1~2주 정도의 실험 기간에는 Treatment가 더 좋았기 때문에 첫인상이 주는 효과가 개선되었다고 볼 수 있다고 해석하신거 같다. 
- airbnb 의 경우 유저의 행태를 보면 2가지로 나누어집니다.
  - 바로 화면에서 숙소를 예약하는 유저 (시간 조금 걸림)
  - 개인에게 직접 연락하여 예약하는 유저 (3~4주 걸림)
- 실험 초기에는 바로 화면에서 예약 가능한 유저들이 대부분 실험의 표본으로 잡히게 됩니다. 
- 실험 기간이 늘어나면서 개인에게 직접 연락하여 예약하는 유저까지 실험의 표본으로 잡히게 됩니다.
- 즉 우리가 실험할때에는 전체 population 에게 실험을 해야하므로 결국, 실험은 4주까지 하는것이 맞는것이고, 그에 따라서 실험 결과도 '유의하지 않음!' 이 되어야 합니다.

> 여러 실험이 같이 진행될 때 유저가 여러 실험에서 경험이 달라지는 부분을 통제하는 방법?

- 여러 실험이 같이 진행될때 , 다양한 조합의 실험을 보게 될 수 있는데, 이때 주의할점은 서로가 서로의 실험을 고려해서 개발을 했는지? 를 잘 생각해야됨
  - 빨간 글씨 + 빨간 배경 과 같은 조합은 재앙을 초래함..
- 위와 같이 모든 조합을 통제하는게 어려우면 그냥 유저 풀을 잘게 쪼개서 1인 1실험이 되도록 하는 방법도 있음!

> 유저를 버킷에 분류하는데 랜덤성을 어떻게 관리하는가?

- 랜덤하게 유저를 분배하는 방법을 활용. 
- 자신들만의 특별한 방법은 아니고, 믿고 쓸 수 있는 수학적인 알고리즘을 썼음. 

> 도출된 결과가 괜찮다고 판단할 수 있는 기간은? 최소 1주일 + 1000명 이상이라고 설명해주셨는데 예외적인 케이스는 없나?

- 최소한의 통계적인 유의미성을 판단할 정도는 1000명이라고 정한것!
- 이러한 여건 하에서 도출된 결과의 경우 통계적인 유의성 (pvalue) 에 도달하였는지를 살펴보면 됩니다.

> 외부요인 통제 관련해서 광고나 입점 가맹점 수나 코로나 관련과 같은 이슈는 통제가 불가능한데 어떻게 하는가?

- 사실 A/B Test 를 할때에, A 와 B 유저는 화면만 다르게 보고 나머지는 같으므로 통제가 자연스럽게 됩니다. 
- 그러므로 A/B Testing 에서는 이러한 통제는 자연스럽게 이루어집니다.

> 여러개의 Variant를 이용하면 false positive가 커져서 문제가 되는데 이것은 어떻게 해야할까?

- 여러개의 실험을 하게되면(A/B/C/...) 당연히 통계적인 오류가 커질수밖에 없음
  - 우리도 고객사분들에게 가급적이면 A/B 두가지 그룹으로 실험하는것을 권장
- 반드시 테스트를 해야되는 상황에서만 부득이하게 A/B/C.. 테스트를 사용! 

> Test의 평균값의 변화가 없을 때 세부 분석은 어떻게 , 얼마나 수행해야 할까요? 

- 서비스가 커지면 QA를 완벽하게 하지 못합니다. 
- 빠르게 기능을 추가하는 과정에서 인과관계를 확인하기 위해 A/B 테스트를 하는건데, 결과가 유의미하지 않아도 우리가 놓친 포인트를 찾는데도 도움이 된다. (airbnb 케이스에서도 보다시피)
- 세부분석은 의심이 되는 부분이 있을 때, 문제점을 찾기 위해서 수행합니다.
  - ex : 디바이스별로 에러가 잘 일어나므로 이것을 segment 로 해서 확인해보자! 

> 제품 개발 단계에서도 A/B Test를 활용할 방법이 있는지?

- 개발 단계에서 A/B 테스트를 하기는 어려움. (왜냐하면 애초에 서비스를 경험한 유저가 없으므로)
  - 억지로 실험환경을 조성해서 A/B Test를 할수도 있는데 (베타 테스터 처럼), 지금은 프로토타입이므로 아직 보여줄 서비스가 아닌 경우에는 A/B Test가 필요한 단계는 아니다.
- 잠재고객에 해당되는 분들에게 프로토타입을 보여주면서 인터뷰하는게 현실적인 방향일듯 
  - 인터뷰, 설문조사 등을 적극적으로 활용하자!

---

**reference**

- <https://www.youtube.com/watch?v=ZBooJi6iF5g>
