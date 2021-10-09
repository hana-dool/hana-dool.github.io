---
title: "Patterns of Trustworthy Experimentation &#58; During-Experiment Stage"
excerpt: "Microsoft 에서 실험 도중에 실험의 신뢰성을 살펴보는법"
categories:
  - AB_Testing
last_modified_at: 2021-10-09

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 AB Testing 도중에 실험이 얼마나 유의한지, 중단해야 하지는 않는지, 우리가 예측하는 효과대로 흘러가고 있는지 에 대해서 알아보는 방법에 대해서 알아봅시다.
{: .notice--warning}

# [Patterns of Trustworthy Experimentation](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction 

- A/B Testing 을 통하여 시험하고 싶은 좋은 아이디어가 있다고 합시다. 
  - 그렇다면 우리는 아이디어를 실험 가능하게 실험설계 한 뒤 실제 A/B Testing 결과로부터 아이디어에 대해 판단하게 될 것입니다. 
- 이 게시물에서는 A/B  테스팅 실험 도중에 우리가 실험에 관한 인사이트를 얻기 위해서는 어떠한 측정 기준을 확인하고, 분석해야 하는지에 대해서 알아봅니다. 
- 여기에서 논의되는 많은 부분이 사실은 실험 후 분석 단계에서도 적용됩니다.
  - 하지만 여기에서는 '실험 중간에' 사용자의 경험을 왜곡하는 에러들을 잡아내고, 초기 효과를 방지하는것에 촛점을 맞춥니다.

![png](/assets/images/Stat/73_1.png)

- Truth worthy Analysis 에서는 잘 설계된 Metric 과 신뢰 가능한 Segment 가 필요합니다. 우리는 패턴을 위와 같이 3개로 분류할 수 있습니다. 
  - 실험주 메트릭을 자주 측정하면서 위험을 조기 진단하기
  - 메트릭을 모니터링 하면서 필요하다면 자동 중단시키기
  - 적절한 세그먼트로 나누어 세분화 하여 살펴보기

# [Measure metrics](#link){: .btn .btn--primary}{: .align-center}

> ## Capture Unexpected Effects Early with a Complete Metric Set

- Product 의 변경으로 인해 일부 측면은 개선되지만 일부 측면은 오히려 안좋아지는 현상은 자주 있는 일입니다. 
- 그러므로 A/B Testing 은 제품의 거의 모든 측면을 포함할 수 있는 매우 다양한 메트릭 세트를 사용하여 분석하는것이 중요합니다. 
- 정확한 의사 결정을 위해서라면, 우리는 이러한 Trade off Improvement 에 대해서 잘 관찰하는것이 중요합니다. 
  - 예를 들어서 빨간색 글씨로 바꾸엇더니 세션수는 증가했으나 체류시간이 감소했다면 , 이러한 메트릭의 Trade off 들에 대해 종합적으로 관찰하고 결정을 잘 내리는것이 필요하다는 이야기입니다.
- Microsoft 에서의 경험과 [3],[4]  여러 연구 [5],[6] 에 의해 우리는 아래 와 같은 메트릭들의 분류법을 따를것을 추천합니다. 
  - 아래와 같은 메트릭 분류법은 메트릭 설계 프로세스를 안내하고, 테스트 결과 해석시에 매우 유용합니다.

| Type                                      | Description                                                  | Examples                                                     |
| ----------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Data Quality Metrics                      | Feature 간의 데이터가 일치하는지에 대해서 측정하고,  실험이 에러없이 진행되는지를 검사 | Error Rates, Data Loss Rates, Join Rates, [Sample Ratio Mismatch (SRM)](https://www.microsoft.com/en-us/research/group/experimentation-platform-exp/articles/diagnosing-sample-ratio-mismatch-in-a-b-testing/) |
| Overall Evaluation Criteria (OEC) Metrics | 우리의 목표를 달성하기 위해 제일 먼저 챙겨야 할 메트릭으로, 평가에서 제일 우선순위가 되는 메트릭. 일반적으로 유저 만족도, 매출 등이 된다. | Session Count, Session Success Rate, Utility Rate [6]        |
| Local Feature and Diagnostic Metrics      | Feature 들에 대한 다른 측면에서의 값들을 측정한다. 이는 OEC 에 대한 Movement 를 해석할때에도 보조적인 도움을 준다. | Feature Coverage, Click Through Rate, Messages Received      |
| Guardrail Metrics                         | Treatment 가 이 부분에 대해서는 개선시켜주는것까지는 원하지 않으나, 악화시키는것은 원하지 않는 메트릭. | Page Load Time, Crash Rate, Abandonment Rate                 |

> ## Measure Early and Often

- A/B Testing 의 duration 은 시작하기 전에 미리 설정하고, 그 기간동안 실험하게 됩니다.
  - 이 경우 실험 내내 metric 의 변화를 모니터링 하는것을 추천드립니다. 
- Microsoft 의 경우 A/B Testing 의 일반적인 기간은 7일입니다. 
  - 이 기간동안 Treatment 의 효과를 평가하며, 의도적이지 않은 결과를 파악하기 위해 메트릭을 계속 정기적으로 감시합니다. 
- 실제로 Exp 에서는 테스트가 시작되자 마자 metric set 에 대해 거의 real time 에 가깝게 메트릭의 값들을 계산하고, 감시하도록 권장하고 있습니다. 
  - 이런 일들을 통하여 사용자 경험에 큰 악영향을 미치는 경우라던지, Treatment 에 대한 에러가 있는 경우에 대해서 탐지할 가능성을 높혀줍니다.
- 물론 이러한 메트릭에 대한 실시간 감시는 multiple hypothesis testing  / early peeking 에 대한 문제를 고려해야 합니다. [7],[8],[9]
  - EXP 에서는 이러한 감시에 대한 early 결과 (초기 결과)에 대해 더욱 신뢰하기 위하여 더욱 강력한 Statistical significant level 을 요구합니다. 
  - 또한 메트릭 Movement 가 우리 경보수준에 미치지 않을 경우 , 실험은 미리 지정된 기간만큼 진행디며 , 시험이 끝난 후에 그 결과를 해석하게 됩니다.

# [Monitor Metrics to Intervene when Needed](#link){: .btn .btn--primary}{: .align-center}

- 이전에 설명한것과 같이 , A/B 테스트 내내 메트릭을 모니터링 하는것이 중요합니다.
  - 즉 A/B Testing 이 끝날떄까지 장님처럼 가만히 있으면 안된다는 의미입니다. 
- 하지만 A/B Testing 에 대해서 많이 실행하고, 측정지표가 실험 도중 계속 계산됨에 따라서 , 이러한 Metric 들을 모두 감시하고 대처하는것은 어려운 일입니다.
  - 우리는 '자동화' 된 방법을 이용한다면, 좀 더 쉽고 많은 테스트에 대해서 대처할 수 있을것입니다.

> ## Set Up Alerts to Detect Unintended Degradations

- Microsoft 처럼 매우 많은 A/B Testing 이 실행될 때에는, 주요한 metric 의 Movement 에 대해 자동으로 경고하고, 통보하는 프로세스는 조사가 필요한 A/B Test 를 조기에 식별하는데에 도움을 줍니다. 
- Exp 에서는 Feature 담당아가 업무상 중요한 Guardrail metric (페이지 로드 시간 , 오류듈 등) 과 OEC (사용자 만족도) 에 대해 Alert 를 설정할것을 권장드립니다.
  - 이러한 경고는 큰 이동이 감지되거나, p-value 가 특정 임계값 아래로 떨어질 경우 울릴 수 있습니다. 
- Alert 를 설정하는 가장 기본 메트릭은 바로 SRM(샘플 비율 불일치) 매트릭입니다. 
  - SRM 은 Treatment 및 Control 에 있는 사용자의 비율이 예상되는 균형을 이루지 못할떄에 발생합니다.
  - 이러한 SRM 은 Control 과 Treatment 가 랜덤하게 잘 분배되었는지를 나타내는 중요 지표이므로 이 값이 손상된다면 다른 전체적인 Metric 값을 신뢰할 수 없게됩니다. 
- 즉 SRM 을 조기에 Test 하고 SRM 이 감지되면 경고를 설정해야 할 것입니다.

> ## Auto-Shutdown Egregious A/B Tests

- A/B Testing 을 위해, quality control process (품질 관리 시스템) 을 통과하지 못한 문제 / 버그는 안전하게 롤아룻 할 수 있도록 하는것이 좋습니다. 
- 우리가 설정한 Alert(경보) 를 설정한 metric 에 대해서 , 경보를 탐지하였을떄에 이 metric 에 대해서 검사를 할 것입니다.
  - 하지만 이러한 검사는 시간이 걸리고 그동안 사용자의 경험이 크게 안좋아질 수 있습니다.
- 그러므로 사용자 경험을 크게 저하시키는 경우 자동 종료를 설정함으로서, 경보가 울리고 이를 검사하는 귀찮은 단계 없이 바로 대처가 가능하게 됩니다. 
- 이러한 Auto Shutdown 은 빙 A/B Testing 에서 의도치 않은 404 버그를 만났을떄에 도입되었습니다. 

# [Slice the Analysis with the Appropriate Segments](#link){: .btn .btn--primary}{: .align-center}

- Treatment 는 사용자에 따라 다르게 영향을 미칩니다. 
- 예를 들어서 화장품에 대해 실행하는 Treatment 는 남성보다 여성에게 더 그 효과가 클것입니다. 
- 우리는 Change 를 좀 더 올바르게 평가하기 위해서는 사용자 특성에 따라 Segment 를 분할하고, 각 Segment 에 따라서 우리가 설정한 전체 Metric set 를 계산합니다. 
  - 이를 통해서 Segment 별 존재할 수 있는 이질적인 Treatment 의 효과에 대해서 포착할 수 있습니다. 
- 이렇게 Segment 를 분할하여 보면 , Sensitivity 가 증가하고 (영향을 미치는 group 만 분리하여 볼 수 있으므로) 또한 더욱 정확한 결과해석이 가능할 것입니다.
- 이후 다음에 우리는 두가지 세그먼트에 대해서 알아보겠습니다.

> ## Use Segments that are Stable during the A/B Test

- Exp 에서는 Treatment 에 대해서 거의 영향을 받지 않는 static 한 segment 를 권장합니다. 
  - static segment 란 사용자는 A/B Testing 내내 동일한 semgment 값을 유지해야 한다는 것입니다. 
  - 참고로 dynamic segment 는 treatment 의 영향을 받는 segment (예로 사용자 행동 관련 segment) 는 사용자가 테스트 도중 한 세그먼트에서 다른 세그먼트로 이동될 수 있습니다.
- Exp 에서 사용하는 Segment 는 주로 시장 , 국가, 브라우저, 앱버전 등입니다. 
- 이떄에 Product 에 대한 segment 를 정의할떄에는 SRM 을 유발하지 않도록 각 Segment 의 크기가 Control 과 Variation 사이에 균형을 이루는것이 중요합니다. 
  - static segment 는 treatment 의 할당과는 독립적으로 결정되므로 전체 Population 에 대해서 SRM 이 없는 한 segment 에서도 SRM 은 없습니다.
- 실험중 Segment 에 SRM 이 있는지 없는지를 검사한다면 Segment 분석에 기반한 초기 분석(즉 실험 도중에 segment 분석) 이 신뢰할 수 있다는것을 보장할 수 있습니다.

> ## Segment by Date

- Treatment 의 효과는 두가지 이유로 인하여 A/B Testing 실행에 따라 변경될 수 있습니다. 
  - 시간에 따른 유저의 행동 변화 
  - 요일에 대한 효과 
- 테스트의 초기 단계에서 분석 결과만을 살펴본다면, 편향된 결과를 얻을 수 있습니다.

![png](/assets/images/Stat/73_2.png)

- Microsoft New 는 Outlook 버튼을 홈페이지의 메일 앱 버튼으로 교체해 보았더니 메일 버튼을 클릭하는 횟수가 28% 늘었다고 합시다. 
  - 이 결과는 매력적으로 보였습니다. 이 결과는 믿을 수 있을까요? 
- Twyman의 법칙[10] 에 따라서 우리는 좀 더 지켜보기로 하였습니다.
  - 그래서 metric set 를 테스트 기간의 각 날짜별로 분할하여 계산해 보았습니다. 
- 그러자 우리는 매일 앱 버튼의 수가 급격히 내려가고 있음을 볼 수 있었습니다. 
- 위 그림은 바로 '사용자가 혼동하여' [3] 버튼을 반복적으로 클릭하는 새로운 효과의 증거였습니다. 
  - 날짜 세그먼트를 본 결과 계속 클릭률이 감소하고 있었습니다.
  - 즉 매일 앱 버튼으로 고치는것은 생각보다 좋은 영향이 없을것입니다. 
- Exp 에서는 모든 A/B Testing 분석을 날짜별로 분할하기를 추천드립니다. 
  - A/B 검정에서 날짜 세그먼트에 대해서 Treatment 의 효과가 빠르게 감소한다는 것은 바로 novelty effect 에 대한 효과입니다. 
- 테스트 시작시점과 종료 시점을 비교하여 Treatment 의 effect 가 다르다는것은 treatment 와 상호작용하는 환경에 대한 요인입니다. 
  - 즉 Treatment 를 적용한 이후에 시간에 따라 그 효과가 변한다는 것을 의미합니다. 즉 안정적인 효과를 제대로 측정하지 못하고 있는것이죠 
- 만약 하루만에 Treatment effect 가 급증한다면 데이터 품질 / 특정한 Event (휴일 등) 에 대한 요인으로 인해 Treatment 와 상호작용 한 것이라 볼 수 있습니다. 

# [Conclusion](#link){: .btn .btn--primary}{: .align-center}

- 신뢰할 수 있는 A/B Testing 을 위해서라면 다음과 같은것들이 고려되어야 할 것입니다. 
  - product 와 user 의 모든 측면을 잘 측정할 수 있는 metric set 를 설정하세요
  - 의도하지 않은 결과에 대한 자동화된 Alert 기능을 구현하고, 실험 내내 관찰하세요.
  - 안정적이고 , 인사이트를 제공할 수 있는 Segment를 만들고, 이를 쪼개서 관찰하세요.

# [Reference in Article](#link){: .btn .btn--primary}{: .align-center}

[1] R. Kohavi, D. Tang, and Y. Xu, Trustworthy Online Controlled Experiments: A Practical Guide to A/B Testing. Cambridge University Press.<br>
[2] S. Gupta, X. Shi, P. Dmitriev, X. Fu, and A. Mukherjee, “Challenges, best practices and pitfalls in evaluating results of online controlled experiments,” in WSDM 2020 – Proceedings of the 13th International Conference on Web Search and Data Mining, Jan. 2020, pp. 877–880, doi: 10.1145/3336191.3371871.<Br>
[3] P. Dmitriev, S. Gupta, D. W. Kim, and G. Vaz, “A Dirty Dozen: Twelve common metric interpretation pitfalls in online controlled experiments,” in Proceedings of the ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, 2017, vol. Part F1296, pp. 1427–1436, doi: 10.1145/3097983.3098024.<Br>
[4] W. Machmouchi and G. Buscher, “Principles for the design of online A/B metrics,” SIGIR 2016 – Proc. 39th Int. ACM SIGIR Conf. Res. Dev. Inf. Retr., pp. 589–590, 2016, doi: 10.1145/2911451.2926731.<br>
[5] K. Rodden, H. Hutchinson, and X. Fu, “Measuring the User Experience on a Large Scale : User-Centered Metrics for Web Applications,” Proc. SIGCHI Conf. Hum. Factors Comput. Syst., pp. 2395–2398, 2010, doi: 10.1145/1753326.1753687.<br>
[6] W. Machmouchi, A. H. Awadallah, I. Zitouni, and G. Buscher, “Beyond success rate: Utility as a search quality metric for online experiments,” in International Conference on Information and Knowledge Management, Proceedings, 2017, vol. Part F1318, doi: 10.1145/3132847.3132850.<br>
[7] E. Kharitonov, A. Vorobev, C. Macdonald, P. Serdyukov, and I. Ounis, “Sequential Testing for Early Stopping of Online Experiments,” Aug. 2015, doi: 10.1145/2766462.2767729.<Br>
[8] A. Malek, S. Katariya, Y. Chow, and M. Ghavamzadeh, “Sequential multiple hypothesis testing with type I error control,” 2017.<Br>
[9] D. J. Benjamin et al., “Redefine statistical significance,” Nature Human Behaviour, vol. 2, no. 1. 2018, doi: 10.1038/s41562-017-0189-z.<Br>
[10] R. Kohavi, “Twyman’s Law.” .<Br>
[11] N. Chen, M. Liu, and Y. Xu, “How A/B tests could go wrong: Automatic diagnosis of invalid online experiments,” WSDM 2019 – Proc. 12th ACM Int. Conf. Web Search Data Min., pp. 501–509, 2019, doi: 10.1145/3289600.3291000.<br>

**Reference**

- <https://www.microsoft.com/en-us/research/group/experimentation-platform-exp/articles/patterns-of-trustworthy-experimentation-during-experiment-stage/>

 실험 도중에 유저에게 안좋은 영향을 끼치면 안되니까, 메트릭을 살펴보다가 중단한다는 부분은.. Peeking problem 에 해당하는 부분인데 이것을 해결한 논문을 또 추가로 읽어야될것 같네요... 얘네들은 뭔가 획기적인것을 사용한다는듯이 말하다가 구체적 방법론은 논문으로 다 빼버리는게 마음에 안들지만 그래도 인터넷에 있는 A/B Testing 아티클중에는 그 질이 압도적이라(무려 Microsoft 의 공식문서...)... 울며 겨자먹기로 읽는중..
{: .notice--success}

