---
title:  "Autocorrelation plot"
excerpt: "자기상관 plot"
categories:
  - Py_Arviz
last_modified_at: 2021-10-31
date : 2021-10-31 09:00:00 +0900

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 자기상관을 알아보는 Plot 입니다.
{: .notice--warning}

# [Autocorrelation Plot](#link){: .btn .btn--primary}{: .align-center}

> ## When to use? 

- 이를 측정하는 이유는, MCMC 는 '이전 Step' 에 영향을 받는 샘플링이기 떄문에 결국에 IID 이지 않고 서로 연관되어 있습니다.
- 그러므로 MCMC 방법의 대표값의 정확성을 검증해야 합니다. (얼마나 이 샘플이 정확하느냐?) 
  - 따라서 표본 이 얼마나 독립적인지를 측정하기 위해서 자기상관성 을 측정해야 합니다. 
- 자기상관성을 측정하기 위해서는 중첩된 단계에 대하여 자기상관함수(ACF; Autocorrelation Function)를 사용한다. 
  - ACF는 그래프로 표현할 수 있는데 이 그래프를 통해 독립되지 않는 결과값이 있는지 파악할 수 있다.
- 자기상관 내에서 독립적인 정보가 얼마나 형성되어 있는지를 파악하는 방법은 유효 표본크기(ESS; Effective Sample Size) 를 측정하는 것이다. (이것은 나중에 알아봅시다.)

> ## Example

![png](/assets/images/Python/48_1.png)

- 체인 1의 ACF Plot 은 짧은 시차에서 크지만 (MCMC 니까요) 빠르게 0 이 되는것을 볼 수 있습니다. 
  - 즉 문제가 없음! 
- 체인 2,3 의 ACF Plot 은 짧은 시차에서도 크고, 큰 시차에서도 큰 값을 가지고 있습니다. 
  - 이는 우리가 '각 샘플은 Correlation 이 크기떄문에' target distribution 에 잘 맞는 분포를 만들기 위해서는 '많은 샘플' 을 만들어내야 함을 알 수 있습니다.

> ## Plotting

- 자기상관을 알려주는 plot 입니다.

```python
import matplotlib.pyplot as plt
import arviz as az

az.style.use("arviz-darkgrid")
data = az.load_arviz_data("centered_eight")
az.plot_autocorr(data, var_names=("tau", "mu"))

plt.show()
```

![png](/assets/images/Python/48_2.png)

---

**Reference**

- <https://arviz-devs.github.io/arviz/examples/plot_autocorr.html>
- <https://www.koreascience.or.kr/article/JAKO201917971494629.pdf>
- <https://www.statlect.com/fundamentals-of-statistics/Markov-Chain-Monte-Carlo-diagnostics>

