---
title:  "Model Agnotic Method?"
excerpt: "왜 모델과 상관없는 해석이 더 좋을까?"
categories:
  - Interpretable_ML
last_modified_at: 2021-09-01

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [Model Based Interpret](#link){: .btn .btn--primary}{: .align-center}

> ## Model Based Interpret

![jpg](/assets/images/ML/1_8.jpg)

- 모델의 종류에 구애받지 않는 방법론을 Model - Agnostic 이라고 합니다.
- 왜 이러한 해석방법이 중요한지 알아보겠습니다.

![jpg](/assets/images/ML/1_9.jpg)

![jpg](/assets/images/ML/1_10.jpg)

- 위와 같이 해석을 '모델' 입장에서 바라보았습니다. 
  - NN , 앙상블 트리 같은 모델의 경우 해석이 매우 어렵습니다.

> ## Model 중심 해석의 단점

![jpg](/assets/images/ML/1_10.jpg)

- 해석력이 모델에 종속되어있기 떄문에 다른 모델과 비교하기가 힘듭니다.(유연성이 떨어짐)
  - Tree 모델의 경우 Feature importance 가 기준 
  - Regression 의 경우 Coef 가 기준 
- 그러므로 모델에 구애받지 않는 (Model - Agnotic) 방법론이 있다면 모델의 비교가 가능할 것이다. 
- 물론 Model - Agnotic 이라는 방법론을 위 그림에서는 노란 동그라미 위치로 매우  좋다고 말하고있지만 , 사실 Trade Off 는 존재합니다.

> ## Model Agnotic Methods

![jpg](/assets/images/ML/1_11.jpg)

- Model Agnotic 방법론은 모델을 블랙박스로 그대로 둔 뒤에 Output 을 살펴보며 해석하게 됩니다. 

> ## Agnotic 방법론이란?

![jpg](/assets/images/ML/4_2.png)

- 위 그림처럼 첫 단계에서는 데이터가 현실세계를 요약하게 됩니다.
- 두번쨰 단계에서는 요약된 데이터를 블랙박스 모델이 최대한 학습하게 됩니다.
- 세번쨰 단계에서는 기계학습을 '인간이 받아들일 수 있도록' 해석하는 단계입니다.

> ## Agnotic 방법론이 가져야할 바람직한 특성

> 모델 유연성

- 이러한 해석법은 대게 모델에 구애받지 않습니다. 그러므로 어떠한 모델을 사용하더라도, 같은 Form 으로 해석할 수 있게됩니다.
- 즉 다른 모델끼리도 같은 기준으로 해석을 비교할 수 있게됩니다. 
  - 전통적인 경우 Linear regression 의 Coef 와 트리 모델의 Feature importance는 비교하기가 힘듭니다.

> 설명 유연성 

- 특정한 양식의 설명에만 한정되지 않습니다. 
- 즉 선형공식으로 설명 / 특성값 중요도로 설명 등 다양한 방법으로 해석이 가능합니다. (모델과는 상관없이!)

> 표현 유연성 

- 설명 시스템은, 모델과 다른 특성값 표현도 사용할 수  있어야 합니다.
- 즉, 이미지 분류기의 해석의 경우 pixel 만 사용한것보다는, 다양하게 나눈 지역을 통해서 해석을 할 수도 있습니다.

**Reference**

- http://dmqa.korea.ac.kr/activity/seminar/297
- https://brunch.co.kr/@natrsci/86
