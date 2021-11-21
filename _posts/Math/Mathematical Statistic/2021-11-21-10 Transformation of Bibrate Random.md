---
title:  "Transformation of Bibrate Random"
excerpt: "2개 변수에 대한 R.V."
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-18

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
---

 두개의 R.V. 에 대해서 Distribution 을 알아보도록 하겠습니다.
{: .notice--warning}

# [Transformation](#link){: .btn .btn--primary}{: .align-center}

> ## Method

- 우리가 이전에 단일 Variable 일때에 Transformation 을 했던것처럼, 다중변수일때에도 변수변환을 할 수 있을것입니다.
- 이때에 중요하게 생각해야하는것은 다음과 같습니다.
  - 자코비안 메트릭스를 곱해줄것
  - 바뀐 Support 를 잘 적용할것
- 위의 2개를 잘 명심하면서 예제를 풀어봅시다. 
  - Jacobian 을 왜 적용해야하는지는 math 쪽에 제가 정리한거 보세요~

> ## Example

> Example

Let $Y_{1}=\frac{1}{2}\left(X_{1}-X_{2}\right)$ and $Y_{2}=X_{2}$ , where $X_{1}$ and $X_{2}$ have the joint pdf

$$f_{X_{1}, X_{2}}\left(x_{1}, x_{2}\right)= \begin{cases}\frac{1}{4} \exp \left(-\frac{x_{1}+x_{2}}{2}\right) & 0<x_{1}<\infty, 0<x_{2}<\infty \\ 0 & \text { elsewhere. }\end{cases}$$

> 1.$X_1 ,X_2$ 로 표현하기

$y_{1}=\frac{1}{2}\left(x_{1}-x_{2}\right), y_{2}=x_{2}$ or, equivalently, $x_{1}=2 y_{1}+y_{2}, x_{2}=y_{2}$ 

> 2.Support 추정하기

define a one-to-one transformation from $$\mathcal{S}=\left\{\left(x_{1}, x_{2}\right): 0<x_{1}<\infty, 0<x_{2}<\infty\right\}$$ onto $$\mathcal{T}=\left\{\left(y_{1}, y_{2}\right):-2 y_{1}<y_{2}\right.$$ and $$\left.0<y_{2}<\infty,-\infty<y_{1}<\infty\right\}$$. 

> 3.Jacobian 구하기

The Jacobian of the transformation is

$$J=\left|\begin{array}{ll}
2 & 1 \\
0 & 1
\end{array}\right|=2$$

> 4.pdf 구하기

hence the joint pdf of $Y_{1}$ and $Y_{2}$ is

$$f_{Y_{1}, Y_{2}}\left(y_{1}, y_{2}\right)= \begin{cases}\frac{|2|}{4} e^{-y_{1}-y_{2}} & \left(y_{1}, y_{2}\right) \in \mathcal{T} \\ 0 & \text { elsewhere }\end{cases}$$

Thus the $\operatorname{pdf}$ of $Y_{1}$ is given by
> 5.marginal 구하기

$$f_{Y_{1}}\left(y_{1}\right)= \begin{cases}\int_{-2 y_{1}}^{\infty} \frac{1}{2} e^{-y_{1}-y_{2}} d y_{2}=\frac{1}{2} e^{y_{1}} & -\infty<y_{1}<0 \\ \int_{0}^{\infty} \frac{1}{2} e^{-y_{1}-y_{2}} d y_{2}=\frac{1}{2} e^{-y_{1}} & 0 \leq y_{1}<\infty\end{cases}$$

or

$$f_{Y_{1}}\left(y_{1}\right)=\frac{1}{2} e^{-\left|y_{1}\right|}, \quad-\infty<y_{1}<\infty$$

---

**Reference**

- Hoggs Introduction to Mathematical Statistics 7ed



