---
title:  "베르트랑의 역설"
excerpt: "고전적 확률 정의의 폐인"
categories:
  - Stat_Paradox
tags:
  - 1
last_modified_at: 2021-08-05

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# 베르트랑의 역설

- 확률론에서 베르트랑의 역설은 , 확률의 고전적 정의에 대한 역설입니다.
- 조제프 베르트랑이 확률론이라는 책에서 제시한 역설입니다.

> 원에 내접하는 정삼각형을 그리고 원에서 임의의 현을 선택할 때, 현의 길이가 정삼각형의 한 변의 길이보다 클 확률은?

<br>

# 1. 첫번쨰 답 (1/3)

![png](/assets/images/Stat/30_1.png)

<br>

# 2. 두번째 답 (1/2)

![png](/assets/images/Stat/30_2.png)

<br>

# 3. 세번째 답 (1/3)

![png](/assets/images/Stat/30_3.png)

<br>

# 왜 이런일이..?

- 이는 '랜덤을 어떻게 정의하느냐' 에 따라 달라지는것입니다. 
- 만약 우리가 현들을 무작위로 그린다고 합시다. 그러면 어떻게 무작위로 그릴 수 있죠? 

## 1번 풀이의 Random

1. Uniform($0,2\pi R$) 분포에서 원의 둘레중 하나의 점을 선택한다. 이 점이 현의 시작점이 된다.
2. 선택한 점에서, Unif(0,180) 에서 각도를 하나 선택하여, 이 각을 그리게 현을 그린다.  

## 2번 풀이의 Random 

1. Uniform($0,2\pi R$) 에서 원의 둘레중 하나의 점을 선택한다. 
2. 그 점을 원의 중심과 이은 선을 L 이라 하자. 이 선 위에서 , 즉 Uniform($0,R$) 에서 하나를 골라 그 점이 현의 중심이 되게 하고, L 과 수직이 되게 한다.  

## 3번 풀이의 Random

1. 원의 중심을, 원에서 Random 하게 고른다. 즉 2-dimensional Uniform distribution with Circle 분포를 통해 중심을 고른다. 

2. 고른 중심에 대해서, 원의 중심과 이었을때에 수직이 되게 현을 그린다. 

<br>

# 각 풀이의 Simulation

![png](/assets/images/Stat/30_4.png)

- 위와 같이 Simulation 을 하게되면 각각 다른 랜덤성에 의해 다른 현들의 분포가 나오게 됩니다. 
- 즉.. 이 문제는 '랜덤성이 제대로 정의되지 않았기 때문에 나오는 Paradox 인 것입니다.'

# Solutions

- 이러한 역설은 어디에서 나오는 것일까요? 
- 그것은 바로 확률의 고전적 정의에서 오는 에러입니다. 
