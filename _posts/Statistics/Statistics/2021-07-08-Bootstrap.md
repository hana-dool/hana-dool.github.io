---
title:  "Sampling Distribution and Bootstrap"
excerpt: "부트스트랩의 응용과 기본규칙"
categories:
  - Stat
tags:
  - 1
last_modified_at: 2021-07-08

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# 1. Overview

![png](/assets/images/Stat/14_1.png)

- 대부분의 Statistic Analysis 는 통계량 (Statistics) 의 분포에 근거하고 있습니다.
  - $T(X_1 , ... X_n) $ 이 Statstics 가 되고, 이게 어떠한 parameter 를 요약한다면 estimator $\hat{\theta}$  가 됩니다.
- 즉 우리는 $T$ 에 대한 분포를 찾게 된다. (Sampling Distribution)
  - $X_1 .... X_n \sim N(\mu, \sigma^2)$ 이면 $\bar{X}\sim N(\mu, \sigma^2 / n)$ 
  - $X_1 .... X_n \sim (\mu, \sigma^2)$ 이면 $\bar{X} \to N(\mu, \sigma^2 / n)$ 

- 위와 같이, Exact 하게 구한다거나 또는 Assymptotic 하게 구하게 된다. 
- 하지만 위와 같은 추정이 어려울때는 어떻게 해야할까요? 

![png](/assets/images/Stat/14_2.png)

> Large Sample Theory (~1970)

- MLE Estimation 을 구할 수 있다면 Assymptotic Property 가 있고 이를 이용할 수있습니다. 
- 또는 CLT 로 근사합니다. 
- 수학만 쓰던 시절에 유행하던 방법

> Resampling Method 

- 데이터 $X_1....X_n$ 을 재사용해서, 이 데이터의 Structure 를 잡아내는것 
- 대표적을 Jacknife 와 Bootstrap 이 있다. 
- 기본적으로 모수에 대한 Sample Distribution 을 어느정도 가능하게 해 준다. 
- CI , Variance Estimation 등이 가능
- 컴퓨터가 슬슬 발전하던 시절에 썼던 방법

> Bayesian Estimation

- $P(\theta \mid X)$ 를 구해버린다. 
- 바로 업데이트가 되어버림. (Test 등이 가능.) 
- 컴퓨터의 발전이 매우 되고나서 적분 등이 쉬워지고 나서 유행한 방법 (요즘 유행이라네요..?)



<br>

# 2. Non parameteric Bootstrap

![png](/assets/images/Stat/14_3.png)

- 매우 일반적인 방법입니다. 
- 원래 데이터로부터 Resampling 을 통해서 $T_n$ 들을 생성해내고, 이 $T_n$ 들을 Variance 를 추정하게 됩니다. 

<br>

# 3. Parameteric Poostrap

![png](/assets/images/Stat/14_4.png)

- 파라매트릭 과정에서는 약간 다릅니다.
- 위처럼, 특정한 분포에서  데이터 $X_1 .... X_n $ 이 나왔다고 가정을 합니다.
- 먼저 데이터를 이용해 먼저 '$\theta$' 를 추정합니다. 
- 그 이후, 추정된 분포 $F(\hat \theta)$ 에서 Bootstrap Sample 을 구성하고, 여기에서 $T_n^*$ 를 만들어냅니다. 

<br>

# 4. Remark!!

- Random Sample 이 아닌경우 부트스트랩이나, Jackknife 는 variance estimation 을 과소평가하게 됩니다. 
- 과소추정을 하게되면, 마치 의미가 있는것처럼 생각할 수 있다. (Wrong Decision..) 
  - 부트스트랩이 iid 가 아닐경우 부트스트랩을 Modify 해야한다..(헉!)
  - Random Sample 이 아닌상태에서의 Bootstrap 방법론이 엄청 많다.. 
  - 데이터 구조에 따라서 Bootstrap 의 종류도 엄청 많다.. 

<br>

# 5. 부트스트랩 신뢰구간

- 부트스트랩은 확률 분포의 가정을 두지 않고 주어진 데이터를 원래의 모집단을 대표하는 독립 표본으로 가정하고 진행한다. 
- 그리고 중복을 허용한 무작위 재추출로(복원추출로) 각각에서 얻어진 통계량을 계산한다.

- 부트스트랩은 큰 수의 법칙에 기반을 두고있다. 이는 표본의 크기가 커진다면, 표본의 분포는 모집단의 분포의 근사치가 된다는 말이다. 

> 1.데이터에서 복원추출 방식으로 크기 n 인 표본을 뽑는다.(재추출)
>
> 2.재표본된 표본에 대해서 원하는 통계량을 구하고 기록한다.
>
> 3.1~2 단계를 k 번 반복한다.
>
> 4.x% 신뢰구간을 구하기 위해 R개의 재표본 결과로부터 분포의 양쪽 끝에서 (100-x) / 2 % 만큼 잘라낸다.
>
> 5.절단이 끝난 뒤 나머지 점들의 분포는 x% 부트스트랩 신뢰구간의 양 끝점이 된다.
