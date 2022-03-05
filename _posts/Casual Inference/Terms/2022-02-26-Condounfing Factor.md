---
title:  "Confounding Factor (교란요인)"
excerpt: ""
categories:
  - Casual_Inference_Terms
last_modified_at: 2022-01-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 상관관계와 인과관계의 relationship
{: .notice--warning}

# [Confounding Factor](#link){: .btn .btn--primary}{: .align-center}

> ## Definition

- 이번에 살펴볼 개념은 상당히 통계적이면서도 **Causality**를 연구하는 사람들에게 꼭 필요한 내용이다. 바로, **Confounding factor (Confounder)**에 대해서 살펴보겠다. 먼저, **Confounding 효과**에 대한 상황을 살펴보면, 아래와 같이 X라는 입력 변수가 의약품이라고 하고, 이 의약품을 먹었을 때, 실제로 회복이 되는지 (Y)의 출력을 확인해보고자 한다. 하지만, 만약에 이 의약품이 성별(Z)의 영향을 받는다고 한다면, 사실은 성별에 의해서 이 의약품이 진정한 원인이 아닐 수도 있게 된다. 이러한 상황에서 Z 라는 변수가 Confounding Factor (Confounder)가 된다. 

![jpg](/assets/images/Stat/156_1.jpg)

- 위의 상황을 수학적인 용어로 정의해보면, 아래와 같이 된다. 

$$P(y \mid d o(x)) \neq P(y \mid x)$$

- 여기서 do() 라는 표기법이 의미하는 것은 x를 통제한다는 것으로 영어로 하다(do)라고 해서 실제로 x를 조절해보는 것이다. 즉, x를 조절했을 때, y의 확률이라는 것은 x를 내가 직접 바꾸었을 때, y가 바뀌는 효과를 보는 것이므로, 실제로 원인인지 아닌지를 확인할 수 있다. 그런데 그것을 그냥 조건부 확률로 나타낸 경우와 차이점을 생각 해본다면, 조건부 확률, P(y | x)에서는 x에 영향을 주는 z의 효과가 들어간다. 따라서, 위의 상황에서는 z가 x에 영향을 주기 때문에 아무래도 x에 들어 있는 값들이 순수하게 x를 조작해서 얻을 수 있는 값이 아니다. 따라서, 두 값은 달라지고, 이 조건을 토대로 **Confounding 효과**를 검사해볼 수 있다. 
- 개념을 간략히 정리하면 아래와 같다. 

> *Y의 원인이 X라고 하고 싶은데,*
>
> X와 Y에 동시에 영향을 주는 제 3의 변수 Z가 존재할 때 Confounding Effect가 발생하고,
>
> 해당 변수 Z를 Confounding Factor또는 Confouder 라고 부른다.

- 사실 **Confounding Effect**에 대해서는 최근 AI가 발달하면서 관련된 알고리즘적인 접근법이 발달하고, Inference 를 해야 하는 일이 많아 지면서 많이 알려졌기 때문에 개념 정도는 대부분 이해하고 있을 것이다. 내가 이 주제를 꺼낸 것은 이와 비슷한 개념은 **Collapsibility**의 개념을 보다 쉽게 설명하기 위해서이다. 이후 포스팅에서 **Confounding과 Collapsibility를 비교하면서 이 둘의 차이**를 이해하고, Causality 연구에서 Confounding 만큼 Collapsiblity도 고려되어야 한다는 것을 강조하고자 한다. 

---

**Reference**

- https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=sw4r&logNo=221527236795
