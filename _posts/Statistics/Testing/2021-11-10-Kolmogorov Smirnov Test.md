---
title:  "Kolmogorov-Smirnov test"
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

 Kolmogorov-Smirnov test 는 두 분포가 같은지 테스트 하는 방법입니다. 이를 어떻게 알 수 있는지 한번 알아보도록 합시다.
{: .notice--warning}

# [Kolmogorov-Smirnov test](#link){: .btn .btn--primary}{: .align-center}

> ## Kolmogorov-Smirnov test

- 우리는 $\mathbb{P}$ 로부터 추출한 iid 한 샘플 $X_1 ... X_n $ 을 가지고 있다고 합시다. 
- 그리고 우리는 이 분포가 특정한 분포인 $\mathbb{P_0}$ 에서 나왔는지를 알고 싶습니다. 
  - 즉 다음과 같은 분포를 테스팅 하고 싶다고 합시다.

$$H_{0}: \mathbb{P}=\mathbb{P}_{0}, \quad H_{1}: \mathbb{P} \neq \mathbb{P}_{0}$$

- 위를 테스트 하는 방법중에는 Chi - squared 방법론이 있습니다. 
  - 하지만 Chi Squared 방법론은 Discretized 하기 때문에 다소 Continuous 데이터의 정보량을 뭉게버리는 단점이 있습니다.
  -  여기에서는 뭉게버리지 않고 CDF 를 비교하는 방법론으로 이 가설을 한번 검증해 보겠습니다.

> ## kolmogorov smirnov statistic

- $F_n$ 은 empirical CDF 로서 다음과 같이 정의됩니다.

$$F_{n}(x)=\mathbb{P}_{n}(X \leq x)=\frac{1}{n} \sum_{i=1}^{n} I\left(X_{i} \leq x\right)$$

- 이때 위와 같은 값은 , n 이 커질수록 F 와 같아질 것입니다. 즉 

$$F_{n}(x)=\frac{1}{n} \sum_{i=1}^{n} I\left(X_{i} \leq x\right) \rightarrow \mathbb{E} I\left(X_{1} \leq x\right)=\mathbb{P}\left(X_{1} \leq x\right)=F(x)$$

- 위와 같은 식이 성립합니다. 

> Statistics

$$D_n = sup_x |F_n(x) - F(x) | $$

- Kolmogorov Statistic 은 위와 같은 값을 사용하는데요, 이때 위에서 $F$ 는 Cumulative Distribution 입니다. 
- 직관적으로, Null hypothesis 가 맞다면, 샘플 수가 많아질수록 위 값은 0 으로 갈 것이라는것을 예상할 수 있습니다.

![png](/assets/images/Stat/99_1.png)

- 위 그림과 같이, 우리가 비교하고자 하는 CDF 와, 데이터의 Empirical cdf 를 같이 두고, 최대 거리를 통계량으로 사용한다고 이해하시면 됩니다. 

> Distribution 

$$\sqrt{n} D_{n} \stackrel{n \rightarrow \infty}{\longrightarrow} \sup _{t}|B(F(t))|$$

- 일반적으로 Null Hypothesis 하에서 n 이 커질수록 위와 같은 수식이 성립한다고 알려져 있습니다. 
  - 위처럼 극한분포의 수렴성을 이용해서 테스트를 진행하게 됩니다. 
- 자세하게 얘기하자면 다음과 같습니다.

![png](/assets/images/Stat/99_2.png)

- 자세한것은 다음의 링크를 참조하면 될 것 같습니다.
  - <https://en.wikipedia.org/wiki/Kolmogorov%E2%80%93Smirnov_test>
  - <http://www.maths.qmul.ac.uk/~bb/CTS_Chapter3_Students.pdf>

> ## 2.Kolmogorov–Smirnov two - test

- , "서로 다른 2개의 Distribution" 에 대해서도 검정이 가능합니다. 
  -  그때의 가설은 다음과 같습니다. 

$$H_{0}: F=G \quad \text { vs. } \quad H_{1}: F \neq G$$

- 이떄 $X_1., X_2 ... X_m$ 을 cdf $F(x)$ 에서 나온 값이라고 가정합시다. 
- 그리고 $Y_1 .... Y_m$ 을 cdf $G(x)$ 에서 나온 값이라고 가정합시다. 
- $F_m(X)$ 와 $G_n(x)$ 를 각각에 대응하는 empirical cdf 라 하면 다음의 statistic 은 

$$D_{m n}=\left(\frac{m n}{m+n}\right)^{1 / 2} \sup _{x}\left|F_{m}(x)-G_{n}(x)\right|$$

![png](/assets/images/Stat/17_4.png)

- 위와 같이 통계량은 두개의 ECDF 간의 최대 거리를 통계량으로 하고 있습니다.

> Distribution under Null Hypothesis

![png](/assets/images/Stat/99_3.png)

- 위와 같이 극한분포가 따르는 분포를 이용하여 검정하게 됩니다.

> ## Properties

> In practice, the statistic requires a relatively large number of data points (in comparison to other goodness of fit criteria such as the [Anderson–Darling test](https://en.wikipedia.org/wiki/Anderson–Darling_test) statistic) to properly reject the null hypothesis.
>
> https://en.wikipedia.org/wiki/Kolmogorov%E2%80%93Smirnov_test

- 즉, Null Hypothesis 를 기각하려면 (차이가 있다고 말하려면) 다른 테스트보다 큰 샘플이 필요하다고 합니다. 이는 꽤 보수적인 방법론이라는것을 의미합니다.

> It only applies to continuous distributions.
>
> <https://www.itl.nist.gov/div898/handbook/eda/section3/eda35g.htm>

- 오로지 Continuous 에 대해서 성립하는 정리이기 때문에 Discrete 의 경우 잘 적용되지 않을 수 있습니다.

> It tends to be more sensitive near the center of the distribution than at the tails.
>
> <https://www.itl.nist.gov/div898/handbook/eda/section3/eda35g.htm>

- 'CDF 차이가 최대' 인 지점은 통상 분포의 중간쯤에서 나타나기 때문에, 분포의 처음 지점이나 마지막 지점에서 분포가 다른점은 과소평가 하는 경향이 있습니다.

> Perhaps the most serious limitation is that the distribution must be fully specified. That is, if location, scale, and shape parameters are estimated from the data, the critical region of the K-S test is no longer valid. It typically must be determined by simulation.
>
> <https://www.itl.nist.gov/div898/handbook/eda/section3/eda35g.htm>

- '비교하고자 하는 분포는 Fully Specifc' 하게 모두 알려져야 한다는 단점이 있습니다. 
  - 즉 Location, scale, shape parameter 를 모두 정확하게 해야한다는 점이죠.

---

   **Reference**

- <https://myweb.uiowa.edu/pbreheny/uk/teaching/621/notes/10-11.pdf>
- <http://www.maths.qmul.ac.uk/~bb/CTS_Chapter3_Students.pdf>
- <https://www.itl.nist.gov/div898/handbook/eda/section3/eda35g.htm>
