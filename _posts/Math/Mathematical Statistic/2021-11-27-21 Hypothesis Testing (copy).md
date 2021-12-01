---
title:  "Hypothesis Testing"
excerpt: "가설검정의 기초"
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

# [Introduction to Hypothesis Testing](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

> Intuition

우리의 interest 는 random variable X 에 있다고 합시다. 이때 $X \sim f(x ; \theta)$ where $\theta \in \Omega$ 입니다. 우리의 관심사를  parameter $\theta$ 에 매핑하여 표현한다고 합시다. 그러면  $w_0, w_1$ 영역을 잘 정의하여 , 우리 가설과 매칭할 수 있습니다. 즉  $\theta \in \omega_{0}$ or $\theta \in \omega_{1}$, where $\omega_{0}$ and $\omega_{1}$ are disjoint subsets of $\Omega$ and $\omega_{0} \cup \omega_{1}=\Omega$. We can label these hypotheses as

$$H_{0}: \theta \in \omega_{0} \text { versus } H_{1}: \theta \in \omega_{1}$$

위처럼 우리의 가설이 표현될 수 있을것입니다. (예 : 내 몸무게의 평균($\mu$) 이 궁금하므로 다음과 같이 가설을 세울 수 있습니다. $H_0 : \mu$ = 70kg , $H_1 : o.w.$) 

> Definition : null / alternative

- The hypothesis $H_{0}$ is referred to as the null hypothesis, 
- The hypothesis $H_{1}$ is referred to as the alternative hypothesis. 
- 이때 주로 $H_0$ 은 차이가 없음 , 특정한 값 등을 나타낼때에 사용됩니다. 
- $H_1$ 은 차이가 있음 , 특정한 값이 아님 등으로 나타납니다.

> Decision Rule

- 우리가 실험하고자 하는 가설을 설정했다고 합시다. 그러면 이게 맞는지 틀리는지는 어떻게 알 수 있을까요? 
- 그것은 바로 Based on sample $X_1 ... X_n$에 근거하여 선택하게 됩니다. 이때에 생기는 에러를 Type 1 error, Type 2 erorr 라 합니다. 
- 즉 우리는 이러한 에러를 잘 컨트롤 하도록 실험을 설계해야 할 것입니다. 즉 Optimal Test (최적의 테스트) 를 나중에 더 알아보겠습니다. 

> ## Definition : Critical Region

> Definition

To complete the testing structure for the general problem described at the beginning of this section, we need to discuss decision rules. 

Recall that $X_{1}, \ldots, X_{n}$ is a random sample from the distribution of a random variable $X$ which has density $f(x ; \theta)$, where $\theta \in \Omega .$ Consider testing the hypotheses $H_{0}: \theta \in \omega_{0}$ versus $H_{1}: \theta \in \omega_{1}$, where $\omega_{0} \cup \omega_{1}=\Omega .$ 

Denote the space of the sample by $\mathcal{D} ;$ that is, $\mathcal{D}=$ space $\left\{\left(X_{1}, \ldots, X_{n}\right)\right\} .$ A test of $H_{0}$ versus $H_{1}$ is based on a subset $C$ of $\mathcal{D}$ This set $C$ is called the **critical region** and its corresponding decision rule (test) is

$$\begin{array}{ll}
\text { Reject } H_{0}\left(\text { Accept } H_{1}\right) & \text { if }\left(X_{1}, \ldots, X_{n}\right) \in C \\
\text { Retain } H_{0}\left(\text { Reject } H_{1}\right) & \text { if }\left(X_{1}, \ldots, X_{n}\right) \in C^{c}
\end{array}$$

> Note

- 즉 Testing 은 다음과 같습니다.

1) Hypothesis 에 의하여 Parameter Space 를 Null / Alternative 로 나눔
2) Decision Rule 에 의하여 Sample Space 를 Critical Region / O.W 로 나눔

-  즉 파라미터 Space 와 Sample space 를 각각 두 영역으로 나눈 뒤에 짝지어주는것이 Testing 이라고 할 수 있죠.

> ## Definition : Error

> definition

$$\begin{array}{ll}\text { Reject } H_{0}\left(\text { Accept } H_{1}\right) & \text { if }\left(X_{1}, \ldots, X_{n}\right) \in C \\ \text { Retain } H_{0}\left(\text { Reject } H_{1}\right) & \text { if }\left(X_{1}, \ldots, X_{n}\right) \in C^{c}\end{array}$$

For a given critical region, the $2 \times 2$ decision table as below 

![png](/assets/images/Stat/116_1.png)

위와 같이 Decision 은 2가지가 있으므로 그에 따라서 Error 도 두가지가 생깁니다. A Type I error occurs if $H_{0}$ is rejected when it is true, while a Type II error occurs if $H_{0}$ is accepted when $H_{1}$ is true.

우리의 목표는 당연히 이러한 error 들을 최소화 하면서 좋은 Testing 을 만든는 것입니다. 두가지의 에러는 일반적으로 Trade off 가 있어서 minimize 하는것이 어렵습니다. 하나의 예시로 단순하게 Type I error (Null 이 맞는데 기각함) 를 줄이기 위하여 $C=\phi$ 로 설정했다고 합시다. 이러한 Critical Region 에서는 Type I error 는 0 일테지만 Type II error 는 1 이 되고 맙니다. 

즉 우리느 효율적인 테스트를 만들어야 합니다. 이때 우리는 대게 Type 1 error 를 고정시킨 상태에서 Type 2 error 를 minimize 하는 테스트를 선택하게 됩니다.

> ## Definition : Size $\alpha$

> We say a critical region $C$ is of size $\alpha$ if

$$\alpha=\max _{\theta \in \omega_{0}} P_{\theta}\left[\left(X_{1}, \ldots, X_{n}\right) \in C\right]$$

> Note

- 이전에 $w_0$ 은 Null Hypothesis 에 해당되는 parameter space 라는것을 기억합시다. 
- 'space' 이므로 여러 parameter 들이 존재하고, 이는 Decision rule 이 정해지더라도 $\alpha$ 가 하나만 정해질 수 없음을 의미합니다.
  - 그러므로 우리는 maximum 값으로 이러한 에러를 조절하려 하고, 그것을 $\alpha$ 라고 합니다.

> ## Definition : Power 

> Definition : power

$$1-P_{\theta} \text { [Type II Error] }=P_{\theta}\left[\left(X_{1}, \ldots, X_{n}\right) \in C\right]$$

The probability on the right side of this equation is called the power of the test at $\theta$. It is the probability that the test detects the alternative $\theta$ when $\theta \in \omega_{1}$ is the true parameter. 

> Note 

- 위에서 Type II 를 minimize 하는것은 power 를 최대화 한다는것을 알 수 있습니다.
- power 는 하지만 $\theta$ 에 의해 값이 계속 바뀌기 때문에, 이 역시 하나의 값 (0.80 ...) 이 아니라 $\theta$ 에 대한 함수로 나타나게 되죠. 

> Definition : powerfunction

We define the power function of a critical region to be

$$\gamma_{C}(\theta)=P_{\theta}\left[\left(X_{1}, \ldots, X_{n}\right) \in C\right] ; \quad \theta \in \omega_{1}$$

> Note : Compare Critical Region

Hence, given two critical regions $C_{1}$ and $C_{2}$, which are both of size $\alpha, C_{1}$ is better than $C_{2}$ if $\gamma_{C_{1}}(\theta) \geq \gamma_{C_{2}}(\theta)$ for all $\theta \in \omega_{1}$. we can obtain optimal critical regions for specific situations. In this section, we want to illustrate these concepts of hypotheses testing with several examples.

> ## Exmple

> Example

Let $X$ be a Bernoulli random variable with probability of success $p$. Suppose we want to test, at size $\alpha$,

$$H_{0}: p=p_{0} \text { versus } H_{1}: p<p_{0}$$

Let $X_{1}, \ldots, X_{n}$ be a random sample from the distribution of $X$ and let $S=\sum_{i=1}^{n} X_{i}$ be the total number of successes in the sample. An intuitive decision rule (critical region) is

$$\text { Reject } H_{0} \text { in favor of } H_{1} \text { if } S \leq k \text {, }$$

where $k$ is such that $\alpha=P_{H_{0}}[S \leq k] .$ Since $S$ has a $b\left(n, p_{0}\right)$ distribution under $H_{0}, k$ is determined by $\alpha=P_{p_{0}}[S \leq k] .$ Because the binomial distribution is discrete, however, it is likely that there is no integer $k$ which solves this equation. For example, suppose $n=20, p_{0}=0.7$, and $\alpha=0.15 .$ Then under $H_{0}, S$ has a binomial $b(20,0.7)$ distribution. Hence, computationally, $P_{H_{0}}[S \leq 11]=0.1133$ and $P_{H_{0}}[S \leq 12]=0.2277 .$ Hence, erring on the conservative side, we would probably choose $k$ to be 11 and $\alpha=0.1133 .$ As $n$ increases, this is less of a problem; see, also, the later discussion on $p$-values. In general, the power of the test for the hypotheses $(4.5 .6)$ is

$$\gamma(p)=P_{p}[S \leq k], \quad p<p_{0}$$

.....

나중에 더 넣을게요~



---

**Reference**

- Hoggs Introduction to Mathematical Statistics 7ed



