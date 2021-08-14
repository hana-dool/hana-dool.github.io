---
title:  "Introduction"
excerpt: "왜 Paradox 를 공부하게 되었나."
categories:
  - Stat_Paradox
tags:
  - 1
last_modified_at: 2021-08-12

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# Why?

- 통계 분석을 할 때에는 모델링 / 분석도 중요하지만 해석시 함정에 빠지지 않는것도 중요합니다. 
- 오류와 역설은 대부분 가설(모형) 설계 과정에서 잘못된 판단을 했을 때 생길 수 있는 문제들입니다. 
- 즉 이러한 Paradox 를 공부한다면 내가 함정에 빠지지 않을 수 있으므로 의미가 있습니다.

# Reference 

- https://careerly.co.kr/comments/18785
- https://en.wikipedia.org/wiki/Category:Statistical_paradoxes

1) Absence of evidence - https://www.bmj.com/content/311/7003/485.long
- 증거의 부재를 부재의 증거로 판단하는 오류
- p-value 가 높아서 통계적 유의성을 갖지 못한다고 해서 실제 아무런 효과가 없는 것이라고 판단해서는 안됨

2) Ecological fallacy - https://web.stanford.edu/class/ed260/freedman549.pdf
- 집단에서 관측된 현상이 개체에서도 적용된다고 판단하는 오류
- 예를 들어, 지방 섭취량이 많은 나라의 유방암 발생률이 높다고 해서 지방을 많이 섭취하면 유방암 발생률이 높아진다 라고 단정할 수 없음

3) Stein's paradox - https://www.researchgate.net/profile/Carl-Morris-3/publication/247647698_Stein%27s_Paradox_in_Statistics/links/53da1fe60cf2631430c7f8ed/Steins-Paradox-in-Statistics.pdf

- 그냥 평균을 구한 값보다 평균에 편향을 준 값이 더 좋은 추정값을 갖는 현상
- James-stein 추정량 (james-stein estimator) 이라는 방법이 있음

4) Lord's paradox - https://errorstatistics.com/2019/08/02/s-senn-red-herrings-and-the-art-of-cause-fishing-lords-paradox-revisited-guest-post/
- 두 집단에 대해 사전사후 분석을 할 때 변화값에 대해 t-검정한 결과와 ANCOVA로 검정한 결과가 달라지는 현상

7) Prosecutor's fallacy - https://academic.oup.com/aje/article/179/9/1125/103523

- P(A|B) 와 P(B|A) 가 같다고 가정하는 오류
- P(A) 와 P(B) 가 같을 경우에만 맞음

8) Gambler's fallacy - https://en.wikipedia.org/wiki/Gambler%27s_fallacy
- 서로 독립적인 사건임에도 불구하고 과거에 발생 빈도가 낮다는 이유로 앞으로 발생 확률이 높아질 것이라고 믿는 것
- 예를 들어 지난 주 로또 당첨 번호는 이번 주에 당첨될 확률이 낮다고 생각하는 것

9) Lindley's fallacy - https://link.springer.com/article/10.1007/s11229-014-0525-z
- 빈도주의 통계 검정 결과와 베이지안 통계 검정 결과가 완전히 다르게 나오는 현상
