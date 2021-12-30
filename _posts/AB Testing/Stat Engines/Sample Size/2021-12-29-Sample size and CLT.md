---
title: "Why 50 vs 50 Split"
excerpt: "샘플의 수는 왜 50 50 으로 나누는가"
tags:
  - AB_Stat
last_modified_at: 2021-12-13
toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

A/B Testing 에서 Proportion 검정하는방법
{: .notice--warning}

# [Sample size in CLT](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

- 우리는 AB 테스트를 할때에, 늘 정확치 않은 Treatment 에 대해서 정확히 추정하고자 합니다,
- 그래서 기존의 50% vs 50% 분할을 사용하지 않고, 10% vs 90% 를 사용할 수 있을까? 라고 물어보기도 합니다.
- 결론부터 말하자면 '테스트를 할 수 있으나, 그 정확성이 감소' 하게 됩니다.
  - 왜냐하면 주로 , AB Test 가 검정하고자 하는것은 Control 과 Treatment 의 차이입니다.
  - 즉 Control 의 평균과 Treatment 의 평균 모두 정확하게 측정해야 하기 때문에 둘다 50/50 으로 공평하게 분배하는게 좋습니다.
- 물론, "Control 의 경우 히스토리가 충분히 있는데 굳이 50% 로 배분해줘야 할까요?" 라고 할 수 있겠지만,  '실험을 진행할떄의 Control' 값은 아무도 모릅니다. 과거 데이터로도 추정이 불가능하고, 오로지 실험을 통해서 추정해야 되는 값인 것입니다.
  - 그러므로 50 / 50 분배가 최고입니다.

> ##  동일하지 않은 표본 크기가 효율적입니까?

- 여기에서는  15% conversion rate / 90% power /  90% confidence 를 이용하여 총 50000 샘플을 비교시에, 50:50 분배와 10:90 분배를 진행할 경우 어떻게 달라지는지에 대해서 살펴봅시다.

```R
library(pwr)

n1 = 25000
n2 = 25000
p1 = 0.15
p2 = 0.16
h = abs(2*asin(sqrt(p1))-2*asin(sqrt(p2)))

pwr.2p2n.test(h, n1=n1, n2=n2, sig.level=0.10
```

```
n1 = 25000
n2 = 25000
sig.level = 0.1
power = 0.9257466
alternative = two.sided
```

- 따라서 50-50 분할로 원하는 결과를 얻으려면 총 사용자 50,000명(변이 항목당 25,000명)을 대상으로 실험을 실행해야 합니다. 대신 10-90 분할을 사용하면 어떻게 됩니까?

```R
n1 = 5000
n2 = 45000
```

```
pwr.2p2n.test(h, n1=n1, n2=n2, sig.level=0.10)
             n1 = 5000
             n2 = 45000
      sig.level = 0.1
          power = 0.5829899
    alternative = two.sided
```

- 위를 보면 Power 가 0.58 까지 급격하게 떨어지는것을 볼 수 있습니다. 
- 과연 이전과 비슷한 (50/50) 수준을 맞추려면 어떻게 해야할까요?

```R
n1 = 5000 * 2.8
n2 = 45000 * 2.8

pwr.2p2n.test(h, n1=n1, n2=n2, sig.level=0.10)
             n1 = 14000
             n2 = 126000
      sig.level = 0.1
          power = 0.9274638
    alternative = two.sided
```

- 따라서 10-90 할당은 50-50 분할과 유사한 결과에 도달하기 위해 총 사용자 수의 **2.8배가** 필요합니다 . 

> ## Math

- Two - sample binomal Test 의 경우, 아래와 같이 

$$S E_{\Delta}=\sqrt{\frac{p_{a}\left(1-p_{a}\right)}{n_{a}}+\frac{p_{b}\left(1-p_{b}\right)}{n_{b}}}$$

- 우리는 신뢰 구간의 폭을 정의하는 두 이항 비율의 차이의 표준 오차 공식을 보면 이것이 왜 그런지 이해할 수 있습니다.에스이자형△=피ㅏ(ㅏ-피ㅏ)Nㅏ+피비(1-피비)N비표준 오차가 낮을수록 확실성이 높아집니다. 전체 항은 두 변형 중 하나에서 샘플을 수집할 때마다 감소하고 둘 중 하나를 증가시킵니다.N1 또는 N2. 그러나 다음과 같이 수익이 감소하고 있습니다.N나증가합니다. 변형 A에서 이미 1000개의 샘플을 수집했지만 변형 B에서는 100개의 샘플만 수집했다고 가정합니다. A에서 추가로 100개의 샘플을 수집하면 제곱근 아래 항의 절반만 10% 감소하는 반면 B에서 추가로 100개의 샘플은 반으로 그 기간.

## 동일하지 않은 표본 크기는 언제 의미가 있습니까?

위의 R 출력을 자세히 살펴보면 필요한 *총* 사용자 수는 2.8x이지만 컨트롤 그룹( `n1`)에 할당된 사용자 수 는 실제로 14k 대 25k로 더 적습니다. 따라서 우리가 우리의 변화에 대해 매우 강한 [사전 믿음](https://en.wikipedia.org/wiki/Prior_probability) 을 갖고 있지만 여전히 형식적인 실험을 수행하고 싶다면 표본 크기가 같지 않다는 것이 여기에서 의미가 있을 수 있습니다. 그러나 그것은 양날의 검입니다. 변경 사항이 기준선보다 *나쁘면* 궁극적으로 결정적인 결과에 도달하는 데 필요한 것보다 더 많은 사용자를 변경 사항에 노출하게 될 것입니다. 일반적인 A/B 테스트 디자인에는 [이미 고려할 요소가 충분히](https://geoffruddock.com/ab-testing-with-a-symmetric-risk-profile/) 포함되어 있으므로 50-50으로 유지하는 것이 가장 좋습니다 .

---

**reference**

- https://geoffruddock.com/run-ab-test-with-unequal-sample-size/



