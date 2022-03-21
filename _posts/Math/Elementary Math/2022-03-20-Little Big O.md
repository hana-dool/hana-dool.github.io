---
title:  "Little , Big O Notation"
excerpt: "수렴성 판정시에 이용하는 O,o Notation"
categories:
  - Elementary_Math
last_modified_at: 2022-03-20

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 맨날 헷갈리는 O , o Notation 에 대해서 정리해보자.
{: .notice--warning}

# [점근 표기법](#link){: .btn .btn--primary}{: .align-center}

> ## Definition

- 점근 표기법(asymptotic notation)은 어떤 함수의 증가 양상을 다른 함수와의 비교로 표현하는 수론과 해석학의 방법이다. 알고리즘의 복잡도를 단순화할 때나 무한급수의 뒷부분을 간소화할 때 쓰입니다.
- 대표적으로 다음의 다섯 가지 표기법이 있다.
  - 대문자 O 표기법
  - 소문자 o 표기법
  - 대문자 오메가(Ω) 표기법
  - 소문자 오메가(ω) 표기법
  - 대문자 세타(Θ) 표기법
- 이 중 압도적으로 많이 쓰이는 것이 대문자 O 표기법으로, 란다우 표기법이라고도 합니다.

$$\begin{array}{|c|l|c|}
\hline \text { 표기법 } & {\text { 설명 }} & {\text { 수학적 정의 }} \\
\hline f(n) \in O(g(n)) & \text { 상한 점근 } & \lim _{n \rightarrow \infty}\left|\frac{f(n)}{g(n)}\right|<\infty \\
\hline f(n) \in o(g(n)) & & \lim _{n \rightarrow \infty} \frac{f(n)}{g(n)}=0 \\
\hline f(n) \in \Omega(g(n)) & \text { 하한 점근 } & \lim _{n \rightarrow \infty}\left|\frac{f(n)}{g(n)}\right|>0 \\
\hline f(n) \in \omega(g(n)) & & \lim _{n \rightarrow \infty} \frac{f(n)}{g(n)}=\infty \\
\hline f(n) \in \Theta(g(n)) & \text { 상한/하한 점근 } & 0<\lim _{n \rightarrow \infty}\left|\frac{f(n)}{g(n)}\right|<\infty \\
\hline
\end{array}$$

> ## Big O 

- 함수 $f(x), g(x)$ 에 대해 $f(x)$ = $O(g(x))$ 라는것은 아래와 같습니다. (아래 3개의 정의는 모두 동치입니다)

> Definition

- $$|f(x)| \leq \varepsilon g(x) \quad \text { for all } x \geq x_{0}$$ 을 만족하는 $\epsilon , x_0 $ 이 존재한다. 
- $\limsup _{x \rightarrow a}\left|\frac{f(x)}{g(x)}\right|<\infty$.

> Intuition

![jpg](/assets/images/Stat/162_1.jpg){: .align-center}

- 위의 그래프처럼 f(n) 과  cg(n) 가 있다고 합시다.
  - f(n) = O(g(n)) 은 n 이 커진다면, 언젠가 cg(n) 이 f(n) 을 추월한다는것을 의미합니다.
- 즉 이는 근본적으로 $f(x)$ 의 증가율이 $g(x)$ 보다 같거나 더 크기 때문에 나타나는 현상이라 할 수 있습니다.

> Note 

- 이떄 $f(x)=O(g(x))$ 혹은 $f(x) \in O(g(x))$ 로 표기하기도 합니다.
- 이때 $f(x)=O(g(x))$ 라는 표현에서, 등호는 원래의 등호와는 다른 의미를 가집니다. 
  - 예를 들어, 어떤 함수가 $O(x)$ 이면 $O\left(x^{2}\right)$ 이므로 $O(x)=O\left(x^{2}\right)$ 로 표기할 수는 있지만, $O\left(x^{2}\right)=O(x)$ 와 같이 쓰는 것은 잘못된 표기입니다. 
  - 이 때, 등호 표기는 일반적인 표기법과 다르게 사 용된 기호의 남용으로 볼 수 있습니다.
- 이러한 문제를 방지하기 위해, $O(g(x))$ 를 원래 정의에서 해당하는 함수들의 집합으로 정의하는 경우도 많이 사용됩니다. 
  - 이러한 경우 $f(x) \in O(g(x))$ 과 같이 표기할 수 있고, 이것은 기호의 원래 정의와 잘 맞아 떨어집니다!

> Example

-  다항식 $f, g$ 를 다음과 같이 정의했다고 합시다.

$$
\begin{aligned}
&f(x)=6 x^{4}-2 x^{3}+5 \\
&g(x)=x^{4}
\end{aligned}
$$
- $\left|6 x^{4}-2 x^{3}+5\right| \leq 6 x^{4}+2 x^{3}+5(x>1$ 일 때)
- $\left|6 x^{4}-2 x^{3}+5\right| \leq 6 x^{4}+2 x^{4}+5 x^{4}\left(x^{3}<x^{4}\right.$ 와 같은 방법 $)$
- $\left|6 x^{4}-2 x^{3}+5\right| \leq 13 x^{4}$
- $\left|6 x^{4}-2 x^{3}+5\right| \leq 13\left|x^{4}\right|$
- 즉  $f(x)=O(g(x))$ or $O\left(x^{4}\right)$ 이 됩니다.

> ## Little o

- 함수 $f(x), g(x)$ 에 대해 $f(x)$ = $o(g(x))$ 라는것은 아래를 의미합니다.
  - 어떠한 $\varepsilon >0$ 에 대해서도, $$|f(x)| \leq \varepsilon g(x) \quad \text { for all } x \geq x_{0}$$ 을 만족하는 $x_{0}$ 이 존재한다.
  - $$\lim _{x \rightarrow \infty} \frac{f(x)}{g(x)}=0$$

![jpg](/assets/images/Stat/162_2.jpg){: .align-center}

- x가 증가함에 따라 $x^2$에 0.5을 곱하든, 0.1을 곱해도... 훨씬 더 작은 수를 곱하더라도 3x (검은색 선 )보다는 커지게 되는 x를 반드시 찾을 수 있습니다.
- 이는 근본적으로 $f(x)$ 의 증가율이 $g(x)$ 보다 더 크기 때문에 나타나는 현상이라 할 수 있습니다.

> ## Comparison With Little o and Big o 

- 이전에 definition 을 다시 상기해봅시다.

> Comparison

- big O $f(x)$ = $O(g(x))$ 
  - $$|f(x)| \leq \varepsilon g(x) \quad \text { for all } x \geq x_{0}$$ 을 만족하는 $\epsilon , x_0 $ 이 존재한다. 
  - $\limsup _{x \rightarrow a}\left|\frac{f(x)}{g(x)}\right|<\infty$.
  - 근본적으로 $f(x)$ 의 증가율이 $g(x)$ 보다 같거나 더 커야함
- Little o $f(x)$ = $o(g(x))$ 
  - 어떠한 $\varepsilon >0$ 에 대해서도, $$|f(x)| \leq \varepsilon g(x) \quad \text { for all } x \geq x_{0}$$ 을 만족하는 $x_{0}$ 이 존재한다.
  - $$\lim _{x \rightarrow \infty} \frac{f(x)}{g(x)}=0$$
  - 근본적으로 $f(x)$ 의 증가율이 $g(x)$ 보다 더 커야함
- 즉 위를 비교하면 "증가율이 같거나 커야" Big O 이고, 증가율이 "더 크면" Little o 라는것을 볼 수 있습니다. 

# [Using In Statistics](#link){: .btn .btn--primary}{: .align-center}

> ## Statistic Notation

- 위와 같은 Big O , Little O 를 이용하여서 통계학에서 Converge 를 표현하기도 합니다.

> Small O : convergence in probability 

- For a set of random variables $X_{n}$ and a corresponding set of constants $a_{n}$ (both indexed by $n$, which need not be discrete), the notation

$$
X_{n}=o_{p}\left(a_{n}\right)
$$
- 즉 위를 풀어쓰면 set of random variable $X_{n}$ and a corresponding set of constants $a_{n}$, $X_{n}=o_{p}\left(a_{n}\right)$ if and only if

$$
\lim _{n \rightarrow \infty} P\left(\left|\frac{X_{n}}{a_{n}}\right| \geq \epsilon\right)=0, \forall \epsilon>0
$$
- 다시 말해, $X_{n}=o_{p}\left(a_{n}\right)$ 의 필요충분조건은 $\frac{X_{n}}{a_{n}} \stackrel{p}{\rightarrow} 0$ 이라는 것입니다.

- Spacial Case : $X_{n}=o_{p}(1)$ is defined for every positive $\varepsilon$

$$
\lim _{n \rightarrow \infty} P\left(\left|X_{n}\right| \geq \varepsilon\right)=0
$$

- 즉 위처럼 $a_n = 1$ 을 넣는다면, $X_p \stackrel{p}{\rightarrow} 0$ 은 $o_p(1)$ 와 같다는 것입니다.

> Big O: stochastic boundedness

- The notation
  $$
  X_{n}=O_{p}\left(a_{n}\right) \text { as } n \rightarrow \infty
  $$

- means that the set of values $X_{n} / a_{n}$ is stochastically bounded. 

- 즉 위의 정리를 다시쓰면 아래와 같습니다. 

- For a set of random variable $X_{n}$ and a corresponding set of constants $a_{n}$, $X_{n}=O_{p}\left(a_{n}\right)$ if and only if $\forall \epsilon>0, \exists M, N>0$ such that

$$
P\left(\left|\frac{X_{n}}{a_{n}}\right|>M\right)<\epsilon, \forall n>N
$$

- 이는 $X = \mathrm{O}_{p}(1)$  경우, Bounded in Probability 임을 의미합니다. $\mathrm{O}_{p}(1): \forall \varepsilon \quad \exists N_{\varepsilon}, \delta_{\varepsilon} \quad$ such that $P\left(\left|X_{n}\right| \geq \delta_{\varepsilon}\right) \leq \varepsilon \quad \forall n>N_{\varepsilon}$

> Comparison 

- Big O :  $\mathrm{O}_{p}(1): \forall \varepsilon \quad \exists N_{\varepsilon}, \delta_{\varepsilon} \quad$ such that $P\left(\left|X_{n}\right| \geq \delta_{\varepsilon}\right) \leq \varepsilon \quad \forall n>N_{\varepsilon}$ 
  - 즉 Bounded in Probability 
- Small o : ${o}_{p}(1): \forall \varepsilon, \delta \quad \exists N_{\varepsilon, \delta} \quad$ such that $P\left(\left|X_{n}\right| \geq \delta\right) \leq \varepsilon \quad \forall n>N_{\varepsilon, \delta}$
  - 즉 Converge in Probability to zero : $X_n \stackrel{p}{\rightarrow} 0$ 

> ## Tailor Expansion

- http://www.ma.huji.ac.il/~razk/iWeb/My_Site/Teaching_files/Chapter6_2.pdf

$$P_{f, n, a}(x)=f(a)+f^{\prime}(a)(x-a)+\frac{f^{\prime \prime}(a)}{2}(x-a)^{2}+\cdots+\frac{f^{(n)}(a)}{n !}(x-a)^{n}$$

- Notation 을 위처럼 정의합시다.
- 그리고 Lophital 의 정리는 아래와 같습니다.

> 로피탈의 정리

- Suppose that $f$ and $g$ both vanish at $a$ and have continuous derivatives in a neighborhood of $a$;

  moreover, assume that neither $g$ nor $g^{\prime}$ vanish in this neighborhood. If

$$
\lim _{x \rightarrow a} \frac{f^{\prime}(x)}{g^{\prime}(x)} \quad \text { exists, }
$$
- then

$$
\lim _{x \rightarrow a} \frac{f(x)}{g(x)}=\lim _{x \rightarrow a} \frac{f^{\prime}(x)}{g^{\prime}(x)}
$$

> Tailor Expansion 

- L'Hopital's rule is a useful tool for calculating limits. In the present context, it is helpful in the following sense. Consider the difference between a function and its linear approximation divided by the distance of the point of evaluation from the point of expansion:

$$
\frac{f(x)-P_{f, 1, a}(x)}{x-a} .
$$
- L'Hopital's rule tells us that the limit as $x \rightarrow a$ exists is the limit of the ratios of the derivatives does. The latter is equal to

$$
\frac{f^{\prime}(x)-P_{f^{\prime}, 0, a}(x)}{1},
$$
- which tends to zero as $x \rightarrow 0$. Thus, we recover once again the property of the linear approximation,

$$
\lim _{x \rightarrow a} \frac{f(x)-P_{f, 1, a}(x)}{x-a}=0 .
$$
- Consider now the Taylor polynomial of degree 2 , and consider the ratio

$$
\frac{f(x)-P_{f, 2, a}(x)}{(x-a)^{2}} .
$$

- By L'Hopital's rule,

$$
\lim _{x \rightarrow a} \frac{f(x)-P_{f, 2, a}(x)}{(x-a)^{2}}=\lim _{x \rightarrow a} \frac{f^{\prime}(x)-P_{f^{\prime}, 1, a}(x)}{2(x-a)}
$$
- provided that the right-hand side exists, but by the very same rule,

$$
\lim _{x \rightarrow a} \frac{f^{\prime}(x)-P_{f^{\prime}, 1, a}(x)}{2(x-a)}=\lim _{x \rightarrow a} \frac{f^{\prime \prime}(x)-P_{f^{\prime \prime}, 0, a}(x)}{2}
$$
- provided that the right-hand side exists. It does; it is zero. Hence,

$$
\lim _{x \rightarrow a} \frac{f(x)-P_{f, 2, a}(x)}{(x-a)^{2}}=0
$$
- Equivalently, we an use the "little $o$ " notation,

$$
f(x)=P_{f, 2, a}(x)+o\left((x-a)^{2}\right) \quad \text { as } x \rightarrow a .
$$
- 즉 위와 같이, Taylor Expansion 에 대해서 로피탈 정리를 이용하면 , little o expansion 으로 테일러 정리를 표시할 수 있음을 알 수 있습니다.

> Theorem 

- Let $f$ be $n$ times differentiable at $a$. Then

$$
\lim _{x \rightarrow a} \frac{f(x)-P_{f, n, a}(x)}{(x-a)^{n}}=0
$$
- or using the "little $o$ " notation,

$$
f(x)=P_{f, n, a}(x)+o\left((x-a)^{n}\right) \quad \text { as } x \rightarrow a
$$

> ## Delta Method

- 이러한 little o 를 이용하여서 Delta Method 에 적용되곤 합니다.
- $g(x)$ 가 $x$ 에서 미분 가능하면 다음과 같이 나타낼 수 있습니다. (이전 정리에 당연하겠죠?)

$$
g(y)=g(x)+g^{\prime}(x)(y-x)+o(|y-x|)
$$

- 여기서 기호 $o$ 에 대해서 다시 상기하면 아래와 같습니다.
  - $b \rightarrow 0$ 일 때 $\frac{a}{b} \rightarrow 0$ 인 경우에 한하여 $a=o(b)$

- 이떄 $o($ little $o)$ 는 확률수렴의 개념으로도 이용됩니다. 종종 $o_{p}\left(X_{n}\right)$ 은 다음과 같은 의미로 쓰입니다.
  - $n \rightarrow \infty$ 일 때 $\frac{Y_{n}}{X_{n}} \stackrel{P}{\rightarrow} 0$ 인 경우에 한하여 $Y_{n}=o_{p}\left(X_{n}\right)$


> Lemma

- $\left\{Y_{n}\right\}$ 이 확률유계인 확률변수 열이라고 하자. $X_{n}=o_{p}\left(Y_{n}\right)$ 이면 $n \rightarrow \infty$ 일 때 $X_{n} \stackrel{P}{\rightarrow} 0$ 이다.

> Lemma Proof

- 증명: $\epsilon>0$ 이라고 하자. 열 $\left\{Y_{n}\right\}$ 이 확률유계이므로 다음과 같은 양의 상수 $N_{c}$ 과 $B_{\epsilon}$ 이 존재한다.

$$
n \geq N_{\epsilon} \Longrightarrow P\left[\left|Y_{n}\right| \leq B_{\epsilon}\right] \geq 1-\epsilon \quad ...(1)
$$

- 또한 $X_{n}=o_{p}\left(Y_{n}\right)$ 이므로 $n \rightarrow \infty$ 일 때 다음을 얻는다.

$$
\frac{X_{n}}{Y_{n}} \stackrel{P}{\rightarrow} 0 \quad ...(2)
$$

- 그러면

$$
\begin{aligned}
P\left(\left|Y_{n}\right| \geq \epsilon\right) &=P\left(\left|Y_{n}\right| \geq \epsilon,\left|X_{n}\right| \leq B_{\epsilon}\right)+P\left(\left|Y_{n}\right| \geq \epsilon,\left|X_{n}\right|>B_{\epsilon}\right) \\
& \leq P\left(\left|Y_{n}\right| \geq \epsilon,\left|X_{n}\right| \leq B_{\epsilon}\right)+P\left(\left|X_{n}\right|>B_{\epsilon}\right) \\
& \leq P\left(\left|\frac{Y_{n}}{X_{n}}\right| \geq \frac{\epsilon}{B_{\epsilon}}\right)+P\left(\left|X_{n}\right|>B_{\epsilon}\right) \rightarrow 0,
\end{aligned}
$$

- (1) 과 (2) 에의해 오른쪽의 첫째($$P\left(\left|\frac{Y_{n}}{X_{n}}\right| \geq \frac{\epsilon}{B_{\epsilon}}\right)$$)와 둘째 항 ( $$P\left(\left|X_{n}\right|>B_{\epsilon}\right)$$ )은 $n$ 을 충분히 크게 함으로써 얼마든지 작게 만들 수 있습니다. 즉 따라서 이 결과는 성립하게 됩니다.

>  Delta Method

- 다음과 같은 확률변수 열을 $\left\{X_{n}\right\}$ 이라고 하자.
- $$ \sqrt{n}\left(X_{n}-\theta\right) \stackrel{D}{\rightarrow} N\left(0, \sigma^{2}\right) $$ 함수 $g(x)$ 가 $\theta$ 에서 미분 가능하고 $g^{\prime}(\theta) \neq 0$ 라고 하면 

$$ \sqrt{n}\left(g\left(X_{n}\right)-g(\theta)\right) \stackrel{D}{\rightarrow} N\left(0, \sigma^{2}\left(g^{\prime}(\theta)\right)^{2}\right) $$

> Delta Method Proof

- Using the Taylor series expansion, we have

$$g\left(X_{n}\right)=g(\theta)+g^{\prime}(\theta)\left(X_{n}-\theta\right)+o_{p}\left(\left|X_{n}-\theta\right|\right)$$

- 이떄 위의 식을 재배치하면 아래가 성립합니다.

$$\begin{aligned}
\sqrt{n}\left(g\left(X_{n}\right)-g(\theta)\right) &=g^{\prime}(\theta) \sqrt{n}\left(X_{n}-\theta\right)+o_{p}\left(\sqrt{n}\left|X_{n}-\theta\right|\right) \\
& \stackrel{P}{\rightarrow} g^{\prime}(\theta) \sqrt{n}\left(X_{n}-\theta\right) \\
& \stackrel{D}{\rightarrow} N\left(0, \sigma^{2}\left\{g^{\prime}(\theta)\right\}^{2}\right)
\end{aligned}$$

> 해설

- $$ \sqrt{n}\left(X_{n}-\theta\right) \stackrel{D}{\rightarrow} N\left(0, \sigma^{2}\right) $$ 가 성립하므로 , $\sqrt{n}\left|X_{n}-\theta\right|$ 는 Bounded in Probabaility 입니다.
  - 왜냐하면 Converge in Distribution $\to$ Converge in Probability 가 성립하기 때문입니다.
- 그러므로 $$g^{\prime}(\theta) \sqrt{n}\left(X_{n}-\theta\right)+o_{p}\left(\sqrt{n}\left|X_{n}-\theta\right|\right)
  \stackrel{P}{\rightarrow} g^{\prime}(\theta) \sqrt{n}\left(X_{n}-\theta\right)$$ 가 성립합니다.
  - 왜냐하면 이전 lemma 에서  $\left\{Y_{n}\right\}$ 이 확률유계인 확률변수 열이라고 할때 $X_{n}=o_{p}\left(Y_{n}\right)$ 이면 $n \rightarrow \infty$ 일 때 $X_{n} \stackrel{P}{\rightarrow} 0$ 라는것을 증명했던것을 기억하나요?
  - 즉 현재 $\sqrt{n}\left|X_{n}-\theta\right|$ 가 확률유계이므로 $o_p(\sqrt{n}\left|X_{n}-\theta\right|) \stackrel{P}{\rightarrow} 0$ 이 성립하기 떄문입니다.
- 이제 $$ \sqrt{n}\left(X_{n}-\theta\right) \stackrel{D}{\rightarrow} N\left(0, \sigma^{2}\right) $$ 이므로 $$g^{\prime}(\theta) \sqrt{n}\left(X_{n}-\theta\right)\stackrel{D}{\rightarrow} N\left(0, \sigma^{2}\left\{g^{\prime}(\theta)\right\}^{2}\right)$$ 가 성립합니다.

---

**Reference**

- https://sdolnote.tistory.com/entry/BigOLittleo
- http://www.ma.huji.ac.il/~razk/iWeb/My_Site/Teaching_files/Chapter6_2.pdf
- https://statkim.github.io/2021/08/o_pbig-op%EC%99%80-o_plittle-op/





