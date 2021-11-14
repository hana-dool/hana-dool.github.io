---
title:  "Expectation"
excerpt: "통계학적인 기댓값"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-13

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
---

 제일 기초가 되는 기댓값 , 분산 등에 대한 정리를 알아봅시다. 
{: .notice--warning}

# [Expectation](#link){: .btn .btn--primary}{: .align-center}

> ## Discrete Case

> Defitinion

Let $X$ be a discrete random variable with $\operatorname{pmf} p_{X}(x)$ and

$$\sum_{x}|x| p_{X}(x)<\infty$$

then the expectation of $X$ is

$$E(X)=\sum_{x} x p_{X}(x)$$

> Note

- Discrete 일때에는 그저 Sigma 만 잘 더해주면 됩니다.
- Continuous 일때보다 상대적으로 훨씬 간단합니다. (적분할 필요가 없이 그냥 Summation 만 잘 하면 되니까요)

> ## Continuous Case

> Definition

Let $X$ be a continuous random variable with $\operatorname{pdf} f_{X}(x)$ and

$$\int_{-\infty}^{\infty}|x| f_{X}(x) d x<\infty$$

then the expectation of $X$ is

$$E(X)=\int_{-\infty}^{\infty} x f_{X}(x) d x$$

> Note

- Continuous 일때에는, '적분' 을 해야되서 약간 어려울 수 있습니다.

> ## Example

> Example 

Let $X$ have the pdf Find Expectation of x

$$f(x)= \begin{cases}4 x^{3} & 0<x<1 \\ 0 & \text { elsewhere }\end{cases}$$

> Answer

$$E(X)=\int_{0}^{1} x\left(4 x^{3}\right) d x=\int_{0}^{1} 4 x^{4} d x=\left[\frac{4 x^{5}}{5}\right]_{0}^{1}=\frac{4}{5}$$

> ## Thm : Lotus (Law of the unconscious statistician)

- <https://en.wikipedia.org/wiki/Law_of_the_unconscious_statistician>

> Theorems 

Let $X$ be a random variable and let $Y=g(X)$ for some function $g$

(a) Suppose $X$ is continuous with pdf $f_{X}(x) .$ If $$\int_{-\infty}^{\infty} \mid g(x) \mid f_{X}(x) d x<\infty$$, then the expectation of $Y$ exists and it is given by

$$E(Y)=\int_{-\infty}^{\infty} g(x) f_{X}(x) d x$$

(b) Suppose $X$ is discrete with $p m f p_{X}(x)$. Suppose the support of $X$ is denoted by $\mathcal{S}_{X} .$ If $$\sum_{x \in \mathcal{S}_{X}} \mid g(x) \mid p_{X}(x)<\infty$$, then the expectation of $Y$ exists and it is given by

$$E(Y)=\sum_{x \in \mathcal{S}_{X}} g(x) p_{X}(x)$$

> Continuous case Proof

For a continuous random variable $X$, let $Y=g(X)$, and suppose that $g$ is differentiable and that its inverse $g^{-1}$ is monotonic. By the formula for inverse functions and differentiation,

$$\frac{d}{d y}\left(g^{-1}(y)\right)=\frac{1}{g^{\prime}\left(g^{-1}(y)\right)}$$

Because $x=g^{-1}(y)$,

$$d x=\frac{1}{g^{\prime}\left(g^{-1}(y)\right)} d y$$

So that by a change of variables,

$$\int_{-\infty}^{\infty} g(x) f_{X}(x) d x=\int_{-\infty}^{\infty} y f_{X}\left(g^{-1}(y)\right) \frac{1}{g^{\prime}\left(g^{-1}(y)\right)} d y$$

Now, notice that because the cumulative distribution function $F_{Y}(y)=P(Y \leq y)$, substituting in the value of $g(X)$, taking the inverse of both sides, and rearranging yields $F_{Y}(y)=F_{X}\left(g^{-1}(y)\right)$. Then, by the chain rule,

$$f_{Y}(y)=f_{X}\left(g^{-1}(y)\right) \frac{1}{g^{\prime}\left(g^{-1}(y)\right)}$$

Combining these expressions, we find

$$\int_{-\infty}^{\infty} g(x) f_{X}(x) d x=\int_{-\infty}^{\infty} y f_{Y}(y) d y$$

By the definition of expected value,

$$\mathrm{E}[g(X)]=\int_{-\infty}^{\infty} g(x) f_{X}(x) d x$$

> Discrete Case Proof

Let $Y=g(X)$. Then begin with the definition of expected value.

$$\begin{aligned}
&\mathrm{E}[Y]=\sum_{y} y f_{Y}(y) \\
&\mathrm{E}[g(X)=Y]=\sum_{y} y P(g(X)=y) \\
&\mathrm{E}[g(X)]=\sum_{y} y \sum_{x: g(x)=y} f_{X}(x) \\
&\mathrm{E}[g(X)]=\sum_{x} g(x) f_{X}(x)
\end{aligned}$$

> Note

- 이 법칙의 이름은 '통계학자의 무의식 법칙' 인데, 그 이유는 수학적으로 동일한것을 제대로증명해야하는 thm 인데에도 불구하고, 그냥 niave 하다고 생각한 상태에서 사용하는 사람이 많기 때문입니다.
- 위 규칙을 직관적으로만 생각해보면 다음과 같습니다.
  - 'Variable '을 다른 입장에서 바라보았다고 , Expectation 이 바뀔수는 없으니까 동일하다! 
  - 만일 X 로 볼때의 평균이나, g(X) 입장에서의 평균이나 모두 같은 '기댓값' 을 바라보고있는것인데, 변하는것은 말이 안되기 때문이죠...

---

**Reference**

- 호그의 Introduction to Mathematical Statistics 7ed
- <https://en.wikipedia.org/wiki/Law_of_the_unconscious_statistician>

