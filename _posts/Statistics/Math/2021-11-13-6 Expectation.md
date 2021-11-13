---
title:  "Expectation"
excerpt: "통계학적인 기댓값"
categories:
  - Stat_Math_Testing
last_modified_at: 2021-11-13

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
---

 제일 기초가 되는 기댓값 , 분산 등에 대한 정리를 알아봅시다. 
{: .notice--warning}

# [Expectation](#link){: .btn .btn--primary}{: .align-center}

> ## Discrete 

> Definition. Let $X$ be a discrete random variable with $\operatorname{pmf} p_{X}(x)$ and
> $$
> \sum_{x}|x| p_{X}(x)<\infty
> $$
> then the expectation of $X$ is
> $$
> E(X)=\sum_{x} x p_{X}(x)
> $$

- Discrete 일때에는 그저 Sigma 만 잘 더해주면 됩니다. 
- Continuous 일때보다 상대적으로 훨씬 간단합니다.

> ## Continuous

> Definition. Let $X$ be a continuous random variable with $\operatorname{pdf} f_{X}(x)$ and
> $$
> \int_{-\infty}^{\infty}|x| f_{X}(x) d x<\infty
> $$
> then the expectation of $X$ is
> $$
> E(X)=\int_{-\infty}^{\infty} x f_{X}(x) d x
> $$

- Continuous 일때에는, '적분' 을 해야되서 약간 어려울 수 있습니다.

> ## Example



**Reference**

- 호그의 Introduction to Mathematical Statistics 7ed

