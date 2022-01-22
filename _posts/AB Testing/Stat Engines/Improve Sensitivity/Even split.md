# [Sample size 50/50](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

- 우리는 AB 테스트를 할때에, 늘 정확치 않은 Treatment 에 대해서 정확히 추정하고자 합니다,
- 그래서 기존의 50% vs 50% 분할을 사용하지 않고, 10% vs 90% 를 사용할 수 있을까? 라고 물어보기도 합니다.
- 결론부터 말하자면 '테스트를 할 수 있으나, 그 정확성이 감소' 하게 됩니다.
  - 왜냐하면 주로 , AB Test 가 검정하고자 하는것은 Control 과 Treatment 의 차이입니다.
  - 즉 Control 의 평균과 Treatment 의 평균 모두 정확하게 측정해야 하기 때문에 둘다 50/50 으로 공평하게 분배하는게 좋습니다.
- 물론, "Control 의 경우 히스토리가 충분히 있는데 굳이 50% 로 배분해줘야 할까요?" 라고 할 수 있겠지만,  '실험을 진행할떄의 Control' 값은 아무도 모릅니다. 과거 데이터로도 추정이 불가능하고, 오로지 실험을 통해서 추정해야 되는 값인 것입니다.
  - 그러므로 50 / 50 분배가 최고입니다.

> ##  동일하지 않은 표본 크기가 효율적일까?

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

- Two - sample Test 의 경우, 아래와 같이 식이 계산됩니다. 
- Proportion 의 경우 Standard Error 는 아래와 같습니다.

$$S E_{\Delta}=\sqrt{\frac{p_{a}\left(1-p_{a}\right)}{n_{a}}+\frac{p_{b}\left(1-p_{b}\right)}{n_{b}}}$$

- Mean 의 경우 Standard Error 는 아래와 같습니다.

$$SE_{\Delta} =\sqrt{\frac{s_{a}^{2}}{n_{a}}+\frac{s_{b}^{2}}{n_{b}}}$$

- 위에서, Standard Estimator 안의 값을 최소화 하기 위해서라면 어떤 값을 넣어야 할까요? 이떄 필요한 정리는 아래의 $T_2$ 정리가 필요합니다.

> T $_{2}$ 의 도움정리(Titu's lemma)

- 임의의 $n$ 개의 실수 $a_{1}, a_{2}, \ldots, a_{n}$ 과 $n$ 개의 양의 실수 $b_{1}, b_{2}, \ldots, b_{n}$ 에 대하여, 다음 부등식이 성립한다.

$$\frac{a_{1}^{2}}{b_{1}}+\frac{a_{2}^{2}}{b_{2}}+\cdots+\frac{a_{n}^{2}}{b_{n}} \geq \frac{\left(a_{1}+a_{2}+\cdots+a_{n}\right)^{2}}{b_{1}+b_{2}+\cdots+b_{n}}$$

- 등호 성립은 $\frac{a_{1}}{x_{1}}=\frac{a_{2}}{x_{2}}=\cdots=\frac{a_{n}}{x_{n}}$ 이다.

> SE Calculation

- 위 정리에 따르면 , SE 가 최소화 되기 위해서는 아래와 같아야 합니다. 
  -  $n_a/n_b =  $ $p_a(1-p_a)/p_b(1-p_b)$ 
  -  $n_a/n_b = s_a^2 /s_b^2$
- 하지만.. 위 경우에 대해서 우리는 True 값인 비율 , 분산을 알 수 있나요? 없습니다!
  - Treatment 의 분산을 생각해보세요. Treatment 의 효과 '우리가 실험을 하고 난 이후' 에나 알 수 있는 효과인데, "실험 전에 샘플 수" 를 결정해야 되는 입장에서는 모순이 됩니다.
  - 이 경우에 $s_a$ 와 $s_b$ 에 대해서 어떤 추정을 해야할까요?

> Estimating

-  '대부분의 A/B Testing' 의 경우 Treatment 와 Control 가 거의 비슷하다. 라는것을 생각해봅시다. 
-  즉 Variance 도 거의 일치하겠죠. 이런 상황에서 두개의 분산이 어느정도 일치한다고 가정하는것은 합리적이고, 이러한 맥락에 따라 필요한 샘플 수의 비는 아래와 같습니다.
-  SE 가 최소화 되기 위해서는 아래와 같아야 합니다. 
   -  $n_a/n_b =  $ $p_a(1-p_a)/p_b(1-p_b) = 1$ 
   -  $n_a/n_b = s_a^2 /s_b^2 = 1$

> ##  동일하지 않은 표본 크기는 언제 의미가 있을까?

```
n1 = 25000
n2 = 25000
sig.level = 0.1
power = 0.9257466
alternative = two.sided
```

```
n1 = 14000
n2 = 126000
sig.level = 0.1
power = 0.9274638
alternative = two.sided
```

- 위처럼 이전의 R 출력을 자세히 살펴보면, 전체적으로 필요한 사용자 수는 2.8배가 되었지만 (n = 25000 + 25000 -> n = 14000 + 126000) Control Group 에 속한 사용자 그룹은 14k 로, 이전의 25k 보다 더 작습니다.
- 즉 우리가 Treatment 에 대해서 '이 Treatment 는 무조건 좋을거야!' 라는 확신(사전 믿음) 을 가지고 있지만, 여전히 실험을 어느정도 수행하고 싶을때에 위처럼 power 를 유지한채로 테스트를 수행할 수 있겠죠. 
- 또는 그 반대로 , Treatment 에 대해서 "이 Treatment 는 안좋을거같아 !" 라는 확신 (사전믿음) 을 가지고 있으면 n1 을 크게 한 채로 n2 를 줄일수도 있겠습니다. 
- 하지만 위와 같은 설정은 양날의 검입니다. Treatment 에 많은 사용자를 할당햇는데, Treatment 가 안좋으면 많은 사용자에게 안좋은 경험을 하게 할 것입니다. 
- 일반적인 A/B 테스트 디자인에는 [이미 고려할 요소가 충분히](https://geoffruddock.com/ab-testing-with-a-symmetric-risk-profile/) 를 충분히 고려하므로 50-50으로 유지하는 것이 가장 좋습니다 .

> ## Conclusion

- A,B 두 샘플을 동일하게 나누어야, 더 높은 품질(Sensitivity) 의 실험을 만들 수 있습니다!

---

**reference**

- https://geoffruddock.com/run-ab-test-with-unequal-sample-size/