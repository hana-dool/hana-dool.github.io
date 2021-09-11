---
title:  "Permutation importance"
excerpt: "열을 무의미하게 만들어서 중요도 체크"
categories:
  - Interpretable_ML
tags:
  - 1
last_modified_at: 2021-09-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# [Permutation Importance](#link){: .btn .btn--primary} 

![jpg](/assets/images/ML/1_19.jpg)

- 주 아이디어는 다음과 같습니다. 
  - 동네 축구를 하고있는데 박지성(변수) 가 빠지자 골을 5골 먹혔다고 하자.
  - 그러면 박지성은 매우 중요한 사람이라는것을 알 수 있습니다. 
- 즉 , 우리가 살펴보고자 하는 특성 열을 셔플해서 의미없게 만듭니다. 
  - Permutation 된 열의 데이터와($X_{permutation}$) 기존의 데이터($X$) 를 집어넣었을떄에 성능 차이를 보게 됩니다. 
  - 만일, 특성 열을 섞었을때에 효과가 매우 떨어진다면 , 그 특성 열은 매우 중요한 변수라고 볼 수 있습니다. 

![jpg](/assets/images/ML/1_20.jpg)

- 모델간의 동등한 비교를 위해서, 정규화를 해준 값을 주로 사용하게 됩니다. 
  - j 번째 특성치에 대해서 그 성능을 $FI^j = e^{pemutation} / e^{base} $ 로 추정하게 된다. 
  - 이런 경우 최소한 j 가 의미가 있다면, permutation 시킨 값의 에러(로스) 가 , 원본 데이터보다 클 것이기 떄문에 대게 1보다 큰 값을 나타나게 됩니다. 

<br>

# [장단점](#link){: .btn .btn--primary} 

![jpg](/assets/images/ML/1_21.jpg)

- 장점 : 오류 '비율' 이 된다면 정규화가 되므로 다른 문제끼리 비교가 가능합니다. 
- 단점 : Loss 를 기반으로 Importance 가 매겨지기떄문에 Supervised Learning 일때에만 사용이 가능합니다. 
- 단점 : 또한 Permutation 을 한다는것은 , 비현실적인 데이터가 발생할 수 있습니다.
  - 키 : 120cm , 몸무게 300kg 같은 변수
- 무작위로 섞는것이여서 '큰 수' 로 시험하지 않는 경우 순서가 바뀔 여지가 있다. (Shap 에서 해결되었다고 합니다.)

# [Reference](#link){: .btn .btn--primary} 

- http://dmqa.korea.ac.kr/activity/seminar/297
- https://godongyoung.github.io/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D/2019/04/13/Partial-Depedence-Plot.html
- https://eair.tistory.com/

