---
title:  "Transformation"
excerpt: "변수 변환과 자코비안"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-12
toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 제일 기초가 되는 기댓값 , 분산 등에 대한 정리를 알아봅시다. 
{: .notice--warning}

# [Transformation](#link){: .btn .btn--primary}{: .align-center}

> ## Discrete R.V. Transformation

> How to

Suppose we have a random variable $X$ and its pmf. We are interested, though, in a random variable $Y$ which is some transformation of $X$, say, $Y=g(X) .$ Then, the pmf of $Y$ is obtained as

$$p_{Y}(y)=P(Y=y)=P(g(X)=y)=P\left(X=g^{-1}(y)\right)=p_{X}\left(g^{-1}(y)\right)$$

> Note

- Discrete Random Variable 에 대하여, pdf 의 변환은 위처럼 일어납니다.
  - 사실 증명은 필요 없는것이, 위의 수식을 보면 그냥 '명확' 합니다. 
  - Equality 로 너무 자명한 관계를 이루는 것들이라... 

> ## Example : Discrete

> Problems

Find the pmf of $Y=X^{2}$, where $X$ has the pmf

$$p_{X}(x)=\left\{\begin{array}{cl}
x / 6 & \text { if } x=1,2,3 \\
0 & \text { otherwise }
\end{array}\right.$$

> Answer 

The transformation $Y=g(X)=X^{2}$ maps $$\mathcal{D}_{X}=\{x: x=1,2,3\}$$ onto $\mathcal{D}_{Y}=\{y: y= 1,4,9\}$, which is a one-to-one transformation because the space of $X$ is positive. Then, we have the single-valued inverse function $X=g^{-1}(Y)=\sqrt{Y}$, and the pmf of $Y$ is obtained as

$$p_{Y}(y)=\left\{\begin{array}{cl}
\sqrt{y} / 6 & \text { if } y=1,4,9 \\
0 & \text { otherwise }
\end{array}\right.$$

> Note

- 즉 위처럼 pmf 의경우에는 별 다를거 없이 함수만 잘 적용해 주고 Support 만 제대로 바꾸어 주면 됩니다.
- '각 점에는 probability mass 가 정확히 존재하므로 , Transformation 때에도 편한 것이죠'

> ## Continuous R.V. Transformation

> How to

Theorem 1.7.1. Let $X$ be a continuous random variable with $p d f f_{X}(x)$ and support $${S}_{X}$$. Let $Y=g(X)$, where $g(x)$ is a one-to-one differentiable function, on the support of $X, S_X$. Denote the inverse of $g$ by $x=g^{-1}(y)$ and let $d x / d y=d\left[g^{-1}(y)\right] / d y$. Then the $p d f$ of $Y$ is given by

$$f_{Y}(y)=f_{X}\left(g^{-1}(y)\right)\left|\frac{d x}{d y}\right|, \quad \text { for } y \in \mathcal{S}_{Y}$$

where the support of $Y$ is the set $$\mathcal{S}_{Y}=\left\{y=g(x): x \in \mathcal{S}_{X}\right\}$$.

> Proof

Since $g(x)$ is one-to-one and continuous, it is either strictly monotonically increasing or decreasing. Assume that it is strictly monotonically increasing, for now. The $\operatorname{cdf}$ of $Y$ is given by

$$F_{Y}(y)=P[Y \leq y]=P[g(X) \leq y]=P\left[X \leq g^{-1}(y)\right]=F_{X}\left(g^{-1}(y)\right)$$

Hence, the $$\operatorname{pdf}$$ of $$Y$$ is

$$f_{Y}(y)=\frac{d}{d y} F_{Y}(y)=f_{X}\left(g^{-1}(y)\right) \frac{d x}{d y}$$

where $d x / d y$ is the derivative of the function $x=g^{-1}(y) .$ In this case, because $g$ is increasing, $d x / d y>0 .$ Hence, we can write $$d x / d y= \mid d x / d y \mid $$.

Suppose $g(x)$ is strictly monotonically decreasing. Then $F_{Y}(y)=$ $1-F_{X}\left(g^{-1}(y)\right) .$ Hence, the pdf of $Y$ is $f_{Y}(y)=f_{X}\left(g^{-1}(y)\right)(-d x / d y) .$ But since $g$ is decreasing, $d x / d y<0$ and, hence, $$-d x / d y=\mid d x / d y \mid $$. Thus Equation is true in both cases.

> Note : Jacobian

- 위처럼 Continuous 한 경우에는 Jacobian 이 들어가게 됩니다. 이는 각 point of mass 를 바로 변환할 수가 없기 때문이죠. 
- 이에 대해서는 짧게 언급만 하고 넘어가겠습니다.

Henceforth, we refer to $d x / d y=(d / d y) g^{-1}(y)$ as the Jacobian $($ denoted by $J)$ of the transformation. In most mathematical areas, $J=d x / d y$ is referred to as the Jacobian of the inverse transformation $x=g^{-1}(y)$, but in this book it is called the Jacobian of the transformation, simply for convenience.

- Transformation 을 할때에 , 위처럼 Jacobian 을 곱해주어야 합니다. 이때 Jacobian 은 다른쪽에서 다루었으므로 생략!

> ## Example : Continuous

> Example

Find the pdf of $Y=-2 \log X$, where the pdf of $X$ is

$$f_{X}(x)= \begin{cases}1 & \text { if } 0<x<1 \\ 0 & \text { elsewhere }\end{cases}$$

> Answer

The support sets of $X$ and $Y$ are given by $(0,1)$ and $(0, \infty)$, respectively. The transformation is one-to-one between these sets. The inverse of the transformation is $x=g^{-1}(y)=e^{-y / 2}$ and the Jacobian of the transformation is

$$J=\frac{d x}{d y}=-\frac{1}{2} e^{-y / 2}$$

Thus, the pdf of $Y$ is obtained as

$$f_{Y}(y)=\left\{\begin{array}{cc}
\frac{1}{2} e^{-y / 2} & \text { if } 0<y<\infty \\
0 & \text { elsewhere }
\end{array}\right.$$

---

**Reference**

- 호그의 Introduction to Mathematical Statistics 7ed

