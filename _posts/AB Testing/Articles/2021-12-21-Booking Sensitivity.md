---
title: "How Booking.com increases the power of online experiments with CUPED"
excerpt: "Booking 에서 Metric 의 Sensitivity 를 올리기 위한 방법"
categories:
  - AB_Article
last_modified_at: 2021-12-09

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

Outlier 와 A/B Testing
{: .notice--warning}

# [Booking AB Testing](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

- 데이터 기반 결정은 [Booking.com](https://www.booking.com/) 의 핵심입니다. 
- 모든 제품(Product) 팀은 통제된 실험(A/B 테스트)을 수행하고 웹사이트에 대한 변경 사항을 테스트할 수 있습니다( [Kaufman, Pitchforth, & Vermeer, 2017](https://arxiv.org/pdf/1710.08217.pdf) ).

> ## Small Effects and the Challenge of Statistical Power

- [Booking.com](https://www.booking.com/) 은 사이트가 계속해서 제품(Product)을 최적화 함에 따라 새로운 기능은 점점 더 작은 효과를 만들어냅니다.(즉 이미 혁신적인 변화는 모두 마친 상태라, 크개 개선할게 없는것이죠..)
  - 그러나 우리는 여전히 실험을 통해 이러한 변화를 감지해야 합니다.
  - 왜냐하면 [Booking.com](https://www.booking.com/)  주요 지표 에 대한 작은 영향이라도 여전히 막대한 수익 차이를 의미하기 때문입니다.
  - ex :  **매일 150만 개가 넘는 객실 숙박이 저희 사이트에 예약되어 있으므로 전환율이 아주 조금이라도 증가하면 수익에 큰 영향을 미칠 수** 있습니다.
- 이때 작은 지표에 대한 영향력을 측정하는것은 매우 어려운 작업입니다. Conversion Rate 가 2% 인 실험에 대해서 AB Testing 을 진행한다고 합시다. 이때 1% 의 상대적인 차이를 검정하기 위해서 우리는 1200만명의 유저가 필요합니다. (*Using* [Booking.com’s power calculator](https://bookingcom.github.io/powercalculator/) *(*[open-source code here](https://github.com/bookingcom/powercalculator)*)*)
- Experiments 에서 작은 효과를 감지하는 문제는, 낮은 통계적 검정력과 관련이 있습니다.
  - 검정력이 낮을 경우에, Statistical Test는 Treatment 가 의미 있는 영향을 미친 경우에도, '차이가 없음!' 이라고 결론 내릴 수 있습니다. 
  - 이는 **주어진 표본 크기를 고려해볼 때, 메트릭의 분산이 너무 크고 Effect Size 가 너무 작아서 실험이 제대로 작동하지 않았던 것입니다.** (An experiment is underpowered when the treatment effect is too small relative to the metric’s variance for a given sample size.)

![jpg](/assets/images/Stat/130_1.jpg)

- 이를 설명하기 위해 그림 1은 세 가지 실험에서 메트릭에 대한 Control 및 Treatment 의 분포를 보여줍니다.
  - 실험 2는 Effect Size 가 너무 작고, Variance 가 너무 커서, 실제로 효과가 있는 모습이지만 실험이 이러한 효과를 잡아내기는 힘듭니다.
  - 실험 1은 실험 2와 동일한 분산을 갖지만 훨씬 더 큰 Effect 를 가져서 power 가 높습니다. 
  - 실험 3은 실험 2와 동일한 작은 effect 를 가지지만 훨씬 더 작은 분산을 생성했으므로 큰 Power 를 가지게 됩니다.

> ## CUPED: Controlled-experiment Using Pre-Experiment Data

- Cpued 방법론이란, Experiment Platform team at Microsoft ([Deng, Xu, Kohavi, & Walker, 2013](http://www.exp-platform.com/Documents/2013-02-CUPED-ImprovingSensitivityOfControlledExperiments.pdf)) 에서 발견한 방법론입니다. 
- 이는 메트릭의 분산을 줄여서 작은 Treatment effect 를 탐지하는 Power 를 넢히는데에 도움을 줍니다. 

![jpg](/assets/images/Stat/130_2.jpg)

- CUPED 방법론 실험 2의 metric 에 적용한다고 합시다. 그러면 위처럼 실험 2의 Metric 분포를 사전 실험 데이터를 이용하여 실험 3의 metric 분포처럼 같은 effect 를 가지지만 작은 Variance 를 가지게 바꾸게 됩니다.
  - 이때 핵심 아이디어는 **실험 전(Pre-experiment Data) 데이터가 메트릭에서 설명할 수 있는 분산은 실험의 효과와 관련이 없으므로 제거** 한가는 것이고, 그를 통해서 분산이 줄어드는 것입니다.

> Example

- 매일 예약을 받는 숙박 시설을 대상으로 평균 예약 수 를 메트릭으로 실험을 진행한다고 상상해 봅시다. 
- 숙박시설 하나당 하루당 받는 예약의 수는 0에서 수천까지 다양하므로 이 측정항목의 편차가 엄청날 수 있습니다. 
  - 그러나 우리는 실험 전에 각 숙박시설에 대한 평균 일일 예약을 알고 있습니다. 즉 이러한 사전 지식을 사용하여 숙박시설이 실험 전과 비교하여 실험 후에 많거나 적은 예약을 받기 시작하는지 또는 거의 같은 수의 예약을 받기 시작하는지 테스트할 수 있습니다. 
  - 실험 전 정보를 이용한다면 측정항목의 편차는 원래보다 상당히 작을 것입니다. (큰 예약을 받는 숙박업소는 실험 이전에도 많은 예약이 있었을 것이고, 실험전 조정을 통해서 큰 값은 작아지기 때문입니다.)
- CUPED는 사전 실험 데이터를 사용하여 간단하고 확장 가능한 방식으로 설명 가능한 분산을 제거하기 위한 선형 기반 모델입니다. [Microsoft의 원본 문서](http://www.exp-platform.com/Documents/2013-02-CUPED-ImprovingSensitivityOfControlledExperiments.pdf) 와 Netflix 실험 팀에서 발행한 검증 문서( [Xie, & Aurisset, 2016](http://www.kdd.org/kdd2016/papers/files/adp0945-xieA.pdf) )는 모두 대규모 데이터를 사용하는 온라인 실험에 CUPED를 사용하여 좋은 결과를 얻었다는것을 말하고 있습니다.

> ## CUPED’s Covariate Method

- Cuped 방법론을 사용하려면 stratification 과 covariate-based methods 방법론을 사용할 수 있습니다.
  - 계층화(stratification)는 국가 또는 브라우저 유형과 같은 범주형 사전 실험 데이터를 일반적으로 사용합니다. 
- 하지만 우리는 실험에 노출되기 전 (pre-experiments) 각 Randomization Unit 단위(사용자, 쿠키 등)에 대해 계산된 Continuous 측정항목(일별 예약, 클릭 수, 시간 등)을 사용하는 "공변량" 방법에 중점을 두려 합니다.
- 이떄 공변량(Covariates)은 테스트에 관심이 있는 것과 동일한 메트릭인 경우가 많습니다. 이는 Cuped 를 사용하여 분산 감소(및 그에 따른 검정력 증가)의 효과는 공변량(Covariates)과 메트릭 간의 상관 관계가 클수록 크기 때문입니다.

```
CUPED-adjusted metric =
  metric - (covariate - mean(covariate)) x theta
```

- [Booking.com](https://www.booking.com/) 에서는 위와 같이 공변량(Covariates)과 각 단위의 메트릭 점수를 조정하는 CUPED을 구현 하였습니다.
  - 이때 이 방법은, microsoft 나 neflix 에서 구현한 방법과 약간 다른데, `mean(covariate)`가 추가적으로 식에 들어가 있습니다. 하지만 이는  Group Difference 차이에 영향을 주지 않으므로 여전히 유효합니다.)

- 위의 식에서 `mean(covariate)`  는 covariate mean 을 의미하고 `theta` 는 아래와 같이 정의된 상수값을 의미합니다. 
  - 아래와 같이 정의된 이유는 , CUPED 를 적용할떄 아래와 같은 계수를 가져야 분산 감소효과가 최대이기 때문입니다. 

```
theta = covariance(metric, covariate) / variance(covariate)
```

- 사용자에게 적용되는 할인율의 변경에 따서, 주당 평균 예약 수를 증가시키는지 에 대해서 테스트 하는것을 고려해 봅시다. 
  - 이때 각 실험에 참가하는 user 들은 experiment 이전에 Bookings-per-week 데이터를 계산할 수 있습니다. 

![jpg](/assets/images/Stat/130_3.jpg)

- 위 그림처럼 CUPED 를 적용했을떄에, 우리의 메트릭은 `CUPED-Adjusted metric` 으로 계산됩니다.

![jpg](/assets/images/Stat/130_4.jpg)

- 만약 metric 이 mean - centered 되어있다면 , our metric (y-axis) VS our pre-experiment covariate (x-axis) 의 산점도를 살펴봄으로서 직관적으로 어떻게 계산되는지 알 수 있습니다.
  - 위에서 Fitting 된 (OLS) 최적의 기울기는 `theta` 로 정의됩니다.
  - 그리고 CUPED-adjusted metric 은 점선(Fitting 된 line) 에 대한 수직 거리가 됩니다. 
- `theta` is equivalent to the unstandardized coefficient from an ordinary-least-squares regression of the metric on the pre-experiment covariate.
  - 이떄 중요한점은 , intercept 는 우리 방법론에서 사용하지 않는다는 점입니다. 즉 필요한것은 기울기입니다.
- 이제 원래 메트릭 값을 테스트한 것처럼 적절한 통계 테스트(예: *t* -test)를 CUPED로 조정된 메트릭 값에 적하면 됩니다.

> ## Handling Missing Data and Pseudo Code

- 실험 전 공변량에 대한 데이터가 누락된 Unit이 있을 수 있으며, 이는 문제가 될 수 있습니다.
  - 예를 들어 로그인하지 않은 사용자는 실험이 진행되는 동안 [Booking.com](https://www.booking.com/) 가입한 호텔에 대한 이전 기록 데이터 자체가 없습으므로 공변량을 적용할 수 없습니다.
  - 또는 실험 도중에 처음으로 들어오게 되는 유저는 Pre-Experiments 데이터가 없습니다.
- 이런 Pre-experimentr가 없는 데이터는 간단한 방법으로 처리합니다 .
  -  **실험 전 데이터가 누락된 Unit에 대해 Metric 값을 조정하지 않은 상태로 둡니다** .
- 왜 위처럼 처리할까요? 만약 우리가 누락된 데이터를 어떻게 채우고 싶다고 한다면, 결측값에 대한 최상의 추정치는 표본 평균일 것입니다.
  - 누락된 사전 실험 공변량을 표본 평균으로 대체하면 아래와 같이 계산됩니다.

```
if covariate is missing:
 # Substitute covariate with mean
 CUPED-metric = metric - (mean(covariate) - mean(covariate)) x theta
    
 # Which reduces to...
 CUPED-metric = metric - (0) x theta
 # Which reduces to...
 CUPED-metric = metric
```

- 위처럼 best-estimate 를 사용했지만, the CUPED adjustment 값은 사실  no adjustment 일때와 값이 완전히 같습니다. 즉 이러한 이유로 조정하지 않은 상태로 그대로 두는 것입니다.
- 그러므로 최종적으로 Bookings.com 에서 사용하는  pseudo code explaining how [Booking.com](https://www.booking.com/) uses CUPED 는 아래와 같습니다.

```
covariate_mean = mean(covariate)
theta = covariance(metric, covariate) / variance(covariate)
for each unit:
  if covariate is missing:
    cuped_metric = metric
  else:
    cuped_metric = metric - (covariate - covariate_mean) x theta
```

> ## Real Example

- 이제 CUPED의 가치를 보여주는 [Booking.com의](https://www.booking.com/) 실험 결과를 확인해 보겠습니다. 
- 이 실험에서 우리는 새로운 캘린더 인터페이스의 효용을 알아보기 위하여 실험을 설계하였습니다.
  -  실험은 6주 동안 실행되었고, 분명히 Significant 한 결과를 얻었습니다.
  - key business metric에 대한 Control 과 Treatment 의 일일 p-value 를 비교하는 그림은 아래와 같습니다. 

![jpg](/assets/images/Stat/130_5.jpg)

- 트래픽이 적은 실험에서, CUPED 조정은 조정을 하지 않았을 때보다 더 작은 샘플에서 중요한 결과를 더 빨리 감지하는 데 도움이 되는것을 알 수 있습니다.

# [Big Data Application](#link){: .btn .btn--primary}{: .align-center}

> ## 하이브의 CUPED

- Hive를 사용한 실험에 대해서 CUPED를 대규모로 구현하는 방법을 살펴보겠습니다.
-  `exp_data`라고 불리우는 아래와 같은 실험 테이블이 있다고 가정해 보겠습니다 .

![jpg](/assets/images/Stat/130_6.jpg)

- 위 표는 CUPED 조정을 적용할 수 있는 여러 실험에 대한 예제 데이터. 
  - 왼쪽에서 오른으로 각 열은 실험의 ID, 실험의 각 단위(사용자, 속성 등)에 대한 ID, 단위가 속한 조건 그룹(Control , Variant ..), 실험 중에 얻은 측정항목 값 , Pre-experiment 공변량. 을 의미합니다.
- 각 실험에 대해 두 개의 상수가 필요합니다. 실험 전 공변량의 평균과 조정 값 `theta`. 다음과 같이 테이블에 생성합니다.

> Hive query for computing constants needed by CUPED adjustment

```sql
CREATE TABLE cuped_constants AS

SELECT        exp_id
            , AVG(covariate) AS covariate_mean
            , COVAR_SAMP(metric, covariate) / VAR_SAMP(covariate) AS theta
  
FROM        exp_data
  
GROUP BY    exp_id
```

- Join these constants to the unit-level data to do the CUPED adjustment

> joining CUPED constants and completing CUPED adjustment

```sql
CREATE  TABLE cuped_adjusted AS

SELECT  -- All unit-level, experiment variables
          E.* 

        -- CUPED-adjusted metric
        , COALESCE(metric - (covariate - covariate_mean) * theta,
                   metric) AS cuped_metric
        
FROM    exp_data E
  
JOIN    cuped_constants C
  
ON      E.exp_id = C.exp_id
```

- 우리는 original metric data 인`E.*`를 다양한 이유로 냅두려고 합시다. 
  - (예: 나중에 원래 메트릭과 CUPED 조정 버전을 비교할 수 있음).
- The CUPED adjustment makes use of `COALESCE`(an alternative is `nvl`) to revert to the original metric value whenever the CUPED adjustment produces a `NULL`
  - 이것은 공변량이 누락된 Unit 뿐만 아니라 전체 샘플에 대해서 실험 전 데이터가 없는 경우(즉 신규 서비스의 실험 등) 발생할 수 있는 공변량 평균 또는 세타 누락과 같은 다른 경우를 처리합니다.
- 이제 `cuped_metric` 를 테스트를 위한 Metric 으로 취급할 수 있습니다 . 예를 들어 일반적인 A/B 시나리오에서 Hive를 사용하여 평균, 표준 편차 및 표본 크기 를 계산하고 Two Sample T test 를 수행할 수 있습니다. 

> ## Spark 의 CUPED

- 또한 인기 있는 또 다른 빅 데이터 엔진인 Spark로 CUPED 조정을 수행하는 방법을 보여주는 코드 스니펫을 공유하려고 합니다
  -  Spark는 다양한 언어로 API를 제공하며 여기에서는 sparklyr 패키지 덕분에 R을 사용합니다.

```sql
# Packages
library(sparklyr)
library(tidyverse)

# Simulate some data
n_experiments <- 3
n_users_per_exp <- 10000
set.seed(171104)

d <- cross_df(list(exp_id = seq(n_experiments),
                   user_id = seq(n_users_per_exp))) %>% 
  mutate(group = sample(c("base", "variant"), n(), replace = TRUE),
         covariate = rnorm(n()), 
         metric = covariate + rnorm(n(), sd = 0.3) + as.numeric(group == "variant"), 
         covariate = if_else(runif(n()) > 0.2, covariate, NA_real_))

print(d, n = 5)
#> # A tibble: 30,000 x 5
#>   exp_id user_id   group  covariate      metric
#>    <int>   <int>   <chr>      <dbl>       <dbl>
#> 1      1       1 variant -0.9815665 -0.07581224
#> 2      2       1 variant         NA -0.13754373
#> 3      3       1 variant -1.6105574 -0.79136708
#> 4      1       2 variant -1.2811401 -0.72244066
#> 5      2       2 variant  0.1324251  1.37553241
#> # ... with 3e+04 more rows

# Connect to Spark
sc <- spark_connect(master = "local")
#> * Using Spark: 2.1.0

# Copy data to spark (and keep connection to it)
d_tbl <- copy_to(sc, d)

# Do CUPED adjustment per experiment in Spark
cuped_results <- d_tbl %>%
  group_by(exp_id) %>%
  mutate(cuped_metric = metric - (covariate - mean(covariate)) * cov(metric, covariate)/var(covariate)) %>% 
  mutate(cuped_metric = coalesce(cuped_metric, metric))

# Collect results into local memory
d <- collect(cuped_results)

d
#> # A tibble: 30,000 x 6
#> # Groups:   exp_id [3]
#>    exp_id user_id   group   covariate     metric cuped_metric
#>     <int>   <int>   <chr>       <dbl>      <dbl>        <dbl>
#>  1      2       1 variant         NaN -0.1375437  -0.13754373
#>  2      2       2 variant  0.13242509  1.3755324   1.24621238
#>  3      2       3    base  1.96319126  1.6714552  -0.28382946
#>  4      2       4    base  0.44404116  0.3664763  -0.07364255
#>  5      2       5 variant  0.02134668  0.9870520   0.96851903
#>  6      2       6 variant         NaN  1.2720197   1.27201966
#>  7      2       7    base -0.35044885 -0.2419659   0.11032162
#>  8      2       8 variant         NaN -0.8750044  -0.87500437
#>  9      2       9 variant  0.81343645  1.3115542   0.50300887
#> 10      2      10 variant -0.18234841  0.6818743   0.86650225
#> # ... with 29,990 more rows

# Disconnect form Spark
spark_disconnect(sc)
```

- The CUPED adjustment is done where `cuped_results` is being created.

---

**reference**

- <https://booking.ai/how-booking-com-increases-the-power-of-online-experiments-with-cuped-995d186fff1d>



