---
title:  "Multiple and Test Correction"
excerpt: "다중 비교 문제점 보완하기"
categories:
  - Stat_Testing
last_modified_at: 2021-11-07

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 다중 비교는 False Positive Inflation 이라는 문제점을 가지고 있습니다. 이러한 문제점을 해결하기 위해서 어떤방법을 활용할 수 있을까요? 
{: .notice--warning}

# [Introduction](#link){: .btn .btn--primary}{: .align-center}

> ## Family - wise Error rate (FWER)

- Family wise Error rate (FWER) 은 하나 이상의 False Positive discovery 를 할 확률입니다. 
  - 여러개의 Testing 을 한번에 진행할때에 하나 이상 False Positive (Type 1 error) 의 오류를 범할 확률을 나타냅니다. 

> ## Multiple Comparison Problem

- Multiple Comparison 이란, 여러개의 가설을 한꺼번에 검정하는 것 입니다. 
  - 하지만 이렇게 설정할 경우, 여러개의 비교가 틀릴 확률 (즉 한개 이상의 비교가 틀릴 확률) 은 매우 커지게 됩니다. 이는 아래 경우를 살펴보면 알 수 있습니다.

![png](/assets/images/Stat/93_3.png)

- 위의 그래프를 볼때, 
- 그러므로 이러한 다중비교시에 일어나는 False Positive Inflation 을 해결하기 위하여 어떠한 조절 (Correlation) 을 해야될지 살펴봅시다.

# [Multiple Test Correlation : FWER](#link){: .btn .btn--primary}{: .align-center}

> ## Bonferroni Correlation

- 만약 m 개의 Comparison 을 하게 된다면 테스트의 Sigfnificant level 을 $\alpha/m$ 으로 조절하는 것을 Bonfferoni Correlation 이라고 합니다. 

$$\alpha_{Bon} = \alpha / m$$

- 즉 0.05 를 사용하고, 3개의 Comparison 을 사용하게 된다면 0.0166 이 Significant level 이 되는것입니다.
  - 만일 A/B/C/D/E 를 사용한다면 0.0125가 될 것입니다. 

> Proof

- 이러한 방법은 사실 아래와 같은 Proof 에 기초합니다.

![png](/assets/images/Stat/93_1.png)

- 즉 Bonferroni Correlation 은 '부등식' 기반으로 FWER 을 Control 하기 때문에 실제 Significant level 보다 더 작게 잡아버린다는 것입니다. (지나치게 Conservative)
  - 테스트 갯수가 3개라 0.0166 으로 Significant level 을 잡은 경우 정확한 FWER 값은 $1-0.983^3 = 0.049$ 
  - 테스트 갯수가 4개라 0.0125 로 Significant level 을 잡은경우 정확한 FWER 값은 $1-(1-0.0125)^4 = 0.049$
- 물론 Variant 가 적은 경우 위와 같은 차이는 어느정도 감수할만 할 것입니다. (Variant 의 수가 많아질수록 왜곡이 심해지기는 함)

> 특징

- 지나치게 Conservative 하여 FWER 은 잘 조절하지만 Power 가 약할 우려가 있습니다.
- 매우 이해하기 쉽고, 적용이 쉬워 다양한 분야에서 이용됩니다.

> ## SIdak Correlation

- Sidak Correlation 이란 m개의 multiple comparison 비교에 대해서 다음과 같이 유의수준 ($\alpha$) 을 조절하는 방법입니다.

$$\alpha_{SID} = 1 - (1-\alpha)^{1/m}$$

- 위와 같이 설정하게 된다면, 우리는 정확한 FWER 값을 조절할 수 있습니다. 
- 위의 Sidak Correlation 을 적용하여 우리의 테스트에 Correlation 을 줄때 FWER 은 다음과 같이 계산됩니다. 

$$FWER(\alpha,m) = 1- (1 - \alpha_{SID})^m = \alpha$$

- 즉 FWER 을 정확하게 $\alpha$ 로 조절할 수 있습니다.

> 특징 

- Bonferrnoni 방법보다 더 정확하게 FWER 을 조절할 수 있습니다. 
- 또한 Bonferrnoi 방법보다 약간 덜 Conservative 합니다. 
  - $\alpha = 0.05 , m =10$ 인 경우 Bonferonni adjustment level 은 0.005 이고 Sidak Correlation 은 0.005116 입니다. (매우 미세한 차이)

> ### Tukey's procedure (Tukey's rang Test)

- Tukey method, tuckey test 등으로 불리우는 이러한 방법은 Studentized range distribution 에 기반하여 Two means 를 테스트 하는 방법론입니다. 
  - 이는 모든 Treatment 끼리의 평균을 비교할 수 있는 방법론입니다.  즉 모든 $\mu_i - \mu_j$ 를 비교할 수 있는 방법론입니다.  
  - 여기에서 논의되는 방법은 Treatment 끼리 Equal Variance 일때의 경우라는것을 명십합시다.
- Tukey Procedure 은 오로지 Pairwise comparison 에만 적용됩니다. 그리고 다음과 같은 Assumption 이 있으므로 주의하는게 좋습니다.
- Assumption 
  1. The observations being tested are [independent](https://en.wikipedia.org/wiki/Statistical_independence) within and among the groups.
  2. The groups associated with each mean in the test are [normally distributed](https://en.wikipedia.org/wiki/Normal_distribution).
  3. There is equal within-group variance across the groups associated with each mean in the test ([homogeneity of variance](https://en.wikipedia.org/wiki/Homoscedasticity)).
- 정확하게 말하자면 다음과 같습니다.

![png](/assets/images/Stat/93_2.png)

- 즉 $X_{ij} = \mu_i + \epsilon_{ij}$ 이고 $\epsilon_{ij}\sim N(0,\sigma^2)$ 와 같이 각 그룹의 Mean 은 다르되, 가 데이터가 등분산 Normal 을 따를때에 쓸 수 있는 방법론이라는 것이죠. 
- 이러한 한계를 가지기 떄문에 여기에서는 생략하도록 하겠습니다. 

> ## Dunnett , Fisher LSD, Scheffe ...

- 이 밖에도 ANOVA 이후에 행해지는 사후 평균 비교 방법으로 다양한 방법론들이 있습니다.
  - <http://www.stat.uchicago.edu/~yibi/teaching/stat222/2017/Lectures/C05.pdf>
- 하지만 이러한 방법론들은 결국에 ANOVA 의 Assumption (그룹별로 Normal 분포 등) 를 공유합니다.
  - 여기에서는 그러한 제한이 있는 방법론은 일단 다루지 않으려고 합니다. (나중에 ANOVA 와 그 이후 방법론에 대해서는 정리하도록 하겠습니다.) 



# [Multiple Test Correlation : FDR](#link){: .btn .btn--primary}{: .align-center}

> ## False Discovery Rate (FDR)

- False discovery tate 는 다중비교에서 False positive / Total Positive 의 비율을 의미합니다.
  - 즉 False Positive / (False Positive + True Positive) 입니다.
  - 이는 유의하다고 판단한것 중에서 실제로 유의하지 않은것의 비율이라고 할 수 있습니다.

> Example 

- 한 제약 회사에서 96개의 세포 종류 대해서 약의 효과를 검정한다고 합시다. 

![png](/assets/images/Stat/93_4.png)

- 위와 같이 p- value 를 0.027 로 기준을 삼았고, 이에 대해서 총 6개의 세포에게 약이 효과가 있었다고 결과가 나왔습니다.

![png](/assets/images/Stat/93_5.png)

- 하지만 위와 같이 False Positive 의 (즉 효과가 없는데 효과가 있다고 함) 경우는 3개가 있었습니다. 
  - 이는 산술적으로도 96개에서 0.027 의 p-value 수준에서는 대충 3개의 False Positive 가 발생한다고 생각할 수 있을것입니다. 
- 즉 FDR 는 50%라는 것을 알 수 있습니다. 

> ## Benjamini-Hochberg method

- 위와 같은 FDR 을 조절하는 방법은 Benjamini 방법이 있습니다.
  - 이 방법론에 대해서는 별도 문서로 나누어 놓았으니 거기에서 확인하는게 좋을것 같습니다.

> # Coclusion

- 이러한 Multiple Comparison 은 문제가 있음에도 불구하고 여러 분야에서 별다른 조치 없이 비교되고 있는 실정입니다. 
- 한 연구의 결과에 의하면, 3개의 의학 학술지에 10년간 발표 된 논문들의 다중 비교의 적합성을 조사하였는데, 조사대상의 33% (47/142)의 논문이 다중 비교 보정을 사용하지 않았고, 61% (86/142)의 논문에서는 근거 없는 보정이 적용되었으며, 단지 6.3% (9/142)의 논문만이 적합한 보정법이 적용되었다고 보고하였다고 합니다.
- 그리고 전체 논문의 35.9% 가 Bonferroni 방법을 사용하였으며, 논문의 대부분(71%)은 이에 관한 고찰을 거의 또는 전혀 제공하지 않았고, 29%만이 보정 방 법에 대한 합리적인 고찰을 기술하고 합니다. 
-  일부 저자는 보정된 P 값을 사용하지 않고 결정을 내리거나, 보정된 P 값과 보정되지 않은 P 값의 결과를 서로 비교 하기도 합니다.
- <https://ekja.org/upload/pdf/kja-71-5-353-ko.pdf>

---

**Reference**

- <https://slideplayer.com/slide/16129683/>
- <https://en.wikipedia.org/wiki/Holm%E2%80%93Bonferroni_method>
- <https://en.wikipedia.org/wiki/Multiple_comparisons_problem>
- <https://ekja.org/upload/pdf/kja-71-5-353-ko.pdf>
- <https://riffyn.com/blog/the-most-important-scientific-calculation-you-were-never-taught>

 다양한 방법론이 존재하고, 이 중에서 우리 계획에 맞게 좋은 방법론을 고르는게 좋을것입니다. ANOVA 의 후속 조치로 알려진 Dunnet , Tuckey 와 같은 방법론들은 대부분 Assumption 에 대해 종속적이기 떄문에 여기에서는 배재하였습니다.
{: .notice--success}

