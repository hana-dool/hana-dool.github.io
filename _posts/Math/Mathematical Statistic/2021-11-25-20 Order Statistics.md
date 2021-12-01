---
title:  "Order Statistics"
excerpt: "순서통계량에 대한 계산하기"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-25

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
---

  순서통계량에 대해서 알아보기
{: .notice--warning}

# [Distributions of Order Statistics](#link){: .btn .btn--primary}{: .align-center}

> ## Distributions of Order Statistics

> Definition

Let $X_{1}, X_{2}, \ldots, X_{n}$ denote a random sample from a distribution of the continuous type having a pdf $f_{X}(x)$ that has support $\mathcal{S}=(a, b)$, where $-\infty \leq a<b \leq\infty .$ Let $Y_{1}$ be the smallest among these $X_{i}$ 's, $Y_{2}$ the second smallest among these $X_{i}$ 's, $\ldots$, and $Y_{n}$ the largest among these $X_{i}$ 's such that

$$Y_{1}<Y_{2}<\cdots<Y_{n}$$

We call $Y_{i}$ the $i$ th order statistic of the random sample $X_{1}, X_{2}, \ldots, X_{n}$

> ## Theorem : pdf of order statstics

> Theorem

Let $Y_{1}<Y_{2}<\cdots<Y_{n}$ denote the $n$ order statistics based on the random sample $X_{1}, X_{2}, \ldots, X_{n}$ from a continuous distribution with pdf $f_{X}(x)$ and support $(a, b)$. Then the joint pdf of $Y_{1}, Y_{2}, \ldots, Y_{n}$ is given by

$$\begin{aligned}
f_{\mathbf{Y}}\left(y_{1}, y_{2}, \ldots, y_{n}\right)=& f_{\mathbf{X}}\left(x_{1}=y_{1}, x_{2}=y_{2}, \ldots, x_{n}=y_{n}\right)|J| \\
&+f_{\mathbf{X}}\left(x_{1}=y_{2}, x_{2}=y_{1}, \ldots, x_{n}=y_{n}\right)|J| \\
&+\cdots+f_{\mathbf{X}}\left(x_{1}=y_{n}, x_{2}=y_{n-1}, \ldots, x_{n}=y_{1}\right)|J| \\
=& n ! f_{X}\left(y_{1}\right) f_{X}\left(y_{2}\right) \cdots f_{X}\left(y_{n}\right), a<y_{1}<y_{2}<\cdots<y_{n}<b
\end{aligned}$$

> Note

- 위와 같이 n! 번을 더하는 이유는 뭘까요?
  - $ \{ y_1,y_2,y_3\}$ = (1,2,3) 의 경우를 생각해봅시다.
  - 이 경우, $\{x_1,x_2,x_3\}$ 가 가질수 있는 경우의 수는 다음과 같습니다.
    - (1,2,3) / (1,3,2) / (2,1,3) / (2,3,1) / (3,1,2) / (3,2,1) 
    - 즉 경우의수가 6개이므로 3! 을 pdf 에 더해져야하는것입니다. 

> ## Example

> Examples

Let $X_{1}, X_{2}, X_{3}$ denote a random sample from $f_{X}(x)$ and let $Y_{1}<Y_{2}<Y_{3}$ denote the order statistics of the sample. Compute the probability that $Y_{2} \leq m$, where $F_{X}(m)=\frac{1}{2}$

> joint pdf 구하기

The joint pdf of the three order statistics is

$$f_{\mathbf{Y}}\left(y_{1}, y_{2}, y_{3}\right)=6 f_{X}\left(y_{1}\right) f_{X}\left(y_{2}\right) f_{X}\left(y_{3}\right), a<y_{1}<y_{2}<y_{3}<b$$

> Marginal pdf 구하기

Thus, the marginal pdf of $Y_{2}$ is

$$\begin{aligned}
f_{Y_{2}}\left(y_{2}\right) &=\int_{y_{2}}^{b} \int_{a}^{y_{2}} f_{\mathbf{Y}}\left(y_{1}, y_{2}, y_{3}\right) d y_{1} d y_{3} \\
&=6 f_{X}\left(y_{2}\right) \int_{y_{2}}^{b} f_{X}\left(y_{3}\right)\left(\int_{a}^{y_{2}} f_{X}\left(y_{1}\right) d y_{1}\right) d y_{3} \\
&=6 f_{X}\left(y_{2}\right) F_{X}\left(y_{2}\right)\left[1-F_{X}\left(y_{2}\right)\right], a<y_{2}<b
\end{aligned}$$

> $P\left(Y_{2} \leq m\right)$ 구하기

Thus, the probability of interest is

$$\begin{aligned}
P\left(Y_{2} \leq m\right) &=\int_{a}^{m} f_{Y_{2}}\left(y_{2}\right) d y_{2} \\
&=6 \int_{a}^{m}\left[f_{X}\left(y_{2}\right) F_{X}\left(y_{2}\right)-f_{X}\left(y_{2}\right) F_{X}\left(y_{2}\right)^{2}\right] d y_{2} \\
&=6\left\{\frac{F_{X}\left(y_{2}\right)^{2}}{2}-\frac{F_{X}\left(y_{2}\right)^{3}}{3}\right\}_{a}^{m} \\
&=6\left(\frac{1}{8}-\frac{1}{24}\right)=\frac{1}{2}
\end{aligned}$$

> Note : interpret

-  위의 경우, 3개의 R.V. 에 대해서, 중간의 값이 중앙값보다 작은 값을 가질 확률이 1/2 라는 것입니다. 

> ## Facts : marginal pdf 

> Facts

By using the fact that

$$\int_{a}^{x} f_{X}(y) F_{X}(y)^{m-1} d y=\frac{F_{X}(x)^{m}}{m}$$

and

$$\int_{x}^{b} f_{X}(y)\left[1-F_{X}(y)\right]^{m-1} d y=\frac{\left[1-F_{X}(x)\right]^{m}}{m}$$

it is easy to express the marginal pdf of any order statistic in terms of $F_{X}(x)$ and $f_{X}(x)$. That is, when $a<Y_{1}<\cdots<Y_{k-1}<Y_{k}<Y_{k+1}<\cdots<Y_{n}<b$, the marginal pdf of $Y_{k}$ is obtained as

$$\begin{aligned}
f_{Y_{k}}\left(y_{k}\right) &=\int_{a}^{y_{k}} \cdots \int_{a}^{y_{2}} \int_{y_{k}}^{b} \cdots \int_{y_{n-1}}^{b} n ! f_{X}\left(y_{1}\right) \cdots f_{X}\left(y_{n}\right) d y_{n} \cdots d y_{k+1} d y_{1} \cdots d y_{k-1} \\
&=\frac{n !}{(k-1) !(n-k) !} f_{X}\left(y_{k}\right) F_{X}\left(y_{k}\right)^{k-1}\left[1-F_{X}\left(y_{k}\right)\right]^{n-k}, a<y_{k}<b
\end{aligned}$$

> Note : Smallest order statistics

- In particular, the marginal pdf of the smallest order statistic is given by

$$f_{Y_{1}}\left(y_{1}\right)=n\left[1-F_{X}\left(y_{1}\right)\right]^{n-1} f_{X}\left(y_{1}\right) \Leftarrow P\left(Y_{1}>y_{1}\right)$$

> Note : largest order statistics

- and the marginal pdf of the largest order statistic is given by

$$f_{Y_{n}}\left(y_{n}\right)=n F_{X}\left(y_{n}\right)^{n-1} f_{X}\left(y_{n}\right) \Leftarrow P\left(Y_{n}<y_{n}\right)$$

> ## Joint pdf

- The joint pdf of any two order statistics, say $Y_{i}<Y_{j}$, can be also expressed in terms of $F_{X}(x)$ and $f_{X}(x)$, i.e.,

$$f_{Y_{i}, Y_{j}}\left(y_{i}, y_{j}\right)=\frac{n !}{(i-1) !(j-i-1) !(n-j) !} f_{X}\left(y_{i}\right) f_{X}\left(y_{j}\right) F_{X}\left(y_{i}\right)^{i-1}\left[F_{X}\left(y_{j}\right)-F_{X}\left(y_{i}\right)\right]^{j-i-1}\left[1-F_{X}\left(y_{j}\right)\right]^{n-j}$$

for $a<y_{i}<y_{j}<b$.

> ## Examples 

Let $Y_{1}, Y_{2}, Y_{3}$ be the order statistics of a random sample of size 3 from a distribution having pdf
$$
f_{X}(x)=1,0<x<1
$$
Find the pdf of $Z_{1}=Y_{3}-Y_{1}$

> Answer 

First we find the joint pdf of $Y_{1}$ and $Y_{3}$. Because $F(x)=x$, we have

$$f_{Y_{1}, Y_{3}}\left(y_{1}, y_{3}\right)=6\left(y_{3}-y_{1}\right), 0<y_{1}<y_{3}<1$$

To make variable transformation, we define the second random variable $Z_{2}=Y_{3}$. The inverse functions are $Y_{1}=Z_{2}-Z_{1}$ and $Y_{3}=Z_{2}$, and the Jacobian of the transformation is $-1 .$ The support of $\left(Z_{1}, Z_{2}\right)$ is $\left\{\left(z_{1}, z_{2}\right): 0<z_{1}<z_{2}<1\right\} .$ Thus, the joint pdf of $Z_{1}$ and $Z_{2}$ is

$$f_{Z_{1}, Z_{2}}\left(z_{1}, z_{2}\right)=6\left(z_{2}-\left(z_{2}-z_{1}\right)\right)|-1|=6 z_{1}, 0<z_{1}<z_{2}<1$$

so the marginal pdf of $Z_{1}$ is

$$\begin{aligned}
f_{Z_{1}}\left(z_{1}\right) &=\int_{z_{1}}^{1} f\left(z_{1}, z_{2}\right) d z_{2} \\
&=\int_{z_{1}}^{1} 6 z_{1} d z_{2} \\
&=6 z_{1}\left(1-z_{1}\right), 0<z_{1}<1
\end{aligned}$$

> Note

- 위처럼, Joint pdf 의 경우에도 order statsitics 를 구할 수 있습니다.

---

**Reference**

- Hoggs Introduction to Mathematical Statistics 7ed



