---
title:  "Individual CI Testing"
excerpt: "각 Confidence Interval 를 비교해서 검정할 수 있을까?"
categories:
  - Stat_Testing
last_modified_at: 2021-11-08

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 우리가 Mean Comparison 을 실시할때에 늘 A-B 의 신뢰구간이 0 을 포함하는지 아닌지를 검정하게 됩니다. 하지만 이때 그냥 각각의 A, B 의 Meam 에 대한 Confidence interval 을 생성한 뒤, 이 각각을 비교한다면 더 편할텐데 왜 이렇게 하지 않을까요? 이 방법이 왜 잘 작동하지 않는지에 대해서 알아봅시다. 
{: .notice--warning}

# [Individual CI Test](#link){: .btn .btn--primary}{: .align-center}

> ## Idea

- 우리는 세개의 집단에 대해서 평균을 비교하고자 할 떄, 다음과 같이 Inference 를 진행합니다.
  - A-B 에 대한 mean difference inference
  - A-C 에 대한 mean difference inference 
  - B-C 에 대한 mean difference inference 
- 위와 같은 상황은 집단이 여러개로 더욱더 많아질수록 Inference 를 하기가 어려워 집니다. 집단이 4개인경우에는 어떻게 Inference 를 진행할까요? 
  - A-B , A-C , A-D , B-C , B-D , C-D 로 총 6번의 inference 를 해야합니다. 
- 그런데 만약 굳이 두 집단을 짝지어서 비교하지 않고 '각 집단의 Mean 의 CI' 만 비교하여서 결론을 내릴 수 있으면 얼마나 좋을까요?

![png](/assets/images/Stat/98_1.png) 

- 즉 위 그림과 같이 여러 집단이여도 그냥 각 평균의 CI 가 겹치지 않으면 평균은 차이가 난다! 라고 결론을 내릴 수 있다면 얼마나 좋을까요? 

> ## Problem

- 아래와 같이 두 집단에 대해서 비교를 하고 있는 상황이라고 헙시다.

> 각 집단의 CI 를 개별로 비교

![png](/assets/images/Stat/98_2.png)

- 위는 One sample t test 를 각각 수행한 결과입니다. 
- 위와 같은 상황에서 이전에 Idea 에서 처럼 검정을 하게 되면 '두 샘플의 평균은 차이가 없다!' 라고 결론을 내리게 될 것입니다.

> 두 집단의 '차이' 를 CI 로 비교 

![png](/assets/images/Stat/98_3.png)

- 위는 Two Sample t - test 를 실시한 결과입니다.
- 위처럼 이전과 같은 상황인데도 우리는 '두 집단은 차이가 있다!' 라고 결론을 내리게 됩니다.

> ## See Detail

- 왜 이런일이 일어났을까요? 다음을 통해서 알아봅시다. 
- independent sample 에 대해서 mean 을 비교하는 예시에 대해서 알아봅시다.
- $Population_1 , Population_2$ 에 대하여 , 각각의 sample mean 을 $\bar{x_1} , \bar{x_2}$ 라 합시다. 그러면 이에 대한 Standard Error 는 각각 $SE_1 , SE_2$ 라고 합시다. 
  - 그러면 mean 차이($ \mu_1 - \mu_2$) 에 대한 Standard error 는 $\sqrt{SE^2_1 + SE^2_2}$ 가 됩니다.

> Overlapping Standard Error

- 이떄 우리는 $\mu_1$ 과 $\mu_2$ 에 대해서 Confidence Interval 에 대해서 다음과 같이 나올 것입니다.
  - $\mu_1$ 에 대한 CI 는 $\bar{x_1} \pm t \cdot SE_1$ 
  - $\mu_2$ 에 대한 CI 는 $\bar{x_2}\pm t \cdot SE_2 $
- 이떄 위의 t 는 적절한 t-value 가 됩니다. $t_{0.95}$ 가 될 수 있을것. 
- Confidence interval 이 겹치지 않는 경우는 다음과 같습니다. 
  - $\bar{x_1} - t \cdot SE_1 > \bar{x_2} + t \cdot SE_2$ $\to$ $(\bar{x_1} -\bar{x_2}) - t \cdot (SE_1+SE_2) > 0$
  - $\bar{x_2} - t \cdot SE_2 > \bar{x_1} + t \cdot SE_1$ $\to$ $(\bar{x_1} -\bar{x_2}) - t \cdot (SE_1+SE_2) < 0$

> DIfference Standard Error

- difference $(\mu_1 - \mu_2)$ 에 대해서, Null hypothis 를 기각하는 경우는 다음과 같습니다.
  - $(\bar{x_1} - \bar{x_2}) + t \cdot \sqrt{SE^2_1 + SE^2_2} < 0$ 
  - $(\bar{x_1} - \bar{x_2}) - t \cdot \sqrt{SE^2_1 + SE^2_2} > 0$

> Comparison

- 이제 두가지에 대해서 비교를 해 보겠습니다.
  - 각각의 CI 를 이용하여 비교한 경우 $\mid x_1 - x_2 \mid > t \cdot \sqrt{SE_1^2 +SE_2^2}$
  - 하나의 CI 를 이용하여 비교한 경우  $\mid x_1 - x_2 \mid > t \cdot (SE_1 +SE_2)$
- 이때에 $\sqrt{SE_1^2 + SE_2^2} \le SE_1 + SE_2$ 가 항상 True 라는것에 집중합시다. 
  - 이는 각각의 CI 를 이용하서 비교한 경우, 하나의 CO 를 이용하여 비교한 경우와 Decision Rule 이 다르다는 것입니다. 
- 즉 하나의 CI 를 이용하여 비교한 경우 평균의 차이가 유의미하였음 $\to$ 각각의 CI 를 이용하여 비교하였을떄에 평균 차이가 유의미하였음 은 성립하지만
- 각각의 CI 를 이용하여 비교하였을때에 평균 차이가 유의미하다고 함 $\not \to$ 하나의 CI 를 이용하여 비교한 경우 평균의 차이가 유의미 처럼 성립하지 않다는 것입니다.

![png](/assets/images/Stat/98_4.png)

- 위처럼 CI overlap 방법은 , '차이가 있다' 라고 말하기 위해서는 좀 더 빡센 기준이라는 것입니다.

> ##  Other Works

- 하지만 여전히 k 개의 평균 비교시에 k(k-1) / 2 개나 되는 비교를 수행해야 되는데 이는 여전히 짜증나는 일입니다..
  - 그러므로 각 집단에 대한 평균의 COnfidence level 을 낮추더라도 (왜냐하면 각 mean 을 비교하는건 빡센 조건이니까) k 개의 mean 의 CI 를 비교하는식으로 하면 되지 않을까? 라는 Insight 가 있습니다.
- http://koreascience.or.kr/article/JAKO201732863553409.page
  - 위에서와 같이, 우리는 각각의 Group 에 대해서 위에서의 Confidence Interval 을 조절할 수 있습니다.
- 우선 $100(1-\alpha)\%$ 의 Confidence interval 은 다음과 같습니다.

$$\begin{aligned}
&\bar{X}_{1} \pm t_{\frac{\alpha}{2}, n_{1}-1} \frac{S_{1}}{\sqrt{n_{1}}} \\
&\bar{X}_{2} \pm t_{\frac{\alpha}{2}, n_{2}-1} \frac{S_{2}}{\sqrt{n_{2}}} \\
&\bar{X}_{1}-\bar{X}_{2} \pm t_{\frac{\alpha}{2}, \mathrm{df}} \sqrt{\frac{S_{1}^{2}}{n_{1}}+\frac{S_{2}^{2}}{n_{2}}}
\end{aligned}$$

- 하지만 Mean 의 Overlap 이 발생할때에 이전처럼 $\alpha$ 가 잘 나오지 않는다는것을 알 수 있습니다.
  - 즉 아래와 같이 각각의 Interval 을 고쳐볼 수 있습니다.

$$\begin{aligned}
&\bar{X}_{1} \pm r_{1} \times t_{\frac{\alpha}{2}, \mathrm{df}} \sqrt{\frac{S_{1}^{2}}{n_{1}}+\frac{S_{2}^{2}}{n_{2}}} \\
&\bar{X}_{2} \pm r_{2} \times t_{\frac{\alpha}{2}, \mathrm{df}} \sqrt{\frac{S_{1}^{2}}{n_{1}}+\frac{S_{2}^{2}}{n_{2}}}
\end{aligned}$$

- 이때 $r_1 + r_2 = 1$ 입니다. 
- 위와 같이 설정하게 될 경우, $m =  t_{\frac{\alpha}{2}, \mathrm{df}} \sqrt{\frac{S_{1}^{2}}{n_{1}}+\frac{S_{2}^{2}}{n_{2}}}$ 라고 할 떄에 아래와 같은 식이 성립합니다. 

$$\begin{aligned}
P\left(\bar{X}_{1}+r_{1} m<\bar{X}_{2}-r_{2} m, \bar{X}_{2}+r_{2} m<\bar{X}_{1}-r_{1} m\right) &=P\left(\left|\bar{X}_{1}-\bar{X}_{2}\right|>\left(r_{1}+r_{2}\right) m\right) \\
&=P\left(\left|\bar{X}_{1}-\bar{X}_{2}\right|>m\right) \\
&=\alpha
\end{aligned}$$

- 즉 $\alpha$ 가 제대로 유지되는것을 볼 수 있습니다.
  -  이때 각각, $\bar{X_1} , \bar{X_2} $ 의 신뢰구간은 각각의 표준오차 $$S_{i} / \sqrt{n_{i}}(i=1,2)$$ 에 비례합니다. 즉

$$\begin{aligned}
&r_{1}=\frac{S_{1} / \sqrt{n_{1}}}{S_{1} / \sqrt{n_{1}}+S_{2} / \sqrt{n_{2}}} \\
&r_{2}=1-r_{1}=\frac{S_{2} / \sqrt{n_{2}}}{S_{1} / \sqrt{n_{1}}+S_{2} / \sqrt{n_{2}}}
\end{aligned}$$

- 위처럼 값을 정의하게 된다면, 우리는 합리적인 Mean Comparison 을 위한 CI 를 얻을 수 있을것입니다.

> Application 

![png](/assets/images/Stat/98_5.png)

- 위의 왼쪽 그래프와 같이 기존의 Confidence interval 은 p-value 가 0.028 임에도 불구하고 겹치고 있습니다.
- 하지만 위의 오른쪽 그래프와 같이 새로 Adjusted 된 Confidence interval 은 p-value 가 0.028 일때 두 구간이 겹치지 않고 있습니다. 

> Limitation

- 하지만 위와 같은 비교는 결국 '두개의 비교(A/B)' 에 한정될 수 밖에 없습니다.
- 그러므로 다양한 비교를 위해서라면 분산이 모두 같은 정규 모집단에서, 그나마 활용이 가능합니다. 

![png](/assets/images/Stat/98_6.png)

- 자세한 내용은 논문 참조

---

   **Reference**

- <https://statisticsbyjim.com/hypothesis-testing/confidence-intervals-compare-means/>
- <https://cscu.cornell.edu/wp-content/uploads/73_ci.pdf>
- Visual inspection of overlapping confidence intervals for comparison of normal population means (paper)

 위와 같은 방법론은 비교하기가 편리해서 많은사람이 잘못 판단하는 부분이라 주의가 필요합니다. Schenker와 Gentleman (2001)은 의학 분 야 학술지에서 이러한 오류를 범한 논문을 60개 넘게 발견했다고 보고했다고 합니다..
{: .notice--success}

