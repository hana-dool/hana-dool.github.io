---
title:  "Anderson-Darling Test"
excerpt: "두 분포가 같은지 테스트 하는 방법"
categories:
  - Stat_Testing
last_modified_at: 2021-11-10

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Anderson-Darling 통계량은 데이터가 특정 분포를 얼마나 잘 따르는지 측정합니다. 지정된 데이터 집합 및 분포의 경우, 분포가 데이터에 더 적합할수록 이 통계량의 값은 더 작아집니다. 예를 들어, Anderson-Darling 통계량을 사용하여 데이터가 t-검정의 정규성 가정을 충족하는지 확인할 수 있습니다.
{: .notice--warning}

# [Anderson Darling test](#link){: .btn .btn--primary}{: .align-center}

> ## Anderson Darling Test

- Test statstic 이 다음과 같이 정의됩니다.

$$A^{2}=n \int_{0}^{1}\left(\hat{F}_{n}(t)-t\right)^{2} \omega(t) d t$$

- where $\omega(t) \geq 0$ is a weight function.

![png](/assets/images/Stat/101_1.png)

- 이때 아이디어는 위와 같습니다. 
  - 우리가 비교하고자 하는 DIstribution 는 t 의 분포라고 합시다. 
  - 우선 기준이 되는 분포는 그림과 같이 직선으로 나타날 것입니다. (어떤 값을 뽑던지, '그 값' 이 y 축이 되는게 아니라 '그 값의 cdf' 가 y 축이 되기 떄문입니다.)
  - 그리고 비교하고자 하는 분포는 위에서 그림과 같이 기준 분포와 완벽하게 일치하지 않는 이상 약간 틀어진 모양을 하게 될 것입니다. ( )
  
   **Reference**
  
- <https://support.minitab.com/ko-kr/minitab/18/help-and-how-to/statistics/basic-statistics/supporting-topics/normality/the-anderson-darling-statistic/>

