---
title:  "Converge in Probability"
excerpt: "확률수렴"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-12-23

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
---

 확률수렴과 그 밖의 성질들!
{: .notice--warning}

# [Converge in Probability](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

- 앞에서 우리는 통계적 추론의 몇 가지 주요한 개념, 즉 점추정, 신뢰구간, 가설검정을 소개했었습니다. 
- 이러한 Statistical Inference 는 pivot 확률변수의 분포에 의존하는 경우가 많습니다. 
- 한 예시로, $X_{1}, X_{2}, \cdots, X_{n}$ 이 $X \sim N\left(\mu, \sigma^{2}\right)$ 을 따르는 분포의 Random Sample 이라고 합시다. 이때  표본평균을 $\bar{X}_{n}=n^{-1} \sum_{i=1}^{n} X_{i}$ 로 하면, 피벗 확률변수는 아래와 같습니다.

$$Z_{n}=\frac{\bar{X}_{n}-\mu}{\sigma / \sqrt{n}}$$

- 위의 확률변수는 $\mu$ 에 대한 신뢰구간과, $\mu$ 와 관련된 가설검정을 할때에 매우 중요한 역할을 하게 됩니다.
  - 하지만 만약 $X$ 가 정규분포를 따르지 않으면 어떻게 될까요? 이때에 (표본 크기 $n$ 이 커짐에 따른) $Z_{n}$ 의 근사적인 분포 (Central Limit Theorem) 에 근거해서 테스트를 할 수 있었습니다.
- 이전의 한 예시처럼, 통계에서는 주로 몇가지 수렴을 사용하게 됩니다. 여기에서는 확률수렴과 분포수렴에 대해서 알아보도록 하겠습니다. 
  - 이러한 근사는, 통계학에서 매우 중요한 역할을 하게 됩니다. 

> ## Converse in Probability 

> Definition

- $\left\{X_{n}\right\}$ 이 확률변수의 Sequanece 이고 $X$ 가 표본공간에서 정의된 확률변수라고합시다. 
- 이때 모든 $\epsilon>0$ 에 대해 다음과 같으면 $X_{n}$ 은 $X$ 에 확률수렴한다(converge in probability)고 합니다.

$$\lim _{n \rightarrow \infty} P\left[\left|X_{n}-X\right| \geq \epsilon\right]=0$$

- 또는 Equivalently

$$\lim _{n \rightarrow \infty} P\left[\left|X_{n}-X\right|<\epsilon\right]=1$$

- 그리고 이를 다음과 같이 나타내게 됩니다.

$$X_{n} \stackrel{P}{\rightarrow} X$$ 

> ## Theorem

- $\left\{X_{n}\right\}$ 을 공통 평균 $\mu$ 와 공통 분산 $\sigma^{2}<\infty$ 을 가진 $\mathrm{iid}$ 확률변수 Sequence라고 합시다.
-  $\bar{X}_{n}=n^{-1} \sum_{i=1}^{n}$ $X_{i}$ 으로 정의한다면 (즉 표본평균)

$$\bar{X}_{n} \stackrel{P}{\rightarrow} \mu$$

> Proof

- $\bar{X}_{n}$ 의 평균과 분산은 각각 $\mu, \sigma^{2} / n$ 임을 기억합시다.
- 따라서 쳬비셰프 부등식에 의해 임의의 $\epsilon>0$ 에 대해서 아래처럼 계산됩니다.

$$P\left[\left|\bar{X}_{n}-\mu\right| \geq \epsilon\right]=P\left[\left|\bar{X}_{n}-\mu\right| \geq(\epsilon \sqrt{n} / \sigma)(\sigma / \sqrt{n})\right] \leq \frac{\sigma^{2}}{n \epsilon^{2}} \rightarrow 0$$

> Note

- 위의 정리는 $n \rightarrow \infty$ 함에 따라 $\bar{X}_{n}$ 의 분포의 모든 값은 $\mu$ 로 수렴한다는 것을 의미합니다. 
- 따라서 $n$ 이 크면 $\bar{X}_{n}$ 은 $\mu$ 에 근접하게 됩니다.
- 좀 더 깊게 들어가면, strong law of large numbers를 쓰기도 합니다. (DIY)

> ## Note 

- 만약 $X_{n} \stackrel{P}{\rightarrow} X$ 이면, $X_{n}-X$ 는  0 으로 수렴하게 됩니다.
- 통계학에서는 종종 극한확률변수 $X$ 가 상수일때도 있습니다. 즉 $X_n$ 이 특정한 상수 a 로 수렴할때에도 있습니다.

> Note : Relation with Convergence

- 위와 같이 상수 $\alpha$ 로 수렴할때 $X_{n} \stackrel{P}{\rightarrow} a$ 로 나타냅니다
  - 이때 실수열이 수렴 하면( $a_{n} \rightarrow a$ ) 즉 $a_{n} \stackrel{P}{\rightarrow} a$ 로 확률수렴 하게 됩니다.
  - 이 증명은 뒤의 Remark 에서 하겠습니다. 

> ## Property 1

$X_{n} \stackrel{P}{\rightarrow} X$ 이고 $Y_{n} \stackrel{P}{\rightarrow} Y$ 이면 $X_{n}+Y_{n} \stackrel{P}{\rightarrow} X+Y$ 이다.

> Proof

- $\epsilon>0$ 일 때 삼각부등식을 이용하여

$$\left|X_{n}-X\right|+\left|Y_{n}-Y\right| \geq\left|\left(X_{n}+Y_{n}\right)-(X+Y)\right| \geq \epsilon$$

- $P$ 는 집합의 포함 관계에 대해 단조증가이므로 아래의 부등식이 성립합니다.

$$\begin{aligned}
P\left[\left|\left(X_{n}+Y_{n}\right)-(X+Y)\right| \geq \epsilon\right] & \leq P\left[\left|X_{n}-X\right|+\left|Y_{n}-Y\right| \geq \epsilon\right] \\
& \leq P\left[\left|X_{n}-X\right| \geq \epsilon / 2\right]+P\left[\left|Y_{n}-Y\right| \geq \epsilon / 2\right]
\end{aligned}$$

- 가정($X_{n} \stackrel{P}{\rightarrow} X$ 이고 $Y_{n} \stackrel{P}{\rightarrow} Y$) 에 의해 마지막 두 항은 0으로 수렴하게 됩니다. 즉 이는 우리가 원하는 결과라고 할 수 있습니다.

> ## Property 2

$X_{n} \stackrel{P}{\rightarrow} X$ 이고 $a$ 가 상수이면 $a X_{n} \stackrel{P}{\rightarrow} a X$ 이다.

> Proof

- $a=0$ 이면 결과가 바로 성립됩니다.
- 즉 $a \neq 0$ 이고 $\epsilon>0$ 이라고 합시다. 그러면 다음 부등식을 얻어낼 수 있습니다.

$$P\left[\left|a X_{n}-a X\right| \geq \epsilon\right]=P\left[|a|\left|X_{n}-X\right| \geq \epsilon\right]=P\left[\left|X_{n}-X\right| \geq \epsilon /|a|\right]$$

- 가정에 의해 $n \rightarrow \infty$ 일 때 마지막 항은 0 으로 수렴하게 됩니다.

> ## Property 3

$X_{n} \stackrel{P}{\rightarrow} a$ 이고 실함수 $g$ 가 $a$ 에서 연속이라면 $g\left(X_{n}\right) \stackrel{P}{\rightarrow} g(a)$ 이다.

> Proof

- $\epsilon>0$ 이라고 하자. $g$ 가 $a$ 에서 연속이므로 $|x-a|<\delta$ 이면 $|g(x)-g(a)|<\epsilon$ 인 $\delta>0$ 가 존재합니다. 즉 

$$|g(x)-g(a)| \geq \epsilon \Rightarrow|x-a| \geq \delta$$

- 위 관계에서 $x$ 를 $X_{n}$ 으로 대체하여 봅시다. 그러면 아래처럼 계산이 됩니다.

$$P\left[\left|g\left(X_{n}\right)-g(a)\right| \geq \epsilon\right] \leq P\left[\left|X_{n}-a\right| \geq \delta\right]$$

- 조건에 의해 $n \rightarrow \infty$ 일 때 마지막 항은 0 으로 수렴하게 됩니다.

> ## Property 4

$$X_{n} \stackrel{P}{\rightarrow} X \text { 이고 } Y_{n} \stackrel{P}{\rightarrow} Y \text { 이면 } X_{n} Y_{n} \stackrel{P}{\rightarrow} X Y \text { 이다. }$$

> Proof

$$\begin{aligned}
X_{n} Y_{n} &=\frac{1}{2} X_{n}^{2}+\frac{1}{2} Y_{n}^{2}-\frac{1}{2}\left(X_{n}-Y_{n}\right)^{2} \\
& \stackrel{P}{\rightarrow} \frac{1}{2} X^{2}+\frac{1}{2} Y^{2}-\frac{1}{2}(X-Y)^{2}=X Y
\end{aligned}$$

- 이떄 위 증명을 할떄에, 이전의 Property 를 이용하여 증명하였습니다.

# [Sampling and Statistics](#link){: .btn .btn--primary}{: .align-center}

> ## Sampling and Statiatic

- 알려지지 않은 모수 $\theta \in \Omega$ 에대해 $\operatorname{pdf}($ 또는 $\mathrm{pmf})$ 를 $f(x ; \theta)$ 로 쓰는 확률변수 $X$ 가 있다고 합시다.
- 예를 들어서 $X$ 의 분포는 평균 $\mu$ 와 분산 $\sigma^{2}$ 이 알려지지 않은 정규분포라고 합시다. 
  - 그러면 $\theta=\left(\mu, \sigma^{2}\right)$ 고 $\Omega=\left\{\theta=\left(\mu, \sigma^{2}\right):-\infty<\mu<\infty, \sigma>0\right\}$ 이 됩니다. 
- 또 다른 예로 $X$ 의 분포는 $\Gamma(1, \beta)$ 라고 합시다. 
  - 그러면 모수는 $\beta>0$ 가 됩니다.
- 이때 우리가 가진 정보는 $X$ 에 대한 random sample인 $X_{1}, X_{2}, \cdots, X_{n}$ 으로 밖에 없습니다.
  -  즉 $X_{1}, X_{2}, \cdots, X_{n}$ 은 $\theta \in \Omega$ 일 때 공통 $\operatorname{pdf} f(x ; \theta)$ 를 가진 독립 이며 같은 분포를 따르는 iid 확률변수입니다.
- 만약 $T$ 가 표본의 함수이면 $T$ 는 통계량 이라고 하고 Statistic 이라 합니다. 
  - 즉 $T=T\left(X_{1}, X_{2}, \cdots, X_{n}\right)$ 이다. 
- 여기서 우리는 $T$ 는 다양한것들을 추정하는 값으로 쓸 수 있지만 여기에서는 $T$ 를 $\theta$ 의 점추정량 $($ point estimator $)$ 으로 쓴다고 합시다.
  - 예를 들어 $\mu$ 가 $X$ 의 알려지지 않은 평균이면 점추정량으로 표본평균인 $\bar{X}=n^{-1} \sum_{i=1}^{n} X$ 를 사용할 수 있다. 
- 표본이 추출되면 $x_{1}, x_{2}, \cdots, x_{n}$ 이 $X_{1}, X_{2}, \cdots, X_{n}$ 의 관측값을 나타낸다고 합시다.
  - 이러한 값을 표본의 실현된(realized) 값이라고 합니다
  - 그리고 실현된 통계량 $t=t\left(x_{1}, x_{2}, \cdots, x_{n}\right)$은 점추정값(point estimate)이라고 합시다.

> ## Unbiased (불편추정량)

- 이후에서는 공식적인 설정에서 점추정량의 속성을 살퍼보고 지금은 불편성(unbiasedness)과 일치성(consistency)을 알아보도록 합시다.
  - 만약 $E(T)=\theta$ 이면 $\theta$ 에 대한 점추정량 $T$ 는 불편하다 (unbiased)고 합니다.
- 표본평균 $\bar{X}$ 와 포본분산 $S^{2}$ 이 각각 $\mu$ 와 $\sigma^{2}$ 의 Unbiased Estimator 였던것을 상기합시다.

> ## Consistency (일치추정량)

> Definition

- $\theta \in \Omega$  일 때 $\operatorname{cdf} F(x, \theta)$ 를 가진 확률변수를 $X$ 라고 하자.
-  $X_{1}, X_{2}, \cdots, X_{n}$ 이 $X$ 의 분포에서 추출 한 표본이고 $T_{n}$ 이 통계량을 나타낸다고 하자. 
- 이때 아래와 같으면 $T_{n}$ 을 $\theta$ 의 일치(consistent)추정량 이라고 합니다.

$$T_{n} \stackrel{P}{\rightarrow} \theta$$

> Note

- Consistency Estimator 는 추정량에 대해서 매우 중요한 성질입니다. 
- 왜냐하면 표본 크기가 커질떄에 목표에 접근한다는, 어쩌면 당연한 사실을 증명하기 때문입니다.
- 뒤에 Estimator 의 성질이 몇개 더 나오겠지만, 일반적으로 이 Consistency 가 제일 중요하다고 생각합니다.

> ## Example  : 표본분산의 Consistency

- 표본분산이, 모분산에 대해서 Consistency 함을 보여 봅시다.
- 확률수렴함을 보이기 위해 추가적으로 $E\left[X_{1}^{4}\right]<\infty$ 라고 가정하자. 그러면 자연스럽게 $\operatorname{Var}\left(S^{2}\right)<\infty$ 이다.
- 그러면 아래가 성립합니다.

$$\begin{aligned}
S_{n}^{2}=\frac{1}{n-1} \sum_{i=1}^{n}\left(X_{i}-\bar{X}_{n}\right)^{2} &=\frac{n}{n-1}\left(\frac{1}{n} \sum_{i=1}^{n} X_{i}^{2}-\bar{X}_{n}^{2}\right) \\
& \stackrel{P}{\rightarrow} 1 \cdot\left[E\left(X_{1}^{2}\right)-\mu^{2}\right]=\sigma^{2}
\end{aligned}$$

- 따라서 표본분산은 $\sigma^{2}$ 의 일치추정량(Consistency)이 됩니다. 
- 위의 결과로부터 $S_{n} \stackrel{P}{\rightarrow} \sigma$ 임을 바로 알 수 있다. 즉 표본표준편차는 모표준편차의 일치추정량(Consistency)입니다.

> ## Example : 균등분포 (cdf 이용)

- $X_{1}, X_{2}, \cdots, X_{n}$ 을 $Unif (0, \theta)$ 에서의 Random Sample 이고 $\theta$ 는 알려지지 않았다고 가정합시다.
- 이때 $\theta$ 에 대한 직관적인 추정값은 표본의 최댓값이 됩니다
- $Y_{n}=\max \left\{X_{1}, X_{2}, \cdots, X_{n}\right\}$ 일 때 $Y_{n}$ 의 $\operatorname{cdf}$ 가 다음과 같습니다. (계산은 Order Statistic 을 이용)

$$F_{Y_{n}}(t)= \begin{cases}1 & t>\theta \\ \left(\frac{t}{\theta}\right)^{n} & 0<t \leq \theta \\ 0 & t \leq 0\end{cases}$$

- 따라서 $Y_{n}$ 의 $\mathrm{pdf}$ 는

$$f_{Y_{n}}(t)= \begin{cases}\frac{n}{\theta^{n}} t^{n-1} & 0<t \leq \theta \\ 0 & \text { 그 외에 }\end{cases}$$

- 이 $\mathrm{pdf}$ 를 가지고 $E\left(Y_{n}\right)=(n /(n+1)) \theta$ 임을 밝히기는 쉽습니다. 그러므로 $Y_{n}$ 은 $\theta$ 의 Biased 추정량 이다. 
  - 그러나 $((n+1) / n) Y_{n}$ 은 $\theta$ 의 Unbised estimator 가 됩니다.
- 게다가 $Y_{n}$ 의 $\operatorname{cdf}$ 를 가지고 $Y_{n} \stackrel{P}{\rightarrow} \theta$ 이며 따라서 표본의 최댓값은 것을 Consistency Estimator 라는 것을 쉽게 증명할 수 있습니다. 
- 즉 $((n+1) / n) Y_{n}$ 는 Unbiased + Consistency Estimator 가 됩니다.

> Note

- 위에서는 수렴성을  CDF 를 이용해서 증명했지만, 통상 CDF 를 이용하는것은 어려운 작업입니다.
- 이때 대수의 법칙에 따라서( Week Law of large number) $\bar{X}_{n}$ 이 $\theta / 2$ 의 Consistnecy Estimator 가 됩니다. 
- 즉 $2 \bar{X}_{n}$ 이 $\theta$ 의 Consistence + Unbiased Extimator 가 됩니다.
- 이전에 CDF 를 이용해 증명한것과 비교해보세요. 이러한 Week Law of Large Number 를 이용한 방법이 훨씬 간단하고 좋지 않나요? 

> ## Remark : Mathmetical Converge -> Probability Converge

> Problem

- Let $\left\{a_{n}\right\}$ be a sequence of real numbers. Hence, we can also say that $\left\{a_{n}\right\}$ is a sequence of constant (degenerate) random variables. 
- Let $a$ be a real number. Show that $a_{n} \rightarrow a$ is equivalent to $a_{n} \stackrel{P}{\rightarrow} a$.

> Solution

- From the given information, let $\left\{a_{n}\right\}$ be a sequence of real numbers.
- From the known information, the expression $a_{n} \rightarrow a$, this means that for each $\in>0$ there is positive integer $N$ such that $n>N$ implies $\left|a_{n}-a\right|<\epsilon$, or equivalently $\left|a_{n}-a\right| \geq \in$ implies $n \leq N$.

- Let $\in>0$, then for each positive integer $n$, then $P\left(\left|a_{n}-a\right| \geq \in\right)=1$ if and only if $\left|a_{n}-a\right| \geq \in$ and $P\left(\left|a_{n}-a\right| \geq \in\right)=0$ if and only if $\left|a_{n}-a\right|<\epsilon$.
- From the definition, the function $a_{n} \stackrel{P}{\rightarrow} a$ if and only if $\lim _{n \rightarrow \infty} P\left(\left|a_{n}-a\right| \geq \in\right)=0$.
- Since, the only possible values of $P\left(\left|a_{n}-a\right| \geq \in\right)$ are 0 and 1 , the limit is 0 if and only if at most finitely many of these probabilities are equal to 1 .
- Thus, this is equivalent to the condition that only finitely many terms of the sequence $\left\{a_{n}\right\}$ satisfy $\left|a_{n}-a\right| \geq \in$. This mean that $a_{n} \rightarrow a$.
  Therefore, $a_{n} \rightarrow a$ is equivalent to $a_{n} \stackrel{P}{\rightarrow} a .$

---

 **Reference**

- Hoggs Introduction to Mathematical Statistics 7ed



