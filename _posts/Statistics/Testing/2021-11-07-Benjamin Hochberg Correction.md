---
title:  "Benjamini Hpchberg Correction Method"
excerpt: "다중 비교에서 BH-adjusted p-values 를 이용하여 FDR 조절하기"
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

# [False Discovery Rate](#link){: .btn .btn--primary}{: .align-center}

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
- 위와 같은 FDR 을 추정 결과로부터 알 수 있다면 우리는 실험에서 좋은 정보가 될 것입니다.

- 하지만 우리는 이러한 값을 어떻게 추정할 수 있을까요? 

# [Main idea](#link){: .btn .btn--primary}{: .align-center}

> ## Example

- 한 제약 회사에서 96개의 세포 종류 대해서 기존약에 대비하여 신약의 효과를 검정하려 한다고 합시다.
  - 각 세포에 대해서 약이 잘 듣는 경우와 효과 없는 경우 두가지가 있을것입니다.

> ## 효과 없는 세포인 경우의 p-value 분포

![png](/assets/images/Stat/93_7.png)

- 위와 같이 같은 분포에 대해서 샘플(다른 색깔) 을 두개 뽑아서 , 그 차이가 유의한지 아닌지에 대해서 p-value 를 형성해 봅시다.

![png](/assets/images/Stat/93_6.png)

- 같은 두개의 분포에 대해서, 그 차이를 검정하는 p-value 를 Generating 하게 되면 위처럼 p-value 는 Uniform 한 분포를 띠게 됩니다. (즉 A/A Testing 을 여러번 한것)
  - 당연히 p-value 는 '귀무가설이 사실일떄 데이터가 이상한 정도를 percentile' 로 표현한 것이므로 A/A Testing 은 귀무가설이 사실인 상태에서 Generating 한 것이기 떄문에, 이러한 분포가 Uniform 하게 나타날수밖에 없습니다.

> ## 효과 있는 세포인 경우의 p-value 분포

![png](/assets/images/Stat/93_8.png)

- 이번에는 위와 같이  Control 과 실제로 다른 Treatment 에 대해서 실제로 A/B Testing 을 수행해 보았습니다.

![png](/assets/images/Stat/93_9.png)

- 그 결과는 위와 같이 p-value 는 Uniform 하지 않고, 0.05 보다 낮은 값에 많이 분포하고 있는것을 볼 수 있습니다. 즉 우리가 원하는 결과입니다!

> ## 두개가 섞인 10000개의 세포에 대한 (Multiple Comparison) p-value 검정 결과

![png](/assets/images/Stat/93_10.png)

- 위와 같이 1000개의 효과가 있었던 세포와 9000개의 효과가 없는 세포의 p-value 결과가 합쳐져서 10000개의 Mutivariate Testing 의 p-value 결과는 약간의 exponential 과 같은 분포가 형성되게 됩니다.

> ## p-value 검정 결과의 분해

![png](/assets/images/Stat/93_11.png)

![png](/assets/images/Stat/93_12.png)

- 우리는 검정 결과를 위와 같이 두가지의 효과로 분해할 수 있습니다. 
- 즉 우리는 그래프를 볼때에 True Positive 와 False Positive 를 분리할 수 있을것입니다. 

> ## 결과로부터의 FDR 추정

- 하지만 우리는 위와 같이 분해된 결과를 얻는게 아니라 , 합쳐진 p-value distribution 을 얻을것입니다. 

![png](/assets/images/Stat/93_13.png)

- 이떄 위와 같이 Uniform 한 Line 은 바로 '효과 없는 대부분의 세포' 에 의한 효과라고 추정할 수 있습니다. 

![png](/assets/images/Stat/93_14.png)

- 즉 위와 같이 우리가 0.05 를 결정의 Threshold 로 여길때에는 Uniform Line 으로부터 False positive 와 True positive 를 분해할 수 있고, 여기에서 우리는 FDR 이 대략적으로 450  / (450+ 450) = 50% 라고 추정할 수 있을것입니다.

# [Benjamini Hpchberg Method](#link){: .btn .btn--primary}{: .align-center}

> ## Method 

- 메인 아이디어는 이전 Example 에서 얻은 아이디어가 될 것입니다.
- Adjusted p value 를 이용하여서 우리는 False positive 의 수를 조절하려고 합니다. 
  - 이러한 adjusted p -value 의 의미는, p 값을 좀 더 크게 키운다는 의미입니다.
  - 즉 FDR correction 을 수행하기 전에 0.04 였다면 FDR correction 을 수행하고 난 이후에는 0.06 이 될 수 있습니다. (더이상 유의하지 않음)
- 만일 cut off sifnificance FDR < 0.05 로 설정한다면 5% 의 significant result 중에서 5% 만이 False Positive rate 가 될 것입니다.
  - 즉 효과가 있다! 라고 말한 결과 중에서 그 말이 틀릴 비율은 5% 미만이 될것이라는 의미입니다.

> ## Procedure

> 1.많은 실험들에 대해서 p value 를 작은것부터 큰것까지 Ordering 시키고 랭킹을 매깁니다..

![png](/assets/images/Stat/93_15.png)

- 위의 경우에, 딱 하나의 실험만 유의 (0.05 이하) 하다는것을 기억합시다.

> 2.FDR 으로 조절될 p-value 를 계산합니다.

- 이때 제일 큰 p-value 에 대해서는 adj p value 값도 이전의 p value 와 동일합니다.

![png](/assets/images/Stat/93_16.png)

- 그리고 이후 낮은 랭크의 실험에 대해서는 다음과 같이 계산됩니다.

$$p-value_{adj} = min(\text{이전의 adj p value , 현재 p value  $\cdot \frac{p \ value\  갯수}{p\  value\  rank}$})$$

![png](/assets/images/Stat/93_17.png)

> 3.위 과정을 계속 반복합니다.

![png](/assets/images/Stat/93_18.png)

- 위 결과를 보면, 더 이상 유의한 실험이 없게 되었습니다 ! 

> ## Example

- 이전에 우리가 고려했던 Example 과 비슷한 상황을 봅시다.

![png](/assets/images/Stat/93_19.png)

- 빨간 박스는 실험이 효과가 없을때에 계산되는 P-value 입니다.
- 파란 박스는 실험이 효과가 있을때에 계산되는 P-value 입니다.
- 0.05 를 기준으로 삼을때에도 우리는 False Positive 의 수가 많은것을 볼 수 있습니다. 

![png](/assets/images/Stat/93_20.png)

- 위처럼 Benjamini Hpchberg 방법을 사용하여 False Discovory rate 를 조절할 수 있게됩니다! 

> ## More

- Benjamini-Hochberg 절차는 개별 검정들이 독립적이라고 가정합니다.
- FDR 을 제어하는 방법론이기 때문에, FWER 에 비해서 좀 덜 Conservative 합니다.
  - 그러므로 더 높은 Power 를 가질 수 있습니다.
  - 하지만 제 1종 오류는 여전히 높을 수 있음을 기억합시다. 
- FWER 통제하는 방법 : 한개 이상의 1종 오류가 발생할 가능성에 대해서 통제하게 됩니다.
  - 즉 100 개의 Comparison 을 실시하는 Multivariate Testing 을 실시한다고 합시다.
  - Multivariate Testing 을 무한히 반복할때에, 100개의 Compariosn 이 모두 효과가 없을때에 , 잘못된 판단을 내릴 확률을 0.05 로 제한합니다.
- FDR 통제 : 실험에 대해서 False Positive / (False Positive + True Positive) 를 제한하는 방법론입니다.
  - 즉 100개의 Comparison 을 실시하는 Multivariate Testing 을 실시한다고 합시다.
  - 이 경우에 FDR 을 0.05 로 설정할 경우 '각 Multivariate Testing' 이 '효과 있다고' 결론 내린 실험들에 대해서 사실 효과가 없는 실험의 비율을 5% 로 제한하는 방법론입니다.
  - 즉 각 Multivariate Testin '어느정도 틀려도 되지만 효과가 있다고 결론내린 경우 그 정확성을 95% 로 유지' 하게 됩니다.
- 정리하면 FWER 보다 FDR 이 좀 더 관대하게 바라보는 방법입니다.

---

**Reference**

- <https://stats.stackexchange.com/questions/238458/whats-the-formula-for-the-benjamini-hochberg-adjusted-p-value>
- <https://www.youtube.com/watch?v=K8LQSvtjcEo>
- <https://ekja.org/upload/pdf/kja-71-5-353-ko.pdf>
- <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6193594/>

