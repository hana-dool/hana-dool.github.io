---
title:  "Expectation and Variance"
excerpt: "기댓값과 분산의 Property 에 대한 수학적 증명"
categories:
  - Stat_Testing
last_modified_at: 2021-11-10

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Testing 에 대해서 수학적으로 어떻게 유도되었는가를 알아봅시다.
{: .notice--warning}

# [Expected Value and Variance](#link){: .btn .btn--primary}{: .align-center}

> ## Definition 1 

> if $X$ is a random variable with pdf f(x) or pmf p(x), and a function g(X) is measurable, then the expected value of g(X) is deined as 
>
> $$E(g(X))= \begin{cases}\int_{-\infty}^{\infty} g(x) f(x) d x, & \text { if } X \text { is continuous } \\ \sum_{-\infty}^{\infty} g(x) p(x) d x, & \text { if } X \text { is discrete }\end{cases}$$
>
> if $$E(\mid g(X) \mid ) < \infty$$ , otherwise $$E(g(X))$$ does not exist

- 위의 식의 경우 단순한 Definition 이기 떄문에 할 말은 없습니다만. 주의해야 할 점 하나는  $$E(\mid g(X) \mid ) < \infty  $$ 의 조건입니다.
- 즉 값이 '유한' 할 때에만 Expectation 이 존재한다고 합니다.

> ## Theorem 1

> If a and b are nite real numbers, and X is a random variable with expected value E(X), then E(aX + b) = aE(X) + b.

**proof : Existence**

- $\int_X f(x)dx = 1$ and $\sum_ p(x)=1 $ 임을 기억합시다! 즉 두 값이 존재한다고 할 수 있습니다. 

$$\begin{aligned}
E(|a X+b|) &=\int_{X}(|a x+b|) f(x) d x \\
& \leq \int_{X}(|a||x|+|b|) f(x) d x \\
& \text { by Triangle Inequality } \\
&=\int_{X}|a||x| f(x) d x+\int|b| f(x) d x \\
&=|a| \int|x| f(x) d x+|b| \int f(x) d x \\
&=|a| E(|X|)+|b|(1) \\
&=|a| E(|X|)+|b| \\
&<\infty
\end{aligned}$$

- 위에서 보다시피 그 존재성 $$<\infty$$ 도 증명할 수 있으므로 우리는 Existence 까지 보일 수 있습니다. 
- 그러므로 $$E(aX+b)$$ 는 존재합니다.

**proof : Calculation**

- 이제 각 값의 계산이 어떻게 되는지도 증명해야 합니다. 
  - Discrete 이나 Continuous 나 같은 맥락으로 증명이 진행되므로 , Discrete Case 만 우선 증명하겠습니다.

$$\begin{aligned}
E(a X+b) &=\sum_{X}(a x+b) p(x) \\
&=\sum_{X} a x p(x)+\sum_{X} b p(x) \\
&=a \sum_{X} x p(x)+b \sum_{X} p(x) \\
&=a E(X)+b(1) \\
&=a E(X)+b
\end{aligned}$$

> ## Theorem 2 

> If X and Y are jointly distributed random variables with expected values E(X) and E(Y ), then E(X + Y ) = E(X) + E(Y ).

**proof : Existence**

- $$f(x,y)$$ 를 joint pdf 라고 합시다. 그리고 $$f_X(x)$$ , $$f_Y(y)$$ 는 marginal pdf 라 합시다.  
- 우선 저는 Existence 에 대해서 증명해 보겠습니다.

$$
\begin{aligned}
E(|X+Y|) &=\iint(|x+y|) f(x, y) d x d y \\
& \leq \iint(|x|+|y|) f(x, y) d x d y \ \ \ \ by Triangle Inequality \\
&=\iint|x| f(x, y) d y d x+\iint|y| f(x, y) d x d y \\
&=\int|x|\left[\int f(x, y) d y\right] d x+\int|y|\left[\int f(x, y) d x\right] d y \\
&=\int|x| f_{X}(x) d x+\int|y| f_{Y}(y) d y \\
&=E(|X|)+E(|Y|) \\
&<\infty
\end{aligned}
$$
- 위 처럼 $$\infty$$ 로 bounded 된다는것을 알았으므로 존재성을 보장할 수 있게됩니다.

**proof : Calculation**

- 이제 존재성을 알았으므로 각 계산이 잘 이루어지는지에 대해서 알아봐야 합니다. 

$$\begin{aligned}
E(X+Y) &=\iint(x+y) f(x, y) d x d y \\
&=\iint(x+y) f(x, y) d x d y \\
&=\iint x f(x, y) d y d x+\iint y f(x, y) d x d y \\
&=\int x\left[\int f(x, y) d y\right] d x+\int y\left[\int f(x, y) d x\right] d y \\
&=\int x f_{X}(x) d x+\int y f_{Y}(y) d y \\
&=E(X)+E(Y)
\end{aligned}$$

- 위처럼 Expectation 은 분해되어 계산되어질 수 있습니다! 

> ## Corollary 2 

> When X and Y are jointly distributed, E(X) and E(Y ) exist, and a, b, and c are nite real numbers, by Theorems 1 and 2, 
>
> $$E(a+bX+cY) = a+ bE(X) + cE(Y)$$

- 위의 증명은 이전과 완전 똑같이 하면 되므로 생략하겠습니다!

> ## Definition 2 

> Random Variables X, Y are independent if anf only if
>
> $$f_{X,Y}(x,y) = f_X(x) f_Y(y)$$

---

   **Reference**

- <https://digitalcommons.usu.edu/cgi/viewcontent.cgi?article=1014&context=gradreports>

 위와 같은 방법론은 비교하기가 편리해서 많은사람이 잘못 판단하는 부분이라 주의가 필요합니다. Schenker와 Gentleman (2001)은 의학 분 야 학술지에서 이러한 오류를 범한 논문을 60개 넘게 발견했다고 보고했다고 합니다..
{: .notice--success}

