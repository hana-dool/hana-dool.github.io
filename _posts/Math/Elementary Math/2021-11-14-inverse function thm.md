---
title:  "Inverse function Thm"
excerpt: "역함수 규칙"
categories:
  - Elementary_Math
last_modified_at: 2021-11-13

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 졸업하고 한참 지나니까 기초적인것도 까먹네요.. 수학과인데.. 
{: .notice--warning}

# [Inverse Function Thms](#link){: .btn .btn--primary}{: .align-center}

> ## 쉬운 버젼

> definition and Proof

$\mathrm{y}=\mathrm{f}(\mathrm{x})$ 의 역함수를 $\mathrm{y}=\mathrm{g}(\mathrm{x})$ 라고 하면 역함수의 성질에 의해서

$$(f \circ g)(x)=x=>f(g(x))=x$$

합성함수 미분법을 이용하면

$$f^{\prime}(g(x)) g^{\prime}(x)=1$$

즉 $\therefore g^{\prime}(x)=\frac{1}{f^{\prime}(g(x))}$ 됩니다.

> Example

$f(x)=x^{3}$ 일 때 역함수를 $g(x)$ 라고 하면 $g^{\prime}(8)$ 의 값은?

> Answer

$$\begin{array}{ll}
g^{\prime}(8)=\frac{1}{f^{\prime}(g(8))} \quad f(x)=x^{3} & <=>x=g(x)^{3} \\
8=g(8)^{3}, \quad g(8)=2 & \text { 이고 } f^{\prime}(x)=3 x^{2}
\end{array}$$

$$g^{\prime}(8)=\frac{1}{f^{\prime}(g(8))}=\frac{1}{f^{\prime}(2)}=\frac{1}{3 \cdot 2^{2}} \text { 이 된다. }$$

> Note 

- 하지만 위의 정리는 아주 단변량일때 아주 대충 증명한것으로, 다음과 같은 것이 훨씬더 Formal 한 정리입니다. 

> ## in Analysis

> definition

Theorem 2.8.1. Suppose that $f: E \subset \mathbb{R}^{n} \rightarrow \mathbb{R}^{n}$ is in $C^{1}$ class. Let $a \in E$ and $D f(a)$ be invertible matrix. Then

(1) $\exists$ an open set $U$ such that $a \in U$ and $f: U \rightarrow f(U)$ is 1-1 with $f(U)$ open set.

(2) Its inverse $f^{-1}: f(U) \rightarrow U$ is in $C^{1}$ class and $D f^{-1}(f(x))=[D f(x)]^{-1}$.

> Proof

- 증명은 생략... (연세대 수학과 김준일 교수님 강의노트 참조)

---

**Reference**

- <https://en.wikipedia.org/wiki/Jacobian_matrix_and_determinant>
- <http://www.stat.rice.edu/~dobelman/notes_papers/math/Jacobian.pdf>
- <https://ride-or-die.info/jacobian-change-of-variable/>
- <https://angeloyeo.github.io/2020/07/24/Jacobian.html>





