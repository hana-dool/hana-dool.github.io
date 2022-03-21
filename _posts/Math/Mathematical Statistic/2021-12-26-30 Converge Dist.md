---
title:  "Converge in Distribution"
excerpt: "확률수렴"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-12-23

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 확률수렴과 그 밖의 성질들!
{: .notice--warning}

# [Converge in Distribution](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

- 앞 절에서 확률수렴의 개념을 소개했었습니다. 이러한 확률 수렴은 어디에 이용할 수 있을까요?
- 이 개념을 이용하여 한 통계량이 모수에 수렴 한다는 사실을 이용해서 ,Exact 한 분포를 굳이 알지 않고 Limiting Dsitribution 을 알 수 있습니다. 
- 그런데 통계량이 '얼마나' 모수에 가까울까? 와 같은 의문이 생길수도 있습니다. 다음의 절들에서는 이러한 의문에 대한 답을 알아보도록 하겠습니다.

> ## Converge in Distribution

> Defintiion

- $\left\{X_{n}\right\}$ 이 확률변수의 열이고 $X$ 가 확률변수라고 하자. $X_{n}$ 과 $X$ 의 $\operatorname{cdf}$ 를 각각 $F_{X_{n}}, F_{X}$ 라고 합시다. $F_{X}$ 가 연속인 모든 점의 집합이 $C\left(F_{X}\right)$ 일 때 다음과 같으면 $X_{n}$ 은 $X$ 에 분포수렴 (converge in distribution)한다고 합니다.

$$\text { 모든 } x \in C\left(F_{X}\right) \text { 에 대해 } \lim _{n \rightarrow \infty} F_{X_{n}}(x)=F_{X}(x)$$

- 이 수렴을 다음과 같이 나타낸다.

$$X_{n} \stackrel{D}{\rightarrow} X$$

> Note

- 확률수렴과 분포수렴은 통계학자와 확률론자가 점근 이론(asymptotic theory)이라고 하는 것 에서 유래했다. 종종 $X$ 의 분포를 열 $\left\{X_{n}\right\}$ 의 점근분포(asymptotic distribution) 또는 극한분포 (limiting distribution)라고 한다. 
- 이러한 "Converge in Distribution" 를 이용하여 특정한 R.V. 가 분포로 접근하는것을 보이기도 합니다. 예를들어 $X$ 가 표준정규분포를 따르면 $X_{n} \stackrel{D}{\rightarrow} X$ 대신 간단한 방법으로 다음과 같이 나타낼 수 있습니다.

$$X_{n} \stackrel{D}{\rightarrow} N(0,1)$$

- 분명히 위 식의 오른쪽은 분포이고 확률변수가 아니지만 관습적으로 이렇게 표현합니다.
- 또한 $X$ 가 표준정규확률변수일 때 $X_{n} \stackrel{D}{\rightarrow} X$ 는 $X_{n}$ 이 극한표준정규분포를 따른다는 것을 의미한다고 볼 수 있습니다.
  - 이를 간단하게 표현하면  $X_{n} \stackrel{D}{\rightarrow} N(0,1)$ 로 나타내기도 한다.


> Note : 왜 $F_X$ 에서 연속인 점만 고려하나요? 

- 연속인점만 고려하지 않게된다면 , $\lim _{n \rightarrow \infty} F_{n}(x)=F(x)$ true for every $x \in \mathbb{R}$ 가 되어야 합니다. 이렇게 고려하게 된다면 우리의 직관과 벗어나는 Converge 경우가 생기게 됩니다. 
  - $F_{X}$ 의 연속인 점만 고려하는 이유는 다음의 단순한 예에서 볼 수 있습니다.
- $X_{n}$ 이 $1 / n$ 에서 모든 질량값을 가지는 pmf 확률변수라고 합시다. 즉 1/n 에서 1의 값을 가집니다.
- $X$ 는 0 에서 모든 질량을 가진 확률변수라고 합시다. 즉 0 에서 1의 값을 가지게 됩니다.

![jpg](/assets/images/Stat/141_2.jpg)

- 그러면 위의 그림과 같이 $X_{n}$ 의 모든 질량(mass) 은 0, 즉 $X$ 의 분포로 수렴하게 됩니다.
  - $F_{X}$ 가 불연속인 점에서는 $\lim F_{X}(0)=0$ $\neq 1=F_{X}(0)$ 
  - $F_{X}$ 의 연속인 점 $x$ (즉 $x \neq 0$ )에서는 $\lim F_{X_{n}}(x)=F_{X}(x)$ 이다. 
- 따라서 정의에 의해 $X_{n} \stackrel{D}{\rightarrow} X$ 입니다.
- 하지만 이것을 오로지 Continuous Point 일때로 국한하면 어떻게될까요? 
  - 그러면 $X_{n} \not\stackrel{D}{\rightarrow} X$ 일 것입니다.

>  CDF

- 분포수렴은 $\operatorname{cdf} F_{X_{n}}$ 과 $F_{X}$ 에만 관심을 가진다는 사실에 주목합시다.	
  - 간단한 예를 통해 이것을 알아볼 수 있습니다.
-  $X$ 가 0 에 대칭인 $\operatorname{pdf} f_{X}(x)$, 즉 $f_{X}(-x)=f_{X}(x)$ 인 연속형 확률변수라고 합시다.
- 그러면 확률 변수 $-X$ 의 밀도함수도 역시 $f_{X}(x)$ 임을 쉽게 밝힐 수 있다.
  - $F_{-X}(x) = f(-X \le x) =F_X(-x)$  
- 따라서 $X$ 와 $-X$ 는 동일한 분포를 따르게 됩니다. 
- 이떄 확률변수 열 $X_{n}$ 을 다음과 같이 정의합시다.

$$
X_{n}= \begin{cases}X & n \text { 이 홀수이면 } \\ -X & n \text { 이 짝수이면 }\end{cases}
$$

- 이제 위의 경우에 대해서, $f_{X}(x)=f_{-X}(x)$ 입니다. 즉 $X$ 의 Support 에 있는 모든 $x$ 에 대해 $F_{X_{n}}(x)=F_{X}(x)$ 입니다.
  -  따라서 $X_{n} \stackrel{D}{\rightarrow} X$ 이다. 
- 반대로 Sequence $X_{n}$ 자체는 절대로 X 에 접근하지 않죠. (부호가 바뀌어갈 뿐이니까요.)

> ## Example

- $\bar{X}_{n}$ 의 $\mathrm{cdf}$ 가 다음과 같다고 합시다.

$$
F_{n}(\bar{x})=\int_{-\infty}^{\bar{x}} \frac{1}{\sqrt{1 / n} \sqrt{2 \pi}} e^{-n w^{2} / 2} d w
$$
- 변수변환 $v=\sqrt{n} w$ 를 하면 다음을 얻을 수 있으며,

$$
F_{n}(\bar{x})=\int_{-\infty}^{\sqrt{n} \bar{x}} \frac{1}{\sqrt{2 \pi}} e^{-v^{2} / 2} d v
$$

- 이는 다음과 같습니다.

$$
\lim _{n \rightarrow \infty} F_{n}(\bar{x})=\left\{\begin{array}{cc}
0 & \bar{x}<0 \\
\frac{1}{2} & \bar{x}=0 \\
1 & \bar{x}>0
\end{array}\right.
$$
- 이제 새로운 CDF 함수 $F$ 를 생각해봅시다. 
- 아래의 함수는 $\operatorname{cdf}$ 이고, $F(\bar{x})$ 의 모든 연속인 점에시서 $\lim _{n \rightarrow \infty} F_{n}(\bar{x})=F(\bar{x})$ 입니다.

$$
F(\bar{x})= \begin{cases}0 & \bar{x}<0 \\ 1 & \bar{x} \geq 0\end{cases}
$$
- 이때 확실하게 $\lim _{n \rightarrow \infty} F_{n}(0) \neq F(0)$ 입니다.
- 하지만 $F(\bar{x})$ 는 $\bar{x}=0$ 에서 연속이 아닙니다
- 따라서 Sequence $\bar{X}_{1}$, $\bar{X}_{2}, \bar{X}_{3}, \cdots$ 은 $\bar{x}=0$ 에서 degenerate distribution 를 따르는 확률변수로 분포수렴 하게 됩니다.
  - 이때 degenerate distribution 을 따르게 됩니다.

> ## Example : 극한분포는 pmf 나 pdf 로 결정될 수 없다.

- Seq $X_{1}, X_{2}, X_{3}, \cdots$ 이 확률변수 $X$ 로 분포수렴한다고 합시다.
  - 하지만 이때 $X_{n}$ 의 pmf의 극한을 이용하여 $X$ 의 분포를 일반적으로 결정할 수는 없습니다. 

-  아래의 Example 을 살펴봅시다.  $X_{n}$ 이 다음과 같은 pmf를 갖는다고 합시다.

$$
p_{n}(x)= \begin{cases}1 & x=2+n^{-1} \\ 0 & \text { 그 외에 }\end{cases}
$$
- 모든 $x$ 에 대해 $\lim _{n \rightarrow \infty} p_{n}(x)=0$ 이다. 이는 $n=1,2,3, \cdots$ 에 대해 $X_{n}$ 이 분포수렴하지 않음을 암시한다. 그런데 $X_{n}$ 의 $\operatorname{cdf}$ 는

$$
F_{n}(x)= \begin{cases}0 & x<2+n^{-1} \\ 1 & x \geq 2+n^{-1}\end{cases}
$$
- 그리고

$$
\lim _{n \rightarrow \infty} F_{n}(x)= \begin{cases}0 & x \leq 2 \\ 1 & x>2\end{cases}
$$
- $\operatorname{cdf}$ 가 다음과 같고 $F(x)$ 의 모든 연속인 점에서 $\lim _{n \rightarrow \infty} F_{n}(x)=F(x)$ 이므로

$$
F(x)= \begin{cases}0 & x<2 \\ 1 & x \geq 2\end{cases}
$$
- 열 $X_{1}, X_{2}, X_{3}, \cdots$ 은 $\operatorname{cdf} F(x)$ 를 가진 확률변수로 분포수렴 하게 됩니다.
- 즉 위의 예제를 살펴보면, 극한분포는 pmf 또는 pdf 에 의하여 결정될 수 없다는 사실을 알려줍니다. 
  - 하지만 다음 예제에서 우리는 특정한 조건에서만큼은 pdf 열을 관찰함으로서 확률 수렴을 결정할 수 있다는것을 보일것입니다. 

> ## Example : T $\to$ N 

- $T_{n}$ 이 자유도 $n(n=1,2,3, \cdots)$ 인 $t$-분포를 따른다고 하자. 
- 따라서 $T_{n}$ 의 cdf는피 적분함수가 $T_{n}$ 의 $\operatorname{pdf} f_{n}(y)$ 일 때 다음과 같다.

$$
F_{n}(t)=\int_{-\infty}^{t} \frac{\Gamma[(n+1) / 2]}{\sqrt{\pi n} \Gamma(n / 2)} \frac{1}{\left(1+y^{2} / n\right)^{(n+1) / 2}} d y
$$
- 따라서

$$
\begin{aligned}
\lim _{n \rightarrow \infty} F_{n}(t) &=\lim _{n \rightarrow \infty} \int_{-\infty}^{t} f_{n}(y) d y \\
&=\int_{-\infty}^{t} \lim _{n \rightarrow \infty} f_{n}(y) d y
\end{aligned}
$$

- 해석학의 결과[르베그 지배 수렴 정리(Lebesgue dominated convergence theorem)]에 의해 $\left|f_{n}(y)\right|$ 가 적분 가능한 함수에 의해 조절된다면 극한과 적분의 순서를 바꿀 수 있다.

$$
\left|f_{n}(y)\right| \leq 10 f_{1}(y)
$$

- 그러므로 이것이 성립하며 모든 실수 $t$ 에 대해

$$
\int_{-\infty}^{t} 10 f_{1}(y) d y=\frac{10}{\pi} \arctan t<\infty
$$
- 따라서 $T_{n}$ 의 $\mathrm{pdf}$ 의 극한을 구함으로써 극한분포를 찾을 수 있다. 즉

$$
\begin{aligned}
\lim _{n \rightarrow \infty} f_{n}(y)=& \lim _{n \rightarrow \infty}\left\{\frac{\Gamma[(n+1) / 2]}{\sqrt{n / 2} \Gamma(n / 2)}\right\} \lim _{n \rightarrow \infty}\left\{\frac{1}{\left(1+y^{2} / n\right)^{1 / 2}}\right\} \\
& \times \lim _{n \rightarrow \infty}\left\{\frac{1}{\sqrt{2 \pi}}\left[\left(1+\frac{y^{2}}{n}\right)\right]^{-n / 2}\right\}
\end{aligned}
$$
- 기초 미적분학의 이론에 의해 다음과 같으므로

$$
\lim _{n \rightarrow \infty}\left(1+\frac{y^{2}}{n}\right)^{n}=e^{y^{2}}
$$
- 세 번째 요소에 있는 극한은 표준정규분포의 pdf이다. 두 번째 극한은 1 이고, 스털링 공식에 의해 첫 번째 극한도 1 이다. 그러므로 다음을 얻게 되며

$$
\lim _{n \rightarrow \infty} F_{n}(t)=\int_{-\infty}^{t} \frac{1}{\sqrt{2 \pi}} e^{-y^{2} / 2} d y
$$

- 따라서 $T_{n}$ 은 극한표준정규분포를 갖는다.

> ## Them : Sterling 공식

- 고급 미적분학에서는 다음 근삿값을 도출한다.
  $$
  \Gamma(k+1) \approx \sqrt{2 \pi} k^{k+1 / 2} e^{-k}
  $$

- 이것은 스털링 공식(Stirling's formula)으로 알려졌으머, $k$ 가 클 경우 훌룽한 근삿값이다.
-  $k$ 가 정수일 때 $\Gamma(k+1)=k !$ 이므로 이 공식은 $k !$ 이 얼마나 빠르게 증가하는지를 알려줍니다.

> ## Example

- $X_{1}, X_{2}, \cdots, X_{n}$  은 균등분포 $(0, \theta)$ 에서 추출한 확률표본이었다
-  $Y_{n}=\max \left\{X_{1}, X_{2}, \cdots, X_{n}\right\}$ 이라 하고 확률변수 $Z_{n}=n(\theta-$ $\left.Y_{n}\right)$ 에 대해 생각해보자. 
- $t \in(0, n \theta)$ 라 하고 식 $(5.1 .1)$ 에 있는 $Y_{n}$ 의 $c d f$ 를 이용하여 $Z_{n}$ 의 $c d f$ 를 구하면

$$
\begin{aligned}
P\left[Z_{n} \leq t\right] &=P\left[Y_{n} \geq \theta-(t / n)\right]=1-\left(\frac{\theta-(t / n)}{\theta}\right)^{n}=1-\left(1-\frac{t / \theta}{n}\right)^{n} \\
& \rightarrow 1-e^{-t / \theta}
\end{aligned}
$$
- 마지막 값은 평균 $\theta$ 인 지수확률변수의 cdf이다. 따라서 $Z_{n} \stackrel{D}{\rightarrow} Z$ 라고 할 수 있으며, 여기서 $Z$ 는 $\Gamma(1, \theta)$ 분포를 따른다.

> ## Lemma

- 이 절에 제시된 몇 가지 증명을 단순화하기 위해 열에 대해서 $\varliminf$  와 $\overline{\lim }$ 를 이용한다. 이러한 개념을 잘 알지 못하는 독자를 위해 부록 $\mathrm{A}$ 에 이에 대한 설명을 수록했다. 여기서는 증명을 이해하는 데 필요한 성질을 강조한다. $\left\{a_{n}\right\}$ 을 실수열이라 하고 2 개의 부분열을 정의한다.

$$
\begin{array}{ll}
b_{n}=\sup \left\{a_{n}, a_{n+1}, \ldots\right\}, & n=1,2,3 \ldots \\
c_{n}=\inf \left\{a_{n}, a_{n+1}, \ldots\right\}, & n=1,2,3 \ldots
\end{array}
$$
- $\left\{b_{n}\right\}$  $\left\{c_{n}\right\}$ 응 각각 Nonincreasing / Nondescreasing 임은 명확합니다. 따라서 이 극한은 ( $\pm \infty$ 일 수도 있지만) 항상 존재하고, 이것을 각각 $\varlimsup_{n \rightarrow \infty} a_{n}, \varliminf_{n \rightarrow \infty} a_{n}$ 으로 나타낸다. 
- 또한 모든 $n$ 에 대해 $c_{n} \leq a_{n} \leq$ $b_{n}$ 이다. 따라서 샌드위치 정리(Sandwich theorem, 부록 $\mathrm{A}$ 의 정리 $\mathrm{A} .2 .1$ 참조)에 의해 $\lim _{n \rightarrow \infty}$ $a_{n}=\varlimsup_{n \rightarrow \infty} a_{n}$ 이면 $\lim _{n \rightarrow \infty} a_{n}$ 이 존재하며 $\lim _{n \rightarrow \infty} a_{n}=\varlimsup_{n \rightarrow \infty} a_{n}$ 으로 주어진다. 
- 부록 $\mathrm{A}$ 에서 설명하듯이 이러한 개념의 몇 가지 다른 성질은 유용하다. 예를 들어 $\left\{p_{n}\right\}$ 이 확 률의 열이며 $\lim _{n \rightarrow \infty} p_{n}=0$ 이라고 하자. 그러면 모든 $n$ 에 대해 $0 \leq p_{n} \leq \sup \left\{p_{n}, p_{n+1}, \cdots\right\}$ 이므로 샌드위치 정리에 의해 $\lim _{n \rightarrow \infty} p_{n}=0$ 이다.
-  또한 임의의 두 열 $\left\{a_{n}\right\}$ 과 $\left\{b_{n}\right\}$ 에 대해 $\lim$ $\left(n+b_{n}\right)<\overline{\lim }_{n \rightarrow \infty} a_{n}+\varlimsup_{n \rightarrow \infty} b_{n}$ 을 십게 유도할 수 있다.

> ## Theorem 

> Theorem

$X_{n}\to X$ Converge in Probability 이면 $X_{n}\to X$  Converge in Distribution

> Proof

 $x$ 가 $F_{X}(x)$ 의 연속인 점이라고 하자. 모든 $\epsilon>0$ 에 대해
$$
\begin{aligned}
F_{X_{n}}(x) &=P\left[X_{n} \leq x\right] \\
&=P\left[\left\{X_{n} \leq x\right\} \cap\left\{\left|X_{n}-X\right|<\epsilon\right\}\right]+P\left[\left\{X_{n} \leq x\right\} \cap\left\{\left|X_{n}-X\right| \geq \epsilon\right\}\right] \\
& \leq P[X \leq x+\epsilon]+P\left[\left|X_{n}-X\right| \geq \epsilon\right]
\end{aligned}
$$
- 이 부등식과 $X_{n} \stackrel{P}{\rightarrow} X$ 에 의해 다음과 같다.

$$
\varlimsup_{n \rightarrow \infty} F_{X_{n}}(x) \leq F_{X}(x+\epsilon)
$$
- 하한을 구하기 위해 단순히 여집합에 대해 같은 방법으로 다음을 밝힌다.

$$
P\left[X_{n}>x\right] \leq P[X \geq x-\epsilon]+P\left[\left|X_{n}-X\right| \geq \epsilon\right]
$$
- 따라서 

$$
\varliminf_{n \rightarrow \infty} F_{X_{n}}(x) \geq F_{X}(x-\epsilon)
$$
- $\varlimsup$ 와 $\varliminf$ 의 관계를 이용하면 

$$
F_{X}(x-\epsilon) \leq \varliminf_{n \rightarrow \infty} F_{X_{n}}(x) \leq \varlimsup_{n \rightarrow \infty} F_{X_{n}}(x) \leq F_{X}(x+\epsilon)
$$
- $\epsilon \downarrow 0$ 으로 하면 $F_{X_n}$에 대해서, Sup 와 Inf 가 같으므로 수렴하게 되고, 즉, $F_{X_n}$  이 존재한다는 결론을 얻게됩니다. 또한

$$F_{X}(x-\epsilon) \leq \lim _{n \rightarrow \infty} F_{X_{n}}(x) \leq F_{X}(x+\epsilon)$$

- 위와 같은 관계가 성립하므로, Converge in Distribution 이라 할 수 있습니다.

> ## Note

- 이전의 예시를 보면 확률변수 열 $\left\{X_{n}\right\}$ 을 다시 생각해보자. 여기서 $X_{n} \stackrel{D}{\rightarrow} X$ 이지만 $X_{n} \stackrel{P}{\not\rightarrow} X$ 입니다.
- 따라서 일반적으로 위 정리의 역은 성립하지 않는다. 그러나 다음 정리에서와 같이 $X$ 가 퇴화 분포이면 성립한다.	

>  $X_{n}$ 이 상수 $b$ 로 분포수렴하면 $X_{n}$ 은 $b$ 로 확률수렴한다.

- 증명: $\epsilon>0$ 이라면 수렴되는 $X=b$ 이므로 다음과 같은 식이 성립합니다.
- $\lim P\left[\left|X_{n}-b\right| \leq \epsilon\right]=\lim _{n \rightarrow \infty} F_{X_{n}}(b+\epsilon)-\lim _{n \rightarrow \infty} F_{X_{n}}[(b-\epsilon)-0]=1-0=1$

> ## Proprties

> $X_{n}$ 이 $X$ 에 분포수렴하고 $g$ 가 $X$ 의 Support 에서 연속인 함수라면 $g\left(X_{n}\right)$ 은 $g(X)$ 에 분포수렴한다.

- 이 정리는 표준정규확률변수 $Z$ 로 분포수렴하는 확률변수 $Z_{n}$ 의 열에 대해 자주 응용된다. $Z^{2}$ 의 분포는 $\chi^{2}(1)$ 이므로 정리 $5.2 .4$ 에 의해 $Z_{n}^{2}$ 은 $\chi^{2}(1)$ 분포에 분포수렴한다.

>  정리 $5.2 .5$ [슬러츠키 정리]
>  $X_{n}, X, A_{n}, B_{n}$ 이 확률변수이고 $a$ 와 $b$ 가 상수라고 하자. $X_{n} \stackrel{D}{\rightarrow} X, A_{n} \stackrel{P}{\rightarrow} a, B_{n} \stackrel{P}{\rightarrow} b$ 이면
>  $A_{n}+B_{n} X_{n} \stackrel{D}{\rightarrow} a+b X$

# [Boundness in Probability](#link){: .btn .btn--primary}{: .align-center}

> ## Boundness in Probability

- 분포수렴과 관련된 또 다른 유용한 개념은 확률변수 열의 확률유계성(boundedness in probability)이다.

- 우선 $\operatorname{cdf} F_{X}(x)$ 를 가진 어떤 확률변수 $X$ 가 있다면 $\epsilon>0$ 이 주어졌을 때 다음과 같은 방범으 로 $X$ 의 한계를 정할 수 있다.
-  $F_{X}$ 의 하한이 0 이고 상한이 1 이므로 다음을 만족하는 $\eta$ 과 $\eta_{2}$ 를 구 할 수 있다.

$$\begin{aligned}
&x \leq \eta_{1} \text { 에 대해 } F_{X}(x)<\epsilon / 2 \\
&x \geq \eta_{2} \text { 에 대해 } F_{X}(x)>1-(\epsilon / 2)
\end{aligned}$$

- $\eta=\max \left\{\left|\eta_{1}\right|,\left|\eta_{2}\right|\right\}$  라고 하면

$$P[|X| \leq \eta]=F_{X}(\eta)-F_{X}(-\eta-0) \geq 1-(\epsilon / 2)-(\epsilon / 2)=1-\epsilon$$

- 따라서 한계가 없는 확률변수[예: $X$ 가 $N(0,1)]$ 도 이러한 확률 방식으로 한계가 주어지게 됩니다.
  - 이것은 다음에 정의하는 확률변수 열에 대해 유용한 개념입니다.

> ## Definition

- The sequence of random variables $\left\{X_{n}\right\}$ is said to be bounded in probability, written as $X_{n}=O_{p}(1)$, 
- 모든 $\epsilon>0$ 에 대해 아래 식을 만족하는 $\eta>0$ and an integer $N$ 가 존재할때 Bounded in Probability 라고 합니다.

$$\begin{aligned}
n \geq N & \Rightarrow P\left(\left|X_{n}\right| \leq \eta\right) \geq 1-\epsilon \\
& \Rightarrow P\left(\left|X_{n}\right|>\eta\right) \leq \epsilon
\end{aligned}$$

> Example

![jpg](/assets/images/Stat/150_1.jpg)

- 위처럼 $\{X_n\}$ 이 Normal 로 수렴한다고 합시다. 그러면 $\eta$ 를 크게 할수록 양 끝의 Probability 는 매우 작아질 수 있으므로 Bounded in Probability 라고 할 수 있습니다.

> ## Theorem : 분포수렴 $\to$ 확률유계

- cdf $F$ 를 가진 확률변수 $X$ 로 분포수렴하는 확률변수 Seq $\left\{X_{n}\right\}$ 을 고려하자.
-  $\epsilon>0$ 일 때 $X$ 에 대해 식 $(5.2 .7)$ 이 성립하는 $\eta$ 를 선택하자. $\eta$ 와 $-\eta$ 가 $F$ 의 연속인 점이 되도록 항상 $\eta$ 를 선택할 수 있다. 그러면 다음을 얻는다.

$$\begin{aligned}
\lim _{n \rightarrow \infty} P\left[\left|X_{n}\right|\right.&\leq \eta] \geq \lim _{n \rightarrow \infty} F_{X_{n}}(\eta)-\lim _{n \rightarrow \infty} F_{X_{n}}(-\eta-0) \\
&=F_{X}(\eta)-F_{X}(-\eta) \geq 1-\epsilon
\end{aligned}$$

- 정확하게 하기 위해 $n \geq N$ 에 대해 $P\left[\left|X_{n}\right| \leq \eta\right] \geq 1-\epsilon$ 이 성립하도록 충분히 큰 $N$ 을 선택할 수 있다. 
- 즉 분포수렴 $\to$ 확률 유계 입니다.

> ## Example : 확률유계 $\not \to$  분포 수렴

- $\left\{X_{n}\right\}$ 이 다음과 같은 퇴화확률변수 열이라고 하자. 
  - 짝수 $n=2 m$ 에 대해 $X_{2 m}=2$ $+(1 /(2 m))$ 일 확률이 1 이고, 
  - 홀수 $n=2 m-1$ 에 대해 $X_{2 m-1}=1+(1 /(2 m))$ 일 확률이 1 이다. 
- 그러면 열 $\left\{X_{2}, X_{4}, X_{6}, \cdots\right\}$ 은 퇴화확률변수 $Y=2$ 에 분포수렴하고, 열 $\left\{X_{1}, X_{3}, X_{5}, \cdots\right\}$ 는 퇴화확률변수 $W=1$ 에 분포수렴한다.
-  $Y$ 와 $W$ 의 분포가 동일하지 않으므로 열 $\left\{X_{n}\right\}$ 은 분포 수렴하지 않는다. 
- 그러나 열 $\left\{X_{n}\right\}$ 의 모든 값이 구간 $[1,5 / 2]$ 안에 있으므로 열 $\left\{X_{n}\right\}$ 은 확률유계이다.

> ## Intuition

- 확률유계인 열(또는 확률변수로 분포수렴하는 것)을 생각하는 한 가지 방법은 $\left|X_{n}\right|$ 의 확률질량이 $\infty$ 로 벗어나지 않는다는 것이다. 
  - 종종 분포수렴 대신 확률유계성을 이용할 수 있다. 다음 정리는 앞으로 필요하게 될 성질이다.

> ## Theorem

> Theorem

$\left\{X_{n}\right\}$ 이 획률유계인 확률변수 열이고 $\left\{Y_{n}\right\}$ 이 0으로 확률수렴하는 확률변수 열이라면

$$X_{n} Y_{n} \stackrel{P}{\rightarrow} 0$$

> Proof

- $\epsilon>0$ 이라고 하자. 다음이 성립하도록 $B_{\epsilon}>0$ 과 정수 $N_{\epsilon}$ 을 선택한다.

$$n \geq N_{\epsilon} \Rightarrow P\left[\left|X_{n}\right| \leq B_{\epsilon}\right] \geq 1-\epsilon$$

- 그러면 다음과 같으며, 이것으로부터 원하는 결과가 도출된다.

$$\begin{aligned}
\varlimsup_{n \rightarrow \infty} P\left[\left|X_{n} Y_{n}\right| \geq \epsilon\right] \leq & \varlimsup_{n \rightarrow \infty} P\left[\left|X_{n} Y_{n}\right| \geq \epsilon,\left|X_{n}\right| \leq B_{\epsilon}\right] \\
&+\varlimsup_{n \rightarrow \infty} P\left[\left|X_{n} Y_{n}\right| \geq \epsilon,\left|X_{n}\right|>B_{\epsilon}\right] \\
\leq & \varlimsup_{n \rightarrow \infty} P\left[\left|Y_{n}\right| \geq \epsilon / B_{\epsilon}\right]+\epsilon=\epsilon
\end{aligned}$$

> ## Delta Method

- 이를 확립하기 위해 영의 정리(Young's theorem)라고도 하는, 나머지가 있는 평균값 정리의 편리한 형식이 필요하다. 
- Hardy(1992) 또는 $\operatorname{Lehmann}(1999)$ 을 참조하라. $g(x)$ 가 $x$ 에서 미분 가능하면 다음과 같이 나타낼 수 있다.

$$
g(y)=g(x)+g^{\prime}(x)(y-x)+o(|y-x|)
$$

- 여기서 기호 $o$ 는 다음을 의미한다.

$$b \rightarrow 0 \text { 일 때 } \frac{a}{b} \rightarrow 0 \text { 인 경우에 한하여 } a=o(b)$$

- 작은 $o($ little $o)$ 는 확률수렴의 개념으로도 이용된다. 종종 $o_{p}\left(X_{n}\right)$ 은 다음과 같은 의미로 쓰인다.

$$n \rightarrow \infty \text { 일 때 } \frac{Y_{n}}{X_{n}} \stackrel{P}{\rightarrow} 0 \text { 인 경우에 한하여 } Y_{n}=o_{p}\left(X_{n}\right)$$

- 큰 $O_{p}\left(\operatorname{big} O_{p}\right)$ 는 다음을 의미한다. 
  - $$ n \rightarrow \infty \text { 일 때 } \frac{Y_{n}}{X_{n}} \text { 이 확률유계인 경우에 한하여 } Y_{n}=O_{p}\left(X_{n}\right) $$ 

> ## Theorem

$\left\{Y_{n}\right\}$ 이 확률유계인 확률변수 열이라고 하자. $X_{n}=o_{p}\left(Y_{n}\right)$ 이면 $n \rightarrow \infty$ 일 때 $X_{n} \stackrel{P}{\rightarrow} 0$ 이다. 

> proof

증명: $\epsilon>0$ 이라고 하자. 열 $\left\{Y_{n}\right\}$ 이 확률유계이므로 다음과 같은 양의 상수 $N_{c}$ 과 $B_{\epsilon}$ 이 존재한다.
$$
n \geq N_{\epsilon} \Longrightarrow P\left[\left|Y_{n}\right| \leq B_{\epsilon}\right] \geq 1-\epsilon
$$
또한 $X_{n}=o_{p}\left(Y_{n}\right)$ 이므로 $n \rightarrow \infty$ 일 때 다음을 얻는다.
$$
\frac{X_{n}}{Y_{n}} \stackrel{P}{\rightarrow} 0
$$
그러면
$$
\begin{aligned}
P\left(\left|Y_{n}\right| \geq \epsilon\right) &=P\left(\left|Y_{n}\right| \geq \epsilon,\left|X_{n}\right| \leq B_{\epsilon}\right)+P\left(\left|Y_{n}\right| \geq \epsilon,\left|X_{n}\right|>B_{\epsilon}\right) \\
& \leq P\left(\left|Y_{n}\right| \geq \epsilon,\left|X_{n}\right| \leq B_{\epsilon}\right)+P\left(\left|X_{n}\right|>B_{\epsilon}\right) \\
& \leq P\left(\left|\frac{Y_{n}}{X_{n}}\right| \geq \frac{\epsilon}{B_{\epsilon}}\right)+P\left(\left|X_{n}\right|>B_{\epsilon}\right) \rightarrow 0,
\end{aligned}
$$
식 (5.2.13)과 (5.2.12)에 의해 오른쪽의 첫째와 둘째 항은 $n$ 을 충분히 크게 함으로써 얼마든지 작게 만들 수 있다. 따라서 이 결과는 성립한다.

> ## Delta Method

- 다음과 같은 확률변수 열을 $\left\{X_{n}\right\}$ 이라고 하자.
-  $$ \sqrt{n}\left(X_{n}-\theta\right) \stackrel{D}{\rightarrow} N\left(0, \sigma^{2}\right) $$ 함수 $g(x)$ 가 $\theta$ 에서 미분 가능하고 $g^{\prime}(\theta) \neq 0$ 라고 하면 

$$ \sqrt{n}\left(g\left(X_{n}\right)-g(\theta)\right) \stackrel{D}{\rightarrow} N\left(0, \sigma^{2}\left(g^{\prime}(\theta)\right)^{2}\right) $$ 

> Proof

-  Let $$\left\{X_{n}\right\}$$ be a sequence of random variables such that

$$\sqrt{n}\left(X_{n}-\theta\right) \stackrel{D}{\rightarrow} N\left(0, \sigma^{2}\right)$$

- Suppose the function $g(x)$ is differentiable at $\theta$ and $g^{\prime}(\theta) \neq 0$. Then

$$\sqrt{n}\left(g\left(X_{n}\right)-g(\theta)\right) \stackrel{D}{\rightarrow} N\left(0, \sigma^{2}\left\{g^{\prime}(\theta)\right\}^{2}\right) .$$

- Proof. Using the Taylor series expansion, we have

$$g\left(X_{n}\right)=g(\theta)+g^{\prime}(\theta)\left(X_{n}-\theta\right)+o_{p}\left(\left|X_{n}-\theta\right|\right)$$

- where $o_{p}(h) / h \stackrel{P}{\rightarrow} 0$ as $h \rightarrow 0$. Rearranging the expression, we have

$$\begin{aligned}
\sqrt{n}\left(g\left(X_{n}\right)-g(\theta)\right) &=g^{\prime}(\theta) \sqrt{n}\left(X_{n}-\theta\right)+o_{p}\left(\sqrt{n}\left|X_{n}-\theta\right|\right) \\
& \stackrel{P}{\rightarrow} g^{\prime}(\theta) \sqrt{n}\left(X_{n}-\theta\right) \\
& \stackrel{D}{\rightarrow} N\left(0, \sigma^{2}\left\{g^{\prime}(\theta)\right\}^{2}\right)
\end{aligned}$$

> ## Example 

- Example. Let $X_{1}, \ldots, X_{n}$ denote an iid random sample from a Bernoulli distribution with $p$. Find the limiting distribution of $W_{n}=e^{Y_{n}}$, where $Y_{n}=X_{1}+\cdots+X_{n}$.
- Because $Y_{n}$ is the sum of Bernoulli random variables, we have
$$
Y_{n} \sim B(n, p)
$$
By CLT, the limiting distribution of $Y_{n}$ is computed as
$$
\frac{Y_{n}-n p}{\sqrt{n p(1-p)}} \stackrel{D}{\rightarrow} N(0,1)
$$
By the delta method, we have
$$
\frac{W_{n}-e^{n p}}{\sqrt{n p(1-p) e^{2 n p}}} \stackrel{D}{\rightarrow} N(0,1)
$$

---

 **Reference**

- Hoggs Introduction to Mathematical Statistics 7ed



