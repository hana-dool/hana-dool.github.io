---
title:  "Limiting Distribution"
excerpt: "분포간의 극한분포"
categories:
  - Stat
tags:
  - 1
last_modified_at: 2021-07-02

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# Binomial -> Normal

아래와 같이 CLT 로 인해서 Binomial 과 Normal 의 관계가 성립하게 된다. (n 이 충분히 크기만 하면 된다!)

![image-20210409133610490](C:\Users\goran\Desktop\Documents\Typora_image\2_9)

# Binomial -> Poisson

$B(n,p) \to Pois(np)$ when $ n \to \inf , p \to 0 $ (가이드는 없지만 $ 100 \le n , p \le 0.01$ 이라고 한다..)

아래 식에서 since , and 부분의 식을 볼때에 n->inf / p->0 의 식이 필요함을 볼 수 있다.

![image-20210410125959087](C:\Users\goran\Desktop\Documents\Typora_image\2_11.png)

아래와 같이 poisson 분포는 lambda 가 커질수록 Normal 에 가까워진다는것을 볼 수 있다.

![poisson3](C:\Users\goran\Desktop\Documents\Typora_image\poisson3.png)

# Poisson -> Normal

$\lambda$ 가 충분히 크다면 $pois(\lambda) \sim N(\lambda , \lambda)$  가 성립한다. 이 이유는 아래와 같다.

![image-20210410130402231](C:\Users\goran\Desktop\Documents\Typora_image\2_12.png)

