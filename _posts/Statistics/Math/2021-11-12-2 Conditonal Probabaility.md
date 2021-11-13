---
title:  "Moment Generating Function"
excerpt: "MGF 를 다루어 보기"
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

# [Conditional Probability](#link){: .btn .btn--primary}{: .align-center}

> ## Definition

$$
P\left(C_{2} \mid C_{1}\right)=\frac{P\left(C_{1} \cap C_{2}\right)}{P\left(C_{1}\right)}
$$
is a suitable definition of the conditional probability of the event $C_{2}$, given the event $C_{1}$, 

> ## Properties

> provided that $P\left(C_{1}\right)>0$. Moreover, we have
>
> 1. $P\left(C_{2} \mid C_{1}\right) \geq 0$.
> 2. $P\left(\cup_{j=2}^{\infty} C_{j} \mid C_{1}\right)=\sum_{j=2}^{\infty} P\left(C_{j} \mid C_{1}\right)$, provided that $C_{2}, C_{3}, \ldots$ are mutually exclusive events.
> 3. $P\left(C_{1} \mid C_{1}\right)=1$

- 위와 같은것들은 쉽게 이끌어 낼 수 있는 Properties 이므로 증명은 생략하겠습니다.

> ## Law of Total probability

Consider $k$ mutually disjoint events $C_{1}, C_{2}, \ldots, C_{k}$ such that $P\left(C_{i}\right)>0$ for $i=1,2, \ldots, k$.
Suppose these events form a partition of $\Omega$. Let $C$ be another event, and $C$ can be expressed as the union of $k$ disjoint events, i.e.,
$$
C=\left(C \cap C_{1}\right) \cup\left(C \cap C_{2}\right) \cup \cdots \cup\left(C \cap C_{k}\right)
$$
Because the events $\left\{C \cap C_{i}\right\}$, for $i=1,2, \ldots, k$, are mutually disjoint, we have by probability axiom
$$
\begin{aligned}
P(C) &=P\left(C \cap C_{1}\right)+P\left(C \cap C_{2}\right)+\cdots+P\left(C \cap C_{k}\right) \\
&=\sum_{i=1}^{k} P\left(C \cap C_{i}\right) \\
&=\sum_{i=1}^{k} P\left(C_{i}\right) P\left(C \mid C_{i}\right)
\end{aligned}
$$
which is called the law of total probability.

- 즉 위처럼 특정한 Event 가 Disjoint 한 Event 로 분해된다면 , 나누어서 계산할수 있다는 정리가 되겠습니다.

> ## Bayes Thm

Suppose that $P(C)>0 .$ Then, the definition of conditional probability implies
$$
\begin{aligned}
P\left(C_{j} \mid C\right) &=\frac{P\left(C \cap C_{j}\right)}{P(C)} \\
&=\frac{P\left(C_{j}\right) P\left(C \mid C_{j}\right)}{P(C)} \\
&=\frac{P\left(C_{j}\right) P\left(C \mid C_{j}\right)}{\sum_{i=1}^{k} P\left(C_{i}\right) P\left(C \mid C_{i}\right)}
\end{aligned}
$$
- 위의 정리는 베이즈 정리가 되겠습니다. 이를 이용한다면 , 우리가 원하는 $A \mid B$ 의 확률을 '역전' 해서 $B \mid A$ 의 확률을 이용해 구할 수 있는 정리이죠.
- 이것의 장점은 바로 베이즈 정리에서 $\theta \mid Data$ 를 구하기 어려우므로 $Data \mid \theta$ 를 이용할떄에 주로 사용됩니다. 하지만 여기에서는 생략하도록 하겠습니다.

---

**Reference**

-  Hogg introdusction to Mathematical Statistics 7ed

