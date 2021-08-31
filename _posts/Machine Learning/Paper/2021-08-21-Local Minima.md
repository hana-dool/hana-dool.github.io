---
title:  "Local Minima"
categories:
  - Stat_Machine_Learning
tags:
  - 1
last_modified_at: 2021-08-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

- 다크프로그래머 님의 블로그 'Local Minima 문제에 대한 새로운 시각' 글을  가져왔습니다.

# Local Minima는 존재하는가?

- 2014 년에 local minima 문제에 대한 흥미로운 논문이 하나 발표되었다. 정식으로 출판된 논문은 아니고 arXiv(아카이브)에만 등록된 논문이다. 

- [Dauphin14] Y. Dauphin, R. Pascanu, C. Gulcehre, K. Cho, S. Ganguli, Y. Bengio. Identifying and attacking the saddle point problem in high-dimensional non-convex optimization.

- Local minima 문제는 에러를 최소화시키는 최적의 파라미터를 찾는 문제에 있어서 아래 그림처럼 파라미터 공간에 수많은 지역적인 홀(hole)들이 존재하여 이러한 local minima에 빠질 경우 전역적인 해(global minimum)를 찾기 힘들게 되는 문제를 일컫습니다.

![png](/assets/images/Machine Learning/1_1.png)

- 기존에 기계학습(machine learning)이 잘 안되거나 성능이 잘 안나오는 이유는 학습 도중 이러한 local minima에 빠졌기 때문이라는 게 일반적인 상식이었다.
- 하지만 이 논문은 기존의 상식을 깨고 local minima 문제가 사실은 고차원(high dimensional)의 공간에서는 발생하기 힘든 매우 희귀한 경우라고 주장한다.
- 그 이유는 예를 들어, local minimum이 형성되기 위해서는 함수의 변화 그래프가 모든 축의 방향으로 밥그릇처럼 오목한 형태가 되어야 하지만 아래 그림의 p처럼 어느 한 방향이라도 아래로 흘러내리면 local minima가 형성되지 않기 때문이다. 그리고 고차원의 공간에서 모든 축의 방향으로 오목한 형태가 형성될 확률은 거의 0에 가깝다는게 주장의 요지이다.

![png](/assets/images/Machine Learning/1_2.png)

- 함수 최적화 문제를 풀때 일차적으로는 미분값이 0인 즉, f' = 0인 지점을 찾는 것이 일반적이다. 
- 그리고 일차 미분이 0인 지점을 critical point라 부른다. 어떤 critical point가 local minima가 되기 위해서는 모든 축의 방향으로 함수 그래프가 아래로 볼록(f''>0)이 되어야만 한다. 
- 즉, n차원의 다변수 함수 f(x1, x2, ..., xn)이 있을 때 다음의 조건을 만족해야 한다.

![png](/assets/images/Machine Learning/1_3.png)

- Critical point에서 모든 축 방향으로 곡률(이차미분)이 양수인 경우는 위로 볼록, 아래로 볼록이 랜덤하게 발생한다고 가정하면 차원이 증가할수록 확률적으로 매우 힘든 일이므로(1/2n) 대부분의 critical point는 local minima가 아니라는 것이다.

- 처음 이 내용을 접했을 때 꽤나 신선하고 재미있는 주장이라고 생각했다. 그러면서 정말 그럴까? 그렇다면 고차원의 최적화 문제에 대해서는 이제 더이상 local minima 문제를 걱정하지 않아도 되는 것일까? 하는 의구심도 들었다.

- 먼저, [Dauphin14] 논문의 내용을 그대로 옮겨보면 다음과 같다.

> Intuitively, in high dimensions, the chance that all the directions around a critical point lead upward is exponentially small w.r.t. the number of dimensions, unless the critical point is the global minimum or stands at an error level close to it, i.e., it is unlikely one can find a way to go further down.

- 즉, 고차원의 공간에서 발생하는 critical point(일차 미분이 0인 지점)는 거의 대부분 saddle point이며 만일 saddle point가 아닌 경우는 global minimum이거나 또는 global minimum과 유사한 수준의 local minima라는 것이다.

- 잘 보면 이 내용에는 2가지 주장이 함께 섞여 있다. 하나는 고차원의 공간에서 대부분의 critical point는 local minima가 아니라 saddle point라는 점이다. 그리고 다른 한가지는 고차원의 공간에서 설령 local minima가 발생한다 하더라도 이는 global minimum이거나 또는 global minimum과 거의 유사한 수준의 에러 값을 갖는다는 것이다.

- 먼저 첫번째 주장은 비교적 직관적으로 쉽게 수긍할 수 있다. Critical point란 모든 축의 방향으로 일차 미분값이 0인 지점(f' = 0)으로서 다른 말로 stationary point라고도 한다. 그리고 이러한 critical point에는 크게 극대점(maxima), 극소점(minima), 그리고 saddle point가 있는데 saddle point란 극대 또는 극소가 아닌 모든 critical point로 정의된다. 따라서, 고차원의 공간에서 critical point는 대부분 확률적으로 saddle point인 것으로 볼 수 있다.

- 그런데 두 번째 주장 즉, 고차원의 공간에서 발생하는 local minima는 global minimum이거나 또는 global minimum과 거의 유사한 수준의 에러 값을 갖는다는 점에 대해서는 쉽게 수긍이 가지 않는다.

- 논문에서는 그 근거로서 실험적으로 critical point들에서 에러를 측정해 보니 critical point에 포함된 위로 볼록인 방향축의 비율이 크면 클수록 높은 에러를 가진다는 실험 결과를 예로 든다. 그리고 local minim는 위로 볼록인 경우가 하나도 없는 경우이기 때문에 결과적으로 매우 낮은 에러를 갖게 될 것이라는 게 이들의 주장이다. 
- 하지만 차원이 증가할수록 만일 critical point 자체의 수도 같이 증가한다면 여전히 local minima도 다수 존재하게 되는 것은 아닐까 하는 의문이 든다. 그리고 고차원의 세계에서는 그만큼 어떤 예측하기 힘든 다양성들이 존재할텐데 global minimum 하나밖에 존재하지 않는다는 것은 그 자체로 상상하기 힘든 측면이 있다.

- 그리고 두 번째 주장에 대해서는 하나의 실험적 사례 외에는 별다른 논리적 근거가 제시되어 있지 않다. 그리고 그 실험적 사례 또한 local minima가 global minimum에 근접할 것이라는 직접적인 증거는 되지 못한다고 생각한다. 그건 하나의 실험 예에서 높은 에러를 가진 local minima를 발견하지 못했다고 해서 다른 문제에서도 나타나지 않을 것이라고 일반화하긴 힘들다고 생각하기 때문이다.

- 하지만 아직은 이들의 주장이 명확하게 증명되거나 반증된 것이 아니기 때문에 어떤 것이 사실인지는 알지 못한다.

# Summary

- 이 글에서는 local minima의 존재 여부에만 초점을 맞추었지만 사실 [Dauphin14] 논문의 초점은 조금 다른데 있습니다. 
- 이 논문의 핵심은 "Critical point 근처에서는 함수의 수렴속도가 느려지기 때문에 기존의 기계학습이나 최적화 기법에서 변화가 거의 없이 정체가 되는 현상이 발생하였는데 이를 기존에는 local minima 문제라고 착각하였다. 
- 하지만 사실은 이들이 local minima가 아니라 실제로는 대부분 saddle point들이며 기존 기계학습 방법 또는 최적화 기법들이 잘 동작하지 않았던 이유는 기존 탐색 방법이 saddle point에서 벗어나지 못하는 문제가 있었기 때문이다. 
- 그리고 우리는 이러한 saddle point 문제를 극복할 수 있는 새로운 탐색 방법을 제시한다"입니다. 이 논문에서 제시한 새로운 탐색 방법도 꽤 유용해 보이며 한번쯤 읽어볼 만한 좋은 논문으로 생각됩니다. 

# Refer

- https://darkpgmr.tistory.com/148?category=761008

  

