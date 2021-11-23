---
title:  "Transformations for Several Random Variables"
excerpt: "변수를 변환해보기"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-23

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
---

 여러 변수들에 대한 변환
{: .notice--warning}

# [Transformations for Several Random Variables](#link){: .btn .btn--primary}{: .align-center}

> ## Transformation

> Theorem

define a one-to-one transformation that $
x_{1}, x_{2}, \ldots, x_{n}
$ maps $\mathcal{S}$ onto $\mathcal{T}$ in the $y_{1}, y_{2}, \ldots, y_{n}$ space and, hence, maps the subset $A$ of $\mathcal{S}$ onto a subset $B$ of $\mathcal{T}$. 

Let the first partial derivatives of the inverse functions be continuous and let the $n$ by $n$ determinant (called the Jacobian) not be identically zero in $\mathcal{T}$. Then

$$J=\left|\begin{array}{cccc}
\frac{\partial x_{1}}{\partial y_{1}} & \frac{\partial x_{1}}{\partial y_{2}} & \cdots & \frac{\partial x_{1}}{\partial y_{n}} \\
\frac{\partial x_{2}}{\partial y_{1}} & \frac{\partial x_{2}}{\partial y_{2}} & \cdots & \frac{\partial x_{2}}{\partial y_{n}} \\
\vdots & \vdots & & \vdots \\
\frac{\partial x_{n}}{\partial y_{1}} & \frac{\partial x_{n}}{\partial y_{2}} & \cdots & \frac{\partial x_{n}}{\partial y_{n}}
\end{array}\right|$$

$$\begin{aligned} & \int \cdots \int_{A} f\left(x_{1}, x_{2}, \ldots, x_{n}\right) d x_{1} d x_{2} \cdots d x_{n} \\=& \int \cdots \int_{B} f\left[w_{1}\left(y_{1}, \ldots, y_{n}\right), w_{2}\left(y_{1}, \ldots, y_{n}\right), \ldots, w_{n}\left(y_{1}, \ldots, y_{n}\right)\right]|J| d y_{1} d y_{2} \cdots d y_{n} \end{aligned}$$

where 

$$y_{1}=u_{1}\left(x_{1}, x_{2}, \ldots, x_{n}\right), \quad y_{2}=u_{2}\left(x_{1}, x_{2}, \ldots, x_{n}\right), \ldots, y_{n}=u_{n}\left(x_{1}, x_{2}, \ldots, x_{n}\right)$$

$$x_{1}=w_{1}\left(y_{1}, y_{2}, \ldots, y_{n}\right), \quad x_{2}=w_{2}\left(y_{1}, y_{2}, \ldots, y_{n}\right), \ldots, x_{n}=w_{n}\left(y_{1}, y_{2}, \ldots, y_{n}\right)$$

즉 우리는 위의 transformation 을 통하여 아래의 함수 $g$ 를 찾는것이라 할 수 있습니다.

$$g\left(y_{1}, y_{2}, \ldots, y_{n}\right)=f\left[w_{1}\left(y_{1}, \ldots, y_{n}\right), \ldots, w_{n}\left(y_{1}, \ldots, y_{n}\right)\right]|J|$$

where $\left(y_{1}, y_{2}, \ldots, y_{n}\right) \in \mathcal{T}$, and is zero elsewhere.

> ## Example

> Problem

Let $X_{1}, X_{2}, X_{3}$ be iid with common pdf
$$
f(x)= \begin{cases}e^{-x} & 0<x<\infty \\ 0 & \text { elsewhere }\end{cases}
$$
joint pdf of $X_{1}, X_{2}, X_{3}$ is
$$
f_{X_{1}, X_{2}, X_{3}}\left(x_{1}, x_{2}, x_{3}\right)= \begin{cases}e^{-\sum_{i=1}^{3} x_{i}} & 0<x_{i}<\infty, i=1,2,3 \\ 0 & \text { elsewhere }\end{cases}
$$
Consider the random variables $Y_{1}, Y_{2}, Y_{3}$ defined by

$$Y_{1}=\frac{X_{1}}{X_{1}+X_{2}+X_{3}}, Y_{2}=\frac{X_{2}}{X_{1}+X_{2}+X_{3}}, \text { and } Y_{3}=X_{1}+X_{2}+X_{3}$$

> 1.변환 찾기

inverse transformation is given by

$$x_{1}=y_{1} y_{3}, x_{2}=y_{2} y_{3}, \text { and } x_{3}=y_{3}-y_{1} y_{3}-y_{2} y_{3}$$

> 2.자코비안 구하기

Find Jacobian

$$J=\left|\begin{array}{ccc}
y_{3} & 0 & y_{1} \\
0 & y_{3} & y_{2} \\
-y_{3} & -y_{3} & 1-y_{1}-y_{2}
\end{array}\right|=y_{3}^{2}$$

> 3.서포트 구하기

The support of $X_{1}, X_{2}, X_{3}$ maps onto
$0<y_{1} y_{3}<\infty, 0<y_{2} y_{3}<\infty$, and $0<y_{3}\left(1-y_{1}-y_{2}\right)<\infty$

which is equivalent to the support $\mathcal{T}$ given by

$$\mathcal{T}=\left\{\left(y_{1}, y_{2}, y_{3}\right): 0<y_{1}, 0<y_{2}, 0<1-y_{1}-y_{2}, 0<y_{3}<\infty\right\}$$

> 4.변환 적용하기

Hence the joint pdf of $Y_{1}, Y_{2}, Y_{3}$ is

$$g\left(y_{1}, y_{2}, y_{3}\right)=y_{3}^{2} e^{-y_{3}}, \quad\left(y_{1}, y_{2}, y_{3}\right) \in \mathcal{T}$$

> Note : Marginal 구하기

The marginal pdf of $Y_{1}$ is

$$g_{1}\left(y_{1}\right)=\int_{0}^{1-y_{1}} \int_{0}^{\infty} y_{3}^{2} e^{-y_{3}} d y_{3} d y_{2}=2\left(1-y_{1}\right), \quad 0<y_{1}<1$$

zero elsewhere. 

Likewise the marginal pdf of $Y_{2}$ is

$$g_{2}\left(y_{2}\right)=2\left(1-y_{2}\right), \quad 0<y_{2}<1$$

zero elsewhere, 

while the pdf of $Y_{3}$ is

$$g_{3}\left(y_{3}\right)=\int_{0}^{1} \int_{0}^{1-y_{1}} y_{3}^{2} e^{-y_{3}} d y_{2} d y_{1}=\frac{1}{2} y_{3}^{2} e^{-y_{3}}, \quad 0<y_{3}<\infty$$

zero elsewhere. 

> Independence 확인하기

Because $g\left(y_{1}, y_{2}, y_{3}\right) \neq g_{1}\left(y_{1}\right) g_{2}\left(y_{2}\right) g_{3}\left(y_{3}\right), Y_{1}, Y_{2}, Y_{3}$ are dependent random variables.

---

**reference**

- Hoggs Introduction to Mathematical Statistics 7ed
- <https://people.math.gatech.edu/~ecroot/3225/rho_notes.pdf>





