---
title:  "Cauchy Schwarz inequality"
excerpt: "코시 슈바르츠 부등식"
categories:
  - Elementary_Math
last_modified_at: 2021-11-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 정말 유명한 부등식이고, 중요한 정리
{: .notice--warning}

# [Cauchy–Schwarz inequality](#link){: .btn .btn--primary}{: .align-center}

> ## Cauchy Schwarz Inequality

> Theorem (The Cauchy-Schwarz inequality) 

Let $V$ be a vector space over $\mathbf{R}$, and let $\langle\cdot, \cdot\rangle$ be an inner product on $V$. Then

$$|\langle u, v\rangle| \leq\langle u, u\rangle^{1 / 2}\langle v, v\rangle^{1 / 2} \text { for all } u, v \in V$$

이때 $\|\mathbf{u}\|^{2}=\langle\mathbf{u}, \mathbf{u}\rangle$ 로 정의한다면

$$|\langle\mathbf{u}, \mathbf{v}\rangle| \leq\|\mathbf{u}\|\|\mathbf{v}\|$$

> Proof 1 : Special case

If either $u$ or $v$ is the zero vector, then above thm holds because both sides are zero. We can therefore assume that both $u$ and $v$ are nonzero vectors. We first prove the result in the special case that $\langle u, u\rangle=\langle v, v\rangle=1$. In this case, we have to show that

$$|\langle u, v\rangle| \leq 1$$

By the property of an inner product, we have $\langle u-v, u-v\rangle \geq 0$. Applying the first two properties of an inner product, we can rewrite $\langle u-v, u-v\rangle$ as follows:

$$\langle u-v, u-v\rangle=\langle u, u\rangle-2\langle u, v\rangle+\langle v, v\rangle=2-2\langle u, v\rangle$$

We then obtain

$$2-2\langle u, v\rangle \geq 0 \Rightarrow\langle u, v\rangle \leq 1$$

Repeating this reasoning, but starting with the inequality $\langle u+v, u+v\rangle \geq 0$ leads to $$-1 \leq\langle u, v\rangle$$, and thus we see that $ \mid \langle u, v\rangle \mid \leq 1$

> Proof : Normal Case

We now consider the general case in which $u, v \in V$ are nonzero vectors. Let us define

$$\hat{u}=\langle u, u\rangle^{-1 / 2} u, \hat{v}=\langle v, v\rangle^{-1 / 2} v$$

Then

$$\langle\hat{u}, \hat{u}\rangle=\left\langle\langle u, u\rangle^{-1 / 2} u,\langle u, u\rangle^{-1 / 2} u\right\rangle=\langle u, u\rangle^{-1}\langle u, u\rangle=1$$

and similarly for $\langle\hat{v}, \hat{v}\rangle .$ It follows that $$ \mid \langle\hat{u}, \hat{v}\rangle \mid \leq 1 .$$ But

$$\begin{aligned}
\mid \langle\hat{u}, \hat{v}\rangle| &=\left|\left\langle\langle u, u\rangle^{-1 / 2} u,\langle v, v\rangle^{-1 / 2} v\right\rangle\right | \\
&=\langle u, u\rangle^{-1 / 2}\langle v, v\rangle^{-1 / 2}|\langle u, v\rangle|
\end{aligned}$$

and hence

$$\langle u, u\rangle^{-1 / 2}\langle v, v\rangle^{-1 / 2}|\langle u, v\rangle| \leq 1$$

which yields the desired inequality:

$$|\langle u, v\rangle| \leq\langle u, u\rangle^{1 / 2}\langle v, v\rangle^{1 / 2}$$

> Note 

- 위 증명은 Finite-Dimensional Linear Algebra 336p 를 가져온 것입니다. 

> ## Application 

> 고등학교에서

$\left(a^{2}+b^{2}\right)\left(c^{2}+d^{2}\right) \geq(a c+b d)^{2} \quad\left(\right.$ 단, 등호는 $\frac{a}{c}=\frac{b}{d}$ 일 때 성립 $)$

- 일반적으로는 위와 같은 식으로 많이 쓰이던것을 기억하나요? 이를 좀더 일반화하면 다음과 같습니다.

$\left(a_{1}^{2}+\cdots+a_{n}^{2}\right)\left(b_{1}^{2}+\cdots+b_{n}^{2}\right) \geq\left(a_{1} b_{1}+\cdots+a_{n} b_{n}\right)^{2}$

> integral Forms

$$\int_{a}^{b} f(x)^{2} d x \int_{a}^{b} g(x)^{2} d x \geq\left(\int_{a}^{b} f(x) g(x) d x\right)^{2}$$

> Probability Forms

$$E\left(X^{2}\right) E\left(Y^{2}\right) \geq E(X Y)^{2}$$

> ## More : Probability Theory

> definition of inner product

After defining an inner product on the set of random variables using the expectation of their product,

$$\langle X, Y\rangle:=\mathrm{E}(X Y)$$

the Cauchy-Schwarz inequality becomes

$$|\mathrm{E}(X Y)|^{2} \leq \mathrm{E}\left(X^{2}\right) \mathrm{E}\left(Y^{2}\right)$$

> Application 

$$\operatorname{Var}(Y) \geq \frac{\operatorname{Cov}(Y, X)^{2}}{\operatorname{Var}(X)}$$

위의 inequality 를 증명하려고 한다고 합시다.

$$\begin{aligned}|\operatorname{Cov}(X, Y)|^{2} &=|\mathrm{E}((X-\mu)(Y-\nu))|^{2} \\ &=|\langle X-\mu, Y-\nu\rangle|^{2} \\ & \leq\langle X-\mu, X-\mu\rangle\langle Y-\nu, Y-\nu\rangle \\ &=\mathrm{E}\left((X-\mu)^{2}\right) \mathrm{E}\left((Y-\nu)^{2}\right) \\ &=\operatorname{Var}(X) \operatorname{Var}(Y), \end{aligned}$$

위처럼 매우 간단하게 증명되는것을 볼 수 있습니다.

---

**Reference**

- Finite-Dimensional Linear Algebra

- [namu.wiki](https://namu.wiki/w/%EC%BD%94%EC%8B%9C-%EC%8A%88%EB%B0%94%EB%A5%B4%EC%B8%A0%20%EB%B6%80%EB%93%B1%EC%8B%9D)

- <https://en.wikipedia.org/wiki/Cauchy%E2%80%93Schwarz_inequality>

  



