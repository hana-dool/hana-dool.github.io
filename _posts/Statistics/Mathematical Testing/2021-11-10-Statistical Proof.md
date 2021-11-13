---
title:  "Expectation and Variance and Independent"
excerpt: "기댓값과 분산 그리고 독립"
categories:
  - Stat_Math_Testing
last_modified_at: 2021-11-10

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 제일 기초가 되는 기댓값 , 분산 등에 대한 정리를 알아봅시다. 
{: .notice--warning}

# [Expected Value](#link){: .btn .btn--primary}{: .align-center}

> ## Definition 1 : Expectation Value

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

> If X and Y are jointly distributed random variables with expected values E(X) and E(Y ), then 
>
> $$E(X + Y ) = E(X) + E(Y ).$$

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

$$
\begin{aligned}
E(X+Y) &=\iint(x+y) f(x, y) d x d y \\
&=\iint(x+y) f(x, y) d x d y \\
&=\iint x f(x, y) d y d x+\iint y f(x, y) d x d y \\
&=\int x\left[\int f(x, y) d y\right] d x+\int y\left[\int f(x, y) d x\right] d y \\
&=\int x f_{X}(x) d x+\int y f_{Y}(y) d y \\
&=E(X)+E(Y)
\end{aligned}​
$$



- 위처럼 Expectation 은 분해되어 계산되어질 수 있습니다! 

> ## Corollary 2 

> When X and Y are jointly distributed, E(X) and E(Y ) exist, and a, b, and c are nite real numbers, by Theorems 1 and 2, 
>
> $$E(a+bX+cY) = a+ bE(X) + cE(Y)$$

- 위의 증명은 이전과 완전 똑같이 하면 되므로 생략하겠습니다!

# [Independent](#link){: .btn .btn--primary}{: .align-center}

> ## Definition 2 : Independent

> Random Variables X, Y are independent if anf only if
>
> $$f_{X,Y}(x,y) = f_X(x) f_Y(y)$$

> ## Theorem 3 

> If X and Y are independent, and E [g(X)] and E [h(Y )] both exist, then
>
> $$E[g(X) \cdot h(Y)]=E[g(X)] \cdot E[h(Y)]$$

**proof**

$$\begin{aligned}
E[g(X) \cdot h(Y)] &=\iint g(x) \cdot h(y) f(x, y) d x d y \\
&=\iint g(x) \cdot h(y) f_{X}(x) \cdot f_{Y}(y) d x d y \\
& \quad \text { (by assumption of independence) } \\
&=\int g(x) f_{X}(x) d x \cdot \int h(y) f_{Y}(y) d y \\
&=E[g(X)] \cdot E[h(Y)]
\end{aligned}$$

# [Variance](#link){: .btn .btn--primary}{: .align-center}

> ## Definition 3 : Variance

> The variance of X is 
>
> $$Var(X) = E[(X-E(X))^2]$$ 
>
> if variace value exist 

> ## Theorem 4

> $$Var(X) = E(X^2) - (E(X))^2$$

**proof**

$$\begin{aligned}
\operatorname{Var}(X) &=E\left[(X-E(X))^{2}\right] \\
&=E\left[X^{2}-2 X \cdot E(X)+(E(X))^{2}\right] \\
&=E\left(X^{2}\right)-2 E(X) \cdot E(X)+(E(X))^{2} \\
&=E\left(X^{2}\right)-2(E(X))^{2}+(E(X))^{2} \\
&=E\left(X^{2}\right)-(E(X))^{2}
\end{aligned}$$

- 이때 var(X) 가 존재하기 위해서는 $E(X)$ 와 $E(X^2)$ 둘다 Exist 해야 함을 잘 알아둡시다! 

> ## Theorem 5 

> If a and b are nite real numbers, and X is a random variable with finite E(X) and Var(X), then 
>
> $$Var(aX + b) = a^2V ar(X).$$

**proof : Existence**

- Var(aX+b) 의 Existence 를 보이기 위해서는 , $E((aX+b)^2)$ 의 존재성만 보이면 됩니다. 
  - 왜냐하면 Thm 1 에서 이미 $E(aX+b)$ 의 존재성은 보여지기 때문입니다.

$$\begin{aligned}
E\left(\left|(a X+b)^{2}\right|\right) &=E\left((a X+b)^{2}\right) \\
&=E\left(a^{2} X^{2}+2 a b X+b^{2}\right) \\
&=E\left(a^{2} X^{2}\right)+E(2 a b X)+E\left(b^{2}\right) \\
&=a^{2} E\left(X^{2}\right)+2 a b E(X)+b^{2} \\
&<\infty
\end{aligned}$$

- a,b 는 finite constants 이고, $E(X^2)$ 과 $E(X)$ 둘다 exist 하다고 가정했으므로, $Var(aX +b)$ 는 존재합니다. 

**proof : Calculation**

- Thm 1 에 의하여 다음이 성립합니다.

$$\begin{aligned}
\operatorname{Var}(a X+b) &=E\left((a X+b)^{2}\right)-[E(a X+b)]^{2} \\
&=\left[a^{2} E\left(X^{2}\right)+2 a b E(X)+b^{2}\right]-[a E(X)+b]^{2} \\
&=a^{2} E\left(X^{2}\right)+2 a b E(X)+b^{2}-a^{2}(E(X))^{2}-2 a b E(X)-b^{2} \\
&=a^{2}\left[E\left(X^{2}\right)-(E(X))^{2}\right] \\
&=a^{2} \operatorname{Var}(X)
\end{aligned}$$

> ## Theorem 6 

> If X and Y are independent random variables with nite E(X) and V ar(X) and E(Y ) and V ar(Y ), then 
>
> $$Var(X + Y ) = Var(X) + Var(Y ).$$

**proof : Existnce**

- 존재성을 보이기 위해서 우리는 단지 $$E((X+Y)^2)$$ 가 존재ㅏ는지만 알면 됩니다. 
  - 왜냐하면 이미 가정에서 Finite $E(X) ,  E(Y)$ 를 가정하기 떄문에, $E(X+Y)$ 도 Finite 하기 때문입니다.

$$
\begin{aligned}
E\left(\left|(X+Y)^{2}\right|\right) &=E\left((X+Y)^{2}\right) \\
&=E\left(X^{2}+2 X Y+Y^{2}\right) \\
&=E\left(X^{2}\right)+E(2 X Y)+E\left(Y^{2}\right) \\
&=E\left(X^{2}\right)+2 E(X) E(Y)+E\left(Y^{2}\right) \\
&=\text{(because $X$ and $Y$ are independent)}\\
&<\infty
\end{aligned}
$$
**proof : Calculation**

$$\begin{aligned}
\operatorname{Var}(X+Y) &=E\left((X+Y)^{2}\right)-[E(X+Y)]^{2} \\
&=\left[E\left(X^{2}\right)+2 E(X) E(Y)+E\left(Y^{2}\right)\right]-[E(X)+E(Y)]^{2} \\
&=E\left(X^{2}\right)+2 E(X) E(Y)+E\left(Y^{2}\right)-\left[(E(X))^{2}+2 E(X) E(Y)+(E(Y))^{2}\right] \\
&=\left[E\left(X^{2}\right)-(E(X))^{2}\right]+\left[E\left(Y^{2}\right)-(E(Y))^{2}\right] \\
&=\operatorname{Var}(X)+\operatorname{Var}(Y)
\end{aligned}$$

> ## Corollary 2 

> When X and Y are independent random variables, Var(X) and Var(Y) exist, and a, b, and c are finite real numbers, by Theorems 5 and  6
>
> $$\operatorname{Var}(a+b X+c Y)=b^{2} \operatorname{Var}(X)+c^{2} \operatorname{Var}(Y)$$

---

   **Reference**

- <https://digitalcommons.usu.edu/cgi/viewcontent.cgi?article=1014&context=gradreports>

