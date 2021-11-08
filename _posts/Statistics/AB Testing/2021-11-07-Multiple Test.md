---
title: "A/B/n Testing and False Positive"
excerpt: "A/B/n 테스트와 문제점 그리고 이를 해결하는법"
categories:
  - AB_Testing
last_modified_at: 2021-11-07

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 A/B/n 테스트에 대해서 알아보겠습니다. 통계학을 하신 분이라면 딱 보아도 False Positive Inflation 이 걱정될거같은데요.. 이것을 어떻게 Control 할 수 있을지에 대해서 알아보려고합니다.
{: .notice--warning}

# [Tests with More than one variant](#link){: .btn .btn--primary}{: .align-center}

- 우리는 실험을 할때에 다수의 Treatment 에 대해서 동시에 진행할 수 있습니다.
  - 예를 들면  기존의 추천 시스템이 존재하고, 이를 개선하기 위해서 추천시스템1 , 추천시스템2 두개를 한번에 테스트할 수 있다는 것입니다. (이 경우 A/B/C 테스트가 됩니다.)
- 물론 모든 조합에 대해서 검사해보는 Multivariate 실험도 있지만 이 두가지 개념은 혼용되어서 사용되므로 여기에서는 Multivariate = A/B/n Test 로 통일해서 부르도록 하겠습니다.
- 일반적으로 A/B/n Testing Platform 을 들어가보면 Variants 의 갯수 제한 없이 마구잡이로 실험이 전개되는것을 볼 수 있습니다.
  - 하지만 'Theoretically upper limit' 이 존재하고, 이를 인지하는것이 중요합니다.

> ## Type 1 error in A/B/n Test

- A/B/n Test 를 수행할때 주로 pairwise significant test 를 수행하면서 제일 큰 Z - Test 통계량을 가지는 Variant 를 승자로 결정하게 됩니다. 
- 즉 자세히 말하면 다음과 같습니다. 
  - A/B/C/D 테스트를 기획한다고 합시다. 
  - B vs A , C vs A , D vs A 에 대해서 Two sample Test 를 진행하니 p-value 가 (0.3 , 0.11, 0.04) 가 나왔다고 합시다. 그렇다면 이때에 D vs A 만 유의하며 D 를 승자로 처리합니다. 
  - 만일 이에 대해서 (0.3, 0.01, 0.02) 이 나온다면 우리는 더 p 값이 작은 (즉 Z 값이 작은) C를 승자로 처리할 수 있습니다. 
  - 또는 Confidence interval 을 이용하여 테스트할수도 있습니다.
- 하지만 이러한 접근법에 대한 issue 는 바로 False Positive Error (Type 1 error) 입니다.

> Family Wise Error Rate (FWER)

- 일반적으로 m 개의 테스트를 동시에 수행하게 되면 우리는, 이 결과가 틀릴 확률 (즉 하나 이상 틀릴 확률) 은 다음과 같이 계산됩니다. (각 실험의 Type 1 error 는 $\alpha$ 라고 가정합니다.)

$$FWER(\alpha , m) = 1 - (1-\alpha)^m$$

- 만약 4개의 Variant (즉 A,B,C,D) 에 대해서 실험을 진행하게 될 경우 우리는 다음과 같이 실험이 진행됩니다.
  - Test 는 3개로서 , $\mu_A - \mu_B$ , $\mu_A - \mu _c$ , $\mu _A - \mu_D$ 가 진행됩니다.
  - 3개가 진행되므로 FWER 은 $1-0.95^3 \approx 0.86 $ 즉 $14\%$ 의 FWER 가 존재하게 됩니다. 
- 물론 위와 같은 테스트는 매우 보수적인 계산법입니다. 왜냐하면 Test 간의 Dependency 는 고려하지 않은것이기 떄문입니다.
  - 위의 계산에서, FWER 을 계산할때 마치 모든 Test 를 독립된것처럼 취급했던것을 기억하세요! 
  - 하지만 모든 Test 는 독립이 아닙니다. (모두 같은 Control 과 비교중임)

> ## Control of FWER 

- 이러한 FWER 을 컨트롤하기 위해서는 어떻게 해야 할까요? 

> 각 테스트의 Significant level 조절하기 (Bonferroni Correlation)

- 만약 A/B/C/D 테스트를 진행하게 된다면 우리는 총 3개의 Comparison 을 해야 되므로 각 테스트의 Sigfnificant level 을 $\alpha/3$ 으로 조절하는 것입니다.
  - 즉 0.05 를 사용했다라면 0.0166 이 Significant level 이 되는것입니다.
- 만일 A/B/C/D/E 를 사용한다면 0.0125가 될 것입니다. 
- 하지만 이러한 방법은 사실 아래와 같은 Proof 에 기초합니다.

![png](/assets/images/Stat/93_1.png)

- 즉 Bonferroni Correlation 은 '부등식' 기반으로 FWER 을 Control 하기 때문에 실제 Significant level 보다 더 작게 잡아버린다는 것입니다. (지나치게 Conservative)
  - 테스트 갯수가 3개라 0.0166 으로 Significant level 을 잡은 경우 정확한 FWER 값은 $1-0.983^3 = 0.049$ 
  - 테스트 갯수가 4개라 0.0125 로 Significant level 을 잡은경우 정확한 FWER 값은 $1-(1-0.0125)^4 = 0.049$
- 물론 Variant 가 적은 경우 위와 같은 차이는 어느정도 감수할만 하며, 이러한 차이도 사전에 잘 알아두어야 할 것입니다.

> Holm-Bonferroni step down 

- 이 방법도 역시나 FWER 를 Control 하는 방법입니다. (자세한건 Testing 부분에서 다루었습니다. 참조)
- Bonferroni 보다 조금 더 Power 가 높은것으로 알려져 있습니다.

> ## Control FDR

- 이러한 FDR 을 Control 하는 방법은 대표적으로 Benjamin Hochberg Correction 이 있습니다.
  - 이 방법은 p-value 를 조절하는 방법론입니다.
- 이 방법도 자세한것은 다루지 않겠습니다. (Testing 부분 참조)

> ## Adjusted Confidence interval

- 우리는 위와 같이 '조절된 p-value' 를 얻게 되었을때 검정을 할 수 있게 됩니다.
  - 하지만 '우리가 A/B Testing 에서 중요하게 여기는 부분은 바로 CI 입니다' 
- p value 에서 어떻게 하면 Confidence interval 을 얻을 수 있을까요? 
- 만약 unadjusted p-value 가 0.01 이고, adjusted 된 p-value 가 0.03 이라고 합니다. 
  - 그러면 adjusted ratio 는 0.01/0,03 = 1/3 입니다.
  - 즉 95% interval 을 생성할때에 우리는 Confidence level 에서 1/3 을 곱합니다. 
- 즉 1 - (0.05 * 1/3) = 0.983% 의 Confidence interval 을 생성해야 Actual Confidence interval 을 얻을 수 있습니다. 

> ## Sample size Calculations 

- Type 1 error 의 inflation 영향으로 우리는 개별 실험에 대해서 p-value 를 낮추거나 $\alpha$ 를 낮추는 등의 작업을 하였습니다. 
  - 하지만 이러한 작업은 결국 Trade off 가 존재하는데, 여기에서는 각 실험의 1종 오류율을 낮추었으므로 결과적으로 Power 가 감소하게 될 것입니다. 
- 그러므로 일반적으로 같은 Power 을 유지하고자 하면 '각각의 A/B Testing' 을 진행할때에 보다 더 많은 샘플이 필요하게 될 것입니다. 
- 사실 Multiple Testing 에서 통용될만한 Sample size Calcultion 은 아직 없는듯 합니다.. (이 부분은 나중에 추가 예정) 

**reference**

- Statistical Methods in Online A/B Testing (Books)

