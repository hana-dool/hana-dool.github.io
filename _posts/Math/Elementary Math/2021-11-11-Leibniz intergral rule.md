---
title:  "Leibniz integral rules"
excerpt: "적분의 순서를 바꾸어도 유효하게 만들기"
categories:
  - Elementary_Math
last_modified_at: 2021-11-10

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Lebniz Rule 에 대해서 알아봅시다! 
{: .notice--warning}

# [Lebniz Integral Rule](#link){: .btn .btn--primary}{: .align-center}

> ## Lebniz Integral Rule

$f(x, t)$ 와 $\frac{\partial f}{\partial x}(x, t)$ 가 연속이라고 하자. 그러면 아래의 식이 성립한다.

$$\frac{d}{d x} \int_{a}^{b} f(x, t) d t=\int_{a}^{b} \frac{\partial f}{\partial x}(x, t) d t$$

> ## Proof

- 연속이면 적분가능하므로 $u$ 를 다음과 같이 Define 가능할 것입니다.

$$u(x):=\int_{a}^{b} f(x, t) d t$$

- 그러면 다음이 성립합니다.

$$\begin{aligned}
\frac{u(x+h)-u(x)}{h} &=\frac{\int_{a}^{b} f(x+h, t) d t-\int_{a}^{b} f(x, t) d t}{h} \\
&=\frac{\int_{a}^{b}[f(x+h, t)-f(x, t)] d t}{h} \\
&=\int_{a}^{b} \frac{f(x+h, t)-f(x, t)}{h} d t
\end{aligned}$$

- 그리고 고정된 $y$ 에 대하여 $f(x, y)$ 에 평균값 정리를 적용하면 아래의 식을 만족하는 $c \in[x, x+h]$ 가 존재합니다.

$$\frac{f(x+h, t)-f(x, t)}{h}=\frac{\partial f}{\partial x}(c, t)$$

- 이를 $(1)$ 에 대입하면 다음을 얻는다.

$$\frac{u(x+h)-u(x)}{h}=\int_{a}^{b} \frac{\partial f}{\partial x}(c, t)$$

- 이제 임의의 $\epsilon>0$ 에 대해서 $\epsilon_{0}=\frac{\epsilon}{b-a}$ 라고 합시다.
  - $[x, x+h] \times[a, b]$ 는 컴팩트이고 가정에 의해 $\frac{\partial f}{\partial x}$ 는 컴팩트 구간 위에서 연속이므로 균등 연속이다. 
  - 그러면 충분히 작은 $h$ 에 대해서 다음이 성립합니다.

$$\left|\frac{\partial f}{\partial x}(x+h, t)-\frac{\partial f}{\partial x}(x, t)\right|<\epsilon_{0}$$

- 또한 $c \in[x, x+h]$ 이므로 균등 연속의 정의에 의해 다음이 성립한다.

$$\left|\frac{\partial f}{\partial x}(c, t)-\frac{\partial f}{\partial x}(x, t)\right|<\epsilon_{0}$$

- 이제 계산해보면 다음을 얻는다.

$$\begin{aligned}
&\left|\lim _{h \rightarrow 0} \frac{u(x+h, t)-u(x, t)}{h}-\int_{a}^{b} \frac{\partial f}{\partial x}(x, t) d t\right| \\
=&\left|\lim _{h \rightarrow 0} \int_{a}^{b} \frac{\partial f}{\partial x}(c, t) d t-\int_{a}^{b} \frac{\partial f}{\partial x}(x, t) d t\right| \\
=&\left|\lim _{h \rightarrow 0} \int_{a}^{b}\left[\frac{\partial f}{\partial x}(c, t)-\frac{\partial f}{\partial x}(x, t)\right] d t\right| \\
=& \lim _{h \rightarrow 0}\left|\int_{a}^{b}\left[\frac{\partial f}{\partial x}(c, t)-\frac{\partial f}{\partial x}(x, t)\right] d t\right| \\
\leq & \lim _{h \rightarrow 0} \int_{a}^{b}\left|\frac{\partial f}{\partial x}(c, t)-\frac{\partial f}{\partial x}(x, t)\right| d t \\
\leq & \lim _{h \rightarrow 0} \int_{a}^{b} \epsilon_{0} d t \\
=& \lim _{h \rightarrow 0}(b-a) \epsilon_{0} \\
=& \epsilon
\end{aligned}$$

- 위 식은 임의의 $\epsilon>0$ 에 대해서 성립하므로 다음을 얻는다.

$$\lim _{h \rightarrow 0} \frac{u(x+h, t)-u(x, t)}{h}=\int_{a}^{b} \frac{\partial f}{\partial x}(x, t) d t$$

- 또한 $u(x):=\int_{a}^{b} f(x, t) d t$ 이므로 다음이 성립합니다.

$$\frac{d}{d x} \int_{a}^{b} f(x, t) d t=\int_{a}^{b} \frac{\partial f}{\partial x}(x, t) d t$$

**Reference**

- <https://freshrimpsushi.github.io/posts/leibniz-integral-rule/>

