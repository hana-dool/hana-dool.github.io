---
title:  "Bootstrap Testing"
excerpt: "부트스트랩을 이용한 테스트"
categories:
  - Stat_Testing
last_modified_at: 2021-11-06

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Bootstrap 을 이용한 Test 과정에 대해서 알아봅시다.
{: .notice--warning}

# [Bootstrap Testing Procedure](#link){: .btn .btn--primary}{: .align-center}

- 우리는 Montecarlo 방법론에 대해서 알아본적이 있습니다. 
- 여기에서는 Bootstrap 을 이용하여 어떻게 하면 Confidence Interval 을 생성하거나, 검정을 할 수 있을지에 대해서 알아보도록 하겠습니다.

> ## Percentile Boostrap Confidence Interval

- $X' = (X_1 ... X_n)$ 이 random Variable from cdf $F(x ; \theta)$ 라고 합시다.
- $x' = (x_1 ... x_n) $ 은 뽑아낸 랜덤샘플이라고 합시다.
- 우리는 $\theta$ 의 추정에 관심이 있어서 $\hat{\theta_n}$ 를 추정하려 합니다.
- 우리의 목표는 $100(1-\alpha)\%$ 의 신뢰구간을 얻어내려 합니다.
  - 이때 우리는 Exact 한 신뢰구간을 구하고싶지만, 이렇게 정확한 통계량을 구할 수 있는 경우는 매우 드뭅니다.
  - 그래서 현대 통계학은 대게 Asymptotic technique 을 써서 이러한 분포를 구해내려 합니다. 
- 즉, Exact 하게 구하기는 어려우므로 우리는 대안으로 BOotstrap 을 이용하려 합니다. 
- 만약 우리가 $\hat{\theta}$ 의 근사분포를 알아낸다고 합시다. 

![png](/assets/images/Stat/95_1.png)

- 그러면 위 그림에서 처럼 $(a,b)$ 는 $(100-\alpha)\%$ 의 신뢰구간이라고 할 수 있습니다. 
  - 하지만 이러한 분포를 어떻게 알아낼 수 있을까요? 

> Random Samples

- $x_i = (x_{i1} , x_{i2} .... x_{in})$  의 샘플들 이라고 합시다. 
- 이에 대해서 우리는 각각 $\hat{\theta_i} = \hat{\theta}(x_i)$ 으로, 각 샘플을 이용해 통계량의 추정치를 각각 구해낼 수 있습니다.
- 이떄에 $\hat{\theta_1} .... $ 을 이용하여 히스토그램을 그린다면 $\hat{\theta}$ 의 True Distribution 을 얻어낼 수 있을것입니다. 

> Problem

- 하지만 우리는 이러한 샘플을 '오로지 하나' 만 가지고 있다는것입니다.
  - 우리는 지금 그냥 크기 n 짜리 샘플을 하나 얻었을 뿐입니다. 
- Bootstarp 방법은 original sample $x' = (x_1....x_n)$ 에 대해서 다시 리샘플링 하여서 $$x^{*'}= (x_1^*, x_2^*... x_n^*)$$ 와 같이 새로운 샘플을 만들어 냅니다. 
  - 이때 Resampling 할때에 $x_i ... x_n$ 이 뽑힐 확률은 모두 동일합니다. 
  - 그리고 복원추출로서, 한번 뽑힌것은 계속 뽑힐 수 있습니다.
- 위와 같은 Sampling 을 B 회 반복했을때에 우리는 다음과 같은 샘플들을 얻을 것입니다 .

$$x_i^{*''}= (x_{i1}^*, x_{i2}^*... x_{in}^*) , \ \ i = 1\sim B$$

- 이때 위와 같은 행동을 $B \to \infty$ 번 반복한다면 원래 $\hat{\theta}$ 의 분포에 대해서 근사적으로 수렴하게 됩니다.

> Algorithm

1. set j = 1 
2. while $ j \le B$ 일 동안 (2) ~ (5) 의 과정을 반복합니다.
3. Let $x_j^{*'}$ 를 original sample $x' = (x_1 .. x_n)$ 로부터 j 번째 랜덤 샘플링한 샘플이라고 합시다. 
4. $\hat\theta_j^* = \hat{\theta}(x_j^*)$ 처럼 j 번째 Bootstrap sample 을 이용하여 통계량을 추정합니다.
5. j 를 j+1 로 올려줍니다. 
6. $$\hat{\theta^*_{(1)}} \le \hat{\theta^*_{(2)}} \le .... \hat{\theta^*_{(B)}}$$ 가 되게 Reordering 합니다. 그리고 $$m = [(\alpha /2 )B]$$ 라 합시다.  이떄에 $$(\hat{\theta^*_{(m)}} , \hat{\theta^*_{(B+1-m)}})$$ 은 바로 $$100(1-\alpha)\%$$ 의 Approximate Condidence Interval for $$\theta$$ 가 됩니다. 

- 위와 같은 방법을 우리는 Percentile Bootstrap Confidence interval for $\theta$ 라고 합니다.

# [Examples](#link){: .btn .btn--primary}{: .align-center}

> ## Two sample location Testing 

- Bootstrap 을 우리는 Testing 에 어떻게 활용할지에 대해서 알아봅시다.
- 우선 우리는 Two sample location problem 에 대해서 살펴봅시다 .

$$X' = (X_1 .... X_{n_1}) : \text{random sample from distribution with cdf F(x) }$$ 

$$Y' = (Y_1 .... Y_{n_3}) : \text{random sample from distribution with cdf F(x-$\Delta$) }$$

- 이때 두 분포의 퍼진 모양 , 첨도는 일치하되 그 Location 만 다른 경우라는것을 명심합시다. 
- Assuming $E(X_1) = \mu_X$ , $E(Y_1) = \mu_Y$ 라 합시다. 우리는 $\Delta = \mu_Y - \mu_X$ 라 할 수 있고, 다음과 같은 가설을 얻을 수 있ㅅ브니다. 

$$H_0 : \Delta = 0 \ \  vs \ \ H_A : \Delta > 0 $$

- 우리는 Test statstistics 를 정해야 할 것입니다. 
  - 어떤것을 정해도 되기는 하지만 (어짜피 Bootstrap 이용할것이니까) 제일 직관적인 $V = \bar{Y} - \bar{X}$ 라 합시다. 
- reject $H_0$ if $V \ge c$ 로 Decision Rule 을 정하였습니다.  (c 는 결정됨)
- Random Sample 에 대해 관찰된 값은 $(x_1 .... x_{n1})$ , $(y_1 ... y_{n2})$ 라고 하겠습니다. 
- 이떄 P value of the test 는 다음과 같습니다.

$$\hat{p} = P_{H_0} [V \ge \bar{y} - \bar{x}]$$

- 검정 통계량들의 분포를 고려할떄, 우리가 관찰한 값보다 더 극단적일 확률이 p- value 이기 떄문에 위와 같이 추정됩니다. 
- 이를 계산하기 위해서는 $H_0$ 하에서 $V$ 의 분포를 알아내야만 할 것입니다. 
  - 하지만 문제는 귀무가설($H_0$) 하에서 $V$ 의 분포를 구하는게 너무나 어려울때는 어떻게 할까요? 
  - (물론 위 예시에서는 단순히 $\bar{Y} - \bar {X}$  이지만 더 어려워질 수 있다는것을 명심합시다.)
- 부트스트랩 방법을 이용하여 이러한 p-value 를 한번 추정해보도록 합시다. 

> Algorithm

- 우리는 우선 $H_0$ 이 True 라고 가정해야 합니다. 
- 이러한 $H_0$ 하에서는 두개의 Sample (X,Y) 을 합쳐서 하나의 큰 샘플을 만들어낼 수 있습니다.
  - 이때에 귀무가설하에서는 $\Delta  =0$ 이므로 $X \sim F(x) $ , $Y \sim F(x-0)$ 가 되므로 X 와 Y 는 동일한 분포에서 왔다고 생각할 수 있습니다.
- 그러므로 귀무가설하에서는 X 와 Y 를 굳이 따로 고려하지 않고 (X,Y) 를 one large sample 로 여길 수 있다는 것입니다.

1. 두개의 Sample 을 하나의 큰 샘플 $z' = (x',y')$ 로 정의합니다. 
2. j = 1 로 정의합니다. 
3. while $j \le B $ , (3) - (6) 을 반복합니다.
4. Combine Sample $z'$ 로 부터 사이즈 $n_1$ 인 분포를 뽑아냅니다. 
   - 이때 $$x^{*'} = (x_1^* ... x_{n1}^*) $$ 는 다음과 같이 뽑습니다. 
     - $x_i^*$ 는 $z'$ 의 $n_1+n_2$ 개의 샘플에서 Uniform 하게 뽑아낸 샘플입니다.
     - x = (6,1,3) , y = (4,7) 이면 z = (6,1,3,4,7) 이 되고 , $x^*$ = (4,3,3) 이 될 수 있습니다.
   - 그리고 $$\bar{x_j^*} = \frac{1}{n_1} \sum x_i^* $$를 계산합니다.
5. 크기가 $n_2$ 개인 샘플을 $z'$ 로부터 뽑아냅니다. 
   - 이때 위와 똑같이 만들어내면 됩니다. 
     - x = (6,1,3) , y = (4,7) 이면 z = (6,1,3,4,7) 이 되고 , $y^*$ = (1,1) 이 될 수 있습니다.
   - 그리고 $$\bar{y_j^*} = \frac{1}{n_1} \sum y_i^*$$ 를 계산합니다.
6. $v_j^*$ = $\bar{y_j^*} -\bar{x_j^*} $ 를 계산합니다. 
7. Bootstrap Estimated P-value 는 다음과 같이 계산됩니다.
   - $\hat{p^*} = \frac{1}{B} \sum _ {j=1} ^ B I[v_j^* \ge \bar{y}-\bar{x}]$ 로 p-value 를 추정합니다.
   - 이러한 $\hat{p^*}$ 는 이론적으로 B 가 커질수록 $\hat{p}$ 와 같아집니다. 

> ## one sample mean test

- $X_1 , .... X_n$ 을 random sample from $F(x)$ with mean $\mu$ 라고 합시다.
- 우리가 Test 하고 싶은 가설은 다음과 같습니다. 

$$H_0 : \mu = \mu_0 \ \ H_1 : \mu > \mu_0$$

- 우리는 다음과 같이 Decision rule 을 정할 수 있습니다. 
  - $\bar{X}$ 가 너무 크면 $H_0$ 을 기각한다. 
- $(x_1 , ... x_n)$ 을 우리가 얻은 random sample 이라고 합시다. 이떄에 $\hat{p}$ 는 다음과 같이 추정됩니다.  

$$\hat{p} = P_{H_0} [\bar{X} \ge \bar{x}]$$ 

- 이떄 $\bar{X} $ 는 R.V 이고 $\bar{x}$ 는 표본평균이라는 사실을 잘 알아둡시다.
- 우리는 이러한 $H_0$ 하에서 $\bar{X}$ 의 분포를 알아내야 합니다. 
- $$z_i = x_i - \bar{x} + \mu_0$$ 과 같이 새로운 $Z$ 를 정의할 수 있습니다.
  - 위와 같이 정의한다면 우리는 $E(z^*) = \mu_0$ 을 보장할 수 있습니다. 
  - 즉 Null Hypothesis 가 True 가 되게 조절한것이라고 생각하시면 됩니다. 이렇게 조절하면 우리는 Null Hypothesis 가 True 인 상태에서의 분포를 만들어낼 수 있을것입니다. 

1. 새로운 observation $z' = (z_1 , z_2 .. z_n)$ where $z_i = x_i - \bar{x} + \mu_0$ 으로 정의합니다. 
2. Set j = 1 
3. While $j \le B$$ , (3) ~ (5) 를 반복합니다. 
4. $$z$$ 로 부터 size n 개인 random sample 을 계속 뽑아냅니다. 이러한 샘플을 $$z_j ^*$$ 라고 하고, 여기에서 부터 mean $$\bar{z_j^*}$$ 를 계산합니다.
5. j 를 j + 1 로 바꿉니다. 
6. Bootstrap estimated p-value 를 다음과 같이 추정합니다.
   - $$\hat{p^*} = \frac{1}{B} \sum_j ^ B [\bar{z_j^*} \ge \bar{x}]$$ 으로 추정될 수 있습니다.

# [Others](#link){: .btn .btn--primary}{: .align-center}

> ## Cautions

> resampling 을 수행할때에는 Original 데이터와 같은 크기를 뽑아야합니다.

- 샘플링을 수행할때에는 Original Data 와 같은 크기의 데이터를 뽑아내야 합니다.
  - 그 이유는 Statistic 의 Variation 은 그 샘플 사이즈에 depend 하기 떄문입니다.
  - 그러므로 variation 도 똑같이 추정하기 위해서라면, resampling 시에도 같은 사이즈를 만들어야 합니다.

> Bootstrap 은 최소 1000번 이상이 좋습니다.

- 아무래도 샘플을 통해서 데이터의 분포를 알아내려고 하는 만큼, 1000번 이상의 Sampling 이 필요할 것입니다. (Davison and D.V. Hinkley (1997) *Bootstrap Methods and their Application*. Cambridge: Cambridge University Press) 
- 또는 다른데에서는 (Introduction to Mathemtical Statistics 7ed) Practically 3000번 이상을 사용항다고 합니다.

- 왜 위와 같은 추정이 가능할까요? 이는 바로 '검정 통계량의 분포' 를 Bootstrap 을 이용하여 근사하였기 떄문에 가능했던 것입니다.
- 요즘은 그래서 '복잡한 수식' 으로 푸는것도 중요하지만, 손으로 풀 수 없는 문제도 컴퓨터로 풀어버릴 수 있는 시대가 되었다는게 중요합니다!

---

**reference**

- <https://ocw.mit.edu/courses/mathematics/18-05-introduction-to-probability-and-statistics-spring-2014/readings/MIT18_05S14_Reading24.pdf>
- 위 소스를 꼭 읽어주세요! (아직 모르는 부분이 여기 있어서)
