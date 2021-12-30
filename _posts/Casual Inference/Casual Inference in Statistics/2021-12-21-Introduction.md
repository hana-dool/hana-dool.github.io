---
title:  "Introduction"
excerpt: "인과성을 연구하는 이유"
categories:
  - Casual_Inference_in_Statistics
last_modified_at: 2021-12-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 인과성을 왜 연구할까
{: .notice--warning}

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## 인과성을 왜 연구하는가?

- 인과성을 연구하는 이유에 대한 답은 통계학을 왜 공부하는가? 와 이유가 비슷합니다.
- 데이터를 이해하고, 정책에 대해 결정을 내리고 성공과 실패를 통해 배우기 위하여 인과성을 연구하게 됩니다.
  - 즉 흡연이 폐암에 미치는 영향, 교육과 급여의 영향 등을 배우기 위함이죠

> ## 심슨의 역설 1 : 신약의 효과

- 심슨의 역설은 , 이러한 역설을 처음 대중화한 통계학자 심슨(1922) 의 이름을 따서 명명한 것입니다.
- 이 역설은 전체 인구에서는 유지되는 통게적 연관성이 하위 집단에서는 유지되지 않는 현상을 말하게 됩니다.

$$\begin{array}{lll}
\hline & \text { 신약 복용 } & \text { 신약 복용 안 함 } \\
\hline \text { 남성 환자 } & 87 \text { 명 중 } 81 \text { 명 회복 }(93 \%) & 270 \text { 명 중 234명 회복 (87\%) } \\
\text { 여성 환자 } & 263 \text { 명 중 192명 회복 }(73 \%) & 80 \text { 명 중 55명 회복 (69\%) } \\
\text { 전체 환자 } & 350 \text { 명 중 273명 회복 (78\%) } & 350 \text { 명 중 289명 회복 (83\%) } \\
\hline
\end{array}$$

- 위를 볼때 '각각의 부분' 에 대해서는 신약이 좋으나, '전체' 에 대해서는 신약이 안좋아보이는듯 합니다.
  - 위 결과를 볼때 , 신약이 효과가 있다고 말할 수 있을까요?

- 이 문제에 대한 답은 어떠한 통계적 방법으로도 찾을 수 없습니다. 신약의 효과를 추정하기 위해서라면, 데이터에서 직접적으로 드러나지 않는 인과적 매커니즘을 이해해야 됩니다.
- 예시로 에스트로겐은 회복에 부정적인 영향을 미치므로 약의 종류에 관계없이 여성이 남성보다 회복 가능성이 낮다고 합시다. 
  - 실제로 데이터를 통해서 여성이 남성보다 약물 복용률이 횔씬 높은 것을 확인할 수 있습니다. 
  - 즉 이 약이 해로운것처럼 보이는 이유는 약을 복용한 사람들 중에서 랜덤하게 고르게 되면, 그 사람이 여성일 확률이 높았으며, 약을 복용하지 않은 임의의 사람보다 회복될 가능성이 낮았습니다.
- 그렇다면, 여성이라는 점이 약물 복용과 회복률 저하의 공통된 원인이라는 것을 분명히 해야 합니다.
  -  따라서 신약의 효과를 평가하기 위해서는 동일한 성별의 피험자를 비교해야 한다. 

- 즉 '약의 효과' 가 아니라. '에스트로겐' 의 차이에 의하여 약의 효과를 왜곡하고 있지 않은지 고민해야 합니다. 
  - 이는 결국, 전체 데이터가 아니라 성별로 나누어진 데이터를 고려해서 에스트로겐의 차이를 동일하게 한 상태에서 비교해야 된다는것을 의미합니다.


> ## 심슨의 역설 2 : 운동량과 콜레스테롤

![jpg](/assets/images/Stat/129_1.jpg)

- 여러 연령대의 주간 운동 (weekly exercise)과 콜레스테롤을 측정하는 연구를 생각해봅시다.
-  위 그림은 $\mathrm{X}$ 축은 운동량, $\mathrm{Y}$ 축은 콜레스테롤의 양을 나타냅니다.
- 이떄 연령 별로 그릅을 만들어 보면, 각 연령별로 일반적인 추세가 있음을 알 수 있다.
  -  젊은 사람들이 운동을 할수록 콜레스테롤 수치가 낮아지는데, 이것은 중년층과 노년층에서 도 마찬가지이다. 

> 연령별로 구분하지 않는 

![jpg](/assets/images/Stat/129_2.jpg)

- 그러나 동일한 산점도 (scatter plot)를 이용하면서 데이터를 연령별로 구분하지 않으면, 그림 $1.2$ 에서는 운동을 할수록 콜레스테롤 수치가 높아지는 양상을 보인다. 
  - 이 문제를 해결하기 위해서 다시 한 번 데이터와 관련된 이야기를 살펴보도록합시다. 
- 그림 $1.1$ 에서 나이가 많으면 운동량에 상관없이 전반적으로 콜레스테롤 수치 가 높은 경향을 보인다. 
  - 이러한 사실을 알고 있다면 하위 그룹 데이터와 전체 데이터가 보여주는 다른 결과에 대해서 쉽게 이해할 수 있습니다.
- 나이는 Treatment(운동)과 결과(콜레스테롤 수치)의 공통 원인 (common cause)이 됩니다.
- 따라서 같은 연령대의 사람 들을 비교하기 위해 연령별로 데이터를 조사해야 한다. 
- 운동을 많이 하지만 콜레스태 롤이 높은 이유는 운동으로 인한 것이 아니라 나이 때문일 가능성이 높기 때문이다.

> ## 심슨의 역설 3 : 혈압과 신약회복

- 그러나 그룹별로 나누어진 데이터가 항상 정확한 답을 제공하지는 않을 수도 있다. 

$$\begin{array}{lll}
\hline & \text { 신약 복용 안함 } & \text { 신약 복용 } \\
\hline \text { 혈압이 낮아진 환자 } & 87 \text { 명 중 } 81 \text { 명 회복 }(93 \%) & 270 \text { 명 중 } 234 \text { 뗭 회복 }(87 \%) \\
\text { 고혈압이 유지된 환자 } & 263 \text { 명 중 } 192 \text { 명 회복 }(73 \%) & 80 \text { 명 중 } 55 \text { 명 회복 }(69 \%) \\
\text { 전체 환자 } & 350 \text { 명 중 } 273 \text { 명 회복 }(78 \%) & 350 \text { 명 중 } 289 \text { 명 회복 }(83 \%) \\
\hline
\end{array}$$

- 첫 번째 신약 복용 및 회복 사례와 같은 숫자를 가진 표를 살펴보도록 합시다. 
- 이번에는 환자의 성별을 기록하는 대신에, 실험이 끝날 때의 환자의 혈압을 기록했습니다.
- 이경우에는 약을 복용하면, 환자들의 혈압을 낮춤으로서 회복에 영향을 미친다는 사실이 있다고 합시다. 하지만, 이것은 안타깝게도 독성 효과로 인한 혈압 강하 효과로 인한 것이다. 
- 실험이 끝나면 표 $1.2$ 와 같은 결과를 얻는다. (표 $1.2$ 는 표 $1.1$ 과 표 안의 수치는 같지만 수치가 의미하는 바는 다르다.)
- 이제 환자들에게 이 약을 추천하겠는가?

> interpret

- 이 문제에 대한 답을 하려면 데이터가 생성된 방식을 따라가야 합니다. 
- 이 약이 혈압에 영향을 주기 때문에 전체 환자의 회복 가능성을 높일 수 있습니다.
  - 그러나 하위 집단, 즉 약 복용 후에도 혈압이 높은 집단과 약 복용 후 혈압이 낮아진 집단에는 신약이 효과가 있다고 볼 수 없습니다. 단지 약물의 독성 효과가 나타남을 알 수 있습니다 (오히려 회복력이 낮아짐).
- 성별로 나누어서 고려한 데이터 예제에서와 같이, 이 실험의 목적은 회복 가능성에 대한 신약의 전반적인 효과를 측정하는 것이었습니다. 
- 그러나 이 예에서는 혈압을 낮추는 것이 신약이 회복에 영향을 미치는 매커니즘 중 하나이기 때문에 혈압을 기준으로 결과를 분리하는 것은 의미가 없습니다. (물론 치료 전에 환자의 혈압을 기록하고, 혈압이 치료에 효과가 있다면 이것은 의미가 있는 다른 이야기일 것이다.) 
- 따라서 전체 환자에 대한 결과를 참고하면, 이 약의 처방이 회복 가능성을 높이며 이 약의 복용을 권장해야한다고 결정해야 한다. 놀랍게도 숫자는 성별과 혈압의 예와 동일하지만, 전자의 예 에서는 전체 데이터가 아닌 분리된 데이터를 이용할 때에 올바른 결론을 내릴 수 있고, 후자의 예에서는 전체 데이터를 이용할 때에 올바른 결론을 내릴 수 있다.
- 혈압을 측정하는 시간, 치료가 혈압에 영향을 미치고 혈압이 회복에 영향을 준다는 사실과 같은 정보를 데이터로부터는 그 어떤 것도 얻을 수가 없습니다. 사실, 통계학 교과 서는 전통적으로 (그리고 정확하게) 상관성은 인과성이 아님을 (correlation is not causation) 가르치므로, 데이터만으로 인과 이야기 (causal story)를 결정할 수 있는 통계적 방법은 없다. 결과적으로, 우리의 결정에 도움이 되는 통계적 방법은 없다.

> Note

- 그러나 통계학자들은 항상 이러한 종류의 인과 가정 (causal assumptions)에 근거하여 데이터를 해석한다. 
- 사실, 이 책의 첫 부분에 다루었던 심슨의 문제의 한 사례인 정성적인 (qualitative) 성별의 예에서 드러나는 매우 역설적인 성격은 치료가 성별에 영향을 미치지 않을 것이라는 우리의 강한 확신으로부터 비롯된 것이다. 데이터에 숨어 있는 인과 이야기를 통해 혈압의 예와 같은 구조를 쉽게 가정할 수 있기 때문에 역설을 피할 수도 있다.
- "치료로 인한 효과가 성별에 따라 다르다"는 가정이 사소해 보일 수도 있지만, 데이터를 통해서 이것을 확인할 방법이 없으며, 일반적인 통계학에 서 이용하는 수학적 방법으로는 이것을 표현할 방법이 없다.
- 실제로, 통계적 추론이 종종 기초를 두는 분할표 (contingency table, 표 $1.1$ 과 표 $1.2$ )에서 인과 정보 (causal information)를 표현할 수 있는 방법은 없다.
- 그러나 인과 가정을 표현하고 해석하는 데 이용할 수 있는 또 다른 통계 방법이 있 다. 이 책은 이러한 인과 관계에 대한 방법과 해석에 초점을 두고 있다. 이 방법을 통하여 독자는 복잡성의 인과 시나리오 (causal scenarios)를 수학적으로 설명하고, 대수학 문제에서 $X$ 에 대해 풀 수 있는 것처럼 심슨의 역설이 제기한 것과 유사한 의사 결정 문제에 대해 신속하고 편안하게 대답할 수 있다. 
- 또한 이 방법을 통해 위의 세 가지 예를 십게 구별하고, 적절한 통계 분석 및 해석을 할 수 있다. 간단한 논리적 작 업으로 인과성을 계산할 수 있고, 이미 우리가 직관적으로 생각하고 있는 것들, 남성 과 여성을 치료하는 데 도움이 되지만, 전체 인구에게 해를 끼치는 약물은 존재하지 않는다는 것, 혈압이 같은 사람을 비교할 필요가 없다는 것에 대해 명확한 답을 줄 수 있다. 
- 이러한 방법을 통해 심슨의 역설을 뛰어넘어 더 이상 직감으로 분석을 할 수 없는 복잡한 문제에 대해서도 접근할 수 있을 것이다. 간단한 수학적 도구를 이용 하면 정책 평가의 실질적인 문제는 물론 사건이 어떻게 그리고 왜 발생하는지에 대한 과학적인 문제에 대한 답을 얻을 수 있다.
- 그러나 우리는 아직까지 그렇게 할 수 있는 준비가 되어 있지 않다. 데이터에 숨어 있는 인과 관계에 대해서 철저히 접근하기 위해서 다음과 같은 네 가지를 필요로 한다.
  1) 인과성 (causation)에 대한 실제적인 정의
  2) 인과 가정 (causal assumptions)을 공식으로 표현하는 방법, 즉 인과 모형 (causal models)을 만드는 방법
  3) 인과 모형의 구조를 데이터의 특징과 연결시키는 방법
  4) 모형과 데이터에 포함된 인과 가정의 결합으로부터 결론을 이끌어내는 방법
- 이 책의 1 장과 2 장은 인과 가정을 모형화하고, 이를 데이터에 연결하는 방법을 제공하는 데 초점을 맞추고 있으므로, 3 장에서는 인과 문제에 대한 답을 찾기 위해 이 러한 가정 및 데이터를 이용할 수 있다. 그러나 계속 진행하기 전에 우리는 인과성 (causation)을 정의해야 한다. 직관적이거나 단순해 보일지 모르지만 일반적으로 합의된 인과성의 정의는 수 세기 동안 통계학자와 철학자를 비켜 갔다. 우리의 목적에 부합하는 인과성의 정의는 간단하면서, 약간 은유적인 면이 있다. 어떤 식으로든 변수 $Y$ 가 변수 $X$ 에 의존하면 변수 $X$ 는 변수 $Y$ 의 원인 (cause)이다. 나중에 인과성에 대한 정의를 약 간 확장할 것이지만, 지금은 인과성을 듣기의 한 형태 (a form of listening)로 생각하기 바란다. $Y$ 가 $X$ 를 든고, 듣는 것에 따라 값을 결정하면 $X$ 는 $Y$ 의 원인이 된다. $(X$ is a cause of $Y$ if $Y$ listens to $X$ and decides its value in response to what it hears.)

---

**Reference**

- 책