---
title:  "Distribution(~ing)"
excerpt: "다양한 분포들"
categories:
  - Stat
tags:
  - 1
last_modified_at: 2021-03-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true

---

# Geometric Distribution

$$\begin{gathered} X \sim Geometric(p) \cr f_X(x) = (1-p)^{x-1}p,\space x=1,2,\cdots \end{gathered}$$

- X 는 성공을 얻기위해 걸린 시행 횟수
- p : 성공 확률





## Memoryless property

$ P(X=x+k \vert X>k) = P(X=x) $  의 성질을 가질 때에 무기억성을 가진다고 한다. 즉, 이전에 k 번 기다린것은, 확률에 아무런 영향을 끼치지 않는다는것입니다.

$\begin{aligned} P(X=x+k) &= (1-p)^{x+k-1}p \cr P(X>k) &= \sum_{x=k+1}^\infty (1-p)^{x-1}p \cr &= \frac{p}{1-p} \sum_{x=k+1}^\infty (1-p)^x \cr &= (1-p)^{k} \cr P(X=x+k \vert X>k) &= \frac{P(X=x+k)}{P(X>k)} \cr &= \frac{(1-p)^{x+k-1}p}{(1-p)^{k}} \cr &= (1-p)^{x-1}p\cr &= P(X=x), \space x=1,2,\cdots \end{aligned}$



# Negative Binomial

$\begin{gathered}X \sim NB(r,p) \\ f_X(x) = \binom{x-1}{r-1}p^r (1-p)^{x-r},\space x=r, r+1, \cdots\end{gathered}$

- $X$ : r 번째 성공을 얻을때까지 걸리는 시행횟수

$X_1, \cdots, X_r \overset{iid}{\sim} GEO(p) \implies X=X_1+\cdots+X_r \sim NB(r,p)$



# <center><font size="20"> Binomial and poisson </font></center>

Binomial 분포와 포아송 분포의 분포의 근사에 대해서 알아보자.

$Claim : \ \ \begin{aligned} &n \to \infty , p\to 0, \lambda = np \text{ 에 따라서}\\&\text{Bin}(k ;N, \mu) = \binom{N}{k} \mu^k (1-\mu)^{N-k} \to \text{Poi}(k ; \lambda) = \frac{\lambda^k e^{-\lambda}}{k!}\end{aligned}$

$P(X=x)$

 $=\binom{n}{k}p^x (1-p)^{n-x} \\  =  \dfrac{n!}{(n-x)!\ x!} \left(\dfrac{\lambda}{n}\right)^x \left(1-\dfrac{\lambda}{n}\right)^{n-x}  \\ $

$ =  \dfrac{n(n-1)(n-2)\cdots(n-x+1)}{x!} \dfrac{\lambda^x}{n^x} \left(1-\dfrac{\lambda}{n}\right)^{n-x}   \\ $

$ =  \dfrac{n(n-1)(n-2)\cdots(n-x+1)}{n^x} \dfrac{\lambda^x}{x!} \left(1-\dfrac{\lambda}{n}\right)^{n-x}$



$lemma1 \ \ : \dfrac{n(n-1)(n-2)\cdots(n-x+1)}{n^x} \approx 1$

$lemma 2  :\left(1-\dfrac{\lambda}{n}\right)^{n-x} = \left(1-\dfrac{\lambda}{n}\right)^n \left(1-\dfrac{\lambda}{n}\right)^{-x}  \approx e^{-\lambda}$

$\text{by lem1,2 }\ \ P(X=x) =\binom{n}{k}p^x (1-p)^{n-x} \approx   \dfrac{\lambda^x e^{-\lambda}}{x!}$



# <center><font size="20">NB and poisson </font></center>

Binomial 분포와 포아송 분포의 분포의 근사에 대해서 알아보자.

$ Claim : \ \ \begin{aligned} &r\to \infty , \frac{pr}{1-p}=\lambda \text{ 에 따라서}\\&\text{NB}(x ;r,p) = \binom{r-1+x}{x} (1-p)^x p^r \to \text{Poi}(x ; \lambda) = \frac{\lambda^k e^{-\lambda}}{x!}\end{aligned} $

$Proof \ \ : \ p=\frac{\lambda}{r+\lambda}$  임은 쉽게 알 수 있다. 즉 이를 이용하자. 

$P(X=x) = \binom{r-1+x}{x}(1-\frac{\lambda}{r+\lambda})^r(\frac{\lambda}{r+\lambda})^x$ 

$=\frac{(r-1+x)!}{x!(r-1)!} (\frac{r}{r+\lambda})^r (\frac{\lambda}{r+\lambda})^x$ 

$= \frac{\lambda^x}{x!} \frac{(r-1+x)!}{(r-1)!} (\frac{r}{r+\lambda})^r (\frac{1}{r+\lambda})^x$ 

$= \frac{\lambda^x}{x!} (\frac{r}{r+\lambda})^r \ \ \text{since r -> inf}$

$=\frac{\lambda^k e^{-\lambda}}{x!}$



## NB and poisson in Bayes

베이즈에서 Poisson 과 NB 로 발생확률을 모델링할 수 있음을 기억하는가? 이때에  같은 mean 에 대해서 분산을 NB 와 Poisson 에 대해서 비교해보자. 

$X\sim NB(x;r,p)$ 이라 하면 $E[X] = \frac{pr}{1-p}=\lambda $  ,  $Var(X) = \frac{pr}{(1-p)^2} = \lambda (\frac{\lambda}{r}+1)$ 

$X\sim Poisson(\lambda)$ 이라 하면 $E[X] =\lambda $  , $Var(X) = $ $\lambda$

즉 NB 의 경우, Variance 를 r 이라는 파라미터를 이용하여 조절할 수 있다.

