---
title: "Peeking at A/B Tests"
excerpt: "Sequential Test"
categories:
  - AB_Paper
last_modified_at: 2022-03-10

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 Outlier 를 검정하기 위해서 어떻게 해야할까?
{: .notice--warning}

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## Abstract 

- 온라인 실험은 인터넷 회사에서 신제품 기능을 평가하는 데 널리 사용되어 왔습니다. 하지만 이떄 Outlier 값의 존재는 실험 결과의 유효성에 영향을 끼치게 됩니다.
- 이 연구에서는 mechanism-independent outlier filter 를 다양한 메트릭에 대해서 적용해 보았습니다.
- 이러한 Outlier filter 를 적용함으로서 나타나는 효과를 정량화 하고, Outlier filter 가 다양한 유형의 메트릭에 대해서 적용될 수 있음을 보이려고 합니다.

> ## INTRODUCTION

- 특이치는 데이터 오류, 웹 크롤러, impression 상의 fruad , 클릭의 farud 등 다양한 출처에서 발생되곤 합니다.[6] [18]
- 특이치 생성 및 검출 메커니즘은 
-  사기 및 클릭 사기를 포함한 여러 출처에서 발생한다 [6] [18]. 
- 특이치 생성 및 검출 메커니즘은 여러 문헌[4] [10]에서 광범위하게 연구되었다. 
- Oath 에서는, 대부분의 robotic traffic 은 자체적인 사내 traffic protection engine 이 작동하여서 filering 하고 이쓴 중입니다. 
- 하지만 실제로, 우리는 특히 온라인 실험에서 소수의 특이치가 이 traffic protection 엔진에서 벗어날 수 있고 데이터 분석을 복잡하게 할 수 있다는 것을 관찰했습니다.

> Online Controlled Experiment

- A/B 테스트라고도 불리는 온라인 제어 실험은 아마존, 페이스북, 구글, 링크드인, 넷플릭스, 빙, 야후 등을 포함한 인터넷 회사에서 신제품 기능을 평가하는 데 널리 사용되어 왔습니다[11] [13] [15]. 
- 하지만 이떄 특이치(Outlier)의 존재는 제품 의사결정 과정에서, 중요한 경험적 결과의 타당성에 위협이 된다.
- 최근의 연구는 소량의 이상치라도 잘못된 분석을 유발할 수 있으며, 극단적인 경우 실험 결과를 완전히 되돌릴 수 있다는 것을 입증했습니다.[16] [9].
- 대규모 실험 플랫폼에서는 남은 특이치를 제거하고 제품 및 장치에 걸쳐 다양한 유형의 메트릭에 대처하기 위한 필터가 필요하다. 
  - 또한 specific outlier generation mechanism 에 의존하지 않는 것이 바람직하다.

> paper 에서 다루는것

- 본 논문은 mechanism- independent filter 를 실제로 적용할때에 Oath 에서 일어났던 문제들을 다루어볼 것입니다.
- 이 연구의 맥락을 설정하기 위해 우리는 우선 최근에 발표된 통계 방법과 관련된 배경 정보를 먼저 제시할 것입니다[9]. 
- 우리는 대규모 실험 플랫폼에서 이 필터의 구현에 초점을 맞출 것입니다. 
- 또한 actual experiment data 를 이용하여 outlier filter 에 대한 성능을 검정하고, 다양한 유형의 메트릭에 확장 가능하다는것을 보이려고 합니다. 

# [Methodology](#link){: .btn .btn--primary}{: .align-center}

> ## Methology

- 데이터 점이 특이치가 될 확률을 정량화하기 위해서 분포 기반 이상치 검출 방법이 최근 도입되었습니다[9].
- 이 프레임워크에서는 온라인 카운트 데이터의 분포를 모델링하기 위해 파라메트릭 허들 모델[12]을 제안하려고 합니다.
- 시뮬레이션 연구에 따르면 정규성 기반 방법, 비모수 방법(상자 그림 및 햄펠), 분류 방법(Kmean 및 상형 군집화)을 포함하여 기울어진 온라인 데이터에서 일반적으로 사용되는 특이치 방법보다 성능이 우수하다고 합니다. 
- 이는 two-component model 로서 0 값을 다루기 위한 positive observations 에 대한 생성모델과, truncated Negative Binomial distribution 이 있습니다.

$$Y_{i} \sim \begin{cases}0 & \text { with probability } 1-p \\ Z T N B(\rho, \gamma) & \text { with probability } p\end{cases}$$

- 이때 $$Z T N B(\rho, \gamma)$$ 는 zero-truncated Negative Binomial Distribution 으로서 다음과 같은 Probability Function 을 가지게 됩니다.

$$P\left(y_{i} \mid y_{i}>0, \rho, \gamma\right)=\frac{1}{1-(1-\rho)^{\gamma}} \frac{\Gamma\left(y_{i}+\gamma\right)}{y_{i} ! \Gamma(\gamma)}(1-\rho)^{\gamma} \rho^{y_{i}}$$

- 이때 $$\Gamma(\cdot)$$ 는 Gamma Function 을 말합니다.

> 과연 $ZTNB$ 가 Log Data 를 잘 모델링 하는가? 

- AIC (Akaike Information Criterion) 기준으로 Page View 를 잘 모델링 하는지를 검사해 보았습니다.
  - 이떄 Normal, Poisson, Negative Binomial and Hurdle model 을 비교해 보았습니다.

$$\begin{array}{cc}
\hline \text { Model } & \text { AIC } \\
\hline \text { Normal } & 613,363 \\
\text { Poisson } & 2,102,440 \\
\text { Negative Binomial } & 404,037 \\
\text { Hurdle Model } & 365,531 \\
\hline
\end{array}$$

- 그 결과를 보면 위와 같습니다. AIC 기준으로 Hurdle Model 이 제일 우수한 성능을 보여주고 있는것을 볼 수 있습니다.

![jpg](/assets/images/Program/72_1.jpg){: .align-center}

- 위 그림은 20이 넘는 Page View 는 짤라낸뒤에 그린 그래프입니다.
  - 막대는 실제 실험값을 의미하고, 각각의 선들은 그에 따른 분포들을 나타냅니다.
- 이 분포를 살펴볼때에, Hurdle model 이 어느정도 그 분포를 잘 근사하고 있음을 알 수 있습니다.
- 관측된 실험 데이터의 최대값은 , 허들 모형에 근거하여 특이치 검정의 대상이 됩니다. 
- 다중 특이치의 결과로 마스킹 및 스웜핑 효과를 처리하기 위해서 [1] [8] OPTSM Sample maximum 을 검정하는 방법을 제시하려고 합니다.

> ## OPTSM

- 관측된 표본 최대값은 허들 모형에서 도출된 표본 최대값의 분포에 기초한 특이치 검정의 대상이 됩니다. 
- 다중 특이치의 결과로 마스킹 및 스웜핑 효과를 처리하기 위해 [1] [8], OTPSM 이라고도 하는 샘플 최대값을 갖는 외부 시험 절차를 다음과 같이 채택하였습니다.

> 들어가기 전에 : DFBETAS 란 무엇인가?

- DFBETAS(DFference in BETAS)는 특정 데이터를 제외한 회귀 계수와 모든 데이터를 이용한 회귀 계수의 차이를 이용하며 다음과 같이 정의합니다.

$$(D F B E T A S)_{k(i)}=\frac{\hat{\beta}_{k}-\hat{\beta}_{k(i)}}{\sqrt{M S E_{(i)} c_{k k}}}, k=1,2, \cdots, p \quad ...(3)$$

- 여기서 $c_{k k}$ 는 $\left(X^{t} X\right)^{-1}$ 의 $k$ 번째 대각원소입니다. (3)식은 다음과 같이 변형가능합니다.

$$(D F B E T A S)_{k(i)}=\frac{a_{k i} e_{i}}{1-h_{i i}}\left[\frac{1}{n-p-1}\left(S S E-\frac{e_{i}^{2}}{1-h_{i i}}\right)\right]$$

- 영향점을 판단하는 기준은 데이터의 개수가 적은 경우에는 $(D F B E T A S)_{k(i)}$ 의 절대값이 1 보다 큰 경우, 데이터가 많은 경우에는 $(D F B E T A S)_{k(i)}$ 의 절대값이 $2 / \sqrt{n}$ 보다 큰 경우 영향점이라고 판단합니다.

> Procedure

1. Calculate DFBETA [7] for each data point in the complete sample $Y$
2. Divide $Y$ into two sets $Y_{N}$ and $Y_{O}$,  where $Y_{N}=\left\{y_{i}\right.$ : $y_{i} \in Y$ and $\left.D F B E T A_{i} \leq \frac{2}{\sqrt{n}}\right\}$ and $Y_{O}=\left\{y_{i}: y_{i} \in\right.$ $Y$ and $\left.D F B E T A_{i}>\frac{2}{\sqrt{n}}\right\} . Y_{O}$ contains all influential data points to be further examined.
3. Estimate the parameters of target distribution $F$ using sample $Y_{N}$. For count data, we use the Hurdle model as described.
4. Locate the minimum value in $Y_{O}$, and test whether it is an outlier in $Y_{N}$ with hypothesis testing.
5. If it is not an outlier, move it from $Y_{O}$ to $Y_{N}$ and iterate steps 3-5. If it is an outlier, the procedure terminates. The sample  minimum of the resultant $Y_{O}$ is set as the threshold for outliers.

# [Implementation](#link){: .btn .btn--primary}{: .align-center}

> ## Implementation

- Oath 에서는 다양한 국가, 언어 및 장치의 여러 웹 및 앱 제품에 걸친 온라인 실험을 위한 내부 플랫폼이 구축되었습니다.[16] [17] [3] [5]. 
- 사용자 행동(User Experience) 및 수익 지표와 같은 각 실험의 주요 지표가 통계 분석을 위해 매일 집계됩니다.
- 최종 사용자에게 결과가 Tableau 대시보드에 표시되기 전에 OTPSM에 의해 결정된 이상 필터가 데이터 파이프라인에 추가되게 됩니다.

> ## ETL Process for Experimentation Data

![jpg](/assets/images/Stat/157_3.jpg){: .align-center}

- 위 그림은 우리가(Oath) 구현한 아키텍쳐 설계를 보여줍니다.
- 실험이 생성되고 배포될 때 트래픽 Splitter 는 사용자를 사전 정의된 크기의 테스트 샘플에 무작위로 할당하기 시작합니다. 
- 또한 테스트 샘플의 메타데이터는 배치 데이터 파이프라인에서 테스트 샘플을 식별하기 위해 ETL 프로세스에서 사용되는 차원 테이블로 유입됩니다. 
- 실험 데이터는 매시간 수집되고 추가 처리를 위해 매일 사용자 수준에서 집계됩니다. 
- 일별 측정지표는 제품명, 장치 등을 포함한 제품차원별로 그룹화됩니다. 
  - 예를 들어, 제품 C App에 기록된 페이지 뷰 이벤트는 제품에 대한 사용자당 일별 페이지 뷰 수로 집계됩니다.

> ## Implementation of OTPSM

- 제안된 이상치 필터는 일일 메트릭이 집계된 후 적용됩니다. 
- OTPSM을 구현하기 위한 한 가지 과제는 각 이상치 임계값을 결정하는 것과 관련된 계산 부담입니다. 
- 플랫폼에 매일 수백 개의 실험이 병렬로 실행 중일 때 모든 실험 메트릭에 대해 반복하는 것은 매우 비용이 많이 드는 작업입니다. 
- products 에 대한 정상 데이터의 분포가 일반적으로 안정적이라는 사실을 고려할 때, 우리는 products 수준에서 범용적이고 일정한 필터를 구현하려 했습니다. 
- 이는 모든 실험마다 반복적인 계산 없이 알고리즘의 실행 횟수를 크게 줄이게 되었습니다.
  - 예를 들어, 제품 C 앱의 경우 페이지 뷰와 같이 일반적으로 사용되는 메트릭을 선택하고 OTPSM 절차를 한 번 실행하여 해당하는 Outlier 임계값을 얻게 됩니다.
  - 그런 다음 데이터 파이프라인에 적용되어 이 임계값보다 큰 페이지 뷰를 가진 특이치를 제거합니다. 
- 이러한 접근 방식을 통해 플랫폼에서 수백 개의 동시 실험을 수행할 수 있도록 확장할 수 있는 강력한 필터를 구현할 수 있습니다. 

# [PERFORMANCE AND EVALUATION](#link){: .btn .btn--primary}{: .align-center}

- 이 섹션에서는 세션, 페이지 뷰 및 클릭이라는 일반적으로 사용되는 세 가지 온라인 메트릭에 대한 OTPSM 이상치 필터의 성능에 대해 논의하려고 합니다.
- Evaluation 은 제품 A, B, C에서 데스크톱 웹 및 모바일 앱 버전으로 총 6개에 대해서 평가가 이루어졌습니다.

> ## Robustness of Hurdle Model

- 기본 허들 모델(Hurdle)이 온라인 데이터에 얼마나 적합한지 평가하기 위해, 아래 표 2는 정규, 포아송 및 음이항 분포를 포함하여 일반적으로 사용되는 다른 세 가지 분포와 비교하여 허들 모델의 AIC를 정량화 해 보았습니다.

![jpg](/assets/images/Stat/157_4.jpg){: .align-center}

- 'Next Best' 열은 다른 세 개의 경쟁 분포(정규, 포아송 및 음이항) 중에서 가장 낮은(최고) AIC입니다. 
- 이전에 관찰된 것과 유사하게, 허들 모델은 측정 기준, 제품에 관계 없이 다른 모든 모델보다 일관되게 우수했던것을 볼 수 있습니다.
- 이러한 유연한 모델 구조는 향상된 AIC를 통해 스스로 온라인 데이터의 다양한 분포에 적응할 수 있게 합니다.
- 이 데이터를 통해서 허들 모델이 다재다능하고 강력하며 다양한 제품 설정에 대처할 수 있음을 입증했습니다!!

> ## 4.2 Stability of Outlier Thresholds

- 섹션 3.2에서 논의된 바와 같이, OTPSM 필터는 계산량을 줄이기 위해 제품 수준에서 구현됩니다. 
- 또한 더 나아가서 사용자에 대한 사용 패턴이 안정적인 제품의 경우 이상치 임계값이 크게 변하지 않기 때문에 자주 업데이트할 필요가 없습니다. 

![jpg](/assets/images/Stat/157_5.jpg){: .align-center}

- 그림 3에 표시된 것처럼 세션 및 페이지 뷰 메트릭을 모두 사용하여 몇 개월 동안 이상 임계값(Threshold) 의 안정성을 조사했습니다. 
- 제품 A 데스크톱의 경우 페이지 뷰 이상값(파란색 실선)은 2018년 1월 말부터 5월 초까지 ±5% 범위 내에서 변화했습니다. 
  - session outlier threshold (빨간색, 마스크된 척도)의 변동은 오히려 더 작았습니다.

> ##  Improvement of Experiment Measurement

- OTPSM 필터는 실험 측정 품질을 두 번 개선합니다.

![jpg](/assets/images/Stat/157_6.jpg){: .align-center}

> 첫째, 특이치로 인한 편향을 제거하고 실험 효과 측정의 정확도를 향상시킵니다. 

- 표 3은 특이치 필터링 전후의 실험 결과를 비교합니다.
- 특이치가 제대로 제거되지 않으면 크기와 방향 면에서 상당히 다른 결과가 도출될 수 있음을 알 수 있습니다.

> 반면에 OTPSM 특이치 필터는 메트릭 분산을 줄이고 실험의 통계적 검정력을 높입니다. 그 결과, 최소 샘플 크기의 요구사항을 줄입니다. 

- 특히 작은 모바일 앱의 경우 사용자를 많이 이용하기 힘들기때문에 이러한 이점은 상당한 이익이 됩니다.
- 표 4는 이상치 제거 전후의 필요한 표본 크기를 OTPSM과 비교한다.

![jpg](/assets/images/Stat/157_7.jpg){: .align-center}

- 위의 경우 아래와 같은 실험 세팅을 적용했습니다.
  - False Positive rate $\alpha= 0.05$ 
  - False Negative Rate $\beta = 0.02$
- 특이치로 인한 높은 분산으로 인해,  필요한 표본 크기는 거의 백만 개까지 커질 수 있습니다. 
- 예를 들어, 특이치 필터링 전에 제품 C 앱에서 클릭을 측정하는 데 필요한 표본 크기는 998,714입니다. 
  - 특이치가 제거된 후에는 필요한 표본 크기가 85% 감소한 151,485가 됩니다.

> ## 5. CONCLUSIONS AND FUTURE WORK

- 본 논문에서 우리는 온라인 실험을 위한 강력한 OTPSM 이상치 필터의 구현을 제시하였습니다. 
- OTPSM은 범용 허들 모델에 기반한 순차 테스트 절차를 채택했습니다.
  - 이는 광범위한 온라인 데이터 분석 스펙트럼에 적용될 수 있습니다.
- OTPSM 이상치 필터의 성능은 Oath 의 대규모 온라인 실험 플랫폼에서 평가되었습니다. 
- OTPSM에 의해 결정된 threshold는 시간이 지나도 어느정도 크게 변하지 않고 안정적입니다. 
  - 데스크톱 및 모바일 장치에 걸친 세 가지 지표와 여섯 가지 다른 온라인  실험에서의 결과는 OTPSM 필터가 온라인 실험 측정에서 이상값으로 인한 소음을 효과적으로 교정하고 감소시킬 수 있음을 보여줬습니다.
- OTPSM 이상치 필터는 확장 가능하고 강력하며 다양한 제품 설정에서 효과적으로 작동할 수 있습니다. 
- 우리는 4.2절에서 OTPSM에 의해 결정된 이상치 Threshold 가 몇 개월의 기간 동안 충분히 안정적이라는 것을 입증한다. 
  - 이를 통해 반복적인 임계값 계산을 건너뛰고 구현을 단순화할 수 있습니다. 
- 향후 연구에서는 실시간으로 Outlier Threshold 를 찾기 위해서 빠른 계싼 방법을 찾으려 합니다. 
- 또한 이 일변량 분포 기반 필터에서 다변량 분포 기반 필터로 확장하거나, 최소한 주요 메트릭에 대한 다변량 분포 기반으로 확장한다면 온라인 데이터 분석의 정확성을 더욱 향상시킬 수 있을것입니다.

---

**reference**

- https://alexdeng.github.io/public/files/jsm2011-deng.pdf

 
