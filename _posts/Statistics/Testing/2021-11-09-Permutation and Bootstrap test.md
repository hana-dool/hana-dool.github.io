---
title:  "Permutation and Bootstrap test"
excerpt: "Permutation test 와 boo"
categories:
  - Stat_Testing
last_modified_at: 2021-11-09

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Permutation 와 Bootstrap 테스팅의 차이에 대해서 알아보도록 하겠습니다.
{: .notice--warning}

# [Testing](#link){: .btn .btn--primary}{: .align-center}

> ## Permutation Testing

- Permutation test 는 F 에 대해서 어떠한 추정도 하지 않습니다. 
- Two Sample Mean Testing 을 하는 경우를 생각해 보겠습니다.
  - $X\sim F $ , $Y \sim G$ 라고 합시다. 하지만 Permutation Testing 의 경우 $H_0 : F = G$ 를 가정하게 됩니다.
  - 하지만 우리는 $H_0 : E(X ) = E(Y)$ 에 대해서 테스트 하고 싶은것인데 말입니다. 
  - 다시 말하면, F 와 G 는 평균만 다른게 아닐 수 있을 것입니다. (ex $V(X )\not =  V(Y)$) 하지만 $E(X)= E(Y)$ 인 이상 Null Hypothesis 를 만족한다고 나오게 되는것이죠. 
- 이렇게 특정한것 (평균이라던지..) 을 비교하고 싶은 경우에는 Permutation Test 로는 불가능합니다. 하지만 Bootstrap 은 'F' 를 아예 추정해서 통계량을 추정하는 형식이므로 가능합니다.



> ## Bootstrap Testing

- Bootstrap Testing 은 실제 F 에 대해서 emprirical cdf $\hat{F}$ 를 추정하려 하고, 여기에서 p-value 를 이끌어내려 합니다.
- Two Sample Mean Testing 을 하는 경우를 생각해 보겠습니다. 
- 

---

   **Reference**

- <https://myweb.uiowa.edu/pbreheny/uk/teaching/621/notes/10-11.pdf>

 위와 같은 방법론은 비교하기가 편리해서 많은사람이 잘못 판단하는 부분이라 주의가 필요합니다. Schenker와 Gentleman (2001)은 의학 분 야 학술지에서 이러한 오류를 범한 논문을 60개 넘게 발견했다고 보고했다고 합니다..
{: .notice--success}

