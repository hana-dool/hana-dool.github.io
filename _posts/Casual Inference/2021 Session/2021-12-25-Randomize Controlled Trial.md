---
title:  "인과추론의 정석 &#58; 무작위 통제실험"
excerpt: ""
categories:
  - Casual_Inference_Session2021
last_modified_at: 2021-12-20

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Casual Inference 와 철학
{: .notice--warning}

> ## Law of Large number

- 동전 던지기를 하게 되면 앞면과 뒷면이 나올 확률은 50%
- 처음에는 Toss 와 Head 가 각각 50% 로 나오지 않지만 Trial 을 반복함에 따라서 이론적인 확률에 가까워진다는 법척
- Random Assignment 는 이러한 동전던지기와 똑같음
  - 동전을 던져서 앞면이면 Treatment , 뒷면이 나오면 Control 그룹으로 배정한다고 할때, 동전을 조금 던지면 50% / 50% 의 확률이 되지 않지만 많이 던질수록 50% 의 확률로 배정이 되게 됨
  - 이렇게 배정이 되면, 다양한 특성을 가진 연구 대상자들이 반반씩 각 그룹에 나뉘게 되고, 어떤 실험 참가자들의 특성이 평균적으로 두 그룹에 균일하게 분포하게 될 것임
  - 단 이때 전제조건은 큰수의 법칙에 의해 Random Assigned 된 사람의 수가 많다는 가정이 있어야 함. 

- 즉 Random Assignment 는 두 집단이 유사한 특성을 가지고, 비교 가능하게 되는 것임 

![jpg](/assets/images/Stat/136_1.jpg)

- 위처럼 Random Assignment 를 하게 되면 , 기존의 분포와 동일하게 나뉨
  - 하지만 샘플 숫자가 너무 적으면, 특정한 특성이 50 : 50 으로 잘 나뉘지 않는 경우도 생김
- 그러므로 샘플 숫자가 너무 적지 않도록 주의를 해야하고, Random Assignment 를 하더라도 경우에 따라서 순수하게 Random Assignment 가 안되는 경우도 존재 
  - 실험 참가자들을 오는 순서대로 배정한다고 할때 우리가 모르는 어떤 다른 요인에 의해서 실험 참가하는 순서가 결정될수도있음. 이런 요인이 끼어있다면 Random Assignment 를 의도했어도 Random 이 안되는 경우도 있음
  - Random Assignment 를 수행한 이후에 Control 과 Treatment 그룹이 균등하게 분포가 되어서 비교 가능한지에 대해서 체크해야할 필요가 있음!

> ## Example (Good)

- 대표적인 Randomization Experiment 의 사례를 살펴보자. 
  - 이 연구는 대학교에서 교실 내에서 노트북이나 태블릿을 허용하는것이 실제 학생들의 성적에 어떤 영향을 미치는지를 분석하고자 Randomize Experiment 를 고안한 실험 

![jpg](/assets/images/Stat/136_2.jpg)

- 50개의 Class 에 대해서 726명의 학생을 대상으로 각 클래스를 3개의 그룹으로 Random 하게 나누었음.
  - 첫번째 Treatment 그룹은 자유롭게 노트북과 태블릿의 사용이 허용됨
  - 두번쨰 Treatment 약간의 제약조건 하에서 노트북과 태블릿의 사용이 허용됨
  - 마지막 Control 그룹은 교실에서 노트북과 태블릿 사용이 완전히 금지됨
- 그 이후 세 그룹간의 기말고사 성적 차이를 비교함으로서 이 Treatment 의 인과적인 효과를 비교하고자 디자인을 한 전형적인 Randomized Experiment 연구 
- 모든 Research Design 을 관통하는 가장 중요한 원칙인 "Treatment 를 제외하고 모든 다른 요인들에 대해서 비교 가능한지?" 은 Randomization Experiment 에도 똑같이 적용됨
  - 교실 내에서 랩탑이나 태블릿을 사용했다는 사실을 제외하고 나머지 요인 (성별, 인종, 수업 듣기전의 성적 등의 모든 요인은 평균적으로 큰 차이가 없어야 함!)

> 비교 가능한지에 대해서 검정하기

![jpg](/assets/images/Stat/136_3.jpg)

- 세 그룹간의 차이를 보여주고 있습니다. 
  - Treatment 그룹간의 대부분의 특성들이 매우 비슷함 (성별, 인종,연령,수업전의 GPA 등) 즉 Random Assignment 는 잘 되었음을 알 수 있습니다. 
- 반면에 아래의 Treatment 변수를 본다면, Main Treatment 의 경우에는 매우 다른것을 볼 수 있습니다. 
- 즉 Random Experiment 에서 기대하는 전형적인 패턴입니다. Treatment 요인 외에 다른 변 요인들은 모두 동일하므로, 측정하는 효과는 모두 Treatment 때문이라고 결정내릴 수 있을것입니다. 

![jpg](/assets/images/Stat/136_4.jpg)

- 위는 이 실험에 대한 결과입니다. 즉 랩탑이나 태블릿을 사용하는것은 기말고사의 성적을 유의하게 낮추고 있다는것을 볼 수 있습니다.
- 또한 Demographic 변수에 대한 영향의 효과는 거의 없다는것 (`X`) 을 볼 수 있습니다. 
  - 이는 당연히 Demographic 의 경우 사전 실험에서 같게 조절했으므로 바람직한 결과임을 알 수 있습니다.

> ## Example (Wrong)

![jpg](/assets/images/Stat/136_5.jpg)

- 이가탄에 대한 광고에서 Randomization Experiment 를 통해서 효과가 검증되었다고 광고를 많이 함
- 이가탄의 성분이 비타민 C , 비타민 E , 리소짐염산염, 카르바조크롬 인데 , 이 성분들의 효과를 검증하는 Randomization Control 실험을 함

> Experiment Setting

![jpg](/assets/images/Stat/136_6.jpg)

- 위처럼 총 112명을 대상으로 무작위 배정을 함.
  - 결과적으로 Control group : 51 명
  - Test Group : 49 명
- 몇명이 충분한지에 대해서는 Research Context 에 따라서 달라지므로, 기준을 제시하기는 힘듦.
  - 하지만 적어도 Randomized 이후에 실험군과 대조군이 잘 분배되었는지 검사를 해야 할 것입니다.

> Experiment Control and Treatment Group

![jpg](/assets/images/Stat/136_7.jpg)

- 위에서 GI , PI ,PD 는 염증지수라고 보면 됩니다.
  - 위를 보면, 이미 염증지수의 차이가 이미 Control 과 Treatment 차이가 큰것을 볼 수 있습니다.
  - 즉 Control 그룹에 비해서 Treatment Group 의 염증 지수가 이미 높은 그룹이라고 볼 수 있습니다. 
- 약을 복용하고 4주후 / 8주후의 기록도 보여주고 있는데, $\Delta$ 를 볼때에 4주/8주 후에는 두 그룹의 염증 지수가 비슷해 졌고, 각 그룹간의 전후 비교를 통해서 약의 효능을 주장하고 있음!
- 그런데 이 연구가 잘 디자인된 랜덤화 실험이 아님
  - 위의 염증지수를 토대로 잇몸 건강상태가 좋지 않은사람이 Treatment 그룹에 많았고, 또 정상적인 사람이 Control 에 더 많았다고 추론할 수 있음.
  - 정상적인 사람들은 약을 안먹어도 잇몸 건강은 크게 안변할것임
  - 잇몸상태가 좋지 않은 사람의 경우 약을 복용 해서든 / 자연적으로 시간이 지나서 잇몸이 정상으로 돌아왔을것 (즉 이가탄 덕분이 아닐수도 있다는것이죠.)
- 즉 애초에 비교 가능한 대상을 가지고 비교한게 아님. 그러므로 이가탄의 인과관계를 제대로 추론하기가 어렵다고 할 수 있습니다. 
- Random Assingment 가 Gold Standard 라 볼 수 있지만, Random Assignmet 이후에 두 그룹에 잘 배정이 되었고, 비교 가능하다는것을 반드시 체크해야 된다는것을 이 사례를 통해서 알 수 있었습니다.

> ## AB Test

- 실제로 기업에서도 이러한 실험분석을 많이 함! 
  - IT 기업에서는 이런 랜덤화 테스트를 AB Test 라고 많이 함.

---

**Reference**

- https://www.youtube.com/watch?v=HKpkgluQypA&list=PLKKkeayRo4PWyV8Gr-RcbWcis26ltIyMN&index=4

