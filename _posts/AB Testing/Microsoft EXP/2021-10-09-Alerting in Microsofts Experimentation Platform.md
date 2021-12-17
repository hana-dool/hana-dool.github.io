---
title:  "Alerting in Microsoft’s Experimentation Platform (ExP)"
excerpt: "Microsoft EXP 에서 적용하는 사전 경보 시스템"
categories:
  - AB_Microsoft
last_modified_at: 2021-10-09

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Treatment 에 빨간색 글씨를 적용하는 실험을 기획하였는데, 사실 많은 사람이 적녹색맹이면 어떡할까요? 분명 A/B 테스팅이 끝나면 빨간색 글씨가 안좋다는것을 알긴 하겠죠. 하지만 테스트 도중 많은 유저들은 끔찍한 경험을 하게 될 것이고, 이러한 고객은 저희 서비스를 떠날것입니다. 하지만 실험 도중에 '우리 실험이 잘못되고 있다.' 라는것을 미리 알 수 있으면 어떨까요? 이 포스팅에서는 이러한 경고 시스템에 대해서 알아보겠습니다.
{: .notice--warning}

# [Alerting System in Microsoft](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

![png](/assets/images/Stat/72_1.png)

- 마이크로 소프트에서는 새로운 기능을 개발해서 제품을 지속적으로 개선하려 합니다. 
  - 이러한 소프트웨어 개발에서 데이터 중심 의사결정을 하기 위해서 수만건의 A/B 테스트를 하게 됩니다. 
- A/B 테스트의 주된 목적은 우리가 추가한 기능에 대해 고객의 만족도를 정확하게 평가하는것입니다. 
- 하지만 또한 유저가 버그/성능저하 로 인한 불만족을 조기에 판단하고 경고하는것도 가능합니다. 
  - 예로 빙은 매년 몇번의 A/B 테스트를 실시하는데, 수백개의 Alert(경고) 를 발생시킵니다.
- 이러한 경고는 중요한 문제점을 조기에 알고 대처하는데에 도움이 됩니다. 
- 이 게시물에서는 '신뢰 가능한' 경고의 중요성을 강조하고, 경고에 대한 방법론을 설명합니다. 

> ## Why are alert important?

2020년에 새로운 제품(Feature) 중 하나가 버그가 있어서, 일부 사용자가 중복된 Device id (현재 A/B Testing 에서 사용중인 ) 에 할당되는 오류가 있었습니다. 버그는 곧 발견되었고, 이 사용자들에게 기존의 ID 가 아닌 새 ID들 할당되었습니다. 며칠 후, 제품에서 시행되던 A/B 테스트중 하나가 , SRM(Sample Ratio Mismatch) 경고가 발생하였습니다. 이는 Treatmetn 와 Control 간의 Sample 비율이 다를때에 나타나는 에러입니다. 연구팀은 기존에 폐기되어야 했던 중복된 ID를 잘못 인식하여 일으킨 문제라는것을 알고 해결한 후, 테스트를 다시 시작할 수 있었습니다. 
{: .notice}

- 위와 같이 이러한 사전 경고는 실험중에 발생할 수 있는 에러를 미리 알게 해주어서 A/B Testing 이 성공적이 되도록 도와줍니다. 
- 마이크로 소프트에서는 경고가 A/B 테스트 도중 발생할 수 있도록 하여서, 문제 파악에 도움을 줍니다. 
- 예시로 Criteo 는 이상한 Feature 또는, 에러로 인해 클릭수나, 매출과 같은 Key metric 가 안좋은 영향을 미치게 된다면 경고를 탐지하는 기능을 실행하고 있습니다. 

> ## What are the main alerts used by Microsoft ExP?

- 이떄에 '어떤것을 Alert 의 기준' 으로 삼아야할지 가 의문일 수 있습니다. 
- 여기에서는 Microsoft EXP 에서 어떤것을 중심적으로 살펴보는지에 대해서 알아보겠습니다.

> SRM(Sample Ratio Mismatch) 

- SRM 은 A/B Testing 에서 매우 중요하므로 다른곳에서도 많이 사용되는 감시 기준중에 하나입니다. 
  - 각 실험은 A/B Testing 을 할떄에 Control 과 Treatment 를 1:1 로 분할합니다. 그러므로 이 1:1 비율이 틀려진다면 SRM 경보가 울리게 됩니다. 
  - 이떄에 , chi - square Test 를 통하여 비율이 1:1 인지 아닌지에 대해서 검정하게 됩니다. 정해진 p-value 이하로 떨어지게 된다면 경고가 발생하게 됩니다. 

> ##### Metric Out of Range

- 대략적으로 말 하자면, metric 이 Treatment 로 인해 달라지는 통상의 범위보다 근본적으로 엄청나게 달라질때에 Alert 가 발생하게 됩니다. 
- 이러한 Alert 의 기준을 상세히 정하기 위해서는 다음과 같이 Alert 실험을 설계해야 합니다. 일반적으로는 아래와 같이 설계가 됩니다. 
  - $H_0$ : metric 의 movement 는 지정된 범위 (ex $\pm 1\%$) 에서 움직인다. 
  - $H_1$ : Not $H_0$
- 이를 좀 더 자세하게 알아봅시다. 위에서 알아본 $H_0$ 은  metric 의 movement 가 $[b_{AL} \le \mu_T - \mu_C \le b_{AU}]$ 안에 있을떄라고 표현할 수 있습니다. 즉 이 이를 가설로 설정하게 된다면 
  - $H_0 :b_{AL} \le \mu_T - \mu_C \le b_{AU}$ 
  - $H_1 : \mu_T - \mu_C < b_{AL}$ or $\mu_T-\mu_C > b_{AU}$ 
- 우리는 직관적으로 메트릭이 normal range 를 벗어나게 된다면 $H_0$ 을 기각하게 됩니다. 즉 경고를 울리게 됩니다.  
  - 이때에 이 Range 는 경험적으로 설정합니다. (잘 변한다면 큰 range / 그렇지 않다면 좁은 range)
- 이제 우리는 두개의 one - sided test 를 진행합니다. 

$$H_{0L} : \mu_T - \mu_C \ge b_{AL} \ and \  H_{0U}:\mu_T - \mu_C \le b_{AU}$$

- 위처럼 두개의 One sided test 에 대한 p-value 를 계산합니다.

$$p_{A L}= \text{Pr} \left(\frac{\left(m_{T}-m_{C}\right)-b_{A L}}{S} \lt z_{\alpha} \mid \mu_{T}-\mu_{C}=b_{A L}\right)$$

$$p_{A U}={Pr}\left(\frac{\left(m_{T}-m_{C}\right)-b_{A U}}{S} \gt z_{1-\alpha} \mid \mu_{T}-\mu_{C}=b_{A U}\right) $$

- 두번쨰로는 $H_{0L}$ 또는 $H_{0R}$ 을 기각할때에 $H_{0}$을 기각합니다. 
  - 즉  $p = min(p_{AL} , p_{AU})$ 가 매우 작을떄에 $H_{0}$ 을 기각하게 됩니다.

$$p_{R L}={Pr}\left(\frac{\left(m_{T}-m_{C}\right)-b_{R L} \mu_{C}}{S} \lt z_{\alpha} \mid \mu_{T}-\mu_{C}=b_{R L} \mu_{C}\right)$$

$$p_{R U}={Pr}\left(\frac{\left(m_{T}-m_{C}\right)-b_{R U} \mu_{C}}{s} \gt z_{1-\alpha} \mid \mu_{T}-\mu_{C}=b_{R U} \mu_{C}\right) $$

- 각각의 기호가 설명하는것은 맨뒤의 Notification 에서 설명하도록 하겠습니다.

![png](/assets/images/Stat/72_2.png)

- 위 검정의 절차를 요약하면 위 그림과 같습니다. 
- 현실적으로는 'Metric' 에 대한 상대적인 움직임으로 정하게 되므로, 다음과 같이 계산되게 됩니다.

![png](/assets/images/Stat/72_3.png)

- bing 에서 사용하는 예시는 위와 같습니다. 
  - Page click rate 라는 메트릭을 metric-out-of-range alert 으로 사용하고 있습니다. 
  - 위 실험은 이 메트릭이 5% 보다 더 안좋아지면(통계적으로) 알람을 울리게 설정을 하였습니다.

> p-value adjustment in aleriting

- 사실, R. Kohavi, A. Deng, B. Frasca, T. Walker, Y. Xu and N. Pohlmann, “Online Controlled Experiments at Large Scale,” 에서 말하듯이, 단순히 '통계적으로' 안좋아지는것에 대해서(ex : p-value 가 0.05 이하일때) 알람을 울리게 된다면 우리는 수없는 알람을 듣게 될 것입니다. 
  - 왜냐하면 False Positive rate 를 기본적으로 5% 를 설정하기 때문입니다. 

- 다음과 같은 시나리오에서 위와 같은 나이브한 접근법은 불가능할 것입니다.
  - There can be multiple A/B tests simultaneously running on the same product line.
  - There can be multiple analyses (e.g., partial-day, 1-day et al.) for an A/B test.
  - There can be hundreds or even thousands of metrics in the analysis.
- 이를 해결하기 위한 일반적인 방법은 다음과 같은 두가지 방법이 있다고 합니다.
  - Common methods include the O’Brien & Fleming procedure
    -  P. O’Brien and T. Fleming, “A Multiple Testing Procedure for Clinical Trials,” Biometrics, vol. 35, no. 3, pp. 549-556, 1979
  - Benjamini & Hochberg false discovery rate control (for independent and dependent cases)
    - Y. Benjamini and Y. Hochberg, “Controlling the false discovery rate: A practical and powerful approach to multiple testing,”
    -  Y. Benjamini and D. Yekutieli, “The control of the false discovery rate in multiple testing under dependency,” Annals of Statistics
- Microsoft EXP 에서는 후자를 사용한다고 합니다. 

> ## How does one get notified?

- 이떄에 이러한 경고를 어떻게 할 수 있을까요? 
- Microsoft 에서는 다음과 같은 경고에 대한 우선순위를 분류하여 통지하게 됩니다. 
  - P0 : 이 경고는 심각한 문제가 발생했음을 나타냅니다. 즉각적인 주의를 요하는 경보입니다. 
  - P1 : P1 경보는 심각한 상황임을 나타냅니다. 이를 받은 실험자는 조사해야 합니다. 
  - P2 : P2 경보는 잠재적으로 잘못된 일이 일어나고 있음을 나타냅니다. 이를 조사해야 할 것입니다.
- 또한 매우 민감한 실험에 대해서는 자동 종료 기능을 설정할 수도 있습니다. 

# [Glossary of terms](#link){: .btn .btn--primary}{: .align-center}

1. Population Mean ($\mu_T$,$\mu_C$): This is the average value for a metric.
2. Sample Mean ($\mu_T$,$\mu_C$): This is the average value of the metric in interest as obtained from the user telemetry after running the experiment for some days.
3. Absolute Sample Delta ($\mu_T$ – $\mu_C$): The difference in sample means between treatment and control group.
4. Sample standard deviation ($s^2_T$ ,$s^2_C$): This is the variance in metric for treatment and control group.
5. Sample Count ($N_T$,$N_C$): This is the total user count obtained from user telemetry.
6. Sample standard deviation (s) of absolute sample delta $s=\sqrt{\frac{s_{T}^{2}}{N_{T}}+\frac{s_{C}^{2}}{N_{C}}}$
7. Equivalence bounds $\left(b_{A L}, b_{A U}, b_{R L}, b_{R U}\right)$

- This is the bound set by the experimenter. This can be understood as the “acceptable” range. Anything outside this range should fire an alert and that’s the hypothesis we have set. The absolute and relative bounds are denoted by:
  - Absolute Lower Bound: $b_{AL}$
  - Absolute Upper Bound: $b_{AU}$
  - Relative Lower Bound: $b_{BL}$
  - Relative Upper Bound: $b_{RU}$

8. Test-Statistic $(t_{A L}, t_{A U}, t_{R L}, t_{R U})$

- A test statistdic is a random variable that is calculated from sample data. It measures the degree of agreement between a sample of data and the null hypothesis. Test statistic is denoted by
  - Absolute Lower $t_{A L}=\frac{\left(m_{T}-m_{C}\right)-b_{A L}}{s}$
  - Absolute Upper $t_{A U}=\frac{\left(m_{T}-m_{C}\right)-b_{A U}}{s}$
  - Relative Lower $t_{R L}=\frac{\left(m_{T}-m_{C}\right)-b_{R L} \mu C}{s}$
  - Relative Upper $t_{R U}=\frac{\left(m_{T}-m_{C}\right)-b_{R U} \mu C}{s}$

9. P-value $\left(p_{A L}, p_{A U}, p_{R L}, p_{R U}\right)$

- It is the probability of obtaining results as extreme as the observed results of a statistical hypothesis test, assuming that the null hypothesis is true.
  - Absolute : $p_{A L}=P\left(X \lt t_{A L}\right), {p}_{A U}=P\left(X \gt t_{A U}\right)$
  - Relative : $p_{R L}=P\left(X \lt t_{R L}\right), {p}_{R U}=P\left(X \gt t_{R U}\right)$

**Reference**

- <https://www.microsoft.com/en-us/research/group/experimentation-platform-exp/articles/alerting-in-microsofts-experimentation-platform-exp/>

Alert 시스템을 어떻게 구성했는지에 대해서 말해주는 좋은 Article 이였던것 같습니다. 다만 False Positive 문제때문에 p-value 를 거의 0.001 수준으로 설정해야할것 같은데, 이것을 어떻게 잘 ㅈ절하는 방법이 있는지는 더 찾아봐야 겠네요. (Reference 링크에 들어가면 더 많이 나오기는 하는데.. 논문 타고타고 읽을것이 너무 많네요...... 시간은 없고... ) 
{: .notice--success}

