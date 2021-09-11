---
title:  "Histogram"
excerpt: "히스토그램의 최적의 bin 수는?"
categories:
  - Stat_Non_Parametric
tags:
  - 1
last_modified_at: 2021-08-12

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# Histogram

![png](/assets/images/Stat/40_3.png)

- 위 그림처럼 히스토그램을 그려서, 원래 분포를 근사할때에 다양한 Bin 의 갯수를 사용할 수 있습니다.
- 그런데 이럴떄에 과연 bin 사이즈의 최적은 얼마일까요? 
  - bin 이 너무 많으면 너무 Sensitive하게 추정하게 됩니다.
  - bin 이 너무 적으면 너무 Robust 하게 추정하게 됩니다. 

<br>

# Theory 

![png](/assets/images/Stat/40_1.png)

![png](/assets/images/Stat/40_2.png)

- http://faculty.washington.edu/yenchic/18W_425/Lec6_hist_KDE.pdf
- 일반적으로 위와 같게 Bin 의 갯수가 정해지게 됩니다. 
- 아래에서 이 내용을 좀 정리해봅시다. 

<br>

# Bias

![png](/assets/images/Stat/40_4.png)

- M 은 bin 의 갯수 , $\mid p'(x) \mid \le L$  를 기억합시다. 
- 즉 Bias 는 Bin 의 갯수가 많을수록 줄어듬을 알 수 있습니다. 

<br>

# Variance

![png](/assets/images/Stat/40_5.png)

- 위는, Histogtam 의 Variance 를 나타냅니다.
- 즉 bin 의 갯수가 많을수록 Variance 가 커지는것을 알 수 있습니다. 

<br>

# MSE 

- Variance - Bias Trade off 에 의하여 Bin 의 갯수를 최소화 하게 됩니다.

![png](/assets/images/Stat/40_6.png)

- 위처럼 MSE 를 최소화 한다는 생각으로 , M 을 계산하게 된다면 위와 같은 식이 나오게 됩니다. 
- 물론 위에서 M 을 계산할 방법이 없어서 실질적으로 이를 위한 추정은 다양하게 이루어집니다. 
- 하지만 대부분 Bias 와 Variance 의 균형을 위해서 추정됨을 기억합니다.

<br>

# Estimation 

![png](/assets/images/Stat/40_7.png)

- 위와 같이 다양한 추정이 존재합니다. 

<br>

# Reference 

- 식 계산 
  - http://faculty.washington.edu/yenchic/18W_stat425.html

- 추정
  - https://en.wikipedia.org/wiki/Histogram

