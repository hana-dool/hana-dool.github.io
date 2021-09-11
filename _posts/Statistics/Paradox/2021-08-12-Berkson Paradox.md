---
title:  "Berkson's Paradox"
excerpt: "표면적으로 보이는 관계와 , 진정한 상관관계는 다를 수 있다"
categories:
  - Stat_Paradox
tags:
  - 1
last_modified_at: 2021-08-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 1. Berkson Paradox란?

- 벅슨의 역설은 "표면적으로 보이는 관계와 , 진정한 상관관계는 다를 수 있다." 라는 것입니다.

![png](/assets/images/Stat/34_1.png)

- 위와 같이 Collider 란 원인 변수와 결과 변수의 영향을 동시에 받는 변수입니다.
- 두 변수의 영향이 하나로 모인다는 의미에서 Collider(충돌체) 라는 용어를 쓰게 됩니다.
- 만일 이러한 Collider 를 통제한 상태에서 실험을 하게되면 어떻게 될까요? 
  - 그렇가면 Collider 의 관계를 만족하는 원인(X)과 결과(Y) 만 남게됩니다. 
  - 즉 이는 현실세계의 결과를 왜곡할 수 있습니다. 이를 Collider Bias 라고 합니다.
- 즉 실험을 할 떄에는 Collider 를 통제하지 않은 상태에서 실험을 제거해야 합니다. 

<br>

# EX : 멋진 남자는 재수없어?

- 흔히 여성들이 '내가 만나봤는데 멋진 남자는 대부분 재수가 없더라!' 라고 하는 말을 들어봤을 것입니다. 

- ''생각과 외모는 무관하다' 라는것을 전재로 hot(외모 수준) 과 nice(성격 수준) 의 상관관계에 대해서 살펴봅시다. 

![png](/assets/images/Stat/34_2.png)

- 위와 같이 모든 데이터를 고려한다면 파란색 선처럼 아무 상관관계가 없게 Fitting 이 되는것을 볼 수 있습니다.

- 그러나 여성에게는 '못생겼지만 싫은 사람(왼쪽)'과 '조금 꽃미남이지만 꽤 싫은 사람(왼쪽 부분)', '매우 못생겼지만 좀 좋은 사람(오른쪽 아래 부분)'은 데이트의 대상이 되지 않기 때문에 '삭제'되어 버립니다.

![png](/assets/images/Stat/34_5.png)

- 이렇게 하여 남은 데이트를 할만한 남자만 분석대상으로 구분하면 hot과 nice의 상관은 (파란색 라인)위와 같습니다.  
- 즉, 'hot과 nice는 부의 상관이 있다(= 미남은 싫은 사람인 경향이 있다)'고 나와, 전제와는 다른 결론이 도출됩니다. 이것이 벅슨의 역설의 일례입니다.

<br>

# EX : 흡연을 많이 하면 코로나가 약해진다?

- COVID-19 심각도와 흡연 사이에 부적(음의 상관) 상관이 발표된 사례([Wenzel 2020](https://ec.europa.eu/jrc/en/publication/smoking-and-covid-19-review-studies-suggesting-protective-effect-smoking-against-covid-19))가 있다. 그런데 최근 Nature에 게재된 [Griffith 2020](https://www.nature.com/articles/s41467-020-19478-2)에서는 이 결과가 [Berkson’s Paradox](https://en.wikipedia.org/wiki/Berkson's_paradox)(벅슨의 역설)라고도 불리는 Collider Bias라고 지적하였습니다.

![png](/assets/images/Stat/34_3.png)

- 왼쪽 그림에서는 COVID-19 심각도와 흡연 담배 사이의 양의 상관 관계를 관찰할 수 있습니다.
  - 흡연이 호흡기 질환의 위험 요소라는 것을 알고 있으니 이게 상식적인 결과입니다.
- 그런데 오른쪽 그림처럼 입원한 사람들의 데이터만 관찰하면 흡연과 COVID-19의 관계가 반전되는 게 보입니다.
  - 즉 마치 흡연을 하면 Covid 를 예방하는듯한 모습입니다.

![png](/assets/images/Stat/34_4.png)

- 이는 위와 같이 '입원한 사람으로만 ' 제한하여 생기는 에러입니다.
- 흡연과 Covid 모두 '입원' 과 양의 상관관계가 있기 떄문에 Collider 가 생겨 왜곡이 발생합니다.
  - 처음부터 샘플을 '입원한 사람' 으로 못박아버리면 위에서 잘생긴 남자의 예시처럼 코로나 심각도가 낮고 담배를 안피는 사람은 대부분 제외됩니다.
  - 즉 왼쪽 아래 데이터가 거의 없어지므로 음의 상관관계가 있는듯이 관찰되는 것입니다.

<br>

# Reference

- https://perfectmoment.tistory.com/2125
- http://hleecaster.com/statistical-paradoxes-in-data-science/
