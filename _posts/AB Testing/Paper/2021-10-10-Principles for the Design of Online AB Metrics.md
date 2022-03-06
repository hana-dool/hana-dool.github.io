---
title: "Principles for the Design of Online A/B Metrics"
excerpt: "Bing 의 Metric Design 을 할 떄의 원칙에 대한 논문"
categories:
  - AB_Paper
last_modified_at: 2021-10-09

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 이 논문에서는 A/B Testing 에서 Metric 의 설계 원칙을 설명합니다. 실험을 설계할때에 나타나는 몇개의 문제점을 공유하고 이러한 함정을 피하기 위한 해결책을 공유하려 합니다.
{: .notice--warning}

![png](/assets/images/Stat/77_2.png)

# [Principles for the Design](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction 

- A/B 테스팅은 데이터를 기반으로 올바른 결정을 하게 해준다는 점에서 매우 중요합니다. 
- 이떄에 A/B Testing 은 '정해진 metric' 의 행동을 살펴보면서 결정을 내린다는 점에서 좋은 Metric 은 매우 중요합니다. 
  - 우리는 잘못된 metric 선정으로 인하여, 잘못된 결정을 하는 경우가 흔합니다. 
  - 그러므로 expressive / robust / trushworthy 한 metric 을 설계하는것이 중요합니다. 
- 이 논문에서 우리는 Bing.com 을 위한 A/B Testing metric 을 설계하면서 배운 몇가지 교훈을 공유하려고 합니다. 
  - 온라인 A/B Testing metric 을 설계할떄에 고려해야 할 많은 측면에 대해서 설명할 것입니다. 

> ## 1. THE A/B METRIC PROBLEM

- A/B Testing 에서는 특히 OEC(Overall Evaluation Criterion) 을 살펴보게 됩니다. 
  - 이 OEC 는 Treatment 가 좋은지 Contol 이 더 좋은지에 대해서 알려주게 됩니다. 
  - 웹 search 서비스 입장에서 보자면, 이러한 OEC 를 이용하여 사용자가 만족된 경험을 하였는지 아닌지에 대해서 살펴보게 됩니다.
- 이렇게 중요한 A/B metric 을 설계할떄에 드는 의문이 있습니다. "어떻게 하면 좋은 metric 을 고를 수 있을까요? "
- 전통적으로 이러한 문제는 prediction problem 으로 여겨졌습니다.
  - 즉 , 유저에 대한 로그 데이터와, 유저에 대한 true label 을 설정합니다. 
  - 그 이후에 true label 를 예측하는 모델들을 구성한 뒤에 recall / precision 등의 입장에서 제일 좋은 모델을 선택합니다 
  - 그리고 최고의 predictor 가 , 최고의 A/B metric 이 될 것이라는 것입니다. 
- 물론 위와 같은 방법은 처음 A/B Testing 의 metric 을 설계할때에는 합리적인듯 보이지만, 결함이 있는 metric 을 설계하게 될 가능성이 있습니다. 이유는 다음과 같습니다.

> predictor 입장에서 고른게 항상 좋은건 아니다.

- 매우 드문 행동의 경우 이를 측정하는 metric 은 predictor 입장에서는 너무 정보량이 적어 안좋은 변수이다. 
- 과적합을 피하기 위해 쳐낸 변수가 사실 좋은 metric 일 수 있습니다. 등등..
- 즉 '결과를 잘 예측하는' 것 을 기준으로 metric 을 고려하면 안된다는 것입니다.

> 내생신호의 사용

- 내생신호와 외생신호는 다음과 같이 정의됩니다.
  - 내생신호 : 시스템의 응답 
  - 외생 신호 : 유저의 반응 
- 이떄에 내생신호를 A/B Testing 의 지표로 삼는 경우에, A/B TEsting 의 신뢰도에 큰 영향을 주게 됩니다.
  - 검색 결과 페이지에 '날씨 관련 검색을 할때에 날씨 예보가 잘 뜨는지' 를 metric 으로 정했다고 합시다.
  - 하지만 위와 같은 metric 은 '모든 검색에 대해서 날씨 예보를 뜨게' 해도 큰 값이 나오는것을 알 수 있습니다. 
  - 이처럼 내생신호를 사용하게 되면, 시스템적으로 치명적인 약점이 있을 수 있습니다.

> 결론

- 그러므로 우리는 A/B Testing 의 metric 을 선정할때에 prediction problem 이라기 보다는 measurement problem 으로 봐야합니다. 
  - 향상이 있었는지 / 없었는지의 label 이 붙은 A/B Testing 셋에 대하여 metric 이 얼마나 alignment 가 잘 되는지를 봐야합니다. (즉 success 라는 결과(label)에 대해서 일관된 방향을 나타내는가?, 또는 잘 변하는가? 등)
  - 이때에 true label 을 붙이는 작업은 metric 이외에도 다양한 요소를 고려하여 전문가가 수행합니다. 
- 다양한 실험의 corpus 를 모으는것이 중요합니다.
  - 왜냐하면 특정(ex 세션당 클릭수에 큰 영향을 미치는 실험들) 에 치우친 실험만 corpus 로 잡게 된다면 , 그에 맞는 메트릭만 중요하다고 왜곡할 수 있습니다.
  - 또한 특정한 Treatment 에 매우 좋은 매트릭에 대해서는, 변하지 않아 안좋다고 잘못 판단내릴 수 있습니다. 
- 위의 corpus 를 이용하여 'directional alignment' 와 statistical sensitivity 두가지를 고려하여 metric 의 품질을 결정하게 됩니다.

> ## 2. DESIGNING A METRIC SYSTEM

- 완벽한 metric 은 없습니다. 많은 metric 들은 우리가 의도하지 않은 방향으로 움직이기도 합니다.
- 따라서 다양한 각도에서 treatment 의 효과를 측정하는 metric 들이 필요합니다. 
- 하지만 많은 수의 metric 을 보유한다는게 늘 좋은것은 아닙니다.
  - 어떤 metric Treatment 의 효과가 없음에도 , p-value (0.05) 에 의하여 효과가 있다고 할 수 있기 때문입니다. 
  - 또한 stong 한 Treatment 는 metric 을 움직이게 할 것입니다만 그중 일부는 모순된 방향으로 움직일 수 있습니다.
  - 즉 실험자들에 대해서 혼란을 줄 수 있다는 것입니다.
- 또한 실험자들은 그들의 직관에 맞는 메트릭을 자기들이 골라서 선택하도록 유인될 수 있습니다.
  - 즉 실험자들이 공들여서, 좋아보이는 Treatment 를 만들었다고 합시다. 여러 Metric set 들 중에 50% 는 좋은 방향으로 움직인 반면, 50% 는 안좋은 방향으로 움직였습니다. 이 경우에 실험자들은 좋은 방향으로 움직인 metric 만 선택해서 상급자에게 보고하게 될 수 있습니다 .
- 이러한 문제를 해결하기 위해서 우리는 일반적으로 계층적 방식을 메트릭 시스템을 설계하려 합니다. 

> 계층적 방식의 metric system

- 제일 상위 수준에는 사용자당 세션 수 와 같이 가장 Robust 한 메트릭을 배치합니다. (High level)
  - Note : 우리는 '사용자' 수준에서의 메트릭을 제일 덜 민감(잘 변하지 않음)하다고 여깁니다.
- 그 다음 레벨에는 세션당 성공률 같은 세션 수준의 메트릭을 보게 됩니다. 
  - '성공' 은 'Treatment' 에 따라서 어떻게 정의될지 '구체적으로' 정하기 떄문에, 이전의 '사용자당 세션 수' 와 같이 Global 한 metric 보다는 덜 Robust 하지만 훨씬 Sensitive 합니다. 
  - 예를 들어 '구매' 를 성공으로 가정한다면, 우리는 세션당 구매전환율 이라고 metric 을 정하게 될텐데, 이는 '구매' 라는 행동에 더욱 촛점을 맞춘 메트릭이기 떄문에 Sensitive 합니다. 
  - ex) 구매기능을 개선하여 구매전환율이 상승했다고 합시다. 하지만 사용자당 세션수 같이 Global 한 경우, 너무 글로벌한 metric 이라 이러한 '세부 수준' 에서의 상승을 잘 잡아내질 못합니다. 하지만 '세션당 구매율' 인 경우는 '사용자의 구매 행동' 에 대해서 초점을 맞추기 때문에 훨씬 더 Sensitive 합니다.
- 세번쨰 수준에서는 기능에 초점을 맞춘 메트릭이 있습니다. (ex : Web result Success Click rate 등)
  - 이 세번쨰 수준은 사용자의 성공을 어떻게 정의할지에 대해서 훨씬 더 구체적으로 정의되기 때문에 제일 Sensitive 합니다. 

> 다양한 영역의 metric

- 또한 위와 같은 계층 구조의 일부로서, 다양한 영역의 metric 을 고려해야 합니다.
- 이 구조에 따라 시스템은 페이지의 여러 부분을 커버하게 됩니다. 
  - 특정 기능에 대한 metic 처럼 좁은 구역에 대한 metric 
  - 페이지당 성공률 처럼 페이지 전체에 대한 metric (이는 특정 기능보다 넓은 범위를 지닙니다.)
- 이렇게 다양한 범위를 가진 메트릭을 정의하게 된다면, 실험이 feature level 에만 집중하느라 global level 의 변화를 놓치지 않게 보장해줍니다. 
  - ex) 구매 페이지의 개선에만 집중하다가, 전체 유저의 세션 수가 감소할수도 있습니다. 

> 해석

- 이러한 계층적 방식의 metric 을 해석할때에는 top - down 방식으로 해석하게 됩니다.

> ## 3. Metric Definitions

- 우리는 metric 을 정의할떄에 고려해야할 여러가지가 있습니다. 

> 값 제한없는 metric 의 경우 outlier 를 조심하자.

- upper bound 가 없는 metric (count 등) 을 고려한다면, 많은 양의 노이즈가 유입되어 덜 sensitive 해질 수 있습니다. 
  - 페이지 요청 후에 , 첫 클릭까지의 시간과 같은 '클릭 시간' 메트릭은 outlier 에 의해 분산이 매우 높습니다. 
  - 이는 덜 Sensitive 하다는 의미이고, 이를 해결하기 위한 방법은 바로 Outlier 를 잘라내는 방법 / Transformation 하는 방법 등을 사용할 수 있습니다 

> 분모가 변한다면 조심히 해석하자.

- 분모의 이동에 따라 메트릭이 변경된다면, 메트릭은 좋지 않습니다.

![png](/assets/images/Stat/77_1.png)

- 위의 예시를 봅시다. 세션당 클릭수 와 페이지당 클릭수 두가지 경우에 대해서 다른 방향으로 변하고 있습니다. 
  - 이는 Control 과 Treatment 를 나눌떄에 '유저' 별로 나누었지만, 그 분모인 Session 과 Pages 가 다르기 떄문에 일어나는 현상입니다. 

> ## 4. Debuggability

- A/B TEsting 시스템이 개발되고 나면, 실험자는 metric 의 movement 에 의거하여 Treatment 를 적용할지 안할지에 대해서 결정하게 됩니다. 
  - 하지만 이러한 metric 의 변화가 특정 feature 에 집중되어 있는 metric 이더라도 이 변화가 나머지 Feature 과 상호작용 하면서 나머지 부분에 영향을 끼칠수도 있습니다.
- 이러한 효과때문에, metric system 은 쉽게 디버그 할 수 있고, 그 움직임을 명확하게 해석 가능해야하는것이 중요합니다. 
  - 즉 metric 의 이동에 기여하는 다양한 부분은 쉽게 분해(decomposition) 가 가능해야 합니다. 
- 단순히 OEC 를 여러 메트릭간의 linear function 으로 정할떄에 (디버그가 쉽게 가능하게) , OEC 의 변화를 쉽게 분해 가능하게 하여 해석이 쉽게 되도록 합니다.
  - A/B Testing 의 결과가 쉽게 해석할 수 없는 black box 인 경우에는 우리가 '해석' 할 수 없기떄문에 오류를 식별하기 어려워지고 직관을 얻기가 힘들어집니다.
  - 예를 들어 세션수 * 매출 / sqrt(유저 수) .... 와 같이 마구잡이로 섞어놓은 매트릭은 분해도 힘들고 해석도 힘드므로 안좋다는 이야기입니다. 

**Reference**

- <https://www.microsoft.com/en-us/research/group/experimentation-platform-exp/articles/patterns-of-trustworthy-experimentation-during-experiment-stage/>

정말 짧고 경험만 말한 논문이라 쉽게 읽었네요~ 계층적 metric 시스템에 대해서 좀만 더 자세히 말해줬으면 좋았을텐데 진짜 그냥 언급만 하고 숑~ 지나가니까 그닥... 좋은 논문은 아니였는듯. (논문이 아니라 걍 지침인가?) 
{: .notice--success}

