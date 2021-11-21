---
title:  "The Correlation Coefficient"
excerpt: "상관관계"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
---

 상관관계에 대한 수리통계. 다양한 Intuition 도 있기는 한데... 여기에서는 진짜 찐 수학내용만 담도록 할게요
{: .notice--warning}

# [The Correlation Coefficient](#link){: .btn .btn--primary}{: .align-center}

> ## Covariance : $\operatorname{cov}(X, Y)$

> Definition : $\operatorname{cov}(X, Y)$

$$\begin{aligned}
E\left[\left(X-\mu_{1}\right)\left(Y-\mu_{2}\right)\right] &=E\left(X Y-\mu_{2} X-\mu_{1} Y+\mu_{1} \mu_{2}\right) \\
&=E(X Y)-\mu_{2} E(X)-\mu_{1} E(Y)+\mu_{1} \mu_{2} \\
&=E(X Y)-\mu_{1} \mu_{2}
\end{aligned}$$

> ## Correlation Coefficient

> Definition

If each of $\sigma_{1}$ and $\sigma_{2}$ is positive, the number (표준편차이므로 당연히 제곱근이라 양수)

$$\rho=\frac{E\left[\left(X-\mu_{1}\right)\left(Y-\mu_{2}\right)\right]}{\sigma_{1} \sigma_{2}}=\frac{\operatorname{cov}(X, Y)}{\sigma_{1} \sigma_{2}}$$

is called the correlation coefficient of $X$ and $Y .$ 

> ## Theorem 

> Theorem

Suppose $(X, Y)$ have a joint distribution with the variances of $X$ and $Y$ finite and positive. Denote the means and variances of $X$ and $Y$ by $\mu_{1}, \mu_{2}$ and $\sigma_{1}^{2}, \sigma_{2}^{2}$, respectively, and let $\rho$ be the correlation coefficient between $X$ and $Y$. If $E(Y \mid X)$ is linear in $X$ then

$$E(Y \mid X)=\mu_{2}+\rho \frac{\sigma_{2}}{\sigma_{1}}\left(X-\mu_{1}\right)$$

and

$$E(\operatorname{Var}(Y \mid X))=\sigma_{2}^{2}\left(1-\rho^{2}\right)$$

> Note 

- 즉, Let $$E(Y \mid x)=a+b x$$ 를 가정한다면, 우리는 이러한 a,b 를 X,Y 의 표준편차와 correlation coefficient 로 쉽게 표현할 수 있다는 이야기입니다.
- 자세한 증명은 생략.. ( 너무 길고, 굳이 이 정리가 그럴 가치가 있는지 모르겠음 )

> ## MGF with Calculation $\rho$

> Propertyes

$$\frac{\partial^{k+m} M\left(t_{1}, t_{2}\right)}{\partial t_{1}^{k} \partial t_{2}^{m}}=\int_{-\infty}^{\infty} \int_{-\infty}^{\infty} x^{k} y^{m} e^{t_{1} x+t_{2} y} f(x, y) d x d y$$

so that

$$\left.\frac{\partial^{k+m} M\left(t_{1}, t_{2}\right)}{\partial t_{1}^{k} \partial t_{2}^{m}}\right|_{t_{1}=t_{2}=0}=\int_{-\infty}^{\infty} \int_{-\infty}^{\infty} x^{k} y^{m} f(x, y) d x d y=E\left(X^{k} Y^{m}\right)$$

For instance, in a simplified notation that appears to be clear,

$$\begin{aligned} \mu_{1} &=E(X)=\frac{\partial M(0,0)}{\partial t_{1}} \\ \mu_{2} &=E(Y)=\frac{\partial M(0,0)}{\partial t_{2}} \\ \sigma_{1}^{2} &=E\left(X^{2}\right)-\mu_{1}^{2}=\frac{\partial^{2} M(0,0)}{\partial t_{1}^{2}}-\mu_{1}^{2} \\ \sigma_{2}^{2} &=E\left(Y^{2}\right)-\mu_{2}^{2}=\frac{\partial^{2} M(0,0)}{\partial t_{2}^{2}}-\mu_{2}^{2} \end{aligned}$$

- 위와 같은 식을 쉽게 알 수 있습니다. 그리고

> Calculating $\rho$

$$E\left[\left(X-\mu_{1}\right)\left(Y-\mu_{2}\right)\right]=\frac{\partial^{2} M(0,0)}{\partial t_{1} \partial t_{2}}-\mu_{1} \mu_{2}$$

- 위의 식도 추가로 이끌어낼 수 있을것입니다! 

# [Properties of Correlation coef](#link){: .btn .btn--primary}{: .align-center}

> ## $-1 \leq \rho \leq 1$

> Proof

To this end, suppose that $t$ is some real number that we will choose later, and consider the obvious inequality

$$\mathbb{E}\left((V+t W)^{2}\right) \geq 0, \text { where } V=X-\mu_{X} \text { and } W=Y-\mu_{Y}$$

Expanding out the left-hand-side, and using the linearity of expectation, we find that

$$\mathbb{E}\left(V^{2}\right)+2 t \mathbb{E}(V W)+t^{2} \mathbb{E}\left(W^{2}\right) \geq 0$$

Note that the left-hand-side is just a quadratic polynomial in $t$.
Now, clearly we have that

$$\mathbb{E}\left(V^{2}\right)=\sigma_{X}^{2}, \mathbb{E}\left(W^{2}\right)=\sigma_{Y}^{2}, \text { and } \mathbb{E}(V W)=\operatorname{Cov}(X, Y)$$

and so, our polynomial inequality becomes

$$\sigma_{Y}^{2} t^{2}+2 \operatorname{Cov}(X, Y) t+\sigma_{X}^{2} \geq 0$$

From this inequality we find that the only way the left-hand-side could be 0 is if the polynomial has a double-root (i.e. it touches the $x$-axis in a single point), which could only occur if the discriminant is 0 . So, the discriminant must always be negative or 0 , which means that

$$4 \operatorname{Cov}(X, Y)^{2}-4 \sigma_{X}^{2} \sigma_{Y}^{2} \leq 0$$

In other words,

$$\frac{\operatorname{Cov}(X, Y)^{2}}{\sigma_{X}^{2} \sigma_{Y}^{2}} \leq 1$$

provided, of course, that the denominator does not vanish.

> Note

- 사실 위 증명을 Cauchy schearz inequality 를 쓸 수 있지만, 이는 A 로 A 를 증명하는것과도 같은 Cheating 이라고 해서, 위처럼 증명했다고 합니다.

> ## $\rho=\pm 1$ implies $X$ and $Y$ are linearly relate

> Proof

이전의 증명을 살펴볼때에 $\rho=\pm 1$ 값을 가진다는것은 , discriminant of that quadratic polynomial 이 0 을 가진다는 것입니다. 즉 이는 mean that the quadratic polynomial vanishes for some value $t_{0}$ for the variable t. This would mean, however, that

$$\mathbb{E}\left(\left(Y-\mu_{Y}+t_{0} X-t_{0} \mu_{X}\right)^{2}\right)=\mathbb{E}\left(\left(V+t_{0} W\right)^{2}\right)=0$$

The only way this could occur is if $Y-\mu_{Y}+t_{0} X-t_{0} \mu_{X}=0$ with probability 1 , which shows that $X$ and $Y$ are linearly related with probability 1 

> ## if $X$ and $Y$ are linearly related, then $\rho=\pm 1$

> Proof

Now suppose that

$$Y=\lambda_{1} X+\lambda_{2}$$

Then, we have that $\mu_{Y}=\lambda_{1} \mu_{X}+\lambda_{2}$; and so,

$$\operatorname{Cov}(X, Y)=\mathbb{E}\left(\left(X-\mu_{X}\right)\left(\lambda_{1} X-\lambda_{1} \mu_{X}\right)\right)=\lambda_{1} \mathbb{E}\left(\left(X-\mu_{X}\right)^{2}\right)=\lambda_{1} \sigma_{X}^{2}$$

Also, by properties of variance,

$$\sigma_{Y}^{2}=V\left(\lambda_{1} X+\lambda_{2}\right)=V\left(\lambda_{1} X\right)=\lambda_{1}^{2} \sigma_{X}^{2}$$

From this it follows that

$$\rho=\frac{\operatorname{Cov}(X, Y)}{\sigma_{X} \sigma_{Y}}=\frac{\lambda_{1}}{\left|\lambda_{1}\right|}$$

which is $\pm 1$, with the sign determined by the sign of $\lambda_{1}$.

> ## Independence $\to$ $\rho=0$ but not the converse

> Independence $\to$ $\rho=0$

If $X$ and $Y$ are independent, then

$$\operatorname{Cov}(X, Y)=\mathbb{E}\left(\left(X-\mu_{X}\right)\left(Y-\mu_{Y}\right)\right)=\mathbb{E}\left(X-\mu_{X}\right) \mathbb{E}\left(Y-\mu_{Y}\right)=0 \cdot 0=0$$

so of course the correlation coefficient is also 0 .

> Independence $\leftarrow$ $\rho=0$

The converse, however, is not true. To see this, we begin by defining independent random variables $A$ and $B$ that take on the values $\pm 1$ with equal probability (i.e. probability $1 / 2$ ) (즉 1/2 확률로 $\pm 1$ 의 값을 가지는 R.V.로 A,B 를 각각 같게 정의)

Then, we define

$$X:=A+B, \text { and } Y:=A-B$$

We have that

$$\operatorname{Cov}(X, Y)=\mathbb{E}(X Y)-\mu_{X} \mu_{Y}=\mathbb{E}\left(A^{2}-B^{2}\right)-0=0$$

since $A^{2}=B^{2}=1$. Yet, $X$ and $Y$ are dependent, since, for example, if $X=2$, then $Y$ is forced to equal 0 .

---

**Reference**

- Hoggs Introduction to Mathematical Statistics 7ed
- <https://people.math.gatech.edu/~ecroot/3225/rho_notes.pdf>





