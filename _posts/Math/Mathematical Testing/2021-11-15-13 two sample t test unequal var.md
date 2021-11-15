---
title:  "Two sample t-test for population means (unequal variances)"
excerpt: "두 표본 평균 T test(이분산)"
categories:
  - Mathematical_Testing
last_modified_at: 2021-11-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 평균에 대한검정
{: .notice--warning}

# [Two sample t-test](#link){: .btn .btn--primary}{: .align-center}

> ## Lemma 8 

> Lemma

If $X_{1}, X_{2}, \ldots, X_{n}$ is a sequence of random variables, $\operatorname{Var}\left(S^{2}\right)=\frac{2 \sigma^{4}}{n-1}$

> Proof 

We know from Theorem 19 , that

$$\frac{(n-1) S^{2}}{\sigma^{2}} \sim \chi_{n-1}^{2}$$

and we know that the variance of a chi-square random variable with $k$ degrees of freedom is $2 k$, by Lemma 2. So

$$\operatorname{Var}\left[\frac{(n-1) S^{2}}{\sigma^{2}}\right]=2(n-1)$$

By Corollary 2 ,

$$\operatorname{Var}\left[\frac{(n-1) S^{2}}{\sigma^{2}}\right]=\frac{(n-1)^{2} \operatorname{Var}\left(S^{2}\right)}{\sigma^{4}}$$

Therefore

$$\frac{(n-1)^{2} \operatorname{Var}\left(S^{2}\right)}{\sigma^{4}}=2(n-1)$$

or

$$\operatorname{Var}\left(S^{2}\right)=\frac{2 \sigma^{4}}{(n-1)}$$

> ## Theorem 23

> Theorem

$$\hat{\beta}\left(\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}\right)^{-1}\left(\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}\right) \stackrel{a p p r o x}{\sim} \chi_{\hat{\beta}}^{2}$$

where

$$\hat{\beta}=\frac{\left(\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}\right)^{2}}{\frac{S_{X}^{4}}{n^{2}(n-1)}+\frac{S_{Y}^{4}}{m^{2}(m-1)}}$$

> Proof

Satterthwaite suggested the approximation

$$\beta\left(\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}\right)^{-1}\left(\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}\right) \sim \chi_{\beta}^{2}$$

If $V=\beta\left(\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}\right)^{-1}\left(\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}\right)$ and $V \sim \chi_{\beta}^{2}$, then we would expect

$$\operatorname{Var}(V)=\operatorname{Var}\left[\beta\left(\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}\right)^{-1}\left(\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}\right)\right]$$

and we know that the variance of a chi-square random variable with $k$ degrees of freedom is $2 k$, see Lemma 2. So $\operatorname{Var}(V)=2 \beta$. By Corollary 2 , where $\beta, n, m, \sigma_{X}^{2}$, and $\sigma_{Y}^{2}$ are constants,

$$\operatorname{Var}\left[\beta\left(\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}\right)^{-1}\left(\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}\right)\right]=\frac{\beta^{2}\left(\frac{\operatorname{Var}\left(S_{X}^{2}\right)}{n^{2}}+\frac{\operatorname{Var}\left(S_{Y}^{2}\right)}{m^{2}}\right)}{\left(\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}\right)^{2}}$$

but by $\operatorname{Lemma} 8, \operatorname{Var}\left(S_{X}^{2}\right)=\frac{2 \sigma_{X}^{4}}{n-1}$ and $\operatorname{Var}\left(S_{Y}^{2}\right)=\frac{2 \sigma_{Y}^{4}}{m-1}$, so

$$\operatorname{Var}\left[\beta\left(\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}\right)^{-1}\left(\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}\right)\right]=\frac{\beta^{2}\left(\frac{2 \sigma_{X}^{4}}{(n-1) n^{2}}+\frac{2 \sigma_{Y}^{4}}{(m-1) m^{2}}\right)}{\left(\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}\right)^{2}}$$

but $\operatorname{Var}(V)=2 \beta$, implying

$$\frac{\beta^{2}\left(\frac{2 \sigma_{X}^{4}}{(n-1) n^{2}}+\frac{2 \sigma_{Y}^{4}}{(m-1) m^{2}}\right)}{\left(\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}\right)^{2}}=2 \beta$$

Solving this equation gives

$$\beta=\frac{\left(\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}\right)^{2}}{\frac{\sigma_{X}^{4}}{(n-1) n^{2}}+\frac{\sigma_{Y}^{4}}{(m-1) m^{2}}}$$

or $\beta=0$, which can be ignored because the degrees of freedom must be greater than zero.

Of course, $\sigma_{X}^{2}$ and $\sigma_{Y}^{2}$ are unknown for a t hypothesis test. So an estimate is

$$\hat{\beta}=\frac{\left(\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}\right)^{2}}{\frac{S_{X}^{4}}{n^{2}(n-1)}+\frac{S_{Y}^{4}}{m^{2}(m-1)}}$$

and

$$\hat{\beta}\left(\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}\right)^{-1}\left(\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}\right) \stackrel{\text { approx }}{\sim} \chi_{\hat{\beta}}^{2}$$

> Note

- 이때 위에서 Approximation 을 제대로 증명하려면 아래와 같은 논문을 보세요
  - [21] Satterthwaite, Franklin E. "Synthesis of Variance." Psychometrika 6.5 (1941): 309-16.
  - [22] Satterthwaite, F. E. An Approximate Distribution of Estimates of Variance Components. Biometrics Bulletin 2.6 (1946): 110-14.
  - 또는 <https://math.stackexchange.com/questions/1746329/proof-and-precise-formulation-of-welch-satterthwaite-equation>

> ## Theorem 24 

> Theorem 

If $X_{1}, X_{2}, \ldots, X_{n}$ and $Y_{1}, Y_{2}, \ldots, Y_{m}$ are independent with $X_{i} \sim N\left(\mu_{X}, \sigma_{X}^{2}\right)$ and $Y_{i} \sim N\left(\mu_{Y}, \sigma_{Y}^{2}\right)$, then the statistic

$$T=\frac{(\bar{X}-\bar{Y})-\left(\mu_{X}-\mu_{Y}\right)}{\sqrt{\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}}}$$

has an approximate $t$ distribution with $v$ degrees of freedom where

$$v=\frac{\left(\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}\right)^{2}}{\frac{S_{X}^{4}}{n^{2}(n-1)}+\frac{S_{Y}^{4}}{m^{2}(m-1)}}$$

> Proof

$$T=\frac{(\bar{X}-\bar{Y})-\left(\mu_{X}-\mu_{Y}\right)}{\sqrt{\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}}} \cdot \frac{\sqrt{\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}}}{\sqrt{\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}}}$$

$$=\frac{(\bar{X}-\bar{Y})-\left(\mu_{X}-\mu_{Y}\right)}{\sqrt{\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}}} \div \sqrt{\frac{\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}}{\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}}}$$

Let $Z=\frac{(\bar{X}-\bar{Y})-\left(\mu_{X}-\mu_{Y}\right)}{\sqrt{\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}}}$, by Theorem $4, Z \sim N(0,1)$.

Now

$$\sqrt{\frac{\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}}{\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}}}=\sqrt{\frac{\hat{\beta}\left(\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}\right)^{-1}\left(\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}\right)}{\hat{\beta}}}$$

And By Theorem 23 

$$V=\hat{\beta}\left(\frac{\sigma_{X}^{2}}{n}+\frac{\sigma_{Y}^{2}}{m}\right)^{-1}\left(\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}\right) \stackrel{\text { approx }}{\sim} \chi_{\hat{\beta}}^{2}$$

Therefore,

$$T=\frac{Z}{\sqrt{\frac{V}{\hat{\beta}}}}$$

where $Z \sim N(0,1)$, and $V$ is approximately distributed $\chi_{\hat{\beta}}^{2} .$ Then by Definition $9, T$ is approximately distributed with $\hat{\beta}$ degrees of freedom, where

$$\hat{\beta}=\frac{\left(\frac{S_{X}^{2}}{n}+\frac{S_{Y}^{2}}{m}\right)^{2}}{\frac{S_{X}^{4}}{n^{2}(n-1)}+\frac{S_{Y}^{4}}{m^{2}(m-1)}}$$

> ## Remark

- 다소 제대로 증명하지는 않았지만 어쨋든 어느정도 왜 위와 같은 통계량을 사용하는지 알 수 있었습니다.
- 제대로 증명은 좀만 더 있다가 할게요..



---

**reference**

- <https://digitalcommons.usu.edu/cgi/viewcontent.cgi?article=1014&context=gradreports>

