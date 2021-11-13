---
title:  "Statistical Independence"
excerpt: "통계적 독립"
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

# [Independence](#link){: .btn .btn--primary}{: .align-center}

> ## Definition

 Let $C_{1}$ and $C_{2}$ be two events. We say that $C_{1}$ and $C_{2}$ are independent if
$$
P\left(C_{1} \mid C_{2}\right)=P\left(C_{1}\right) \text { or } P\left(C_{2} \mid C_{1}\right)=P\left(C_{2}\right)
$$
holds. Then the multiplication rule becomes
$$
P\left(C_{1} \cap C_{2}\right)=P\left(C_{1}\right) P\left(C_{2}\right)
$$

- 기본 아이디어는 A 를 가정했음에도, B 의 확률에 영향이 없다면 우리는 '서로 독립이다!' 라고 생각할 수 있을것입니다. 
  - 그러한 아이디어에 따라 위처럼 정의된다고 생각할 수 있을것입니다.

> ## Mutually independent

Suppose now that we have three events, $C_{1}, C_{2}$, and $C_{3}$. We say that they are mutually independent if and only if they are pairwise independent:
$$
\begin{aligned}
&P\left(C_{1} \cap C_{3}\right)=P\left(C_{1}\right) P\left(C_{3}\right), \quad P\left(C_{1} \cap C_{2}\right)=P\left(C_{1}\right) P\left(C_{2}\right) \\
&P\left(C_{2} \cap C_{3}\right)=P\left(C_{2}\right) P\left(C_{3}\right)
\end{aligned}
$$
and
$$
P\left(C_{1} \cap C_{2} \cap C_{3}\right)=P\left(C_{1}\right) P\left(C_{2}\right) P\left(C_{3}\right)
$$
More generally, the $n$ events $C_{1}, C_{2}, \ldots, C_{n}$ are mutually independent if and only if for every collection of $k$ of these events, $2 \leq k \leq n$, the following is true:
Say that $d_{1}, d_{2}, \ldots, d_{k}$ are $k$ distinct integers from $1,2, \ldots, n$; then
$$
P\left(C_{d_{1}} \cap C_{d_{2}} \cap \cdots \cap C_{d_{k}}\right)=P\left(C_{d_{1}}\right) P\left(C_{d_{2}}\right) \cdots P\left(C_{d_{k}}\right)
$$
In particular, if $C_{1}, C_{2}, \ldots, C_{n}$ are mutually independent, then
$$
P\left(C_{1} \cap C_{2} \cap \cdots \cap C_{n}\right)=P\left(C_{1}\right) P\left(C_{2}\right) \cdots P\left(C_{n}\right)
$$

- Mutually indepdence 는 '모든 pairwise 한 이벤트가 독립이다.' 라는것으로 정의되는데요, 이는 위처럼 모든 Event 의 product 에 대해서 위와 같이 Product 가 성립하면 if and only if 가 성립하는 것입니다. 
- 즉 쉽게 위 Mutually independence 를 정의하려면 아래와 같은 식으로 정의하는게 마음 편할것입니다.

If $k$ events $C_{1}, C_{2}, \ldots, C_{k}$ are mutually independent, then
$$
P\left(C_{1} \cap C_{2} \cap \cdots \cap C_{k}\right)=P\left(C_{1}\right) P\left(C_{2}\right) \cdots P\left(C_{k}\right)
$$
Also, many combinations of these events and their complements are independent.

> properties

Also, as with two sets, many combinations of these events and their complements are independent, such as
1. The events $C_{1}^{c}$ and $C_{2} \cup C_{3}^{c} \cup C_{4}$ are independent,
2. The events $C_{1} \cup C_{2}^{c}, C_{3}^{c}$ and $C_{4} \cap C_{5}^{c}$ are mutually independent.

- 즉 위처럼 A 와 B 가 독립이라면 , 그 Complement 와도 독립이라는 의미입니다.
- 이는 '독립이라면 그 이벤트의 정보량은 의미가 없다' 가 되므로, 위의 properties 는 매우 직관적으로 합리적인 결과입니다.

**Reference**

-  Hogg introdusction to Mathematical Statistics 7ed

