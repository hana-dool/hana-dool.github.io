---
title:  "Cotidence interval based on bootstrap tables"
excerpt: "Bootstrap 방법론을 이용한 Confidence interval 의 추정"
categories:
  - Bayes
last_modified_at: 2021-11-10

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Bayesian Statistics 를 쓴다고 해도, 특정 가설에 대해서 Testing 하고 싶은 니즈는 있을것입니다. 이러한 가설검정을 수행할 수 있는 방법을 소개하고자 합니다.
{: .notice--warning}

# [Hypothesis Testing](#link){: .btn .btn--primary}{: .align-center}

> ## Confidence interval

- estimated $\hat{\theta}$ 에 대하여 우리는 종종 다음과 같이 Confidence interval 을 추정합니다.

$$\hat{\theta} \pm 1.645 \cdot \hat{se}$$

- 이때 위의 1.645 는 standard normal table 에서의 값입니다.
  - 이러한 Confidence interval 은 point estimate $\hat{\theta}$ 보다 훨씬 유용합니다. 
- 우리가 one sample situation 이고, unkown distribution $F , F \to x = (x_1. .. x_n)$  을 알고싶은 상황이라고 합시다. 
  - $\hat{\theta} = t(\hat{F})$ 는 우리가 알고싶은 통계량 $t$ 의 추정량이라고 합시다. 
  - $\hat{se}$ 는 standard error for $\hat{\theta}$ 라고 합시다. 
- 대부분, sample size n 이 커질수록 $\hat{\theta}$ 는 normal distirbution 으로 수렴하고 다음과 같은 식이 성립합니다.

$$\hat{\theta} \sim N(\theta , \hat{se^2})$$ 

$$\frac{\hat{\theta} - \theta}{\hat{se}} \sim N(0,1^2) \tag{12.2}$$

- large sample 에서는 위와 같은 같은 식이 성립합니다. 
- $z^{(a)}$ 를 100*a th percentile point of N(0,1) 이라고 하겠습니다. 
  - 그렇다면 Normal Table 에서 $z^{(0.25)} = -1.96$ 등을 쉽게 알 수 있습니다.
- 우리는 다음과 같은 사실을 알 수 있습니다. 

$$\operatorname{Prob}_{F}\left\{z^{(\alpha)} \leq \frac{\hat{\theta}-\theta}{\widehat{\mathrm{se}}} \leq z^{(1-\alpha)}\right\}=1-2 \alpha$$

- 위 식은 다시 쓰면 아래와 같이 쓰여질 수 있습니다.

$$\operatorname{Prob}_{\theta}\left\{\theta \in\left[\hat{\theta}-z^{(1-\alpha)} \cdot \text { se, } \hat{\theta}-z^{(\alpha)} \cdot \text { se }\right]\right\}=1-2 \alpha$$

- 이때 위에서 $Prob_{\theta}$ 의 Notation 은 Probability 가 True $\theta$ 하에서 계산되었음을 의미합니다. 
  - 즉 $\hat{\theta} \sim N(\theta , se^2)$ 라는 것입니다. 
- 편의를 위해서 우리는 위와 같은 Confidence interval 을 $[\hat{\theta_{lo}} , \hat{\theta_{up}}]$ 으로 정의하기로 하였습니다. 즉 
  - $$\hat{\theta}_{\mathrm{lo}}=\hat{\theta}-z^{(1-\alpha)}$$
  - $$\hat{\theta}_{\mathrm{lo}}=\hat{\theta}-z^{(\alpha)}$$
- 이 경우 우리는 interval $$\left[\hat{\theta}-z^{(1-\alpha)} \cdot \mathrm{se}, \hat{\theta}-z^{(\alpha)} \cdot \mathrm{se}\right]$$ 이 $1-2 \alpha$ 의 확률로 True value of $\theta$ 를 포함한다는 것을 알 수 있습니다.
  - 위처럼 양쪽으로 동일한 interval 로 CI 가 형성된것을 우리는 equal tailed 라고 부릅니다. 
  - 이 게시글 이외에서도 다양한 곳에서 Confidence interval 을 다룰건데요, 별 다른 이야기가 없으면 늘 Equal Tail 에 대해서 이야기하는것으로 하겠습니다. 
- 이때 $z$ statistics 의 성질에 따라서 $z^{(a)} = -z^{(1-\alpha)}$ 를 이용한다면 위의 Form 은 다음과 같이 단순화 되어질 수 있습니다. 
  - $\hat{\theta} \pm z^{(1-\alpha)} \cdot \hat{se}$

> Example

- 한 예시로 평균의 Estimation ($\hat{\theta}$ = 56.44) 이였고, Estimated Standard Error 가 $\hat{se} = 13.33$ 이였다고 합시다. 
  - 이 때에 90% Standard Confidence interval fot $\theta$ 는 다음과 같이 계산됩니다
  - $$56.255 \pm 16.45 \cdot 13.33$$

> ## Relation with Confidence interval and Test

- $(\hat{\theta_{lo}} , \hat{\theta_{up}})$ 가 $1-2\alpha$ 라고 합시다. 그리고 True $\theta$ 는 $\hat{\theta_{lo}}$ 라고 합시다. 즉

$$\hat{\theta}^{*} \sim N\left(\hat{\theta}_{\mathrm{lo}}, \mathrm{se}^{2}\right)$$

- 이때 우리는 $\hat{\theta^*}$ 를 Random Variable 이라고 합시다. (oberserved Eastimate 인 $\hat{\theta}$ 와의 혼란을 피하기 위해서입니다.)
- quantity $\hat{\theta^*}$ 는 fIX 되어있다고 가정합시다. 그러면 다음과 같은 Equality 가 성립합니다. 



$$Prob_{\hat{\theta_{lo}



**reference**

<https://myweb.uiowa.edu/pbreheny/uk/teaching/621/notes/10-11.pdf>

- <https://www.tau.ac.il/~saharon/StatisticsSeminar_files/Hypothesis.pdf>
- <http://www.ru.ac.bd/stat/wp-content/uploads/sites/25/2019/03/501_02_Efron_Introduction-to-the-Bootstrap.pdf>
- <https://en.wikipedia.org/wiki/Bootstrapping_(statistics)>
- 



위와 같이 베이즈에도 Testing 이 있다! 라는걸 알 수 있어요..
{: .notice--success}

