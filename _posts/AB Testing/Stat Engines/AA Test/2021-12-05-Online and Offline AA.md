---
title: "Bayesian Test Early Stopping"
excerpt: "Early Stopping 에 이슈는 없는가?"
Tags:
  - AB_Stat
last_modified_at: 2021-12-05

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

Stack Exchange 에서 A/B 테스트를 수행하는 방식을 Freq 에서 Bayes 로 바꾸지 않고 Freq 를 유지했던 이유는?
{: .notice--warning}

# [A/B Testing at StackExchange](#link){: .btn .btn--primary}{: .align-center}

> ## Run more A/A tests

- An A/A test is the same as an A/B test, but your treatment group receives the same experience as the control group. Instead of telling you the impact of a change, A/A tests help you build trust in your experimentation platform, and can surface a whole host of issues.
- Broadly speaking, there are two types of A/A tests you can run: offline and online.

> ## Offline A/A Test

- 오프라인 A/A 테스트는 유형 1 오류(가양성)가 예상대로(즉, 5%) 제어되는지 확인하는 데 도움이 됩니다. 
- 예상보다 높은 오탐지가 발생할 수 있는 한 가지 방법은 분산 추정이 잘못된 경우입니다. 이는 [무작위화 단위가 분석 단위와 다를](https://ianwhitestone.work/randomization-unit-analysis-unit/) 때 발생할 수 있습니다 . 오프라인 A/A 테스트를 실행하면 이러한 문제가 발생하기 쉬운지 여부를 빠르게 식별하는 데 도움이 됩니다.
- 또한 오프라인 A/A 테스트는 실행 비용이 매우매우 저렴합니다. 간단히 말해서 다음과 같이 작동합니다.

> Algorithm

1. Querying a representative sample of your data.
   - 즉 최근에 실험한 데이터가 있다면, 이 실험 데이터를 완전하게 Copy 해서 가지고온다는 뜻입니다.
2. Randomly assign your subjects (user, session, pageview, etc.) to test or control
3. Calculate your relevant metric (clicks per users, # of conversions, etc.)
4. Run the appropriate test (t-test, two proportion z-test, etc.)
5. Repeat steps 2-5 up 1000 times
6. Analyze the results
   - Ensure that the % of false positives are in line with expectations. 
   - For example, if your p-value cutoff is 0.05, a common industry practice, you’d expect a 5% false positive rate.
   - Plot the distribution of p-values and check that they are uniform

> ## Online testing

- 오프라인 테스트와 달리 온라인 A/A 테스트는 실제 사용자를 대상으로 진행됩니다. 엔지니어는 무작위화 논리를 구현하여 주제를 적절한 그룹에 할당하고 할당을 기록해야 합니다. 두 그룹 모두 통제 경험을 받기 때문에 새로운 치료 경험을 구축할 필요가 없습니다.
- 오프라인 테스트는 메트릭 및 통계 테스트를 검증하는 데 도움이 되지만 온라인 A/A 테스트는 나머지 실험 인프라를 검증하는 데 도움이 됩니다. 
  - 세그먼트에서 샘플 비율이 일치하지 않습니까? 
  - 실험에 필요한 새로운 기능이 의도한 대로 작동합니까? 
  - 데이터 파이프라인이 예상대로 작동하고 있습니까? 
- 예를 들어, 원래 기록 시스템과 다른 위치에서 사용자 또는 이벤트를 기록할 수 있습니다. 온라인 A/A 테스트 데이터를 사용하여 숫자가 일치하는지 확인하고 데이터가 어디에도 누출되지 않는지 확인할 수 있습니다.

> ## Real Application

- A/A 테스트를 시행하면서 다음과 같은 이점을 얻을 수 잇었습니다.

> Statiatical Testing 이 적절한지에 대한 Sanity Check

- 오프라인 A/A 테스트는, 통계 테스트 방법론중 하나에서, 예상보다 높은 False Positive 로 이어지는 버그를 발견하는 데 도움이 되었습니다.
  - 버그가 된 이유는 바로, 다중 비교를 수행할때 p-값에 대한 Cut off 를 조절하지 않는 실수였습니다. 
  - 이러한 코드에서의 실수는두 그룹에 대한 A/B 테스트의 False Positive 를 두배로 높혔습니다.

> Check Randomization Unit

- 오프리인 A/A 테스트 시뮬레이션을 활용하여서, Randomization Unit(User) 과 Analysis Unit(Session) 이 다르더라도 False Positive 가 크게 달라지지 않는다는것을 확인했습니다.
- Randomization Unit 과 Analysis Unit 이 다르면 일반적으로 문제가 일어나지만, 다르더라도  조절하지 않고 Test 를 진행해도 큰 문제가 없다는것을 확인한 것입니다. 
- 이러한 결과를 통해서 Randomization 이 User 이였지만 , 메트릭의 단위도 User 로 바꾸기보다는 기존의 Session 단위의 메트릭을 그대로 사용할 수 있었습니다.

> System Check

-  Online A/A 테스트를 통해서 우리가 새로 추가한 new logging 시스템과 기존의 Record System 간에 불일치가 있음을 알았습니다. 
- 이로 인해서 A/B Test Metric 계산에 사용되는 Data Source 를 변경하게 되었습니다.

> Randomization 방법 체크

- 우리가 구축한 새 앱에서 실행한 또 다른 실험에서는 앱이 로드될 때 필요한 쿠키에 액세스할 수 없었기 때문에 사용자가 적절하게 무작위화할 수 없었습니다. 
- 이러한 문제를 해결하기 위해 브라우저 캐시를 사용하여 각 페이지 보기에서 사용자에 대해 다른 버전의 앱이 로드되는 것을 방지하기로 결정했습니다. 
- 우리는 이 접근 방식을 이해하기 위해 온라인 A/A 테스트를 실행했으며, 사용자가 브라우저 캐시를 거의 지우지 않기 때문에 브라우저 캐시를 사용하면 사용자가 무작위로 추출하는 데 충분한 근사치를 얻을 수 있다는 것을 알게 되었습니다.

> A/B 테스트를 실행하기 전에 변경사항 체크

- 서버 측 리디렉션 과 관련된 A/B 테스트를 실행하기 전에 한 그룹의 사용자가 동일한 페이지로 리디렉션 되는 온라인 A/A' 테스트를 실행해 보았습니다.
- 이를 통해 리디렉션의 영향만 분리할 수 있으므로 다른 페이지로의 리디렉션을 사용한 후속 A/B 테스트에서 다른 페이지를 보는 것과 비교하여 리디렉션에서 발생한 변화의 정도를 알 수 있습니다. 
  - 테스트는 또한 리디렉션을 수행할 때 발생하는 몇 가지 샘플 비율 불일치(SRM) 문제를 보여주었습니다. 리디렉션으로 인해 특정 브라우저에 대한 중복 요청이 발생하여 각 요청이 새 세션을 생성할 때 세션 그레인에서 SRM이 발생했습니다.
  - 봇과 같은 특정 사용자는 리디렉션을 따르지 않아 해당 사용자가 삭제되고 기록 시스템에 표시되지 않아 기록 시스템을 사용할 때 사용자 단위의 SRM으로 이어질 수 있습니다.
  - A/B 테스트 전에 이러한 문제를 발견함으로써 SRM 문제를 제거한 새로운 데이터 소스를 활용하는 사용자 그레인 메트릭으로 전환할 수 있었습니다.

> ## Notes

- 1 The [github repo](https://github.com/marnikitta/stattests) from [this post](https://medium.com/@vktech/practitioners-guide-to-statistical-tests-ed2d580ef04f#6f38) has vectorized implementations of many different statistical tests available for use.
- 2 The more A/A simulations you run, the better, as you’ll get closer to the expected false positive rate. However, depending on the test or size of your dataset, this may take a long time. [Microsoft has found](https://www.microsoft.com/en-us/research/group/experimentation-platform-exp/articles/p-values-for-your-p-values-validating-metric-trustworthiness-by-simulated-a-a-tests/) that 100 simulations is generally sufficient. More simulations can help produce smoother p-value distributions, which helps reduce false positives when testing for uniformity. If you want to run more simulations, employing parallelization or refactoring the statistical test functions to use vectorized numpy operations can help speed things up.
- 3 You can easily run a [Kolmogorov–Smirnov test](https://en.wikipedia.org/wiki/Kolmogorov–Smirnov_test) to test whether the distribution is uniform: `scipy.stats.kstest(p_values, scipy.stats.uniform(loc=0, scale=1).cdf)`
- 4 This is technically not an A/A test, since one group receives a different experience (the dummy redirect), hence the name A/A’

---

**reference**

- <http://varianceexplained.org/r/bayesian-ab-testing/>



