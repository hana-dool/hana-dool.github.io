---
title:  "Hyper Geometric"
excerpt: ""
categories:
  - Mathematical_Distribution
last_modified_at: 2021-11-24

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true

---

 Binomial Distribution
{: .notice--warning}

# [Hyper Geometric](#link){: .btn .btn--primary}{: .align-center}

> ## Definition

> Definition

- 한 상자에 $N$ 개의 공이 들어있다. 이 중에 $K$ 개의 공은 빨간색, $N-K$ 개의 공은 파란색이라고 하자. 이때 $n$ 개의 공 을 꺼냈을 때, 빨간색 공이 몇 개들어 있는지에 대한 문제는 초기하 분포를 따른다.
- Binomial distribution는 $n$ 개의 공 을 꺼낼 때, 하나 꺼낼 때마다 확인하고 다시 집어 넣을 때의 분포가 되고, 초기하 분포는 한번에 $n$ 개의 공을 꺼냈을 때의 분포가 된다.

$$P(X=x)=\frac{\left(\begin{array}{l}
K \\
x
\end{array}\right)\left(\begin{array}{c}
N-K \\
n-x
\end{array}\right)}{\left(\begin{array}{l}
N \\
n
\end{array}\right)} \quad \text { where } x=0,1,2, \cdots, K$$

- 랜덤 변수 $X$ 가 N,K,n 의 초기하 분포를 따른다는 것을 줄여서 다음과 같이 표현합니다.

$$X \sim \text { Hypergeometric }(N, K, n)$$

# [Elementary Properties](#link){: .btn .btn--primary}{: .align-center}

> ## Tables

$$\begin{array}{|l|l|}
\hline \text { Parameters } & N \in\{0,1,2, \ldots\} \\
& K \in\{0,1,2, \ldots, N\} \\
& n \in\{0,1,2, \ldots, N\} \\
\hline \text { Support } & k \in\{\max (0, n+K-N), \ldots, \min (n, K)\} \\
\hline \text { PMF } & \frac{\left(\begin{array}{c}
K \\
k
\end{array}\right)\left(\begin{array}{c}
N-K \\
n-k
\end{array}\right)}{\left(\begin{array}{l}
N \\
n
\end{array}\right)} \\
\hline
\end{array}$$

> ## Proof : pdf

- 상자에서 n 개의 공을 꺼낼 모든 경우의 수는

$$\left(\begin{array}{l}
N \\
n
\end{array}\right)=\frac{N !}{n !(N-n+1) !}$$

- 꺼낸 $n$ 개의 공 중에서 $x$ 개의 공이 빨간색 공일 경우의 수는  $K$ 개의 빨간색 공 중에서 $x$ 개 꺼낼 경우의 수'와 ' $N-K$ 개의 파란색 공 중에서 $n-x$ 개 꺼낼 경우의 수'를 곱한 것이므로

$$\left(\begin{array}{l}
K \\
x
\end{array}\right)\left(\begin{array}{c}
N-K \\
n-x
\end{array}\right)$$

- 랜덤 변수 $X$ 를 꺼낸 공 중에서 빨간색 공의 수라고 정의하면, $x$ 개의 공이 빨간색 공일 확률은

$$P(X=x)=\frac{\left(\begin{array}{l}K \\ x\end{array}\right)\left(\begin{array}{c}N-K \\ n-x\end{array}\right)}{\left(\begin{array}{l}N \\ n\end{array}\right)} \quad$ where $x=0,1,2, \cdots, K$$

> ## Proof : Vendermonde's Identity

> Theorem 

$$\left(\begin{array}{c}
m+n \\
r
\end{array}\right)=\sum_{k=0}^{r}\left(\begin{array}{c}
m \\
k
\end{array}\right)\left(\begin{array}{c}
n \\
r-k
\end{array}\right)$$

> Proof

- Binomial theorem 로부터

$$\begin{aligned}
\sum_{r=0}^{m+n}\left(\begin{array}{c}
m+n \\
r
\end{array}\right) x^{r} &=(1+x)^{m+n} \\
&=(1+x)^{m}(1+x)^{n} \\
&=\left[\sum_{i=0}^{m}\left(\begin{array}{c}
m \\
i
\end{array}\right) x^{i}\right]\left[\sum_{j=0}^{n}\left(\begin{array}{c}
n \\
j
\end{array}\right) x^{j}\right]
\end{aligned}$$

- 이 때, 2 개의 다항식의 곱을 전개하면 다음과 같이 정리된다.

$$\left(\sum_{i=0}^{m} a_{i} x^{i}\right)\left(\sum_{j=0}^{n} b_{j} x^{j}\right)=\sum_{r=0}^{m+n}\left(\sum_{k=0}^{r} a_{k} b_{r-k}\right) x^{r}$$

이를 그대로 마지막 줄에 적용하면,

$$\sum_{r=0}^{m+n}\left(\begin{array}{c}
m+n \\
r
\end{array}\right) x^{r}=\sum_{r=0}^{m+n}\left[\sum_{k=0}^{r}\left(\begin{array}{c}
m \\
k
\end{array}\right)\left(\begin{array}{c}
n \\
r-k
\end{array}\right)\right] x^{r}$$

따라서 계수 비교법에 의해,

$$\left(\begin{array}{c}
m+n \\
r
\end{array}\right)=\sum_{k=0}^{r}\left(\begin{array}{c}
m \\
k
\end{array}\right)\left(\begin{array}{c}
n \\
r-k
\end{array}\right)$$



---

**reference**

- Hoggs Introduction to Mathematical Statistics 7ed
- <https://elementary-physics.tistory.com/139>







