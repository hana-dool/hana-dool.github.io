---
title:  "Discrete Time Markoc Chain"
excerpt: "MCMC 이전에 Markov Chain 에 대해서 알아봅시다."
categories:
  - Bayes
last_modified_at: 2021-10-27

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 MCMC 에 대해서 알아보는 Markov Chian 에 대한 모든것을 알아봅시다. 대부분 훈러닝님의 (본명은 밝히지 않겠습니다.) 블로그를 참고했음을 알려드립니다. 볼떄마다 감탄을 금치 못하는 글이에요.. <https://hun-learning94.github.io/posts/bayesian-ml/week3/01-discrete-time-markov-chaine-with-finite-state-space/> 참고! 
{: .notice--warning}

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## MCMC 

- MCMC 의 이름의 의미는 다음과 같습니다.

1. Markov Chain : 어떤 지점에서 다른 지점으로 점프하는 과정을 Markov chain 으로 간주할것
2. Monte Carlo : 그러한 Markov chain 의 랜덤 샘플을 무진장 찍어낼 것 

- 우리는 Markcov chain 중에서 특수한 ergodic 한 마르코브 체인을 이용하여 확률 과정을 만들게 됩니다. 
  - 이러한 체인을 이용하여 '$g(x) \propto f(x)$ 만을 이용해 우리가 알고싶은 $f(x)$' 에 대한 샘플을 형성해 냅니다. 
- 이때에 이러한 MCMC 샘플링의 이론적 토대가 되는것은 다음과 같습니다. 
  - 이산형 시간
  - 취할 수 있는 상태가 Finite
- MCMC 를 정당화 할떄에 이러한 Discrete + Finite 한 마코브 체인을 이용한다는 가정이 숨어있다는것을 명심 해야합니다.
  - 즉 이후에 얘기하는 MCMC 는 모두 DIscrete + Finite 에 대하여 해당되는 이야기입니다! 

> 모수 공간에 대한 MCMC 샘플링의 숨은 가정과 Computing

1. Discrete (countable) 어짜피 컴퓨터는 32 bit / 64 bit 입니다. 즉 한정된 자릿수밖에 처리할 수 없습니다. 
   - 그러므로 실제 모수공간이 연속일지어도, 마치 Grid 처럼 Discrete 한 공간으로 보게 됩니다.
   - 가장 간단하게 Normal 분포를 나타낸다 하더라도 $R$ 에 대한 실수공간에서 나타내는게 아니라, 기껏해야 2^64 개의 실수선 위에서 표현하는것밖에 하지 못합니다. 즉 'Conti' 분포를 Discrete 하게 바라볼 수 밖에 없다는 것이죠. (실제 구현상에서는) 
2. Finite : 연속인 n 차 공간은 무한하지만 사실 컴퓨터로 시뮬레이션하는거여서 컴퓨터가 처리하는 모수 공간은 Finite 하다고 봐도 됩니다. 
   - 이떄에 Finite 정의는 매우 자비롭습니다. 지구상의 모든 분자의 수 또한 Finite 이니까요. 

> ## Random Process

- 확률과정이 뭘까요? 쉽게 말하자면 확률변수에다가 시간으로 인덱스를 붙이면 확률 과정이 됩니다. ($X(t)$) 
  - 만일 이떄 시간이 첫날 , 둘쨰날처럼 이산형이면 Discrete 확률과정이 됩니다. 
  - 만일 이떄 시간이 임의의 실수가 된다면 Continuous 확률 과정이 됩니다. 

$$\begin{align}
\text{Random Process:} &\quad {X_t, t\in J}\\\
\text{Discrete-time:} &\quad \text{J is a countable set, such as $\mathbb{N}$ or $\mathbb{Z}$}\\\
\text{Continuous-time:} &\quad \text{J is an interval on $\mathbb{R}$}
\end{align}$$

- 다음의 예를 보면 좀 쉽게 감이 올 것입니다. 

1. $N(t),t\in [9,16]$ : 오전 9 시부터 오후 4시까지 은행에 방문한 누적손님의 수 
2. $T(t),t\in[0,inf]$ : 서울의 시(hour) $t$ 에 따른 실시간 온도.

# [Discrete Time Markocv Chain](#link){: .btn .btn--primary}{: .align-center}

> ## Discrete Markov Chain

- 마르코브 체인은 어떤 확률 시스템 내에서 '상태' 를 모델링할떄에 아주 많이 쓰게 됩니다. 
  - 어떤 한 시점에서의 상태가 바로 직전 상태 / 또는 이전의 몇단계 까지에만 의존하게 됩니다. 

> Definition (Discrete Markov Chain)

- 이산형 확률과정 $$\{X_n , n\in 0,1,2,...\}$$ 에 대하여 $X_n$ 이 취할 수 있는 값이 $$dom(X_n) = S(countable \ set)$$ 이라고 합시다.
-  이 프로세스가 모든 m 에 대하여 다음의 조건을 만족간다면 이를 Markov Chain 이라고 부릅니다.

$$p(X_{m+1}=j|X_m=i, \underbrace{X_{m-1}=i_{m-1},,…,X_0=i_0}_\text{useless}) = \underbrace{p(X_{m+1}=j|X_m=i)}_\text{transition probability}$$

- 만일 이때에 S 가 유한하다면 우리는 Finite Markov Chain 이라고 부릅니다.

> Note

- $X_n = j$ 라는 것은 n 시기에 상태가 j 에 있다는 의미입니다. 
- $P(X_{m+1} \mid X_m = i)$ 의 의미는 현재 상태가 i 일때 다음 상태가 j 일 확률을 의미합니다.
  - 다른 말로 transition probability 라고 합니다. 
- 마르코브 체인은 현재 상태에서의 transition probability 가 오직 직전 상태에만 의존하는 확률 과정입니다. 즉 이를 이용하면 n 개 까지지의 joint distribution 을 아래와 같이 쓸 수 있습니다. 

$$\begin{align} p(X_n=i_n, X_{n-1}=i_{n-1},…, X_{0}=i_{0}) =& p(X_n=i_n|X_{n-1}=i_{n-1})\\\ &p(X_{n-1}=i_{n-1}|X_{n-2}=i_{n-2})\\\ &…p(X_1=i_1|X_{0}=i_{0})p(X_0=i_0) \end{align}$$

- 즉 위처럼 마르코브 체인은 현재와 과거 또는 현재와 미래 등 오직 쌍으로만 의존하게 됩니다. 
  - 즉 Pairwise dependent 하다고 생각하면 됩니다. 

> Homogeneous

- 이러한 Transition probability 가 시간(m) 에 대해서 변하지 않는다면 우리는 homogenous 하다고 하고, 이를 수식으로는 아래와 같이 쓰게 됩니다.

$$p_{ij} = p(X_{m+1}=j|X_m=i) \quad ^\forall m \quad \text{(i: now, j: next)}$$

> ## transition probability matrix

> Transition probability matrix

- 총 r개의 state 가 있다면 transition probability 도 또한 총 $r \cdot r$ 개 있습니다. 
  - 이걸 한눈에 보기 쉽게 행렬로 쓴 것을 Transition Probability Matrix 라고 부릅니다.

$$P= \begin{bmatrix} p_{11} & p_{12} & \cdots & p_{1r}\\\ p_{21} & p_{22} & \cdots & p_{2r}\\\ \vdots & \vdots & \ddots &\vdots\\\ p_{r1} & p_{r2} & \cdots & p_{rr} \end{bmatrix}$$

- 위의 행렬을 읽을떄에는 열 방향으로 현재의 상태 / 행 방향이 다음 상태라고 해석하면 됩니다. 
- transition matrix 는 다음의 성질을 만족합니다.

1. $1\ge p_{ij}\ge 0$  for all $i,j$
2. $$\sum_{k=1}^r p_{ik} = \sum_{k=1}^rp(X_{m+1}=k|X_m=i)=1$$

- 1번은 확률이므로 매우 당연한 소리입니다.
- 2번은 현재 상태에서 다음 상태 어디로든 가야한다고 받아들이면 될것입니다. 

> Example 

- 다음과 같이 예를 한번 보겠습니다. $S = 1,2,3$ 인 마르코브 체인에서 다음과 같이 Transition matrix 가 주어졌다고 합시다. 

$$P=\begin{bmatrix} 1/3 & 1/3 &1/3\\\ 1/2 & 1/2 & 0\\\ 1/4 & 0 & 3/4 \end{bmatrix}$$

- 이 행렬이 나타내는 Markov chain 을 아래와 같이 그림으로 그려볼 수 있습니다. (이러한 그림을 state transition diagram 이라고 합니다.)

![png](/assets/images/Stat/87_1.png)

- 위의 그림을 보면 각 노트가 상태 / 화살표는 전환 확률을 의미합니다.

> Relation with Markov chain

- 그러면 위와 같은 Transition Probability 가 Markov chain 과 어떤 관계일까요? 
- Markov chain 은 '바로 이전 단계' 에만 영향을 받는 확률 과정입니다.
- 즉 위처럼 '다음 단계의 행동 확률을 모두 나타내는' Transition probability 는 Markov chain 그 자체라고 볼 수 있습니다. 
- 그러므로 Markov Chain 과 Transition probability 는 1:1 대응(bijection)되는 관계라고 생각할 수 있습니다.

> ## State Probability Distributions

> One step transition probabilities

- Markov chain 에서 우리가 궁금한것은 어떤 시점일때 상태분포입니다.
- 예를 들어서 확률과정 $\{X_n , x= 0,1,2..\}$ 의 state space 가 $X_n \in S = \{1,2...,r\}$ 이라고 하겠습니다. 
  - 이때 처음 시점 $(n=0)$ 에서의 확률 과정이 어떤 상태를 취하는지가 궁금할것입니다. 이 분포를 다음과 같이 써보겠습니다. 

$$\pi(0) = \begin{bmatrix} p(X_0=1) & p(X_0=2) & \cdots & p(X_0=r) \end{bmatrix}$$

- 그러면 다음시기 $n=1,2,...$ 에서 $\pi(1),\pi(2)$.. 는 어떻게 구할 수 있을까요? 	
  - 전사건의 법칙을 이용하면 $P(X_1 = j)$ 를 다음과 같이 나타낼 수 있습니다.

$$\begin{align} p(X_1=j) &= \sum_{k=1}^r p(X_1=j|X_0=k)p(X_0=k)\\\  &= \sum_{k=1}^r p_{kj}p(X_0=k) \end{align}$$

- 그러므로 확률분포 $\pi(1)$ 은 다음과 같이 간단한 벡터와 행렬의 곱으로 나타낼 수 있습니다. 

$$\begin{align} \pi(1) = \pi(0)P  =&\begin{bmatrix} p(X_0=1) & p(X_0=2) & \cdots & p(X_0=r)  \end{bmatrix} \begin{bmatrix} p_{11} & p_{12} & \cdots & p_{1r}\\\  p_{21} & p_{22} & \cdots & p_{2r}\\\  \vdots & \vdots & \ddots &\vdots\\\  p_{r1} & p_{r2} & \cdots & p_{rr} \end{bmatrix}\\\  =& \begin{bmatrix} p(X_1=1) & p(X_1=2) & \cdots & p(X_1=r)  \end{bmatrix} \end{align}$$

- 이를 이용하여 $\pi(2)$ 도 간단하게 쓸 수 있습니다.

$$\pi(2) = \pi(1)P = \pi(0)P^2$$

- 즉 이를 일반화 하면 다음과 같이 쓸 수 있습니다.

$$\pi(n+1)=\pi(n)P, \quad ^\forall n=0, 1,2,…\\\  \pi(n)=\pi(0)P^n,  \quad ^\forall n=0, 1,2,…$$

> n-step transition probabilities

- 아까 보았던 $P$ 와 $p_{ij}$ 는 기간이 하나 넘어갈떄의 전환 확률입니다. 
- 그렇다면 2단계 전환 확률은 어떻게 구할 수 있을까요? 
  - 이 역시 전사건 법칙과 Markov 성질을 이용하게 됩니다.

$$\begin{align} p_{ij}^{(2)}=p(X_2=j|X_0=i)&=\sum_{k\in S}p(X_2=j|X_1=k,X_0=i)p(X_1=k|X_0=i)\\\ &=\sum_{k\in S}p(X_2=j|X_1=k)p(X_1=k|X_0=i)\\\ &=\sum_{k\in S}p_{kj}p_{ik} \end{align}$$

- 이떄에 자세히 보면 $p_{ij}^{(2)}$ 는 전환행렬 $P$ 에서 j 번쨰 열과 i 번쨰 행의 내적입니다.
  - 그러므로 2단계 전환행렬 $P^{(2)}$는 아래와 같습니다.

$$P^{(2)}=  \begin{bmatrix} p_{11} & p_{12} & \cdots & p_{1r}\\\  p_{21} & p_{22} & \cdots & p_{2r}\\\  \vdots & \vdots & \ddots &\vdots\\\  p_{r1} & p_{r2} & \cdots & p_{rr} \end{bmatrix} \begin{bmatrix} p_{11} & p_{12} & \cdots & p_{1r}\\\  p_{21} & p_{22} & \cdots & p_{2r}\\\  \vdots & \vdots & \ddots &\vdots\\\  p_{r1} & p_{r2} & \cdots & p_{rr} \end{bmatrix}=P^2$$

- 쉽게 우리는 이를 n 단계로 확장할 수 있음을 알 수 있습니다. 이를 Chapman- kolmogrov equation 이라고 합니다. 

> Champman-Kolmogrov Equation

$$\begin{align} p_{ij}^{(m+n)}& = p(X_{m+n}=j|X_0=i)=\sum_{k\in S}p_{ik}^{(m)}p_{kj}^{(n)}\\\  P^{(n)}&=P^n \end{align}$$

> ## Classification of States

- 마르코프 체인의 몇가지 정의를 더 알아봅시다. 

> Accessible 

- 상태 $i,j$ 에 대해서 $p_{i,j}^{(n)}>0$ 이면 j 는 i 에서 accessible 하며 $i\to j$ 라고 쓰게 됩니다.

> Communicate 

- 상태 $i,j$ 에 대해서 $i\to j$ , $j \to i$ 이면 communicate 하다고 하며 $i \leftrightarrow j$ 라고 씁니다.

> Communicate Class

- 이떄에 communication oprator $\leftrightarrow$ 는 수학에서의 equivalance relation 이 성립하게 됩니다. 
  - 모든 상태는 스스로와 communicate: $j\leftrightarrow i$
  - $i\leftrightarrow j $ 이면 $j \leftrightarrow i$ 
  - $i \leftrightarrow j $ 이고 $ j \leftrightarrow k$ 이면 $ i \leftrightarrow k$ 
- 이렇게 Communicate 가 equivalance relation 이기 떄문에 우리는 서로 communicate 한 상태들만 모으는 형식으로 Markov chain 을 communicating class 로 분류할 수 있습니다! 
  - equivalance class 이기때문에, chain 을 분할(partition) 할 수 있기 떄문입니다.

> Example 

![png](/assets/images/Stat/87_2.png)

- 위와 같은 그래프가 있다고 합시다. 이 경우에 communicate 한 관계만 묶어본다면 아래의 그림과 같아집니다.

![png](/assets/images/Stat/87_3.png)

- 위 그림에서는 총 4개의 communicate class 가 있다는것을 알 수 있었습니다! 
- 계~속 돌리다 보면 우리는 특정한 markov chain 의 class 에 결국 고이게 될 것입니다!

> ## Irreducible Markov Chain

> irreducibility 

- 전체 마르코프 체인이 하나의 Class 에 속할떄에 우리는 Irreducible 이라고 합니다. 
- 즉 마르코브 체인의 모든 상태들이 서로 Communicate 한 경우에 irreducible 이라고 합니다.
- 수식으로는 다음과 같이 쓸 수 있습니다.

$$^\forall i,j \in S, ^\exists m<\infty \quad s.t.\quad p(X_{n+m}=j|X_n=i)>0$$

- 쉽게 말하면, 어느 위치로나 갈 수 있는 있다는것을 의미한다고 볼 수 있겠네요.

> Note

- 왜 이름이 irreducibility 일까요? 
  - 이전의 예시에서처럼 Class 가 여러개일 경우에, 어쩌다 한 클래스에 빠져버리면 다시는 나올 수 없게됩니다. 
  - 즉 마르코프 체인이 도달하는 상태가 몇개의 클래스로 reduce(환원) 될 수 있다는 것입니다. 
- 만일 모든 상태가 같은 클래스에 속하면 이런일이 없고 이는 '언제 어디서든, 어디로나 갈 수 있다' 가 되며 , 이게 바로 irreducible 의 의미가 됩니다.

> ## Reccurrent / Transient Markov chain

![png](/assets/images/Stat/87_3.png)

> Recurrent 

- Markov chain 에서 Class 4 로 빠지게 되면 다시는 나올 수 없습니다. 
- 좀 유하게 말하면, 한번 특정한 클래스에 들어오게 된다면 나중에 언젠가 반드시 이 클래스로 다시 들르게 됩니다.
- 이러한 Class 에 속하는 상태를 reccurent 하다고 합니다. 

> transient

- 한번 그 클래스에 들어왔다고 해서, 다시 또 그 클래스를 찾아들어갈 수 있다는 것을 보장할 수 없는 클래스를 transient 하다고 합니다. 
- 즉 다르게 말하면 transient한 상태는 어떤 시점M(i)이 있어 그 시점을 지나면 다시는 마코브 체인이 절대로 그 상태로 다시 돌아오지 않는다 ! 라고 생각할 수 있겠지요.

> Note

- 한 클래스에 있는 노드는 모두 communicate 합니다. 즉 한 노드가 Reccurent 하거나 또는 Transient 하게 된다면 클래스 전체가 reccurent / Transient 하게 됩니다. 
- 또한 위의 예제에서도 보듯이, markov chain 은 transient 클래스와 recurrent 클래스가 같이 있을 수 있습니다.
- 위의 정의들을 수식으로 나타내면 다음과 같습니다. 

$$f_{ii} = p(X_{0+k}=i, \text{for some } k> 0|X_0=i) \begin{cases} =1 &\quad \text{state $i$ is recurrent}\\\  <1 &\quad \text{state $i$ is transient} \end{cases}$$

- reccurent 하다는것은 '언젠가는 반드시 돌아온다' 는 의미이므로 1의 값을 가집니다.
- transient 는 '언젠가 반드시 돌아온다는 보장이 없다' 는 의미이므로 1보다는 작습니다.  

> Note

- State space가 유한한 경우 적어도 하나의 클래스는 Recurrent합니다. 
  - 모든 상태가 transient하다는 것은 어떤 큰 수 M이 있어 그 시점을 넘어가면 그 어떤 상태에도 다시 돌아가지 않는다는 것인데, 이는 모순이기 때문입니다.

> Conclusion

- finite state space에 대해서는, 적어도 하나의 recurrent class가 존재하고, 마코브 체인이 무한히 지속될수록 결국 확률과정의 상태는 그 recurrent class 안에서만 머무른다는 것을 알았습니다.
- 그렇다면 확률과정이 모든 노드를 다 지나게 하려면, 모든 노드가 하나의 recurrent한 클래스에 속해야 한다. 즉 irreducible해야 한다. 
  - 이때에 위의 예시를 irreducible하게 만들려면 어떻게 해야할까? 
  - 아래 그림처럼 각각의 클래스를 서로 이어주는 화살표를 그려, 모두 하나의 class가 되도록 하면 된다.

![png](/assets/images/Stat/87_4.png)

- 이 새로운 마코브 체인을 시뮬레이션하면 다음과 같다. 100번 넘어가는 동안 모든 상태를 골고루 누비는 것을 알 수 있다. 이런 마코브 체인을 “irreducible"하다고 한다. 
- 즉 irreducible 한 markov chain 에서 모든 상태는 하나의 reccurent 한 communication class 에 속한 것이라고도 말할 수 있는것입니다.

> ## Periodic

![png](/assets/images/Stat/87_5.png)

- 위 예시를 다시 생각해봅시다.
- 각각의 상태에 대해서 몇번 화살표를 건너가야지 자기 자신으로 돌아올 수 있을까? 를 생각해봅시다. 
- 수식으로 쓰면 우리는 각 상태에 대해서 다음과 같이 숫자 n 을 생각하고 있는것입니다. 

$$n_i \ s.t. \ p_{ii}^{(n)}>0$$

- 먼저 상태 1을 보면 $1\to 2 \to 1$ 혹은 $1 \to 2 \to 2 \to 1$ 의 경로를 거쳐야 합니다. 즉 $n_1= 3,4$ 가 가능합니다. 

> Period of state i

- 이제는 다음과 같이 $d(i)$ 를 periodic 이라고 정의할 수 있습니다.   

$$d(i) = gcd \Big(n_i \text{ s.t. }  p_{ii}^{(n)}> 0 \Big)$$

> Periodicity 

- 어떤 상태 i 에 대하여 
  - $d(i) = 1 $ 이면 aperiodic
  - $d(i)>1$ 이면 periodic 
- 이게 어떤 의미인지 이해하기 위해서는 , $d(i) >1$ 의 의미를 잘 살펴야 합니다. 
- $d(i)>1$ 이라는 의미는 결국에 현재 상태가 i 일때 적어도 다음 상태는 i 가 아니라는것을 확정적으로 아는것입니다. 
  - 즉 현재 상태에 따라 가음 상태가 적어도 뭐가 아닌지를 정확히 알 수있다면, 이러한 Markov chain 에 대해서는 특정한 주기가 있다고 이해할 수 있습니다. 
- $d(i) =1$ 이라는 의미는 현재 상태가 뭐든 간에, 다음 상태로는 모든것이 가능하다는 의미입니다. 
  - 즉 주기성이 없다고 할 수 있을것입니다.

> communication class

- 또한 중요한 성질은  communication class 안의 모든 상태는 주기가 같다는 것입니다. 
  - <https://math.stackexchange.com/questions/112057/show-that-two-states-in-the-same-communicating-class-of-a-markov-chain-must-have>
  
- 이제 state space가 유한하고 irreducible 한 마르코브 체인에 대해서 생각해 봅시다.
  - state space 가 finite 하므로 어떤 클래스는 reccurent 할 것입니다. 
  - 또한 irreducible 하므로 모든 상태가 reccurent 한 하나의 클래스에 속할것입니다.
- 이때 한가지 조건 $d(i)=1$ 만 추가하면 매우 유용한 aperiodic 한 Markov chain 이 됩니다. 

- state space가 유한하고 irreducible한 (homogeneous) 마코브 체인에 한해서, aperiodic하다는 것은 곧 transion matrix P가 0인 원소가 있어도 계속 곱하다보면 결국 $P^n$의 모든 원소는 0보다 크다는 것과 동치가 됩니다.
  - 이를 엄밀히 증명하려면 정수론에서 증명할 수 있습니다.
  - [http://faculty.cs.tamu.edu/klappi/csce658-s18/markov_chains.pdf](http://faculty.cs.tamu.edu/klappi/csce658-s18/markov_chains.pdf)
- state space 가 유한하고, irreducible 한 markov chain 에 대해서는 직관적으로 이해할 수 있습니다.
  - $P^m$ 이라는것은 $P$ 에 대해 m번 움직일떄에 $i \to j$ 일 확률의 행렬입니다.
  - 만일 마르코브 체인이 periodic 하면 모든 상태 ($d(i) = 2$) 라는 것이고 그러면 화살표를 어떻게 타든 결초 도달할 수없는 부분이 있다는 것입니다.
  - 하지만 그에 비해서 $d(i)=1$ 이라는 것은 결국 한번에 두개/세개씩 타다 보면 다른상태에서 다른상태로 한번에 도달할 수 있다는 의미가 됩니다. 
  - 왜냐하면 어쩃든 자기 자신으로 쭈루룩 되돌아오기를 계속 반복하면서, 횟수를 맞출 수 있기 떄문입니다. (gcd 가 1 인 경우(서로소) 이면 어쩃든 저쩃든 덧셈을 통해 일정한 값 이상의 모든 자연수를 표현할 수 있기 떄문입니다.) 

> Example

![png](/assets/images/Stat/87_6.png)

- 위 두개의 Markov chain 모두 finite space 에 irrducible 입니다. 
  - 하지만 MC(1) 에서는 모든 상태의 d(i)  = 4 이고 MC(2) 의 경우는 d(i) = 1 입니다.
  - MC(2) 는 시간이 충분히 지나고 나면 모든 원소가 0 보다 큰 상태로 수렴되지만 (즉 어디든 갈 수 있는 확률이 보장된 상태) MC(1) 은 그러지 못할 것입니다 ! 

> Why? 

- 우리는 왜 이렇게 irreducible , aperiodic 에 집착했을까요? 나중에 말하겠지만, 우리는 '모든 State' 를 자유롭게 탐색할수 있는 좋은 Markov chain 을 원하고 있는 상태입니다. 이러한 Markov chain 을 얻기 위해서는 ireducible 과 aperiodic 은 필요한 조건이였던 것입니다.

> ## Ergodic 

> **Definition (Irreducible and Aperiodic MC)**

- state space가 유한하고, homogeneous한 이산형 마코브 체인에 대하여,

1.  모든 상태가 하나의 communication class 에 속해있으며 (irreducible) (혹은 $$^\forall i,j \in S, \;^\exists m<\infty \quad s.t.\quad p(X_{n+m}=j \mid X_n=i)>0$$)
2.  모든 상태의 주기가 $d(i)=1$ 이면(aperiodic) (혹은 $ ^\exists n \quad s.t.\quad p_{ij}^{(n)} > 0 \quad ^\forall i,j\in S$  )

- 이러한 마르코므 체인을 irreducible 이고 Aperiodic 하다고 합니다. 
  - 또한 state space 가 유한할떄에는 위 두 조건을 만족시키면 Ergodic 하다고 합니다.
- 이러한 Ergodic chain 은 모든 상태를 뛰어놀 수 있는 chain 이 됩니다.

> ## Stationary and Limiting Distribution

- 증명이나 간략한 직관은 없애고 여러 정리를 제시하겠습니다. 
- 이제 우리의 관심은 Marcov chain 의 Long term behavier 입니다. 
  - 즉 $$n \to \infty$$ 일때 finite 한 state space 에서의 분포에 관심이 있습니다.

$$\pi^{(n)} = \begin{bmatrix} p(X_n=0)&p(X_n=1)&\cdots&p(X_n=r) \end{bmatrix}$$

- 이러한 분포를 우리는 Limiting distribution 이라고 합니다. 

> Definition (limiting distribution)

- 다음의 조건을 만족하는 분포 $\pi= \begin{bmatrix} \pi_0& \pi_1&\cdots&\pi_r \end{bmatrix}$ 를 limiting distribution 이라고 합니다. 

1.  $\pi_j = \lim_{n\to \infty}p(X_n=j \mid X_0=i) \quad ^{\forall}i,j\in S$
2.  $\sum_{j\in S}\pi_j =1$

> How to find limiting distribution? 

- 그렇다면 state space가 유한하고 homogeneous한 이산형 마코브 체인에서 이러한 극한 분포를 어떻게 찾을 수 있을까? 일단 다음의 사항을 고려하자.
  - state space가 유한하다는 것은 적어도 하나의 recurrent한 class를 가지고 있다는 말이다.
  - 이때 마코브 체인이 irreducible하다면 모든 상태가 하나의 recurrent한 class에 속해 있다는 말이다. 즉 **모든 상태에 언젠가 한 번씩은 꼭 들른다.**
  - 이때 마코브 체인이 aperiodic하다면 어떤 상태에서도 아무 상태에나 갈 수 있다는 말이다. 즉 **현재 i에 있으면 다음에는 절대 j로 못 가는 그런 일은 없다.**
- 직관적으로 생각해볼떄, Markov chain 이 이러한 조건을 만족하면, 마르코프 체인을 계속 시핼할떄 마코브 체인이 한 상태에 있을 장기 빈도($1/V_n(i) (n \to \infty)$))가 그 상태의 극한 확률 $\pi_i$ 에 수렴할것이라고 생각할 수 있습니다.
  - Note : $V_n(i)$ 는 n 번 움직일때 i 를 들르는 수 
- 그러므로 극한 분포를 찾고 싶다면 그냥 마코브 체인을 계속 실행하여 장기 빈도를 구하면 됩니다. 

> More detale

- 이떄 정확히 말하면 유한한 state space 에서는 irreducible 하기만 하면 모든 상태가 하나의 reccurent class 에 속하기 떄문에 극한분포는 다음과 같이 **유일하게** 존재함을 보일 수 있다.

$$\lim_{n\to\infty}\dfrac{V_n(i)}{n}= \pi_i \quad ^\forall i\in S$$

- 다만 여기에서 마코브 체인이 aperiodic하기까지 한다면, 이 극한분포는 다음과 같이 구할 수 있다.

$$\lim_{n\to\infty} p_{ji}^n= \lim_{n\to\infty} p(X_n=i|X_0=j) =\pi_i \quad ^\forall i,j\in S$$

- 이것을 전환행렬 $P$ 를 이용해 나타내면 다음과 같습니다.

$$\pi = \lim_{n\to\infty}\pi(n) = \lim_{n\to\infty}[\pi(0)P^n] \quad \text{for any $\pi(0)$}$$

- 즉 그냥 극한분포 $\pi$ 를 찾으려면 $P$ 행렬을 무진장 엄청 곱하면 됩니다.
  - 하지만 이게 쉬운일은 아니라서 트릭을 이용해 극한분포를 구하는 방정식을 찾을 수 있습니다.

> ## Find Limiting distribution

> Stationary distribution

- 다음의 조건을 만족하는 분포 $\pi= \begin{bmatrix} \pi_0& \pi_1&\cdots&\pi_r \end{bmatrix}$ 를 $P$ 가 정의하는 마르코프 체인의 stationary distibution 이라고 합니다. 
  - $\pi P = \pi$
  - $\sum_{j\in S}\pi_j =1$
- finite state space에서 stationary 분포는 유일하지 않을 수 있습니다.
- 예컨대 recurrent class가 여러 개 있다면, 여러 recurrent class 중에 어느 곳에 빠지게 되냐에 따라 stationary distribution이 다를 것이다. 
- **그러나 만일 마코브 체인이 irreducible하면 stationary 분포는 유일하게 존재한다.**

> FInding Limiting distribution

- 이제 다음과 같은 논리에 따라 극한분포를 구하는 방정식을 유도해보자. finite state space에 irreducible하고 aperiodic한 마코브 체인에 대해서는 다음과 같은 로직이 성립합니다.

1. 극한분포가 유일하게 존재하며, 그게 곧 stationary 분포이다. (하나의 분포로 수렴하니까)
2. stationary 분포도 유일하게 존재한다.
3. 때문에 stationary 분포를 구하면 그것이 바로 극한분포이다!

- 즉 우리는 transition matrix P를 무진장 곱하지 않고도 위의 방정식 πP=P을 만족하는 π만 구하면, 그게 극한 분포라고 확신할 수 있는 것이다. **(누누이 말하지만 이게 가능한 이유는 우리가 finite state space에 irreducible하고 aperiodic한 마코브 체인에 대해서만 말하고 있기 때문이다!)**
- 이제 우리는 극한분포를 구하기 위해서는 다음의  $r$ 개의 방정식을 풀면 됩니다.

$$\begin{align} \pi_j &= \sum_{k\in S}\pi_k p_{kj} \quad ^\forall j\in S={1,2,…,r}\\\ \sum_{j\in S}\pi_j&=1 \end{align}$$

- 근데 참… 이것도 말은 쉽지 이걸 다 푸는게 또 일이다. 그래서 또 간단한 트릭을 사용한다. 일단 다짜고짜 다음의 정의를 생각해보자.

> Reversibility (Detailed Balance Equation)

- 마르코브 체인 $\{X_n, n=0, 1, 2,…\}$ 이 stationary distribution $\pi$ 를 가진다고 합시다.
- 그렇다면 이떄 다음의 방식을 detailed balance equation 이라고 하며, 이를 만족하는 마르코프 체인을 $\pi$ 에 대하여 reversible 하다고 합니다. 

$$\pi_i p_{ij} = \pi_jp_{ji} \quad ^\forall i,j\in S$$

> Meaning

- 처음 초기 분포가 $\pi(0)= \pi$ 라고 합시다. 그러면 $\pi_i p_{ij} $ 는 i 에서 j 로 흐르는 확률의 양을 나타냅니다. $\pi_jp_{ji}$ 는 j 에서 i 로 흐르는 확률의 양을 나타낸다고 할 수 있습니다.  
- Detailed balance 란 모든 노드에서 흘러들어오는 확률의 양과 흘러 나가는 확률의 양이 같다는 이야기입니다. 그러므로 이것을 만족하는 Markov Chain 을 Reversible 하다고 합니다.

> Relation with Stationary distribution

- 위와 같은 Detailed Balance Equation 은 $\pi P = \pi$ 보다 훨씬 빡센 조건입니다. 
- $\pi P = \pi$  는 r 개의 방정식으로 이루어져 있는 반면에 detailed Balance 방정식은 S 에 대한 모든 i,j 쌍에 대해서 성립해야 합니다. 즉 ${r \choose 2}=\frac{r(r-1)}{2}$ 개의 방정식이 나오게 됩니다. 
- 그러므로 Stationary 분포가 존재하는 Markov chain 에 대해서 위의 detailed balance equation 의 해가 존재하면, 그것이 바로 stationary distribution 일 것입니다. 
- 이를 직접 수식으로 보이기 위해서는, 양변을 각각 i 에 대해서 합치면 $\pi P = \pi$ 임을 알 수 있습니다. 

$$\sum_i \pi_i p_{ij} = \sum_i \pi_jp_{ji} = \pi_j \sum_i p_{ji}= \pi_j$$

> Example

![png](/assets/images/Stat/87_10.png)

- 화살표로 이어진 마코브 체인에서 각 노드를 서울시의 구, 화살표를 각 구를 잇는 도로라고 생각해보자. (irreducible 하므로 모든 구가 적어도 하나의 다른 구와 왕복 도로로 연결되어 있다.) 
- stationary 분포가 존재할 조건은 global balance라고도 하는데, 이는 차들이 쌩썡 지나다니다 보면 어느 순간부터는 모든 시점에서 **각 지역구에 있는 차들의 수가 변하지 않는다**는 의미이다. 
- 여기에다가 detailed balance까지하려면, 두 지역구를 잇는 **모든 도로에서 들어오는 차의 수와 나가는 차의 수가 같다**는 거다. 
- 그림으로 이해해보자. 위의 두 경우 모두 서대문구를 지나는 차의 수는 일정하다. 그러나 오른쪽의 그림에는 서대문구를 지나는 차의 수도 일정하고, 종로구와 마포구에 난 도로를 진입하고 진출하는 차의 수까지 일정하다. 그러니 Detailed balance가 더 강력한 조건이다!
- 극한분포 구하는데 2 (global balance)에서 3(detailed balance)으로 가면 식이 더 많아지니 굳이 이런 수고를 해야 하나 싶을 것이다. 그러나 우리가 공을 들여서 3을 말한 데에는 이유가 있다. MCMC를 하기 위해서이다.

> ## MCMC : Intuition

> Insight

- 지금까지 우리는 어떤 마코브 체인에서 $P$를 알 때 극한분포 $\pi$를 어떻게 구할 수 있는지 알아봤으며, 지난 섹션에서 결국 detailed balance 방정식의 해가 바로 $\pi$인 것을 배웠습니다. 
- 근데 이걸 반대로 생각할 수 있다. **어떤 분포 $\pi$ 를 극한분포로 가지는 마코브 체인을 어떻게 만들 수 있을까?** 마코브 체인을 만든다는 것은 곧 전환행렬 P를 만든다는 것이다. π를 알 때 어떻게 P를 만들어야 하는가! 

> How to?

- Assumption
  - 일단 $\pi$가 이산형이고 유한한 공간에서 정의된 확률분포라는 가정이 있어야 한다. 그래야 위에서 말한 finite space 마코브 체인의 성질을 이용할 수 있으니까. 
  - 서두에서 말했지만 어차피 64비트 컴퓨터로 시뮬레이션을 하기 때문에 크게 무리가 있는 가정은 아니다. 
- 이제 우리는 마코브 체인이 irreducible하고 aperiodic하며, 극한분포가 $\pi$가 되도록 전환행렬 P를 만들어야 한다.
- 그럼 앞서 논의한 1, 2, 3을 거꾸로 타고 올라갈 수 있다. 
  - 일단 내가 원하는 분포 $\pi$에 대해서 다짜고짜 detailed balance equation의 해가 되도록 $p_{ij}$를 만들자. 
  - 그러면 이 $p_{ij}$는 $\pi$에 대해 Reversible한 마코브 체인을 정의하며, $\pi$는 이 마코브 체인의 stationary 분포라는 것을 알 수 있다. 
  - 그렇다면 이제 남은 것은 이 마코브 체인이 실제로 ergodic함을 보이는 것이다.
- 요컨대, 어떤 분포$\pi$를 유일한 극한분포로 하는 마코브 체인을 만들기 위해서는, 전환행렬 $P$가 다음의 조건을 만족해야 한다.
  - P가 정의하는 마코브 체인은 **ergodic(irreducible and aperiodic)하다.** 즉 state space를 골고루 잘 돌아다닌다.
  - P가 정의하는 마코브 체인의 극한분포는 $\pi$이어야 한다.
- 2의 조건은 $\pi$에 대하여 detailed balance 방정식을 풀면 “충분히” 만족할 수 있다. 
  - 문제는 1인데, 우리는 detailed balance의 해인 P가 ergodic함을 보여야 한다. 
- 증명은 보이지 않겠으나, 만일 모든 상태에 대하여 $p_{ij}$와 $\pi_i$모두 양수라면, $\pi$를 stationary 분포로 가지는, P로 정의된 마코브 체인은 ergodic함이 알려져 있다. 자세히 쓰자면,

> Fundamental Thm

*(Leo Breiman. The strong law of large numbers for a class of markov chains. The Annals of Mathematical Statistics, 31(3):801–803, 1960)*

If a homogenous Markov chain on a finite state space with transition probabilities $T(x,x′)$ has $\pi$ as an invariant distribution and

$$v = \min_{x}\min_{x':\pi(x')>0} T(x, x')/\pi(x') >0$$

then the Markov chain is erogic, i.e., regardless of the initiai probabilities $p_0(x)$.

$$\lim_{n \to \infty} p_n(x) = \pi(x)$$

> Insight

- 실제로 마코브 체인을 사용하여 상수배를 모르는 어떤 확률분포 $p(x)$에서 샘플링을 할 때, state space안에서 pdf는 왠만하면 0보다 클 것이고, 전환확률도 0보다 크도록 만들면, 위의 조건은 큰 문제없이 지켜질 것이다.
- 때문에 MCMC 알고리즘을 만들때 가장 중요한 것은 목표확률분포 $p(x)$ 에 대하여 detailed balance 를 만족하는 전환확률 $p_{ij}$ 를 만드는 것이며 이것을 어떻게 만드느냐에 따라서 MCMC 방법이 갈립니다.

**Reference**

- <https://hun-learning94.github.io/posts/bayesian-ml/week3/01-discrete-time-markov-chaine-with-finite-state-space/>
- <https://www.youtube.com/watch?v=VegQC7oCZlc>

다시한번 밝히지만 이 글은 Hunlearning 님의 강의 유튜브와 블로그 + 연세대학교 ESC 통계학회 세션 을 가져왔음을 밝힙니다. 이렇게까지 MCMC를 자세하게 알려주고 이해시켜주는 Article 은 영문 Article 을 포함하더라도 훈러닝 님의 글이 유일합니다. 다시한번 Hunlearning 님에게 감사를 표합니다! 
{: .notice--success}

