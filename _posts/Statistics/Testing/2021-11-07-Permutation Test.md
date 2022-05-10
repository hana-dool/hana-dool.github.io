---
title:  "Permutation and Randomize Testing"
excerpt: "순열 검정 및 Randomize Test"
categories:
  - Stat_Testing
last_modified_at: 2021-11-06

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 Permutation Testing 입니다. 이 방법론은
{: .notice--warning}

# [Permutation Test](#link){: .btn .btn--primary}{: .align-center}

> ## Permuation Test

![png](/assets/images/Stat/96_1.png)

- 두 개 이상의 표본 테스팅에 사용됩니다. 
- 방법의 개요는 다음과 같습니다.
  - 두 데이터 샘플을 하나로 섞습니다.
  - 이 섞은 데이터에 대해서 원래 샘플 크기 만큼 다시 비복원 추출하여 나눕니다. (이때 두 샘플을 나눌때에 복원추출을 하는지, 모든 조합에 대해서 실시하는지에 따라서 Permutation / Randomize Test 가 나뉩니다.)
  - 새로 나눠진 샘플을 이용하여 통계량을 다시 계산하고 기록합니다.
  - 위 과정을 반복하고 통계량의 분포를 만들어 낸 다음, 우리가 얻은 결론이 순전히 우연이였는지 아닌지를 검정합니다.
- 위에서 우리가 두개의 샘플에 대해서 비교할때에는 다음과 같이 가설이 설정된다는것을 명심합시다! 
  - <https://cran.r-project.org/web/packages/flipr/vignettes/alternative.html>
  - Null Hypothesis : 두 population 의 분포는 같습니다. 즉 $F_A(x) = F_B(x)$
  - Alternative Hypothesis : 두 population 의 분포는 다릅니다. 즉 $F_A(x) \not= F_B(x)$
- 즉 우리가 기각하는것은 '두 Population 이 다르다!' 라는것을 기각하게 되는 것입니다.  이전의 부트스트랩과는 약간 다르다는것을 명심하세요
- 그리고 '통계량' 을 하는데 이것은 $F_A(x) \not= F_B(x)$ 를 결론내리기 위하여 DIstribution 의 어떤 측면을 보겠다! 라고 하는것입니다. 
  - Variance 의 차이를 통계량으로 한다면, 두 분포의 Variance 측면만 바라보겠다는 것입니다.
  - Mean 차이를 통계량으로 한다면, 두 분포의 Mean 에 대해서 집중한다는 것입니다. 

> ## Algorithm

- 저희가 검정하고자 하는 통계량 (z-test 통계량, median 차이 , 평균차이..) 을 정합니다. 
- 우선 여러 그룹의 샘플들을 하나의 데이터 집합으로 합칩니다..
  - 두 그룹의 차이에 대해서 검증할 경우 우리가 얻은 데이터 $Data_A , Data_B$ 가 있을텐데 이때 두 데이터를 합쳐서 $Data_{all}$ 로 합칩니다. 
- 결합된 데이터를 잘 섞은 후에 A 그룹과 동일한 크기의 표본을 비복원 무작위 추출합니다. 
  - 이떄의 표본은 A 그룹의 가상의 Sample 이 됩니다. 즉 $Data'_A $ 라고 할 수 있습니다. 
  - 위에서 생성한 데이터를 이용해 A 의 통계량을 계산합니다.
- 나머지 데이터에 대해서 B 그룹과 동일한 크기의 표본을 비복원 무작위 추출합니다.(물론 남아있는것을 모두 뽑아내면 될 것입니다.)
  - 이떄의 표본은 B 그룹의 가상의 Sample 이 됩니다. 즉 $Data'_B$  라고 할 수 있습니다.
  - 위에서 생성한 데이터를 이용해 B 의 통계량을 계산합니다.
- 위에서 구한 통계량을 모두 기록하면서 M 번 반복하여 검정 통계량의 순열 분포를 얻습니다. 
- 그리고 '처음 데이터' 에서 얻은 통계량과 이 분포를 비교하면서 Control 과 Treatment 가 차이가 진짜 있었던 것인지에 대해서 알아볼 수 있습니다.

![gif](/assets/images/Stat/96_1.gif)

> ## Difference with Bootstrap Test

1. 부트스트랩 
   - 데이터에서 계산된 통계량의 표본 분포를 정량화 하는데에 주로 사용됩니다. (즉 CI 를 형성할 수 있다는 것이죠.)
2. 순열 테스트
   - 우리 데이터가 '순전히' 우연히 관찰되는 결과인지에 대해서 수량화 하는것입니다.
   - 즉 '아무런 변화 없이 이전과 같은 분포' 인데도 우리가 검정하려는 통계량 값이 나오는지 안 나오는지를 검정하는 것이죠.

> ## Properties

- 순열 검정은 모든 Test - Statistics 에 대해서 수행이 가능합니다. 
  - 이는 분포가 알려져 있든 없든 가능합니다. 
- 순열 검정은 '분포가 같은지 아닌지' 에 대해서 검정합니다 (A 와 B 의 데이터를 합쳐서 사용하는것만 봐도 알 수 있죠.)
  - 그러므로 Bootstrap (얘는 '매개변수' 입장에서만 볼 수 있죠.) 에 비해서 Null hupothesis가 좀 더 엄격하다는것입니다.

> ## More info

- 좀 더 자세히 알기 위해서라면 아래의 링크를 참조하세요
  - <http://users.stat.umn.edu/~helwig/notes/perm-Notes.pdf>

# [Randomize Test](#link){: .btn .btn--primary}{: .align-center}

> ## Randomize Test 

- 순열 검정의 경우, 데이터를 샘플링하는 방법에 따라서 2가지로 나뉠 수 있습니다.

1. Permutation Test : 데이터를 무작위로 섞고 나누는 과정에서 나눌 수 있는 모든 가능한 조합을 찾습니다.

2. Monte Carlo Test : 샘플링 하는 과정을 복원 추출로 수행합니다.

- 물론 더 권장되는 방법은 모든 경우의 수를 고려하는 Permutation Test 입니다만, 이러한 방법론은 Computational Cost 가 엄청납니다.
- 그러므로 모든가짓수를 고려하는게 아니라 복원추출을 통하여 MonteCarlo 방식으로 테스트 하는것을 말합니다. 즉 무작위 표본을 이용하는 것이며 그래서 Randomize Test 라고 불리웁니다. 

> ## Example

- Pearson Correlation Coeficient 를 통계량으로 정했고, 두 샘플 P,Q 에 대해서 상관계수가 0 인지 아닌지에 대해서 테스팅을 진행하려 합니다.
  - 즉 두 변수의 관련성에 대해서 테스팅을 하려고 합니다.
- 우선 두 샘플의 Correlation r = 0.6183 입니다. 과연 이 값이 우연의 산물로 나올 수 있는 값일까요? 
  - 이를 테스팅 하기 위해서 Permutation Test를 진행하도록 하겠습니다. 

![png](/assets/images/Stat/96_2.png)

- 위처럼 랜덤하게 섞은 후에 50000q번의 샘플링을 통해서 통계량을 계산해 보았습니다.
  - 그 결과 위의 파란색 막대 분포처럼, 상관계수의 분포를 볼 수 있었습니다.
- 우리가 처음 얻었었던 r = 0.618 은 위 테스트를 본다면 매우 희귀한 사건입니다.
  - p-value 는 0.0016 입니다.
  - Two Tail Test 를 진행할것이라면 p-value 는 0.0032 가 됩니다.
- 즉 이 경우 우리는 0.618 의 통계량은 유의했다! 라는 결론을 내릴 수 있을것입니다.
- 즉 P 와 Q 는 Correlated 되어있다고 결론을 내릴 수 있습니다.

> ## Assumption

- Permutation / Randomization Test 는 어떠한 분포 가정 없이 진행되어서 장점이 될 수 있습니다.
- p-value 는 단지 생성된 통계량의 히스토그램일 뿐이라는것에 주의합니다. (즉 우리가 어떤 분포를 만들어서 얻은게 아니라 부정확할 수 있습니다.)
- Sample "섞어서 Testing 을 진행하였는데 이것의 정당성을 미리 확보해야 합니다 (데이터가 Not Exchangable 한 경우도 있기 때문입니다.)

---

  **Reference**

- <https://angeloyeo.github.io/2021/10/28/permutation_test.html>
- https://en.wikipedia.org/wiki/Resampling_(statistics)#Permutation_tests
- https://www.r-bloggers.com/2019/04/what-is-a-permutation-test/
- <http://pillowlab.princeton.edu/teaching/mathtools16/slides/lec21_Bootstrap.pdf>
- <https://en.wikipedia.org/wiki/Permutation_test>
- <https://www.uvm.edu/~statdhtx/StatPages/Randomization%20Tests/RandomizationTestsOverview.html>

 사실 Permutation 이라는 개념이 나온지 얼마 안되어서 크게 사용되지 않기도 하고.. Null hypothesis 가 '두 분포는 같음' 이여서 약간 애매한 구석도 있네요. (이는 Pooled Sample 을 쓰는것만 봐도 알 수 있죠.) 그래도 한가지 희망이 있다면 "Permutation Tests and Bootstrap Tests give very similar solutions (Efron and Tibshirani (1993))" 이라는 사실입니다. 진짜 통계량 분포 구하는게 힘들때에 한번 사용해볼 수 있을것 같아요.
{: .notice--success}

