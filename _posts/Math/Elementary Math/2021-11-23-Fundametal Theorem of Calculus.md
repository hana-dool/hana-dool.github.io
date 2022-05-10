---
title:  "Fundamental Theorem of Calculus"
excerpt: "미적분학의 기본정리"
categories:
  - Elementary_Math
last_modified_at: 2021-11-23

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 미적분학의 기초 공식입니다.
{: .notice--warning}

# [The Fundamental Theorem of Calculus](#link){: .btn .btn--primary}{: .align-center}

> ## Fundamental Theorem of Calculus 1

> Fundamental Theorem of Calculus part 1

함수 $f:[a, b] \rightarrow \mathbb{R}$ 가 연속이라 하자. 이때, 함수 $g:[a, b] \rightarrow \mathbb{R}$ 를 다음과 같이 정의한다.

$$g(x)=\int_{a}^{x} f(t) \mathrm{d} t$$

그러면 함수 $g$ 는 구간 $[a, b]$ 위에서 연속이고, 구간 $(a, b)$ 에서 미분 가능하며,

$$g^{\prime}(x)=\frac{\mathrm{d}}{\mathrm{d} x} \int_{a}^{x} f(t) \mathrm{d} t=f(x)$$

가 성립한다. 즉, $g^{\prime}(x)=f(x)$ 이다.

> Note

- 증명은 여기서 하지 않겠습니다.
- 왜냐하면 해석학으로 깊이 들어가야하는 부분이 있어서.. 이 부분은 나중에 시간이 되면 커버하도록 할게요

> ## Proof

함수 $f(x)$ 는 구간 $[a, b]$ 내의 $[x, x+h]$ 구간에서 연속이므로, 적분의 평균값 정리에 따라

$\frac{1}{h} \int_{x}^{x+h} f(t) \mathrm{d} t=f(c)$

를 만족하는 점 $c$ 가 구간 $[x, x+h]$ 내에 존재한다. 양 변에 $h \rightarrow 0$ 의 극한을 취하면

$\lim _{h \rightarrow 0} \frac{1}{h} \int_{x}^{x+h} f(t) \mathrm{d} t=\lim _{h \rightarrow 0} f(c)$

이다. $h \rightarrow 0$ 으로 가까워짐에 따라 $c \rightarrow x$ 로 가까워지므로 $\lim _{h \rightarrow 0} f(c)=f(x)$ 이고, 따라서

$\lim _{h \rightarrow 0} \frac{1}{h} \int_{x}^{x+h} f(t) \mathrm{d} t=f(x)$

가 성립한다. 또한

$g(x+h)-g(x)=\int_{a}^{x+h} f(t) \mathrm{d} t-\int_{a}^{x} f(t) \mathrm{d} t$

이므로, 이를 정리하면

$\begin{aligned}
g(x+h)-g(x) &=\int_{a}^{x+h} f(t) \mathrm{d} t+\int_{x}^{a} f(t) \mathrm{d} t \\
&=\int_{x}^{x+h} f(t) \mathrm{d} t
\end{aligned}$

> Example

Find $\frac{d}{d x} \int_{1}^{x^{4}} \sec t d t$.

> Answer

Let $u=x^{4}$. Then
$\begin{aligned} \frac{d}{d x} \int_{1}^{x^{4}} \sec t d t &=\frac{d}{d x} \int_{1}^{u} \sec t d t \\ &=\frac{d}{d u}\left[\int_{1}^{u} \sec t d t\right] \frac{d u}{d x} \quad \text { (by the Chain Rule) } \\ &=\sec u \frac{d u}{d x} \\ &=\sec \left(x^{4}\right) \cdot 4 x^{3} \end{aligned}$

> ## Fundamental Theorem of Calculus 2

> Fundamental Theorem of Calculus part 2

- 함수 $f$ 가 $[a, b]$ 위에서 연속이고 함수 $F$ 가 $f$ 의 임의의 부정적분일 때, 다음이 성립한다.

$$\int_{a}^{b} f(t) \mathrm{d} t=F(b)-F(a)$$

- 미적분의 제1 기본정리에서 바로 유도된다. 
- 이로부터, 미분의 역연산으로서 역도함수(부정적분)가 정적분과 어떠한 관계에 있는지 알 수 있다. 즉, FTC2는 정적분을 계산할 때 부정적분이 어떠한 형태로 사용되는지를 나타내는 정리인 것이다.

> Proof

- 미적분의 제 1 기본정리에 의해, 함수

$$g(x)=\int_{a}^{x} f(t) \mathrm{d} t$$

- 는 $f(x)$ 의 부정적분 중 하나이다. 평균값 정리에 의하여, $F(x)$ 가 $f(x)$ 의 부정적분이라면 적당한 상수 $C$ 에 대해

$$F(x)=\int_{a}^{x} f(t) \mathrm{d} t+C$$

- 가 성립한다. 따라서

$$F(b)=\int_{a}^{b} f(t) \mathrm{d} t+C$$

- 이고, 적분의 성질

$$F(a)=\int_{a}^{a} f(t) \mathrm{d} t+C=0+C=C$$

- 를 이용하여 $C$ 를 소거하면 다음과 같이 증명이 완료된다.

$$F(b)-F(a)=\int_{a}^{b} f(t) \mathrm{d} t $$

---

**Reference**

- 스튜어트 미적분 7ed

