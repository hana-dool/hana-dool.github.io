---
title:  "Integral Rules"
excerpt: "기초적인 적분 규칙"
categories:
  - Elementary_Math
last_modified_at: 2021-11-10

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 졸업하고 한참 지나니까 제일 기초적인 적분도 까먹네요.. 여기에서는 기본적인 적분의 방법론엗 대해서 대충 알아보겠습니다.
{: .notice--warning}

# [Integral Rules](#link){: .btn .btn--primary}{: .align-center}

> ## Chain Rule

> Definition

The Chain Rule If $g$ is differentiable at $x$ and $f$ is differentiable at $g(x)$, then the composite function $F=f \circ g$ defined by $F(x)=f(g(x))$ is differentiable at $x$ and $F^{\prime}$ is given by the product

$$F^{\prime}(x)=f^{\prime}(g(x)) \cdot g^{\prime}(x)$$

In Leibniz notation, if $y=f(u)$ and $u=g(x)$ are both differentiable functions, then 

$$\frac{d y}{d x}=\frac{d y}{d u} \frac{d u}{d x}$$

> **proof**

- Let $\Delta u$ be the change in $u$ corresponding to a change of $\Delta x$ in $X$, that is,

$$\Delta u=g(x+\Delta x)-g(x)$$

- Then the corresponding change in $y$ is

$$\Delta y=f(u+\Delta u)-f(u)$$

- It is tempting to write

$$\begin{aligned}
\frac{d y}{d x} &=\lim _{\Delta x \rightarrow 0} \frac{\Delta y}{\Delta x} \\
&=\lim _{\Delta x \rightarrow 0} \frac{\Delta y}{\Delta u} \cdot \frac{\Delta u}{\Delta x} \\
&=\lim _{\Delta x \rightarrow 0} \frac{\Delta y}{\Delta u} \cdot \lim _{\Delta x \rightarrow 0} \frac{\Delta u}{\Delta x} \\
&=\lim _{\Delta u \rightarrow 0} \frac{\Delta y}{\Delta u} \cdot \lim _{\Delta x \rightarrow 0} \frac{\Delta u}{\Delta x} \quad \text { (Note that } \Delta u \rightarrow 0 \text { as } \Delta x \rightarrow 0 \\
&=\frac{d y}{d u} \frac{d u}{d x}
\end{aligned}$$

- 위가 사실 완벽한 증명은 아니지만 충분하다고 생각합니다.

> ## Implicit Differentiation

- 이는 딱히 정리는 아니지만, 알아두면 좋을 적분 기술입니다. 
- 이 방법은 단일 parameter 에 대해서 식을 적분하기가 힘들때에 사용할 수 있는 방법입니다.

> Mothod

(a) If $x^{2}+y^{2}=25$, find $\frac{d y}{d x}$.

(a) Differentiate both sides of the equation $x^{2}+y^{2}=25$ :

$$\begin{aligned}
\frac{d}{d x}\left(x^{2}+y^{2}\right) &=\frac{d}{d x} \\
\frac{d}{d x}\left(x^{2}\right)+\frac{d}{d x}\left(y^{2}\right) &=0
\end{aligned}$$

<br>

Remembering that $y$ is a function of $x$ and using the Chain Rule, we have

$$\frac{d}{d x}\left(y^{2}\right)=\frac{d}{d y}\left(y^{2}\right) \frac{d y}{d x}=2 y \frac{d y}{d x}$$

Thus

$$2 x+2 y \frac{d y}{d x}=0$$

Now we solve this equation for $d y / d x$ :

$$\frac{d y}{d x}=-\frac{x}{y}$$



> ## Substitution Rule (치환 적분)

> How to? 

If $u=g(x)$ is a differentiable function whose range is an interval $I$ and $f$ is continuous on $I$, then

$$\int f(g(x)) g^{\prime}(x) d x=\int f(u) d u$$

> Example

- 위의 정리를 이용하면 , 치환을 통해서 여러 적분을 계산할 수 있습니다.

$\int\left(x^{2}+x\right)^{3}(2 x+1) d x$ 에서 $x^{2}+x=t$ 로 놓으면 $\frac{d t}{d x}=\left(x^{2}+x\right)^{\prime}=2 x+1$ 이므로

$$\begin{aligned}
\int\left(x^{2}+x\right)^{3}(2 x+1) d x &=\int\left(x^{2}+x\right)^{3}\left(x^{2}+x\right)^{\prime} d x \\
&=\int t^{3} d t=\frac{1}{4} t^{4}+C=\frac{1}{4}\left(x^{2}+x\right)^{4}+C
\end{aligned}$$

> ## Product Rule (부분 적분)

> How to?

$$\frac{d}{d x}[f(x) g(x)]=f(x) g^{\prime}(x)+g(x) f^{\prime}(x)$$

위를 응용하면 다음과 같습니다.

$$\int f(x) g^{\prime}(x) d x=f(x) g(x)-\int g(x) f^{\prime}(x) d x$$

> Note

- 위의 정리를 이용하면, 복잡해보이는 두개의 함수가 곱해져 있는 경우를 쉽게 해결할 수 있습니다.
  - 고등학교때도 많이 들었겠지만 지삼다로 기억하시나요? 
  - 적분되어야 하는 함수 ($g(x)$) 는 지수 , 삼각함수가 좋다는 이야기죠. 왜냐하면 이 함수들은 적분되는 형태가 매우 안정적이라서 별로 안변하거덩요

> Example

- (1) $\int x e^{x} d x$ 

$$f(x)=x, g^{\prime}(x)=e^{x} \text { 으로 놓으면 } f^{\prime}(x)=1, g(x)=e^{x}$$

$$\therefore \int x e^{2} d x=x e^{2}-\int 1 \cdot e^{2} d x=x e^{2}-e^{2}+C$$

<br>

- (2) $\int x \cos x d x$ 

$$\begin{aligned}
& f(x)=x, g^{\prime}(x)=\cos x \text { 로 놓으면 } f^{\prime}(x)=1, g(x)=\sin x \\
\therefore & \int x \cos x d x=x \sin x-\int 1 \cdot \sin x d x=x \sin x+\cos x+C
\end{aligned}$$

<br>

- (3) $\int \ln x d x$ 

$$\begin{aligned}
&f(x)=\ln x, g^{\prime}(x)=1 \text { 로 놓으면 } f^{\prime}(x)=\frac{1}{x}, g(x)=x \\
&\therefore \quad \int \ln x d x=\ln x \cdot x-\int \frac{1}{x} \cdot x d x=x \ln x-x+C
\end{aligned}$$



> ## Symmetric and integral

> how to?

Suppose $f$ is continuous on $[-a, a]$.

(a) If $f$ is even $[f(-x)=f(x)]$, then $\int_{-a}^{a} f(x) d x=2 \int_{0}^{a} f(x) d x$.

(b) If $f$ is odd $[f(-x)=-f(x)]$, then $\int_{-a}^{a} f(x) d x=0$.

- 이는 조금만 생각하면 쉽게 알 수 있는 부분입니다.

> ## The Quotient Rule (분수 적분)

> how to?

If $f$ and $g$ are differentiable, then

$$\frac{d}{d x}\left[\frac{f(x)}{g(x)}\right]=\frac{g(x) \frac{d}{d x}[f(x)]-f(x) \frac{d}{d x}[g(x)]}{[g(x)]^{2}}$$

> **proof**

We find a rule for differentiating the quotient of two differentiable functions $u=f(x)$ and $v=g(x)$ in much the same way that we found the Product Rule. If $x, u$, and $v$ change by amounts $\Delta x, \Delta u$, and $\Delta v$, then the corresponding change in the quotient $u / v$ is

$$\begin{aligned}
\Delta\left(\frac{u}{v}\right) &=\frac{u+\Delta u}{v+\Delta v}-\frac{u}{v}=\frac{(u+\Delta u) v-u(v+\Delta v)}{v(v+\Delta v)} \\
&=\frac{v \Delta u-u \Delta v}{v(v+\Delta v)}
\end{aligned}$$

so 

$$\frac{d}{d x}\left(\frac{u}{v}\right)=\lim _{\Delta x \rightarrow 0} \frac{\Delta(u / v)}{\Delta x}=\lim _{\Delta x \rightarrow 0} \frac{v \frac{\Delta u}{\Delta x}-u \frac{\Delta v}{\Delta x}}{v(v+\Delta v)}$$

As $\Delta x \rightarrow 0, \Delta v \rightarrow 0$ also, because $v=g(x)$ is differentiable and therefore continuous. Thus, using the Limit Laws, we get

$$\frac{d}{d x}\left(\frac{u}{v}\right)=\frac{v \lim _{\Delta x \rightarrow 0} \frac{\Delta u}{\Delta x}-u \lim _{\Delta x \rightarrow 0} \frac{\Delta v}{\Delta x}}{v \lim _{\Delta x \rightarrow 0}(v+\Delta v)}=\frac{v \frac{d u}{d x}-u \frac{d v}{d x}}{v^{2}}$$

> **Example**

Find an equation of the tangent line to the curve $y=e^{x} /\left(1+x^{2}\right)$ at the point $\left(1, \frac{1}{2} e\right)$
> Answer

$$\begin{aligned}
\frac{d y}{d x} &=\frac{\left(1+x^{2}\right) \frac{d}{d x}\left(e^{x}\right)-e^{x} \frac{d}{d x}\left(1+x^{2}\right)}{\left(1+x^{2}\right)^{2}} \\
&=\frac{\left(1+x^{2}\right) e^{x}-e^{x}(2 x)}{\left(1+x^{2}\right)^{2}} \\
&=\frac{e^{x}(1-x)^{2}}{\left(1+x^{2}\right)^{2}}
\end{aligned}$$

---

**Reference**

- <https://freshrimpsushi.github.io/posts/leibniz-integral-rule/>
- <https://m.blog.naver.com/CommentList.naver?blogId=sbssbi69&logNo=90164672246>



