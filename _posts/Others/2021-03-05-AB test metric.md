---
title:  "A/B Test Metric"
excerpt: "A/B 테스트에서의 Gaol metric"
categories:
  - Others
tags:
  - 3
last_modified_at: 2021-03-04

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# Primary metric

Testing 을 할 떄에 Primary metric 을 설정하는것이 중요하다. 실험의 목적에 따라서 그에 적절한 Primary metric 을 설정하고, 이 Primary metric 에 따라서 우리의 가설(A/B test) 를 기각하거나 채택하게 된다. 

이러한 Primary metric 을 설정하기 위해서는 몇가지 고려사항이 있는데
Visitor 들의 어떤 Action 이 우리가 원하는 것까지 달성하게 할 수 있을까? 에 대해서 파악하고 있어야 한다. 

예를 하나 들어보자. 수익을 최대화 하고 싶어서 A는 원래 사이트, B는 이벤트 상품을 베너로 걸은 사이트 라고 하고, 평균 구매율만 Primary metric 으로 설정했다고 하자. 그리고 Visitor 들이 사이트를 방문하고 3초만에 이벤트 상품만 사고 나갓다고 해보자. 이 경우에 Primary metric 인 구매율은 높게 나와서 좋아보일 수 있지만 사실 사람들은 '이벤트 상품만' 산 것이다. 이는 B 의 경우 사람들의 구매를 이벤트에만 의존하게 만들어 오히려 골고루 제품을 샀었던 A 보다 안좋은 결과를 이끌어 낼 수 있다. 

이 Primary metric 은 통계적 Test 가 되는 만큼 충분한 사전조사를 통해서 매우 신중하게 접근해야 한다. 

<br>

# Secondary metric

metric 은 하나만 지정하지 않아도 된다. 

| Searches submitted     | See how many searches are submitted                          |
| ---------------------- | ------------------------------------------------------------ |
| Category pageview      | Discover whether visitors navigate the site via Category pages |
| Subcategory pageview   | Learn whether visitors reach Subcategory pages               |
| Product pageview       | Know the percentage of visitors who do or don't view a product during a visit |
| Add-to-Cart            | Understand what percentage of visitors Add-to-Cart per test, category, product type |
| Shopping cart pageview | See how many visitors progress to the shopping cart          |
| Checkout pageview      | Understand how many visitors continue from the shopping cart to checkout |
| Payment pageview       | Learn what percentage of visitors continue from checkout to payment |
| Conversion rate        | Know what percentage of visitors ultimately convert or complete payment |

위 표처럼 많은 metric 을 추가로 선택해 A/B 테스트 동안 더 많은 insight 를 얻을 수 있다. 많은 metric 을 통해서 실패하더라도 많은 정보를 얻을 수 있을것이다.

<br>

# Example of metric

<br>

## Bounce Rate(이탈률)

**이탈률(Bounce Rate) = 이탈 수 / 페이지 세션 X 100%**

여기서 이탈은 페이지에서 고객이 아무런 상호작용을 거치지 않고 떠난 경우이다. 이때 상호작용은 스크롤 다운, 스와이프, 클릭, 재생 등이 있다. <br>
세션은 일정한 기간(30분) 동안 웹사이트에서 발생한 사용자 상호작용의 집합이다. 즉 버튼을 클릭하거나 페이지 이동 등의 모든 행위를 말한다. <br>

![png](/assets/images/{Others}/6_1.png)	

위 예시를 보자. 이용자는 처음 방문한 첫 페이지만을 보고 사이트를 떠나버렸다. 이 경우들이 이탈률을 나타내는 것이다. 

<br>

### 이탈률이 높으면 검색엔진에 상위노출이 될까?

구글은 이탈률은 검색엔진의 결과 순위에 아무런 영향을 끼치지 않는다고 한다. 순위를 결정하는 요소는 이탈률이 아니라 '사용자가 그 사이트와 상호작용을 많이 하면서 남아있었는지' 가 훨씬 중요한것이다.

<Br>

### 이탈률이 낮을수록 좋을까?

이탈률이 낮다고 해서 좋은것은 아니다. 아래 예시를 살펴보자.

![png](/assets/images/{Others}/6_2.png)

빨간옷을 입은 청년의 경우 웹사이트에서 연세대의 위치를 바로 검색해서 알아내었다고 하자. 하지만 갈색옷을 입은 청년의 경우 웹사이트에서 제대로 알아보지 못하여서 궁금증을 해결하지 못하고 탐색하다가 이탈하고 말았다. 

이 경우 빨간옷이 이용한 녹색 사이트가 이탈률이 더 높을것이다.(바로 원하는 결과를 얻었기 때문에 세션이 크지 않음) 하지만 녹색사이트가 미래적으로 더 성장할것이라는것은 분명하다. 즉 이탈률이 낮다고해서 좋은것만은 아니다.

<Br>

### 산업별로 다른 이탈률

![png](/assets/images/{Others}/6_3.png)

위와 같이 산업군마다 목표로(Benchmark) 하는 Industry 가 다르다.  왜 이렇게 다를까? 

이 이유는 바로 웹사이트 별 사람들이 원하는 정보가 다르기 떄문이다. 음식점의 위치를 제공해주는 사이트의 경우,  사람들은 맛집 위치만 추려내고 바로 이탈해 버린다. (즉 세션이 낮다.) 하지만 부동산 사이트의 경우 가격, 위치, 과거 시세 등 전문적으로 검색하면서 정보를 찾으려 하기 때문에 세션이 높다. 그러므로 이런 차이에 이탈률이 달라진다. 

![png](/assets/images/{Others}/6_4.jpg)

<Br>

### 사용하는 Device 별로 다른 이탈률

디바이스 별로도 매우 다른 이탈률을 나타내고 있다. 아래를 보면 Mobile, Tablet , Desktop 중 무엇을 이용했는지에 따라서 Bounce rate 가 달라진다. 

![png](/assets/images/{Others}/6_5.jpg)

핸드폰 유저들의 경우 앱이 많고, 컴퓨터는 거의 인터넷을 중심으로 한 하나의 화면이지만, 핸드폰은 게임, 메신져 등 다중의 앱들로 구성되어있기 때문에 다른것으로 이탈할 확률이 높은것이다.

<Br>

### 이탈률의 설정

산업별, 사용자별로 다른 이탈률때문에 그 기준을 정하기가 쉽지않다. 이 경우에는 이 산업에서의 평균 이탈률은 얼마일까? 라는 질문보다는 우리의 웹페이지와 비슷한 경우의 이탈률은 어떻까? 또는 현재 이탈률을 어떻게 하면 개선시킬 수 있을까? 등의 질문이 더 어울릴 것이다.

<Br>

### 이탈률이 높아지는 이유

**페이지가 하나로만 구성되어있을때**<br>
이 경우, 페이지가 하나뿐이기 때문에 이동할 곳이 없다. 즉 이탈률이 높게 나타난다.

**페이지 로드속도가 느릴때**<br>
페이지 로드속도가 느리다면 특별한 목적이 있지 않는 이상 모두 로드되기 전 나가버린다.

**목적에 맞지 않을때**<br>
내 블로그 포스팅 제목이 파이썬 통계분석 인데, 사실 안에 내용은 통계 이론만 가득하다고 하자. 그러면 내 블로그에 들어온 사람의 목적은 '파이썬으로 통계분석을 해보자!' 인데, 이 목적을 달성할 수 없으므로 바로 나가버린다.

**페이지 가독성/디자인이 나쁠떄**<br>
이는 너무나 당연한 이야기.. 하지만 '무엇이 나쁜가?' 같은 질문에는 쉽게 답할수가 없을거같다.

**모바일로 접속했는데 pc 사이트로 이어질때**<br>
이 경우는 테크적인 문제이다. 

<Br>

### 이탈률 개선법

**1. 페이지 속도 점검**<br>
페이지 속도는 디자인과 마찬가지로 첫 인상에 해당한다. 그러므로 처음 화면에 너무 많은것을 삽입하여 로딩 속도를 느리게 하면 안된다. 주기적으로 가벼운 화면을 유지해야한다.

**2. 콘텐츠의 디자인/가독성 점검**<br>
레이아웃, 디자인 등을 AB test 를 통해서 개선할 수 있다.

**3. 유입 키워드와 콘텐츠가 일치하는지 점검**<br>
유입 키워드와 우리 홈페이지가 일치하지 않으면 필연적으로 이탈률이 높아진다. 주 고객의 니즈를 파악하여 그에 맞게 홈페이지를 바꾸어야 한다.

<Br>

## Exis Rate(종료율)

**종료율(Exit Rate) = 페이지 종료 수 / 페이지 뷰 수 X 100%**

종료란, 해당 페이지가 탐색 페이지의 마지막에 해당하는 페이지 뷰 수를 의미한다.
페이지 뷰랑 사용자가 페이지를 조회한 횟수를 의미한다. 새로고침을 하면 페이지 뷰 수가 증가한다.

예시를 생각해보자. 특정 웹페이지의 총 페이지 뷰 수가 1000회였고, 마지막으로 탐색한 페이지 뷰 수가 200회라고 하자. 그렇다면 (200/1000) * 100% 가 되어서 종료율은 20 %가 된다.

<br>

### 종료율 개선법

종료율을 개선하기 위해서는 고객이 원하는것을 끊임없이 제공해 주어야 한다. 예를 들어서 식당예약사이트에서 식당을 예약하고 나면, 이후에 대리운전 연결 또는 커피집을 연관해서 추천함으로서 고객이 원하는것을 더 추천해줄 수 있다.



## Conversion Rate(전환율)

**전환율**(conversion rate) 이란 사이트를 방문한 사람 중, 소정의 유도된 행위를 한 방문자의 비율을 말한다. 유도된 행위란, 예를 들면, 무언가를 구매한다든가 사이트의 핵심 문서를 읽는다든가, 무언가를 다운로드받는다든가 하는 행위 이다. 

# Reference

https://cxl.com/guides/bounce-rate/benchmarks/

https://www.marketingoptimizer.com/blog/marketing-optimization/metrics-must-track-ab-testing/

https://help.optimizely.com/Ideate_and_Hypothesize/Primary_and_secondary_metrics_and_monitoring_metrics#Primary_metric