---
title:  "Fundamental Theorem of Calculus"
excerpt: "코시 슈바르츠 부등식"
categories:
  - Elementary_Math
last_modified_at: 2021-11-23

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 미적분학의 기초 공식입니다.
{: .notice--warning}

# [The Fundamental Theorem of Calculus](#link){: .btn .btn--primary}{: .align-center}

> ## Fundamental Theorem of Calculus 1

> Fundamental Theorem of Calculus part 1

If $f$ is continuous on $[a, b]$, then the function $g$ defined by

$$g(x)=\int_{a}^{x} f(t) d t \quad a \leqslant x \leqslant b$$

is continuous on $[a, b]$ and differentiable on $(a, b)$, and $g^{\prime}(x)=f(x)$

> Note

- 증명은 여기서 하지 않겠습니다.
- 왜냐하면 해석학으로 깊이 들어가야하는 부분이 있어서.. 이 부분은 나중에 시간이 되면 커버하도록 할게요

> Example

Find $\frac{d}{d x} \int_{1}^{x^{4}} \sec t d t$.

> Answer

Let $u=x^{4}$. Then
$\begin{aligned} \frac{d}{d x} \int_{1}^{x^{4}} \sec t d t &=\frac{d}{d x} \int_{1}^{u} \sec t d t \\ &=\frac{d}{d u}\left[\int_{1}^{u} \sec t d t\right] \frac{d u}{d x} \quad \text { (by the Chain Rule) } \\ &=\sec u \frac{d u}{d x} \\ &=\sec \left(x^{4}\right) \cdot 4 x^{3} \end{aligned}$

> ## Fundamental Theorem of Calculus 2

> Fundamental Theorem of Calculus part 2

The Fundamental Theorem of Calculus, Part 2 If $f$ is continuous on $[a, b]$, then

$$v$$

where $F$ is any antiderivative of $f$, that is, a function such that $F^{\prime}=f$.

---

**Reference**

- 스튜어트 미적분 7ed


