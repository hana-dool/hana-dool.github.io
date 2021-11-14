---
title:  "Probability and Independence"
excerpt: "확률과 조건부 확률 그리고 독립"
categories:
  - Mathematical_Statistics
last_modified_at: 2021-11-12
toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 제일 기초가 되는 기댓값 , 분산 등에 대한 정리를 알아봅시다. 
{: .notice--warning}

# [Probability](#link){: .btn .btn--primary}{: .align-center}

> ## Definition

Definition 1.3.1 (Probability). Let $\mathcal{C}$ be a sample space and let $\mathcal{B}$ be the set of events. Let $P$ be a real-valued function defined on $\mathcal{B} .$ Then $P$ is a probability set function if $P$ satisfies the following three conditions:
1. $P(C) \geq 0$, for all $C \in \mathcal{B}$.
2. $P(\mathcal{C})=1$.
3. If $\left\{C_{n}\right\}$ is a sequence of events in $\mathcal{B}$ and $C_{m} \cap C_{n}=\phi$ for all $m \neq n$, then

$$
P\left(\bigcup_{n=1}^{\infty} C_{n}\right)=\sum_{n=1}^{\infty} P\left(C_{n}\right)
$$

- 위처럼 우리는 3 가지의 정의를 만족하는 함수 $P$ 를 확률 이라고 정의하기로 하였습니다.
  - 물론 측도록까지 필요한 확률론을 공부하시다가 보면, 위의 정리는 약간 틀리다는것을 알 테지만 여기에서는 학부 수준만 다룰거여서 여기까지만 하도록 하죠
- 위에서 정의되는 3개의 공리만으로 우리는 매우 다양한 Property 를 이끌어 낼 수 있습니다.

> ## Properties

> Theorem 1.3.1. For each event $C \in \mathcal{B}, P(C)=1-P\left(C^{c}\right)$.

Proof: We have $\mathcal{C}=C \cup C^{c}$ and $C \cap C^{c}=\phi$. Thus, from (2) and (3) of Definition 1.3.1, it follows that
$$
1=P(C)+P\left(C^{c}\right)
$$

> Theorem 1.3.2. The probability of the null set is zero; that is, $P(\phi)=0$. 

Proof: In Theorem 1.3.1, take $C=\phi$ so that $C^{c}=\mathcal{C}$. Accordingly, we have
$$
P(\phi)=1-P(\mathcal{C})=1-1=0
$$

> Theorem 1.3.3. If $C_{1}$ and $C_{2}$ are events such that $C_{1} \subset C_{2}$, then $P\left(C_{1}\right) \leq P\left(C_{2}\right)$.

Proof: Now $C_{2}=C_{1} \cup\left(C_{1}^{c} \cap C_{2}\right)$ and $C_{1} \cap\left(C_{1}^{c} \cap C_{2}\right)=\phi$. Hence, from (3) of Definition 1.3.1
$$
P\left(C_{2}\right)=P\left(C_{1}\right)+P\left(C_{1}^{c} \cap C_{2}\right) .
$$
From (1) of Definition 1.3.1, $P\left(C_{1}^{c} \cap C_{2}\right) \geq 0$. Hence, $P\left(C_{2}\right) \geq P\left(C_{1}\right)$.

> Theorem 1.3.4. For each $C \in \mathcal{B}, 0 \leq P(C) \leq 1$.

Proof: Since $\phi \subset C \subset \mathcal{C}$, we have by Theorem $1.3 .3$ that
$$
P(\phi) \leq P(C) \leq P(\mathcal{C}) \quad \text { or } \quad 0 \leq P(C) \leq 1
$$

> Theorem 1.3.5. If $C_{1}$ and $C_{2}$ are events in $\mathcal{C}$, then
> $$
> P\left(C_{1} \cup C_{2}\right)=P\left(C_{1}\right)+P\left(C_{2}\right)-P\left(C_{1} \cap C_{2}\right)
> $$

Proof : 생략..!

> Theorem 1.3.7 (Boole's Inequality). Let $\left\{C_{n}\right\}$ be an arbitrary sequence of events. Then
> $$
> P\left(\bigcup_{n=1}^{\infty} C_{n}\right) \leq \sum_{n=1}^{\infty} P\left(C_{n}\right)
> $$

Proof : 생략

> ## Remark

- 위처럼 우리는 확률에 대한 최소한의 정의로부터, 우리가 알고 있었던 다양한 확률의 성질을 알아낼 수 있었습니다. 
- 이제 다음부터는 다양한 확률의 성질에 대해서 알아보도록 합시다.

**Reference**

-  Hogg introdusction to Mathematical Statistics 7ed
