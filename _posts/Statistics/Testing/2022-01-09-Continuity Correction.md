---
title:  "Binomial Test Continuiuty Correction"
excerpt: "Binomial 테스트에서의 연속성 수정"
categories:
  - Stat_Testing
last_modified_at: 2022-01-09

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

연속성을 수정하면 테스트의 질이 쪼오끔 올라갑니다.
{: .notice--warning}

# [Binomial test](#link){: .btn .btn--primary}{: .align-center}

> ## Binomial Test 

- Binomial Test 는, 확률 ($\pi$) 에 대한 검정을 의미합니다.
  - 이때 계산되는 p-value 는 근사값이 아니라 exact 하게 구할 수 있습니다. 

> Test

The binomial test is useful to test hypotheses about the probability $(\pi)$ of success:

$$H_{0}: \pi=\pi_{0}$$

where $\pi_{0}$ is a user-defined value between 0 and 1 .
If in a sample of size $n$ there are $k$ successes, while we expect $n \pi_{0}$, the formula of the binomial distribution gives the probability of finding this value:

$$\operatorname{Pr}(X=k)=\left(\begin{array}{l}
n \\
k
\end{array}\right) p^{k}(1-p)^{n-k}$$

If the null hypothesis $H_{0}$ were correct, then the expected number of successes would be $n \pi_{0}$. We find our $p$-value for this test by considering the probability of seeing an outcome as, or more, extreme. For a one-tailed test, this is straightforward to calculate. Suppose that we want to test if $\pi<\pi_{0}$. Then our $p$-value would be,

$$p=\sum_{i=0}^{k} \operatorname{Pr}(X=i)=\sum_{i=0}^{k}\left(\begin{array}{c}
n \\
i
\end{array}\right) \pi_{0}^{i}\left(1-\pi_{0}\right)^{n-i}$$

An analogous computation can be done if we're testing if $\pi>\pi_{0}$ using the summation of the range from $k$ to $n$ instead.
Calculating a $p$-value for a two-tailed test is slightly more complicated, since a binomial distribution isn't symmetric if $\pi_{0} \neq 0.5$. This means that we can't just double the $p$-value from the one-tailed test. Recall that we want to consider events that are as, or more, extreme than the one we've seen, so we should consider the probability that we would see an event that is as, or less, likely than $X=k$. Let $\mathcal{I}=\{i: \operatorname{Pr}(X=i) \leq \operatorname{Pr}(X=k)\}$ denote all such events. Then the two-tailed $p$-value is calculated as,
$$
p=\sum_{i \in \mathcal{I}} \operatorname{Pr}(X=i)=\sum_{i \in \mathcal{I}}\left(\begin{array}{c}
n \\
i
\end{array}\right) \pi_{0}^{i}\left(1-\pi_{0}\right)^{n-i}
$$
![png](/assets/images/Stat/144_2.jpg)

> ## Large Sample 

For large samples such as the example below, the binomial distribution is well approximated by convenient continuous distributions, and these are used as the basis for alternative tests that are much quicker to compute, Pearson's chi-squared test and the G-test. However, for small samples these approximations break down, and there is no alternative to the binomial test.
The most usual (and easiest) approximation is through the standard normal distribution, in which a z-test is performed of the test statistic $Z$, given by
$$
Z=\frac{k-n \pi}{\sqrt{n \pi(1-\pi)}}
$$
where $k$ is the number of successes observed in a sample of size $n$ and $\pi$ is the probability of success according to the null hypothesis. An improvement on this approximation is possible by introducing a continuity correction:
$$
Z=\frac{k-n \pi \pm \frac{1}{2}}{\sqrt{n \pi(1-\pi)}}
$$
For very large $n$, this continuity correction will be unimportant, but for intermediate values, where the exact binomial test doesn't work, it will yield a substantially more accurate result.

![png](/assets/images/Stat/144_1.jpg)

- 위의 그림을 보면, 왜 연속성 수정이 필요한것인지 알 수 있습니다.







