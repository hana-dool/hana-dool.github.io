---
title:  "무작위 통제실험 연구사례 &#58; 걷기 운동 동기부여를 위한 모바일앱 인센티브 디자인"
excerpt: ""
categories:
  - Casual_Inference_Session2021
last_modified_at: 2022-01-14

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 https://www.youtube.com/watch?v=jDXl8xiO6NI 의 논문 리뷰 
{: .notice--warning}

# [Experiment](#link){: .btn .btn--primary}{: .align-center}

- 회사와 협업하면서 우여곡절이 있었는데, 그 과정에서 누군가 나에게 한번만 말을 했으면 좋았겠다! 라고 생각되는것을 짧게 준비 했음 

> ## Research Questions 

- 현대인의 경우, Physical inactivity 가 굉장한 문제
  - 미국에서는 약 80% 가 매일 달성해야하는 physical activity 를 달성하지 못하고 있다고 합니다. 

![jpg](/assets/images/Stat/149_1.jpg)

- 위와 같은 문제는 개인적인 문제 이상으로 매우 중요합니다.
  - 사회적 지위가 낮거나, 교육 수준이 떨어지거나 또는 리소스가 없는 사람에게 더 강하게 나타나게 됨 
  - 단순히 내가 운동을 안해서 당뇨 , 고혈압이 오는 문제를 넘어서서 글로벌적으로 우리가 주목을 해야 되는 복지와 관련된 문제라 할 수 있습니다.
- 이 연구는 다른 헬스케어 연구들도 비슷하겠지만, 가장 본질적인 질문에서 시작합니다.
  - 우리가 어떻게 하면 이 사람들의 Physical Activity 를 효과적으로 높힐 수 있을까? 

![jpg](/assets/images/Stat/149_2.jpg)

- 이를 위한 솔루션으로 , 위와 같은 핸드폰이 대안으로 떠올랐습니다.
  - 휴대폰을 이용하면 real time 으로 나를 트래래킹하고, 또한 내가 얼마나 걸었고, 어디에서 얼만큼 어떤 운동을 했는지 등을 알 수 있습니다.
  - 또한 센서가 있다보니, 나를 계속 따라다니면서 tracking 할 수 잇음
- 즉 핸드폰을 이용하면 내가 얼마나 activity 한지와 건강한지 등을 잘 체크할 수 있죠.

> ## 핸드폰을 이용한 마케팅 

- 아! 그럼 핸드폰을 이용하면 사람의 activity 를 증가시키고, 비만을 줄이는것을 할 수 있지 않을까?  라는 아이디어가 자연스럽게 나오게 됩니다.
  - 하지만 이러한 시도는 대부분 실패합니다.
- 그 이유는 , physical activity 는 사실 굉장히 self - control 이 필요한 문제이기 떄문입니다!. 
  - 아 나 운동해야지! -> 비가옴 -> 아 안가야겠다.... 
  - 위와 같이 나 자신을 통제하는것이기 떄문에 사람들이 쉽게 move 하기가 힘듬
- 그래서 핸드폰 앱들은 인센티브를 주기 시작했습니다.

![jpg](/assets/images/Stat/149_3.jpg)

- 10만보를 걸으면 10달러 줄게! 또는 10만보를 걸으면 10달러를 기부해주겠다! 처럼 마케팅을 하기 시작했습니다.
  - 이런 인센티브를 줘서 사람들을 motivation 시키기 시작한 것이죠.

> ## Three Factor

- 위와 같이 인센티브를 주기로 결정하면,  이러한 이벤트에 대한 비용을 줄이면서 사람들에게 효과적으로 동기를 주기 위해서 기업의 관점에서 결정해야 되는 세가지 중요한 Factor 가 있습니다.

![jpg](/assets/images/Stat/149_4.jpg)

> 1.Incentive Scheme (동기)

- Egoistic (이기심)
  - 걸으렴 나에게 돈이 된다! 
- Philanthrophic (박애심)
  - 걸으면 다른 사람들에게 기부가 된다! 

> 2.Incentive Requirement

- 위와 같은 보상(동기) 를 얻기 위해서 얼마나 힘든 과제를 해야하는지
  - High : 10만보를 걸어야 100달러 준다! 
  - Low : 1000보만 걸어도 1달러 준다!

> 3.incentive Reward

- 사람들에게 얼마나 많은 reward 를 주느냐? 
  - High : 1000달러 보상
  - Low : 1 달러 보상

![jpg](/assets/images/Stat/149_5.jpg)

- 위처럼 3가지를 잘 정해서, 우리 앱의 incentive 를 잘 결정하는게 중요
- 하지만 아직까지 위의 조합을 어떻게 optimal 하게 만들 수 있을지에 대한 연구가 없었음
- 우리 연구의 목표는 어떻게 하면 incentive 를 디자인할때 reqiremnet, reward 를 조절해서 기업에도 이익이 되고, 사람들에게 incentive 도 줄까? 가 우리의 질문이 됩니다.
  - 한마디로 하면 제일 효과적인 Incentive scheme 을 찾으려 하게 됩니다.

> ## Experment Design

- Randomized Field Experiment 방법론을 채용 

![jpg](/assets/images/Stat/149_6.jpg)

- 위처럼 총 8개의 실험 디자인이 나오게 됩니다.
- Incentive scheme 
  - donate (기부) vs get (내가 얻음)
- incentive reward 
  - 10 달러 vs 20 달러
- incentive requirement
  - 140000 vs 70000
  - (위처럼 정한 이유는 만보가 사실 적정 운동량이기 떄문에
  - 2배 차이가 나는게 가장 명확하다고 생각해서 14만보를 비교하기로 함 

> ## Randomization Design

- 한 그룹당 만약 4000명이라면 한 그룹당 500명 정도의 사람이 할당받게 됩니다. 

![jpg](/assets/images/Stat/149_7.jpg)

- 하지만 이떄 유저를 랜덤하게 어떻게 할당할 수 있을까요? 
- 처음에는 R 에서 random number generator 를 이용해서 유저 번호를 붙여서 드렸지만, 이 방법은 안좋음
  - 회사에서 나에게 주고, 나는 다시 number 를 붙여서 보내줘야 함
- 회사의 일을 최소화 하기가 좋지 않음 그래서, random 하게 분배하는 '방법' 을 전달 
- 위처럼 유저의 id 를 이용해서, Random number generater 를 수고함 
  - 유저의 id 가 랜덤이라는 가정 사에서, Randomization method 를 가정
  - 모든 자릿수를 더한 다음에, mod 8 로 나머지를 찾고, 그것을 이용해 배정한다던지... 등
- 하지만 Random 을 어떻게 하더라도 , 우연성으로 다소 특정 그룹에 Skewed 될 수 있는데, 이는 실험적으로 잘 맞추도록 하자. 

> ## Sample 

- Sample
  - Collaborated with one of the largest fitness app companies in South Korea (has been downloaded more than 500,000 times and has an average of 120,000 weekly active users.)
  - 16 metropolitan areas in South Korea
  - App tracks and presents a user's physical activity
  - 4000명의 유저이고, 즉 각각의 variant 에 500명이 할당됨
- Outcome
  - Accept or not (binary) (도전 메시지가 오는데, 이것에 대해서 도전 수락을 하는지? )
    - 도전 누른다는거 자체가 사실 굉장히 중요함 (동기 부여)
  - Achieve or not (binary)
    - 도전을 달성하느냐, 마느냐
  - Number of Steps
    - 도전 메시지를 받고나서 얼마나 걸었는지

> ## 최적의 조합

- 리워드를 높히는것과 requirement 를 낮추는것중에 어떤게 효과적일까? 
  - 물론 리워드를 많이 주고 requiremnt 를 낮추면 무조건 좋아할것임! 

![jpg](/assets/images/Stat/149_8.jpg)

- 우리가 보고 싶은것은 어떤 incentive scheme (Egoistic / philanthropic) 일떄에 requirement 와 reward 중 어떤것이 효과적일지? 를 보고 싶습니다.
- 이를 위해서 우리는 self- perception theory 를 이용하려고 합니다.

> self-perception Theory

- 사람은 행동할떄 너무나도 많은 동기가 있어서, 행동의 동기를 모두 기억하기는 힘듦
  - 단지 우리는 내가 이 행동을 통해서 추구하는 이미지를 생각하게 됨! 
  - ex : 건강 요거트를 먹으면서 몸짱(김종국 등) 을 생각하면서 먹게됨
  - ex : 기부를 하면서 나는 마더테레사 등을 생각하면서 기부하게 됨 
- Egoistic 
  - 강력한 나의 능력을 보여줄 수 있는 이미지를 추구하게 될때는 Egoistic 함을 추구 
- Pgilanthropic
  - 기부를 할떄, 착한일을 할떄, "아 나는 착한 사람이야~ " 하면서 추구 
- 위처럼 두개 종류의 self-perception 이 있다는것은 알았습니다. 이를 통해서 Egoistic , philandtropic 과 incentive 의 관계를 살펴봅시다.

> ## Egoistic , philandtropic 

![jpg](/assets/images/Stat/149_9.jpg)

- egoistic 한 경우에는 reward 를 높힐때가 클때에 매칭이 잘 될것입니다.
  - 리워드가 높을떄 우리는 "내가 연봉이 1억이야! " 그러면 나는 퍼포먼스가 좋다! 라고 생각 
  - 즉 이런것들은 Egoistic - incentive 와 매칭할 수 있음

![jpg](/assets/images/Stat/149_10.jpg)

- philanthropic intentive
  - requirement 가 낮을떄 : 경쟁이 없고, 허들이 낮음 -> philanthropic 과 매칭이 잘 될거라고 생각
  - philanthropic 입장에서 추구하는 perception 자체가, 편안, 즐거움을 원하기 때문! 

> Note

- 즉 Egoistic 할때는 reward 가 클때 효과가 좋을것이고, philanthropic 할때에는 requirement 가 낮을때 효과가 좋다고 생각할 수 있습니다.

> ## Results : Comparison incentive scheme

![jpg](/assets/images/Stat/149_11.jpg)

- Egoistic 한 효과가 philanthropic 한 경우보다 효과가 더 큰것을 볼 수 있습니다. 
- 또한 Reward 가 클떄 와 Low requirement 일떄에 효과적인것을 볼 수 있으므로 우리의 목적인 incentive scheme 과, high reward / low requirment 를 엮어보는것이 정당하는것을 알 수 있습니다.

![jpg](/assets/images/Stat/149_12.jpg)

- 또한 한가지 놀라운점이 있는데요, low requirment , low reward 일 경우만 philantrophic 한것의 효과가 높다고 나왔습니다. 
  - 이는 매우 좋은 시사점인데요, 필연적으로 초기 스타트업같은 경우에는 low - requirment + Lower reward 인 경우가 많기 떄문입니다.
- 그러므로 초기 스타트업의 경우에는 philanthropic 한 sceme 으로 앱을 개발하는것이 좋을것입니다.

> ## Results Analysis

![jpg](/assets/images/Stat/149_13.jpg)

- 식은 위와 같이 interact 가 있는 regression scheme 을 사용하였습니다.
  - 위의 효과를 분석해보면,

- 위 식에 기반하게 되면, $bete_2$ 와 $\beta_3$ 를 비교해보면, p-value 가 0.01 로 차이가 있음 
  - 
