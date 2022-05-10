---
title:  "Why the P-value culture is bad and confidence intervals a better alternative"
excerpt: "왜 pvalue 보다 CI 로 Teting 하는게 더 좋은가?"
categories:
  - Stat_Testing
last_modified_at: 2021-11-06

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 우리가 Testing 을 할때에는 주로 p-value 를 이용해서 테스트를 하게 되는데요. 사실 이러한 기준은 좋지 않습니다. 여기에서는 p-value 보다 왜 신뢰구간이 선호되어야 하는지에 대해서 논의합니다.
{: .notice--warning}

# [Confidence Interval and P- value](#link){: .btn .btn--primary}{: .align-center}

- P-value 는 거의 업계에서의 표준처럼 자리잡고 있습니다.
- 하지만 이러한 p-value 문화를 비판하는 몇가지 과학적 주장을 살펴볼 수 있습니다.
  - 사실 이러한 비판은 1933년까지 거슬러가는 매우 유서깊은 비판입니다.
- 여기에서는 왜 p-value 가 비판되어야 하는지에 대해서 알아보겠습니다. 

> ## Statistical Precision

- 통계적 정밀도는 두가지로 대표될 수 있습니다.
  - Observation의 수
  - Observation의 Variability 
- 이때에 관측치의 Variability 가 적고, Observation 의 수가 많을수록 통계의 정밀도가 올라간다고 할 수있습니다.
  - 샘플의 수가 많으면 우리는 추정을 더 정확하게 할 수 있을것입니다.
  - 만일 Observation 의 분산이 클 떄에 (즉 이는 Population 의 Varation 이 크다고도 할 수 있겠죠.) 도  그 추정이 정확하지 못할 것입니다.
- 우리가 두개의 Mean 을 테스트 할때에 이러한 Variation 은 아래와 같이 측정됩니다.

$$SE = \sqrt{(SD_A^2/n_1 + SD_B^2/n_2)}$$

- 우리는 위와 같이 '평균의 차이' 라는 추정이 얼마나 정확(Statistical Precision) 한지를 SE 를 통하여 결정할 수 있습니다. 

> ## P-values and Confidence interval

- P - values 는 기본적으로 Null Hypothesis 를 가정할때에 내 데이터가 얼마나 이상한지를 검정하게 됩니다.
  - 내 데이터가 'Null' 을 가정했는데 'Alternative' 쪽으로 '5%' 만 나오는 이상한 데이터라면 귀무가설을 기각하고 대립가설을 선택하게 됩니다.
- 하지만 이러한 P-value 는 매우 많은 Weakness 가 존재합니다

> P 값 만으로는 차이의 방향을 알 수없음

- 양측검정을 실시한다고 했을때에, 그 결과가 p 값이 0.04 로 유의하다고 합시다.
- 하지만 이 경우 효과가 유의했다는 사실만 알 뿐, 대립가설이 더 높았는지 , 낮았는지에 대해서 알지 못하게 됩니다.
- 즉 P-value 만으로는 차이의 방향을 알 수 없어서, '실험의 가설' 또한 같이 제시되어야 합니다. 

> P 값은 차이의 '크기' 를 설명하기 않음

- A 와 B 의 크기를 비교를 다음과 같이 수행했다고 합시다.
  -  귀무가설 A=B , 대립가설은 A<B , p값 = 0.04 
- 위와 같이 수행하였을때에 우리는 B 가 더 좋다는 사실은 알고 있습니다만 도대체 '얼마나' 좋은것일까요? 
- 즉 우리는 이러한 결론 말고도 '실제 표본의 평균' 이 어떠했는지에 대해서도 보고를 해야 할 것입니다.

> p 값은 'Statistical Precision' 의 정보를 제공하지 않음

- A 와 B 의 크기를 비교를 다음과 같이 수행했다고 합시다.
  -  귀무가설 A=B , 대립가설은 A<B , p값 = 0.04  , $\bar{X_A} = 10 , \bar{X_B} = 10.5$
- 하지만 위와 같은 결론이 과연 '얼마나 믿음직' 할까요? 
  - A 표본의 평균은 10이고, B 표본의 평균은 10.5 라고 했는데 이것이 무조건 맞는값은 아니겠죠?
  - 그러므로 우리는 '다른건 알겠는데, 그 불확실성은 어떨까?' 와 같은것을 원할 것입니다.
  - 하지만 위의 p-value 는 '평균이 다른것은 유의하다' 라는것만 제시할 뿐, '평균 추정은 얼마나 유의한지' 에 대해서는 말해주지 않습니다!

> Confidence Interval 과 Practical Significant 를 연관지어 생각할 수 있음

![png](/assets/images/Stat/92_1.png)

- 위와 같이 Confidence Interval을 이용하는 경우 Practical Significant 를 이용하여 직접적인 평가도 가능합니다.
  - '적어도 어느정도 이상의 effect 를 원한다!' 와 같은 상황의 경우 위 그림처럼 평가될 수 있다는 것입니다. 
- 위 그림을 보면 비록 'Statistically Significant' 일 지여도 Practical significant (여기에서는 Clinically significant 라고 쓰임) 이지 않은 경우를 CI 를 통해서 쉽게 알 수 있기 때문입니다.

> ## Conclusion

- P - value 는 결과의 통계적 Plausibility 를 제공합니다. 
  - P - value 는 Binary results ( Yes or NO ) 를 제공할 수 있습니다.
- 하지만 CI 는 P - value 보다 훨씬 많은 정보량을 제공합니다.
  - 추정치의 정확성 , 차이의 방향, 차이의 크기 등을 제공할 수 있습니다.
- 하지만 여기서 p-value 와 CI 의 최종적 의사결정은 '같다' 라는것을 명심합시다! 그저 결과를 얼마나 더 자세하게 설명할 수 있고, 확장성이 있느냐의 차이입니다.

---

**Reference**

- <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2689604/>
- <https://www.sciencedirect.com/science/article/pii/S1063458412007789#bib2>

 Confidence Interval 과 P value 간의 차이를 잘 알아두도록 합시다! 
{: .notice--success}

