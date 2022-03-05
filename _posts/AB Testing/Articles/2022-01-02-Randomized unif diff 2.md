---
title: "Randomization unit and Analysis Unit"
excerpt: "분석단위와 무작위 단위가 다를때에 발생하는 문제"
categories:
  - AB_Article
last_modified_at: 2022-01-01

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

Outlier 와 A/B Testing
{: .notice--warning}

# [randomization unit in online A/B tests](#link){: .btn .btn--primary}{: .align-center}

- 이전 게시물에서 무작위 단위가 (Randomization unit) 독립적이지 않을때에 온라인 실험에서 발생하는 문제에 대해서 알아보았습니다.
- 여기에서는 무작위 단위를 세션으로 유지하지만, 분석 단위 (Randomization Unit)   를 유지할떄에 어떤 일이 일어날지에 대해서 알아봅시다.

> ## Comparing two proportions

- Randomization Unit 이 Analysis Unit 과 다를때에 어떤 일이 일어나는지 알아보기 위하여, 테스트의 작동이 어떻게 일어나는지에 대해서 아주 짧게 알아봅시다.
- 기본적으로는 아래와 같이 Two Sampl z test 를 이용해 계산합니다. (Large Sample 일 경우에는 T - Test 와 동일함)

> Algorithm

$$Z=\frac{\left(\hat{p}_{T}-\hat{p}_{C}\right)-\left(p_{T}-p_{C}\right)}{\sqrt{\operatorname{Var}\left(p_{T}-p_{C}\right)}}=\frac{\hat{p}_{T}-\hat{p}_{C}}{\sqrt{\operatorname{Var}\left(p_{T}\right)+\operatorname{Var}\left(p_{C}\right)}}=\frac{\hat{p}_{T}-\hat{p}_{C}}{\sqrt{\hat{p}(1-\hat{p})\left(\frac{1}{n_{T}}+\frac{1}{n_{C}}\right)}}$$

- $$\hat{p}_{T}$$ and $$\hat{p}_{C}$$ are our observed treatment and control session conversion rates
- $p_{T}$ and $p_{C}$ are the true treatment \& control session conversion rates
- $p_{T}-p_{C}$ is 0 under the null hypothesis
- $n_{T}$ and $n_{C}$ are the number of sessions in treatment and control
- $\hat{p}$ is the pooled session conversion rates (i.e. total number of conversions / total number of sessions, from both groups)

> Note

- 위와 같은 계산 방식에서 우리는 샘플이 iid 이거나 최소한 상관관계가 없다고 가정합니다. 
- 하지만 Randomization Unit 이 Analysis 과 다를때에는 위와 같이 iid 가 아닙니다.
  - 각 측정값들은 독립이 아니기 때문이죠.

> ## Naive Test

![jpg](/assets/images/Stat/143_1.jpg)

- 우리는 분석시에 사용자당 세션과 , 세션 전환율이 독립적이라는 가정을 한 상태에서 분석을 진행했습니다. (즉 각 세션이 독립적이다! 라고 가정하고 분석하기 위해서, 어떤 사용자가 세션을 발생시키던, 각 세션당  Conversion 은 동일하다고 가정한셈이죠)
  - 즉 위 그림의 파란색처럼 "유저가 세션을 얼마나 발생시키던지, Session Conversion 은 각 세션당 일치 한다!" 를 가정한 셈입니다.
- 그러나 현실 세계에서는 일반적으로 그렇지 않습니다. 일부 사용자는 첫 번째 세션에서 전환할 수 있지만 다른 사용자는 전환을 위해 여러 세션을 사용할 수 있습니다. 아래 예시를 볼까요?

![jpg](/assets/images/Stat/143_2.jpg)

- 위의 Terry 와 Jerry 처럼 "어떤 유저가 사용하느냐" 에 따라서 각 세션은 구매 전환의 비율이 달라집니다.
  - Jerry 처럼 충동 구매자일 경우에는 세션 한번만에 신발을 바로바로 삽니다.
  - Terry 처럼 신중 구매자일 경우에는 세션을 여러번 진행하며 신발을 사게 됩니다. 즉 Terry 에 속하는 Session 은 구매전환이 적을수밖에 없죠 
- 그러므로 일반적으로 아래와 같은 그래프를 그리게 됩니다.

![jpg](/assets/images/Stat/143_3.jpg)

> ## Varying the sessions per user distribution

- 이러한 다양한 분포가 우리에게 어떤 영향을 미칠 수 있는지 이해하기 위해 사용자 분포당 세션의 분산을 늘리고 위에서 설명한 이항 z-검정의 결과 p-값을 플로팅하겠습니다.
  - 이때 사용자의 세션 수에 관계없이 전환율을 일정하게 유지했습니다.
- 50,000 users 데이터를 Generate 합니다.
  - Their conversion rate, # of sessions, and how many of those sessions converted
- User 그룹을 정확히 반 나눕니다. 그리고 compute the resulting p-value
  - Repeat this 10,000 times to generate a distribution p-values

![jpg](/assets/images/Stat/143_4.gif)

- 위 그래프의 경우 
  - 좌측상단 그래프는 유저당 세션수를 나타낸다. (추이를 보면 점점 Skewed 되고 있다. 즉 대다수는 세션을 조금 일으키고 , 소수의 Outlier 가 있음을 알 수 있다.)
  - 우측상든 그래프는 '유저당 Conversion' 의 그래프 (즉 유저가 세션을 많이 generate 한다고 해도, 전환율은 똑같이 유지한다.) 
  - 이때 Conversion 은 '평균은 동일' 하게 유지되기는 하지만 , 각각 유저에게 어느정도의 Noise 가 존재합니다. ( 여기에서는 beta 분포로 generating 하였습니다. )
- Randomization Unit 이 유저이므로, 좌하단의 p-value 계산을 할때에, 유저별로 나뉜 뒤에, 세션당 성공율이 Test 되게 됩니다. (Radomization 은 유저 / Analysis 는 세션)
  - 이때 점점 Session Per User 가 극단적이 될수록 p-value 그래프도 False Postiive 가 늘어나는것을 볼 수 있습니다.
  - 이는 Session 수가 엄청 많은 유저의 경우, 어떤 Variant 에 할당되느냐에 따라서 그 값이 크게 변하기 때문입니다.
- 우하단의 그래프는 Uniform 분포와 같은지 아닌지를 Testing 한 결과를 나타냅니다. (KS 그래프)
  - 그래프를 볼때 그 차이가 엄청 커지므로 Uniform 이 아니라는것을 알 수 있습니다.

> Note 

- Conversion 이 모두 20% 수준인데, Outlier user (즉 세션이 많은 유저) 가 어디에 위치해도 Proportion 은 같은거 아닌가요?
  - 여기에서 모든 유저가 0.2 의 Conversion 을 가지는게 아니라 평균적으로 그렇다는 것입니다
  - .즉 Outlier 유저의 경우 0.17 , 0.22 , 0.21 등 다양한 Conversion 을 가지게 될 것이고, 이러한 영향을 받는다는 의미에요~

> ## Varying the conversion rate with sessions per user

- 다음으로 사용자 분포당 세션을 일정하게 유지한 상태에서, 각 유저에 대해서, 세션당 성공률이 크게 변하는 경우를 나타냈습니다.
  - 이전에 우리가 살펴본 직관과 같게, Session 수가 많아질수록 그 성공률이 낮아지게 설정했습니다.

![jpg](/assets/images/Stat/143_5.gif)

- 이 경우에도 역시나, "유저별로 Dependence" 가 존재하게 되므로 Naive 하게 계싼한 Binomial Z-test 의 경우 False - Positive 가 매우 커지는것을 볼 수 있습니다.
  - Outlier 유저가 영향력이 엄청 세므로 이전과 같은 이유이지요...

> ## How can we fix this?

- 사용자당 세션의 분산을 늘리거나(세션 수가 많은 사용자가 많을수록) 전환율을 사용자의 세션 수에 따라 변경하면 Binomial z test 의 경우 False Positive 가 늘어나게 됩니다..
- 이는 직관적으로 의미가 있습니다. user 간의 편차가 클수록 Treatment (또는 Control)에 포함된 특정 사용자가 결과를 크게 좌우할 수 있습니다 
  - 즉 어떤 유저의 경우 Conversion Rate 가 0.9 인데 , 평균은 0.2라면 이 유저가 어디에 속하느냐에 따라서 크게 Treatment 와 Control 을 좌우하게 되겠죠.
- Binomial z-검정은 비율 차이의 True 분산을 작게 평가하고, False Positive를 증가시킵니다. 
  - 이 문제를 해결하기 위해 델타 방법 또는 부트스트래핑을 사용하여 분산을 올바르게 추정하거나 User - Grain 메트릭으로 전환할 수 있습니다.

> ## Delta Method 

$$\begin{aligned}
&\operatorname{Var}\left(p_{T}\right)=\frac{1}{\left(\bar{N}_{i T}\right)^{2}} \operatorname{Var}\left(S_{i T}\right)+\frac{\left(\bar{S}_{i T}\right)^{2}}{\left(\bar{N}_{i T}\right)^{4}} \operatorname{Var}\left(N_{i T}\right)-2 \frac{\bar{S}_{i T}}{\left(\bar{N}_{i T}\right)^{3}} \operatorname{Cov}\left(S_{i T}, N_{i T}\right) \\
&\operatorname{Var}\left(p_{C}\right)=\frac{1}{\left(\bar{N}_{i C}\right)^{2}} \operatorname{Var}\left(S_{i C}\right)+\frac{\left(\bar{S}_{i C}\right)^{2}}{\left(\bar{N}_{i C}\right)^{4}} \operatorname{Var}\left(N_{i C}\right)-2 \frac{\bar{S}_{i C}}{\left(\bar{N}_{i C}\right)^{3}} \operatorname{Cov}\left(S_{i C}, N_{i C}\right)
\end{aligned}$$

- $i$ is the user index
- $\bar{N}_{i T}$ is the mean # of sessions across all users in the treatment group
- $\operatorname{Var}\left(N_{i T}\right)$ is the variance in the # of sessions across all users in the treatment group
 Variance can be calculated normally, i.e. np.var(sessions_per_user)
- $$\bar{S}_{i T}$$ is the mean # of converted sessions across all users in the treatment group and $\operatorname{Var}\left(S_{i T}\right)$ is the variance
- $\operatorname{Cov}\left(S_{i T}, N_{i T}\right)$ is the covariance in converted sessions per user and sessions per user in the treatment group
- Covariance can be calculated normally, i.e. np.cov(conversion_per_user, sessions_per_user)
- These variance estimations can then be plugged into the same Z-test as above:

$$Z=\frac{\hat{p}_{T}-\hat{p}_{C}}{\sqrt{\frac{\operatorname{Var}\left(p_{T}\right)}{n_{T}}+\frac{\operatorname{Var}\left(p_{C}\right)}{n_{C}}}}$$

- Where $n_{C}$ and $n_{T}$ are the number of users in control and treatment, respectively.

> ## Bootstrapping

- 부트스트래핑은 적절한 분산 추정값과 p-값을 얻는 데 사용할 수 있는 또 다른 방법입니다. 
  - 부트스트래핑은 직관적이고 이해하기 쉽지만 계산 비용이 더 많이 듭니다.

![jpg](/assets/images/Stat/143_6.jpg)

- 귀무가설에서는 대조군과 처리군 사이에 차이가 없습니다. 
  - 따라서 귀무 가설에서 샘플을 생성하기 위해 모든 사용자를 혼합한 다음 다음을 수행할 수 있습니다.

> Algorithm

1. Randomly create a new control \& treatment group through sampling with replacement from the "mixed" population
2. Calculate the overall session conversion rate for each group
3. Calculate the difference in conversion rates between the two groups $\left(p_{T}-p_{C}\right)$
4. Repeat $(1-3)$ thousands of time and store the results

> ## Comparison : Delta Method and Bootstrap 

> 사용자당 세션 수 변경

![jpg](/assets/images/Stat/143_7.gif)

- 위와 같이 델타 방법 또는 부트스트랩 방법을 쓰면 균일한 분포를 어느정도 유지하는것을 볼 수 있습니다.

> 사용자당 전환율 변경

![jpg](/assets/images/Stat/143_8.gif)

- 위의 Simulation 도 이전과 같이 잘 작동하는것을 볼 수 있습니다.

> ## User grain metrics

- 이전의 Statistical Test 방식을 변경하는 방식 대신에, randomization unit 와 Analysis Unit 이 일정해질 수 있도록 메트릭을 변경할 수 있습니다.
- 즉 이 게시물 예시에서는 세션 전환율 대신에 사용자 전환율을 확인해야 할 것입니다.
  - 사용자 전환율은 "한번 이상이라도 전환 한" 사용자의 비율로 정의됩니다. 
  - Treatment 가 사용자의 전환 여부 (0,1) 뿐만 아니라, 전환 빈도를 변경할것으로 예상된다면, 사용자당 전환 수 를 대신 정의할수도 있습니다. 
  - 물론 이렇게 사용자당 전환 수 처럼 정의된다면 , 비율 메트릭을 고려하지 않게 되기 때문에 그냥 T-Test 와 같은 방법을 쓰면 되죠
- User Grain 으로 바꾸면 다 해결되는거 아닐까? 할 수 있지만 , 사실 문제가 있습니다.

> Problem

- User grain(즉 User 가 Randomization Unit) 메트릭은 계산 비용이 더 많이 들 수 있습니다.
  - 실제 사용자 전환율을 계산하려면 각 사용자의 **모든 세션** 을 고려해서 "전환 했는지 안했는지" 를 계삲야 합니다.
  - 세션 데이터 볼륨에 따라 실행 불가능할 수 있습니다 (너무 데이터 크기가 방대할 수 있어서요...). 대신 더 짧은 기간의 전환 수를 계산해야 할 수도 있습니다(예: '14일 사용자 전환율')
- Session 기반 메트릭을 사용하면 일반적으로 장치 유형, 리퍼러, 세션이 시작된 페이지 등과 같은 항목으로 분류가 쉽습니다. (세션에 기록이 남겨질 수 있기 떄문이죠)
  - User 메트릭으로 전환할 때, 다양한 로그 데이터로부터 단일 값을 선택해야 하기 때문에 이것은 조금 더 까다로워집니다.  (user 가 동일한데 다른 기기를썼을때, 이 사람은 어떤 기기로 분류되어야 할까요?)
  - 세분화를 수행하기 전에 사용자. 간단한 접근 방식은 첫 번째 세션의 기기, 리퍼러 및 랜딩 페이지를 사용자의 값으로 어떻게 변환할지를 정의해야 할 것입니다.
- Session 메트릭이 더 일반적으로 사용되기 때문에 이해 관계자는 User메트릭에 익숙하지 않을 수 있습니다. 
  - 이를 위해서는 비교 가능한 수치(예: 세션 전환 측정항목의 동일한 증가)를 생성하기 위해서 우리가 좀 더 계산을 해야할 수도 있습니다...

---

**reference**

- https://ianwhitestone.work/randomization-unit-analysis-unit/



