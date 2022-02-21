---
title:  "scale rate location parameter"
excerpt: "parameter 의 3가지 종류" 
categories:
  - Stat
last_modified_at: 2022-02-19

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 3가지 종류의 파라미터
{: .notice--warning}

# [parameters](#link){: .btn .btn--primary}{: .align-center}

> ## Scale parameters

- If a family of [probability distributions](https://en.wikipedia.org/wiki/Probability_distribution) is such that there is a parameter *s* (and other parameters *θ*) for which the [cumulative distribution function](https://en.wikipedia.org/wiki/Cumulative_distribution_function) satisfies

$$F(x ; s, \theta)=F(x / s ; 1, \theta)$$

- 즉 위와 같이 scale parameter 가 s 일때, $x \to x/s$ 로 스케일을 바꾸게 되면 parameter 가 1로 줄어들게 되는 파라미터를 의미합니다.
  - scale parameter 가 클수록 뾰족한 값을 가지게 됩니다.

> ## Rate Parameters

- 그냥 scale parameter 의 역수를 Rate parameter 라고 합니다.

> Example

- Exponential Distribution 은 아래와 같이 Scale parameter 를 쓰느냐, Rate Parameter 를 쓰느냐에 따라서 두가지 form 을 가지게 됩니다.
- Scale Parameter $\beta$ : $$f(x ; \beta)=\frac{1}{\beta} e^{-x / \beta}, x \geq 0$$
- Rate Parameter $\lambda$ : $$f(x ; \lambda)=\lambda e^{-\lambda x}, x \geq 0$$

> ## Location Parameters

- 

---

**Reference**

- <https://link.springer.com/article/10.1007%2Fs10654-016-0149-3>









