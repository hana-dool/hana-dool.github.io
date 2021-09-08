---
title:  "Introduction"
excerpt: "왜 해석력을 가져야 하는가?"
categories:
  - Interpretable_ML
tags:
  - 1
last_modified_at: 2021-09-01

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# Introduction

## 모델 결과를 납득시켜주는 수단

- 우선 왜 모델 해석이 중요한지 알아보자.

![jpg](/assets/images/ML/1_4.jpg)

- 민수가 보험을 들고 싶다고 하자. 
- 머신 러닝 전문가가 건강 데이터를 통해서 민수의 보험료를 추정하게 한다. 

![jpg](/assets/images/ML/1_5.jpg)

- 하지만 고객 입장에서는 이러한 결과가 매우 의아함.
- 고객에게 모델 결과를 자연스럽게 납득 시켜주는 수단으로서 의의를 지닌다.

## 모델 파이프라인을 개선하기 위한 디버깅

![jpg](/assets/images/ML/1_7.jpg)

- 범죄율을 예측할때에 흑인이 더 범죄 확률이 높다고 예측하는것을 볼 수 있다.
  - 모델이 '편향' 을 가지고 있는것임 
  - 이러한 편향에 대해서 개선해야할 수 있다.

<br>

# Model Based Interpret

![jpg](/assets/images/ML/1_8.jpg)

- 모델의 종류에 구애받지 않는 방법론을 Model - Agnostic 이라고 합니다.
- 왜 이러한 해석방법이 중요한지 알아보겠습니다.

![jpg](/assets/images/ML/1_9.jpg)

![jpg](/assets/images/ML/1_10.jpg)

- 위와 같이 해석을 '모델' 입장에서 바라보았습니다. 
  - NN , 앙상블 트리 같은 모델의 경우 해석이 매우 어렵습니다.

<br>

# Model 중심 해석의 단점

![jpg](/assets/images/ML/1_10.jpg)

- 해석력이 모델에 종속되어있기 떄문에 다른 모델과 비교하기가 힘듭니다.
  - Tree 모델의 경우 Feature importance 가 기준 
  - Regression 의 경우 Coef 가 기준 
- 그러므로 모델에 구애받지 않는 (Model - Agnotic) 방법론이 있다면 모델의 비교가 가능할 것이다. 
- 물론 Model - Agnotic 이라는 방법론을 위 그림에서는 노란 동그라미 위치로 매우  좋다고 말하고있지만 , 사실 Trade Off 는 존재합니다.

<br>

# Model - Agnotic - Methods

![jpg](/assets/images/ML/1_11.jpg)

- 이러한 모델 Agnotic 방법의 경우 원래 모델을 블랙박스 취급하게 됩니다.
- input 을 조절하면서 , 모델이 뱉어내는 output 을 살펴보며 모델을 해석하게 됩니다.

<br>

# Refer

- http://dmqa.korea.ac.kr/activity/seminar/297
