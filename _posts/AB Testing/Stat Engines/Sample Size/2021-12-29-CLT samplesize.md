---
title: "CLT sample size"
excerpt: "T Test 를 수행하기 위한 샘플 수"
tags:
  - AB_Stat
last_modified_at: 2021-12-13
toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../../hana-dool.github.io
---

A/B Testing 에서 Proportion 검정하는방법
{: .notice--warning}

# [A/B Testing With unequal](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

- https://exp-platform.com/Documents/2014%20experimentersRulesOfThumb.pdf
- Continuous 지표의 경우, 일반적으로는 정규 분포를 따르는 것으로 가정되는 평균에 의존하게 됩니다.
  - 왜냐하면 Large Sample 일 경우,  CLT 를 기반으로 작동하기 떄문이죠.
- 통계 책들은 대게 이러한 CLT 를 만족시키면서, 검정하기 위해서면, 30명이면 충분하다는 말을 하기도 합니다. 
- 하지만 Online Experiment 의 경우 꼬리가 긴 데이터를 사용하는 경우가 많기 떄문에, 수천의 사용자가 필요할 수 있습니다.
  - Kohavi, Ron, et al. Online Controlled Experiments at Large Scale. KDD 2013: Proceedings of the 19th ACM SIGKDD international conference on Knowledge discovery and data mining. 2013. http://bit.ly/ExPScale
- Neil Patel 의 경우 매월 10000명의 방문자를 제안하기도 합니다.  (물론 이 지침의 경우, 메트릭의 분포에 대해서 각각 다른값을 가져야 할 것입니다.)
  - \29. Patel , Neil . 11 Obvious A/B Tests You Should Try. QuickSprout. [Online] Jan 14, 2013. http://www.quicksprout.com/2013/01/14/11-obvious-ab-tests-youshould-try/
- 물론 MDE 를 이용하여 계산하는 Sample Size 계산이 있기는 하지만, 이러한 방법론은 평균이 Normal 을 따른다고 가정한 상태에서의 계산법입니다. (즉 우리가 고려하는 Assumption 의 만족과는 크게 떨어져있는 상황)
- 우리의 경험에 따르면 온라인 실험의 많은 OEC 메트릭은 Skewed 되어 있습니다. 그리고 이러한 Skewness 로 인하여 많은 샘플사이즈를 요구하게 됩니다.

> ## Rules of Thums

- 이러한 Mean 이 Normal 을 따르게 하기 위해서, 필요한 샘플의 수는 $$355 \times s^{2} $$ 이상이 되는것을 추천드립니다.
  - 이떄 S 는 Skewness 로 아래와 같이 계산됩니다.

$$S=\frac{E[X-E(X)]^{3}}{[\operatorname{Var}(X)]^{3 / 2}}$$

- 이때 위와 같은 기준은 $\mid \text { skewness } \mid>1$ 일때에만 사용하기를 권장드립니다.

> Example 

- 아래와 같은 경우는, 위와 같은 Rules of Thums 를 적용하였을때 필요한 샘플 사이즈를 계산한 표입니다.

$$
\begin{array}{|l|r|r|r|}
\hline \text { Metric } & \mid \text { Skewness } \mid & \text { Sample Size } & \text { Sensitivity } \\
\hline \text { Revenue/User } & 17.9 & 114 \mathrm{k} & 4.4 \% \\
\hline \text { Revenue/User (Capped) } & 5.2 & 9.7 \mathrm{k} & 10.5 \% \\
\hline \text { Sessions/User } & 3.6 & 4.70 \mathrm{k} & 5.4 \% \\
\hline \text { Time To Success } & 2.1 & 1.55 \mathrm{k} & 12.3 \% \\
\hline
\end{array}
$$

- 커머스 사이트에서 Skewness 는 다음과 같이 계산되곤 합니다.
  - purchases/customer >10 
  - revenue/customer >30
- 위와 같은 Rule of Thumb 의 경우, 모두 Tail - probabilities 는 (nominally 0.025) 0.02~0.03 사이였습니다.
  - 이 규칙은 Boos와 Hughes-Oliver의 연구로부터 가져온 값입니다. (How Large Does n Have to be for Z and t Intervals?)
- 긴 꼬리 분포는 웹 데이터에 일반적이며 상당히 치우칠 수 있습니다. 위의 표에서, 우리는 수익/사용자의 편도가 18.2이므로 114k의 사용자가 필요하다는 것을 발견했습니다. 

![jpg](/assets/images/Stat/149_1.jpg)

- Figure 4: QQ-norm plot for averages of different sample sizes showing convergence to Normal when skewness is 18.2 for Revenue/user. Actual data used
- 그림 4는 사용자 100명과 1,000명만 표본으로 추출했을 때, 표본 평균의 분포가 상당히 치우쳐 있고 정규성이 실제 평균을 5% 이상 누락한다고 가정하는 95%의 이면 신뢰 구간을 보여줍니다.
  -  표본 크기를 100k로 늘리면 표본 평균의 분포가 -2 - 2 범위에서 정규 분포에 매우 가깝습니다.
- 메트릭에 큰 왜도가 있는 경우 평균이 더 빨리 정규성으로 수렴되도록 메트릭을 변환하거나 왜도를 줄이기 위해 값을 제한할 수 있습니다.
- 수익/사용자를 주당 사용자당 $10로 제한한 후, 우리는 왜도가 18에서 5.3으로 떨어지고 민감도(즉, 전력)가 증가하는 것을 보았다. 동일한 표본 크기의 경우 사용자당 수익 상한은 사용자당 수익보다 30% 작은 변화를 감지할 수 있습니다. 우리의 경험 법칙은 평균의 분포를 정규 분포로 근사화하는 데 필요한 사용자 수를 평가한다. 대조군과 치료가 동일한 분포를 가질 것으로 예상되는 경우 중요한 권장 사항이 있습니다.
- 대조군과 치료가 동일한 크기인지 확인하십시오. 분할이 동일한 크기(예: 50%/50%)이면 델타 분포는 대략 대칭(Null 가설에서 왜도가 0으로 완벽하게 대칭)이 되며, 경험 법칙은 유용한 하한을 제공하지 않는다(우리는 |sweness| 1 > 1일 때 규칙을 사용할 것을 권장했다). 검정력 계산은 일반적으로 표본 크기에 대한 하한을 제공합니다[16]. 작은 샘플로 치우친 분포의 경우, 부트스트래핑 기술을 사용할 수 있습니다 [44].

# [How Large Does n Have to be for Z and t Intervals?](#link){: .btn .btn--primary}{: .align-center}

https://sci-hub.st/https://doi.org/10.1080/00031305.2000.10474524

---

**reference**

- https://geoffruddock.com/run-ab-test-with-unequal-sample-size/



