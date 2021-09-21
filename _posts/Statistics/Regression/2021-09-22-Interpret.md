---
title:  "Feature importance in OLS(~ing)"
excerpt: "OLS 에서 feature 에 대한 중요도 해석해보기"
categories:
  - Regression
last_modified_at: 2021-09-22

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

OLS 에서 변수의 중요도를 해석하라고 하면 어떻게 할까요? 대부분은 그냥 Weight 를 reporing , p-value 를 reporting 하고 끝내려고 합니다. 하지만 이러한 방법론은 옳지 않습니다. 아래에서 더 정확한 방법론에 대해서 알아보도록 합시다.
{: .notice--warning}

# [Bad idea](#link){: .btn .btn--primary}{: .align-center}

> ## 1. 회귀 계수 비교하기

- 일반적으로, 변수 중요도를 파악하기 위해서 회귀 계수를 비교하는것은 안좋습니다.
- 예측 변수가 1 단위 증가할떄에 크게 기여하기 떄문에 중요하다고 생각할 수 있습니다만, 변수의 단위에 따라 계수가 달라지게 됩니다.
- 예를 들어서 몸무게를 kg 으로 설정한뒤의 계수와 g 으로 설정한 뒤의 계수는 크게 차이가 날 것이기 떄문입니다. 

> ## 2. P-value 

- 일반적으로 P-value 는 데이터가 클 떄에 작은 차이까지 잡아냅니다.
  - 그러므로 데이터가 크다면, 회귀 계수들은 대부분 유의하다고 나오게 됩니다. 
- 또는 추정치를 비교적 정확하게 추정할 수 있는 경우(즉 var(b_1) 이 작음)에도 p-value 는 작게 나오게 됩니다. 
- 즉 , '현재 내가 얻은 Feature 계수가 0이 아니다' 라는것은 말해줄 수 있지만, 이는 '이 Feature 가 중요한가' 와는 다소 다른 맥락이 되는것입니다.



# [Good idea](#link){: .btn .btn--primary}{: .align-center}

> ## 표준화된 계수

- 일반적으로 회귀 계수를 비교하게되면, 단위의 차이떄문에 적절한 비교가 힘들었습니다.
- 하지만 표준화된 계수를 이용한다면 , 이러한 단위의 차이를 상쇄시킬 수 있고 좀 더 객관적으로 비교할 수 있게됩니다.
- 즉 표준화된 계수의 절댓값이 가장 큰 변수를 찾으면 좋습니다.

> ## 변수가 마지막으로 추가될때의 R^2 변화

- 다른 변수가 모두 들어있는 상태에서 A 변수를 추가한다고 합시다.
- 중요한 변수라면, A 변수를 마지막에 추가할때에 R^2 값이 크게 늘어날것입니다. 

# [Cautions](#link){: .btn .btn--primary}{: .align-center}

> ## 다중공선성 Issue

- 하지만 다중공선성이 존재하게 된다면, 효과가 섞이게 되어서 importance 를 잘 ranking 하지 못하게 됩니다.

---

**Refer**

- <https://blog.minitab.com/ko/adventures-in-statistics-2/how-to-identify-the-most-important-predictor-variables-in-regression-models>
- <https://statisticsbyjim.com/regression/identifying-important-independent-variables/>
- <https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiView.kci?sereArticleSearchBean.artiId=ART002066171>



