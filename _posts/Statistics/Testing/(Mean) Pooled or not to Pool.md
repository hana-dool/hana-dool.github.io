---
title:  "Fisher Exact Test"
excerpt: "2*2 분할표에 대해서 분석해보기"
categories:
  - Stat_Testing
last_modified_at: 2021-12-06

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 아앙
{: .notice--warning}

# [Fisher Exact Test](#link){: .btn .btn--primary}{: .align-center}

- 피셔의 정확 검정은 분할표 분석에 사용되는 통계적 유의성 검정입니다.
- 표본의 크기가 작을때에 좀 더 정확한 방법이라, 표본의 크기가 작을떄에 잘 사용됩니다. 
- Fisher 검정은 대부분 2*2 의 분할표 테이블을 사용하게 됩니다.

$$\begin{array}{|c|c|c|c|}
\hline & \text { Men } & \text { Women } & \text { Row total } \\
\hline \text { Studying } & 1 & 9 & 10 \\
\hline \text { Not-studying } & 11 & 3 & 14 \\
\hline \text { Column total } & 12 & 12 & 24 \\
\hline
\end{array}$$

- 24명의 사람중에, 10명이 공부하고 14명은 공부하지 않는, 위와 같은 상황이라고 합시다. 
- 위와 같은 Contingency Table 에 대해서 Null Hypothesis 를 남자와 여자가 공부할 비율이 같다는 것을 검증하려 한다면, 이를 할 수 있을까요? 

> ## 검증

$$\begin{array}{|c|c|c|c|}
\hline & \text { Men } & \text { Women } & \text { Row Total } \\
\hline \text { Studying } & a & b & a+b \\
\hline \text { Non-studying } & c & d & c+d \\
\hline \text { Column Total } & a+c & b+d & a+b+c+d(=n) \\
\hline
\end{array}$$

- 본격적으로 검정을 하기 전에 위와 같인 Contingency Table 을 알아보도록 하겠습니다. 

$$p=\frac{\left(\begin{array}{c}
a+b \\
a
\end{array}\right)\left(\begin{array}{c}
c+d \\
c
\end{array}\right)}{\left(\begin{array}{c}
n \\
a+c
\end{array}\right)}=\frac{\left(\begin{array}{c}
a+b \\
b
\end{array}\right)\left(\begin{array}{c}
c+d \\
d
\end{array}\right)}{\left(\begin{array}{c}
n \\
b+d
\end{array}\right)}=\frac{(a+b) !(c+d) !(a+c) !(b+d) !}{a ! b ! c ! d ! n !}$$

- Fisher showed that conditional on the margins of the table, $a$ is distributed as an hypergeometric distribution with $a+c$ draws from a population with $a+b$ successes and $c+d$ failures. 
- where $\left(\begin{array}{l}n \\ k\end{array}\right)$ is the binomial coefficient and the symbol ! indicates the factorial operator. This can be seen as follows. If the marginal totals (i.e. $a+b, c+d, a+c$, and $b+d$ ) are known, only a single degree of freedom is left: the value e.g. of $a$ suffices to deduce the other values. Now, $p=p(a)$ is the probability that $a$ elements are positive in a random selection (without replacement) of $a+c$ elements from a larger set containing $n$ elements in total out of which $a+b$ are positive, which is precisely the definition of the hypergeometric distribution.

$$p=\left(\begin{array}{c}
10 \\
1
\end{array}\right)\left(\begin{array}{c}
14 \\
11
\end{array}\right) /\left(\begin{array}{c}
24 \\
12
\end{array}\right)=\frac{10 ! 14 ! 12 ! 12 !}{1 ! 9 ! 11 ! 3 ! 24 !} \approx 0.001346076$$

> ## Fisher Exact Test 

Fisher's exact test and the chi-squared test are **two most popular statistical tests for independence**:

- Fisher's test is an **exact test** because we know the exact sampling distribution.
- The chi-squared test is only an **approximate test** because the sampling distribution of the test statistic is only approximately (asymptotically) equal to the chi-square distribution.'

> ## **When to use Fisher's exact test?**

Choose the Fisher exact test rather than the chi-squared test if **the sample size is small, the marginals are very uneven, or there is a small value (less than five) in one of the cells**. This is because the approximation on which the chi-squared test is based might not be very accurate in such conditions.

> ## **When to use chi-square test?**

Since we have to compute factorials, Fisher's exact test is hard to calculate when **the sample is large or the contingency table is well-balanced**. Fortunately, there are the conditions under which the approximation used in the chi-squared test flourishes! 🌼

> ## Definition of Fisher's exact test

- As you now have a general idea of what Fisher's exact test is, it is high time we tell you how to perform it.
- The **null hypothesis is that the two variables are independent**; in other words, that the proportions of one variable are the same for all of the different values of the other variable.
- Consider a 2 x 2 contingency table with the cell frequencies represented by `a`, `b`, `c`, and `d`:

$$\begin{array}{ccc} 
& \text { category 1 } & \text { category 2 } \\
\text { group 1 } & \mathrm{a} & \mathrm{b} \\
\text { group 2 } & \mathrm{c} & \mathrm{d}
\end{array}$$

- We **need to find the marginal totals and the grand total `n`**:

$$\begin{array}{lccc} 
& \text { category 1 } & \text { category 2 } & \\
\text { group 1 } & \text { a } & \text { b } & a+b \\
\text { group 2 } & \text { c } & \text { d } & c+d \\
& a+c & b+d & a+b+c+d=n
\end{array}$$



---

  **Reference**

- https://ijpam.eu/contents/2013-89-4/5/5.pdf





