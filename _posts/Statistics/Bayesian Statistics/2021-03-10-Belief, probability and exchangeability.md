---
title:  "Belief, probability and exchangeability"
excerpt: "베이즈의 추론이 가능한 이유를 정당화 해보자"
categories:
  - Bayes
last_modified_at: 2021-03-10

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [Belief functions and probabilities](#link){: .btn .btn--primary}{: .align-center}

> ## Belief function

- $F$, $G$, $H$ 를 Overlap 을 허용하는 statements 들이라 하자. 예를들면
  - $F$ = { 미분기하를 C- 받은사람 } 
  - $G$ = { 통계학을 복수전공한 사람 }
  - $H$ = { 전공학점이 4가 넘는사람 }
- 위와 같은 특성들은 겹칠 수 있다. $Be$ 를 belief function 이라고 정의하자. 이 함수는 $Be : statesment \to \mathbb{R}$ 로서, 그 값이 높을수록 높은 Beilief 를 나타나게 된다. 
- 예를 들어보자. $Be(F) > Be(G)$ 는 일반적으로 G 보다 F 가 더 맞을 확률이 높다는 뜻이다.
- 또는 다음과 같이 말할 수 있다. $Be(F \mid H) > Be(G \mid H)$  는 H 가 사실일때에 F 가 True 일 확률이 G 가 True 일 확률보다 높다는것이다.

> ## **Axiom of beliefs**

- 다음과 같은 성질들을 만족해야 Belief 라고 말할 수 있다.

- **B1** : $\text{Be}(\text{not H} \mid \text{H}) \leq \text{Be}(\text{F}\mid\text{H}) \leq \text{Be}(\text{H}\mid\text{H})$
  - 이는 해석하기 쉽다. H 를 가정한 상태라면 당연히 not H 가 제일 적은 Belief 값을 가져야 하고, H 가 제일 높은 Belief 값을 가져야 할 것이다.
- **B2** : $\text{Be}(\text{F or G} \mid \text{H}) \geq \text{max}({\text{Be}(\text{F} \mid \text{H}) , \text{Be}(\text{G}\mid\text{H}))} $ 
  - 두 사건(F,G) 를 Union 하였을때는 당연히 각각의 F,G 의 사건보다는 크므로 높은 Belief 값을 가져야 한다.
- **B3** : $\text{Be}(\text{F and G} \mid \text{H})$ 는 $\text{Be}(\text{G}\mid\text{H})$ 와 $ \text{Be}(\text{F}\mid\text{G and H})$ 를 통해서 계산 가능
  - H 를 가정하였을 때에 F 와 G 가 True 인지 알아보고 싶다고 하자. 먼저 H 를 가정하고 G 가 True 인지 검사한다. 만약 True 라면 사실로 밝혀진 H와 G를 가정하고 F 가 사실인지 살펴보자. 그러면 우리가 원래 구하고자 하는 값을 구하게 되는셈이다.

> ## Axiom of Probability

- 위 성질을 정의하고 나면 너무나 반갑게도 Probability는 Belief 의 성질을 만족하게 된다. 이때 $F \cup G$ 는 F or G, $F \cap $G 는 F and G 를 의미함을 기억하자.
  - **P1** : $0 = \text{Pr}(\text{not H}\mid \text{H}) \leq \text{Pr}(\text{F}\mid\text{H}) \leq \text{Pr}(\text{H}\mid\text{H}) = 1$

  - **P2** : $ \text{Pr}(\text{F} \cup \text{G} mid \text{H}) = \text{Pr}(\text{F} \mid \text{H}) + \text{Pr}(\text{G} \mid \text{H}) \ \ \  \text{if F} \cap \text{G} = \emptyset $ 

  - **P3** : $\text{Pr}(\text{F} \cap \text{G} \mid \text{H}) = \text{Pr}(\text{G}\mid \text{H})\text{Pr}(\text{F} \mid \text{G} \cap \text{H})$

- 야호~ 이제 Probability 가 axiom of belief 의 성질을 만족함을 알았다! 그러므로 우리가 Belief 를 Probability 로 나타내도 된다는 정당성을 확보한 셈이다.

# [Independent and Exchangeability](#link){: .btn .btn--primary}{: .align-center}

> **independent random variable**

- $Y_1 .... Y_n$ 을 Random variable 이라 하고,  $\theta$ 를 parameter describing the conditions under which the random variables are generated 이라 하자.
- 우리는 $Y_1 .... Y_n$ 가 모든 n 개의 set $\{A_1...A_n\}$ 에 대해 $Pr(Y_1 \in A_1 .... Y_n \in A_n \mid \theta) = \prod Pr(Y_i \in A_i \mid \theta) $ 를 만족한다면  conditionally independent given $\theta$  라 한다. 
- 이때에 이 독립변수인 $Y_i$ 들에 대해서 indenpendent 이면$ Pr(Y_i \in A_i \mid \theta, Y_j \in A_j) = Pr(Y_i \in A_i \mid \theta)$ 인것을  기억하자 
  - 이를 어떻게 해석할 수 있을까? 이는 $\theta$ 를 알고있을때 $Y_j$ 는 $Y_i$ 에 대해 아무런 정보를 줄 수 없다는것을 의미한다.  
- 이제 pdf 에 대해서 생각해보자. 이 역시 위와같이 $p(y_1, …, y_n\mid \theta) = p_{Y_1}(y_1\mid \theta) \times … \times p_{Y_n}(y_n\mid \theta) = \prod^n_{i=1}p_{Y_i}(y_i \mid \theta)$ 일때에$\{y_1. .. y_n\}$ 은 conditionally independent given $\theta$ 가 된다. 
  - 만약 $\{y_1. .. y_n\}$ 가 비슷한 조건 하에서 실행되었다고 하자. 
  - 그렇다면 $y_i$ 끼리는 전해줄 정보가 없으므로  $p(y_1, …, y_n\mid \theta) = \prod^n_{i=1}p_{Y_i}(y_i \mid \theta)$  가 성립하게 된다. 이를 conditionally independent and iid 라고 한다. 

> ## **Exchangeable**

- Let $p(y_1 .... y_n)$ be the joint density of $Y_1 .. Y_n$. If $p(y_1, …, y_n) = p(y_{\pi_1}, … , y_{\pi_n})$ for all permutation $\pi$, then $Y_1 ... Y_n$ are exchangeable
- 즉 $y_i$ 에서 label i 가 outcome 에 대해 아무런 정보가 없다면 Exchangable 이라 한다. 아래 예시에서 그 Example 을 살펴보자.

> Example

- 어떠한 Survey 에서 참가자들이 행복한지, 안행복한지에 대해서 질문을 받았다고 하자. 그러면 i 번쨰 참가자에 대해서 r.v. 을 다음과 같이 정의하자.

$$Y_i =  \begin{cases} 1 \ \ \text{참가자 i 가 행복하다고 답함} \newline 0 \ \ \text{o.w.} \end{cases}$$

- 5명에 대해서 조사하였다고 하자. 그러면 p(1,1,0,0,0) 과 p(0,1,1,0,0) 은 완전히 같은 확률을 보이고, $y_i$ 와 $y_j$ 는 서로 아무관련이 없다. 즉 이런 실험의 경우 Exchaneable 하다.

> Claim

- If $\theta \sim p(\theta)$ and $Y_1....Y_n$ are conditionally iid given $\theta$, then marginally (unconditionally on $\theta$), $Y_1 ... Y_n$ are exchangable

![png](/assets/images/Bayes/2_1.PNG)

# [de Finetti thm](#link){: .btn .btn--primary}{: .align-center}

![png](/assets/images/Bayes/2_2.PNG)

> ## **Main idea**

- 위 논의들을 모두 정리하면 다음과 같다.
  -  $p(\theta)$ 를 $Y_1 .... Y_n$ 에 대한 belief 라 하자.  $$Y_1...Y_n\mid\theta \  \ are \ \  iid $$ 와 $\theta \sim p(\theta)$ 이면 iff $\{Y_1 ... Y_n\} \text{ are exchangeable for all n} $ 이 된다. 

- **When $Y_1...Y_n$  repeatable?**
  - exchangable **for all n** 이려면 repeatbalility 가 성립해야한다. 
  - 즉 실험이 일관성 있게 계속 같은 조건으로 지속가능해야 한다는 것이다.  이러한 경우는 아래의 경우일때 어느정도 justification 이 된다.
  - $$\\Y_1, … , Y_n \text{가 반복 가능한 실험의 결과일때}\\Y_1, … , Y_n \text{가 유한한 모집단에서 복원추출 되었을 때 }\\ Y_1, … , Y_n \text{가 무한한 모집단에서 비복원 추출 되었을 때}$$

- **Sample size n** 
  - 만약 $Y_1...Y_n$ 이 exchangeable 하고, sampling 되는 모집단의 크기 $N >>> n$ 이며, replacement 없이 sampling 된다면 approximately conditionally iid 하게 모델링 될 수 있다. (Diaconis and Freedman 1980)

- **Justification**
  - 이제 위 논의를 왜 했을까에 대한 총 마무리 이다. 왜 아래와 같은 식이 성립될 수 있을까? 

$$ p(y_1...y_n) = \int p(y_1...y_n \mid \theta)p(\theta)d\theta = \int[\ \prod p(y_i \mid \theta ) \ \ ]p(\theta)d\theta $$ 

- $p(y_1...y_n)$ 은 관찰된 data 에 대한 probability 이다. 그런데 $\int[\ \prod p(y_i \mid \theta ) \ \ ]p(\theta)d\theta$ 의 부분은 확률 모델로 쪼갠 부분이다. 이러한 변환을 막 할 수 있을까?. 
- 위 결과가 정당화 되기 위해서는 repeatably exchangeable 해야한다. (예로 동전던지기 등..). 
- 위 조건이 성립한다면 저 결과는 de finetti thm 에 의해 보장될 수 있다! 즉 베이즈 정리에서 위와 같은 식을 사용하게 될 때의 정당성을 확보하기 위해 여태껏 달려온것 ㅜㅜ

> ## more de Finetti thm

- 베이즈 통계는 주로 Exchangeability를 가정한다. 이는 데이터가 재정렬되도 같다는것을 의미한다. 
- 베이지안은 왜 이를 가정할까? 우선 빈도론자는 어떤것을 가정하는지 살펴보자.  Frequentist 는 iid 를 가정한다. 
  - 이는 law of large number , limiting distribution 등에 사용되는 근본적인 가정으로서, 모든 데이터가 같은 상황임을 가정해야  많은 이론을 전개할 수 있기 떄문이다.  
- 즉 베이즈도 비슷한 맥락이다. Exchangeability 를 가정해야 많은 이론을 전개할 수 있다. 구체적인 내용는 아래 de Finetti thm 을 살펴보면서 알아보자.
- 이떄 주의해야하는 사실은 iid 인 데이터 $(X_1, \cdots , X_N)$은 항상 exchangeable하지만 exchangeable한 확률변수들은 항상 IID인 것은 아니라는 사실이다. 아래의 반례에서 그를 확인할 수 있다. 

Let $(X_1, \cdots , X_N)$ be iid random variables, and $X_0$ be a random variable independent to all $(X_1, \cdots , X_N)$. Then $(X_0 + X_1, \cdots , X_0 + X_N)$ is exchangeable but not independent anymore.
{: .notice}

- De Finetti 정리는 베이지안 통계학에서의 관점을 정당화 시켜준다. 

1. parameter를 확률변수로 보는것에 대한 정당성을 부여해준다.
2. prior distribution을 부여하는 것에 정당성을 부여해준다

- 과연 어떤 내용이길래 베이지안의 관점을 모두 정당화 시켜준다는 것일까? De Finetti 정리의 간소화된 statement는 아래와 같다.(위에서 우리가 본 정리와 같다.)

If $(X_1, \cdots , X_N)$ are infinitely exchangeable, then the joint probability $p(X_1, \cdots , X_N)$ has a representation as a mixture: $ p(X_1, \cdots , X_N)= \int \left( \prod_{i=1}^{N} p(X_i \mid \theta ) \right) \pi(\theta)d\theta $ for some random variable $\theta$
{: .notice}

- 다시 말해서, 어떤 확률변수들 $(X_1, \cdots , X_N)$에 대해 exchangeability를 만족한다면 다음을 만족한다는 것이다. 

  - $(X_1, \cdots , X_N)$의 joint distribution에는 underlying parameter $\theta$ 가 있다. 그 parameter $\theta$는 어떤 분포를 갖는 확률변수이다. 이를 prior distribution으로 부르자.
    - 이를 통해서 parameter $\theta$ 를 r.v. 로 보는것에 대한 정당성이 부여된다! 
  - 우리의 자료는 그 parameter에 대해 conditionally independent하다.
    - parameter가 한 값으로 고정되면 자료들 $(X_1, \cdots , X_N)$가 서로 independent하다는 의미이다.
    - 이를 통해서 베이즈 통계에서의 분해의 정당성이 부여된다!
- 즉 베이즈는 Frequentist 가 iid 를 가정하듯 exchangable 을 가정하고 시작한다.  exchangable 을 가정한다면 parameter 를 r.v. 로 보는것에 대한  정당성이 생기며 또한 베이즈의 기본적인 분해에 대한 정당성도 생기기 떄문이다. 
