---
title: "A Probabilistic, Mechanism-Indepedent Outlier Detection Method for Online Experimentation"
excerpt: "Outlier Detection 방법론 비교 (yahoo)"
categories:
  - AB_Paper
last_modified_at: 2022-03-12

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 Sequential 하게 테스트를 하지만, 이에 대해서 
{: .notice--warning}

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## Abstract 

- A/B Test Platform 인 Optimize가 적용하고 있는 새로운 통계적 방법론에 대한 논문입니다.
- 전통적인 p-값과 신뢰구간은 상황에 따라서 신뢰할 수 없는 값을 출력하게 됩니다.
  - ex : 실험이 진행되다가, p-value 가 우리의 Threshold 보다 낮으면 바로 실험을 중지한다.

- A/B 테스트는 실험이 계속되는 동안, metric 을 계속 모니터링 할 수 있습니다. 
  - 이러한 행위를 Continuous 

- 하지만 우리는 이러한 행동에 대해서도, 유효한 p-value 와 CI 를 뽑아내보려 합니다. 

> ## Instrocution

- 웹 응용 프로그램은 일반적으로 RCT(Randomized Controlled Trial)를 사용하여 제품 Oering을 최적화합니다. 이를 업계 용어로 A/B 테스트라고 합니다. 
- A/B 테스트의 급격한 상승으로 인해, 이러한 실험의 실행을 다루는 널리 사용되는 플랫폼이 많이 등장하였습니다 [10, 20]. ee 
- 전형적인 A/B 테스트는 두 가지 변형(제어 및 처리)에 걸쳐 매개변수의 값을 비교하여 하나의 변형이 서비스를 개선할 기회를 제공하는지 확인하는 한편, A/B 테스트 플랫폼은 표준 빈도수 매개변수 테스트 측정(p-값 및 일관성 간격)을 통해 사용자에게 결과를 전달합니다. 그렇게 함으로써, 그들은 , 매우 낮다는것을 볼 수 있습니다. 

> 

- 결정적으로, 이러한 p-값과 con-dence 간격의 추론적 타당성은 실험의 설계와 분석 사이의 분리를 엄격하게 유지해야 한다. 특히, 표본 크기는 사전에 파악해야 합니다. 실험의 표본 크기를 동적으로 다시 조정하기 위해 사용자가 보고된 p-값과 공칭 간격을 지속적으로 모니터링하는 A/B 테스트 관행과 비교한다[14]. 그림 1은 이러한 동작을 가능하게 하는 일반적인 A/B 테스트 대시보드를 보여줍니다.
