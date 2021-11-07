---
title:  "Holm-Bonferroni Correction method"
excerpt: "다중 비교에서 Bonferroni 방법보다 조금 발전된 방법"
categories:
  - Stat_Testing
last_modified_at: 2021-11-07

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 다중 비교는 False Positive Inflation 이라는 문제점을 가지고 있습니다. 이러한 문제점을 해결하기 위해서 어떤방법을 활용할 수 있을까요? 
{: .notice--warning}

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## Holm Bonferroni Method

- Family wise Error rate 를 제어하기 위한 방법론입니다.
  - 이러한 방법론은 Bonheronni 보정보다 더 Power 가 있고 균일한 테스트를 제공한다고 합니다. 

> ## How to? 

1. m 개의 p value 가 있다고 합시다. 우선 lowest 부터 highest 값까지 P-value 를 정렬합니다. 
   - 정렬했을떄에 P - value 를 $P_1 , P_2 .. P_M $ 라 하고 각 p -value 에 해당하는 가설을 $H_1 ... H_M$ 이라고 합시다. 
   - 우리는 FWER 가 $\alpha$ 보다 낮기를 원합니다.

2. $P_1 < \alpha /m$  이면 $H_1$ 을 reject 합니다. 그리고 다음 step 으로 넘어갑니다. 
   - 만일 이떄 기각하지 못하면 이 단계에서 끝냅니다. 
3. $P_2 < \alpha / (m-1)$ 이면 $H_2$ 를 reject 합니다. 그리고 다음 step 으로 넘어갑니다.
   - 만일 이때에 기각하지 못하면 이 단계에서 끝냅니다. 
4. 위 과정을 계속합니다. 즉 $P_k < \alpha /  (m+1-k)$ 인지를 계속 검정하는데, reject 가 안되면 이 단계에서 끝냅니다. 

> ## Raionale

- Simple Bonferroni correlation 은 $P_k < \alpha /m$ 이 항상 기준점이 되었습니다.
- 하지만 Holm Bonferroni Method 는 family error 를 $\alpha$ 로 동일하게 제한함과 동시에 , reject 의 기준이 Simple Bonferroni 방법보다 좀 더 헐겁습니다.
  - 즉 Power 가 좀 더 높다는 것이죠 

> ## Proof

- $H_{(1)} , H_{(2)} ... H_{(m)} $ 을 실험들이라고 하고 $P_{(1)} \le ... P_{(m)}$ 은 정렬된 P-value 입니다.  그리고 $I_0$ 은 null hypothesis 가 True 인 실험들의 index 집합입니다. (물론 Unknown 입니다.) 그 크기는 $m_0$ 입니다.
- 우리가 Null Hypothesis 가 True 인데 이를 기각했을때, 이러한 확률이 most $\alpha$ 임만 보이면 됩니다.
- h 를 우리가 처음으로 Null Hypothsis 가 True 인데 기각한 실험의 index라 합시다. 그러면 $H_{(1)} ... H_{(h-1)}$ 은 모두 reject False Null hypothesis 인 상태일 것입니다.
  - 그리고 $h-1 \le m-m_0$ 임을 기억합시다.  
- 이로부터 우리는 $\frac{1}{m-h+1} \le \frac{1}{m_0}$ 이 성립합니다. 우리는 현재 h 를 reject 했고 , 즉 $P_{(h)} \le \frac{\alpha}{m-h+1}$ 이 될 것입니다. 
- 이떄 right side 는 기껏해야 $\alpha /m_0$ 이 됩니다.  그러므로 다음과 같이 Rancom Variable A 를 가정합시다.

$$A = \{P_i \le \frac{\alpha}{m_0}\ for \ i \in I_0 \}$$ 

- 위 식은 Bonferroni inequality ($P(\cup X_i)) \le \sum P(X_i)$) 를 이용하면 

$$P(A) \le \alpha$$ 

- 위와 같은 등식이 성립합니다.

> ## Example

- 다음과 같이 Example 을 들고 끝내도록 하겠습니다.

![png](/assets/images/Stat/94_1.png)

- 위처럼 Bonferroni 는 일정한 Threshold 가 있는 반면, Holm Bonferroni 는 점점 그 Threshold 를 높혀갑니다.

> ## Comparison

![png](/assets/images/Stat/94_2.png)

- 위는 Benjamini Hochberg 방법론도 같이 비교한 것입니다. 
  - 확실히 좀 더 관대한 기준을 가지고 있음을 알 수 있습니다. ($\alpha = 0.05$)

---

**Reference**

- <http://www.compbio.dundee.ac.uk/user/mgierlinski/talks/pvalues2/p-values8.pdf>
- <https://en.wikipedia.org/wiki/Holm%E2%80%93Bonferroni_method>



