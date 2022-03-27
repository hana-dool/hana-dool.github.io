---
title:  "Catboost"
excerpt: ""
tags:
  - ML_Model
last_modified_at: 2022-03-14

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io

---

 Decision Tree 에 대해서 알아보도록 하자.
{: .notice--warning}

# [Idea of Decision Tree](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction 

>  의사결정트리(Decision Tree)란?

- 의사결정트리는 일련의 분류 규칙을 통해 데이터를 분류, 회귀하는 지도 학습 모델 중 하나이며, 결과 모델이 Tree 구조를 가지고 있기 때문에 Decision Tree라는 이름을 가집니다.
- 이렇게 Tree 구조를 가지는 이유는 모델자체가 양자택일의 선택을 모아놓은 "Rule" 이고 이를 시각화 하면 Tree 와 같은 구조를 지니기 때문입니다.

![jpg](/assets/images/Stat/164_2.jpg){: .align-center}

- 이때 위와 같은 구조에서, 어떻게 예측이 이루어진다는 것일까요? 
- 만일 어떤 사람의 데이터가 (남자 , 나이=14, sibsp=1) 이라고 합시다. 
  - 그러면 위 Decision rule 에 따라 분류되게 된다면 그 사람은 Decision Rule 에 따라 사망으로 예측되게 될 것입니다.

# [Decision Tree Algorithm](#link){: .btn .btn--primary}{: .align-center}

> ## Idea

- 자 그럼 예측을 어떻게 수행하는지 대충 알았으므로 "어떻게 위와 같은 Tree" 를 구성할 수 있을까요?
- 설명변수를 어떤 기준으로 분리하는 것이 목표변수의 분포를 가장 구별하는 판단 기준이 있어야겠죠.
- 의사결정나무의 분리기준은 해결하고자 하는 문제가 예측(i.e., 회귀(regression)), 분류인지에(classification) 따라 다릅니다.

> ## Terms 

![jpg](/assets/images/Stat/164_1.jpg){: .align-center}

| **No** | **항목**                                           | **설명**                                                     |
| ------ | -------------------------------------------------- | ------------------------------------------------------------ |
| 1      | 루트노드(Root Node)                                | 나무가 시작되는 노드를 의미합니다. **그림** 1과 같이 의사결정나무를 시작화했을 떄 루트노드는 맨 위에 위치합니다. |
| 2      | 자식노드(Child Node)                               | 상위의 노드에서 분리된 하위 노드를 의미합니다.               |
| 3      | 부모노드(Parent Node)                              | 자식 노드의 상위 노드를 의미합니다.                          |
| 4      | 중간노드(Internal Node)                            | 나무 중간에 위치한 노드로 루트노드 또는 최하위 노드가 아닌 모든 노드가 행당됩니다. |
| 5      | 가지(Branch)                                       | 하나의 노드로부터 잎사귀 노드까지 연결된 일련의 노드들을 포함합니다. |
| 6      | 잎사귀 노드(Leaf Node) 또는 끝 노드(Terminal Node) | 각 가지 끝에 위치한 노드                                     |
| 7      | 순수노드(Pure Node)                                | 해당 노드의 목표변수가 동일한 값이나 종류만 가지는 노드를 의미합니다. |
| 8      | 깊이(Depth)                                        | 가지를 이루고 있는 노드의 분리 층수(**그림 1**의 경우 depth = 3) |

# [Metric](#link){: .btn .btn--primary}{: .align-center}

> ## Gini (classification)

- 위와 같은 구조의 "의사 결정" 을 내리기 위해서는, "결정을 위한 기준" 이 필요합니다. 즉 내가 내린 결정이 얼마나 좋은지를 mesaure 할 수 있는 metric 이 필요하다는 것이죠. 
- 그때에 이용할 수 있는것이 바로 불순도 입니다. 

> definition

-  영역 $A$ 가 $m$ 개의 records 를 가지고 있다고 하면,  Gini Index for $A$ 는 아래와 같이 계산됩니다.

$$I(A)=1-\sum_{k=1}^{m} p_{k}^{2}$$

- 이때 $\mathrm{p_k}=$   영역 $A$ 내에서, class $k$ 를 가지는 데이터의 비율로 정의됩니다.
- 특징
  - data 의 class 가 모두 같으면 $\mathrm{I}(\mathrm{A})=0$
  - 모든 class 가 균일한 비율 (1/k) 이면 최댓값을 가집니다. ( $=0.5$ in binary case)

> Example 

![jpg](/assets/images/Stat/164_14.jpg){: .align-center}`

> A 영역을 나눈다면? 

- 이때 A 영역을 나누게 될 수도 있습니다. 그러면 Gini 의 계산은 어떻게 될까요? 
- 만약 영역 A 가 d 개의 영역으로 나뉘게 되면 아래와 같이 정의됩니다.

$$I(A)=\sum_{i=1}^{d}\left(R_{i}\left(1-\sum_{k=1}^{m} p_{i k}^{2}\right)\right)$$

- $\mathrm{R}_{\mathrm{i}}$ = i 번째 영역의 전체 데이터에 대한 비율 
- $p_{ik}$ = i 번쨰 영역의 k class 데이터 비율

![jpg](/assets/images/Stat/164_15.jpg){: .align-center}`

> information Gain 

- 이때 A 영역을 빨간 점선으로 나누자 , Gini 가 0.47 -> 0.34 가 되었습니다. 
- 즉 이떄에 Information Gain 은 0.47 - 0.34  = 0.13 이 됩니다.

> ## Deviance (classification)

> Definition

- 영역 $D_i$ 에 대한 deviance 는 아래와 같습니다.

$$D_{i}=-2 \sum_{k} n_{i k} \log \left(p_{i k}\right)$$

- $\mathrm{i}$ : node index, k: class index
- $p_{\mathrm{ik}}$ : probability of class $\mathrm{k}$ in node $I$
- 이떄 Deviance = 0 dms 

> Example 

![jpg](/assets/images/Stat/164_16.jpg){: .align-center}

> Split - Example 

![jpg](/assets/images/Stat/164_17.jpg){: .align-center}

- Information Gain 은 21.17 - 16.62 = 4.55

> ## Entropy

> Definition

$$E=-\sum_{i=1}^{k} p_{i} \log _{2}\left(p_{i}\right)$$

> Example 

![jpg](/assets/images/Stat/164_19.jpg){: .align-center}

> Split

- 분기시에도, 이전과 같은 

# [Examples](#link){: .btn .btn--primary}{: .align-center}

> ## Classification Example 

![jpg](/assets/images/Stat/164_4.jpg){: .align-center}

- 위와 같이 테니스 경기 참가 여부를 예측하는 데이터가 있다고 합시다. 

> Step 1.: Root 노드의 불순도 계산

$$E(\text { 경기 })=-\frac{9}{14} \log _{2}\left(\frac{9}{14}\right)-\frac{5}{14} \log _{2}\left(\frac{5}{14}\right)=0.940$$

> Step 2 : 나머지 Feature 에 대해 분할해본 후, 자식노드의 불순도 계산

- 2-1) 날씨

![jpg](/assets/images/Stat/164_5.jpg){: .align-center}

- 2-2) 온도

![jpg](/assets/images/Stat/164_6.jpg){: .align-center}

- 2-3) 습도

![jpg](/assets/images/Stat/164_7.jpg){: .align-center}

- 2-4) 바람

![jpg](/assets/images/Stat/164_8.jpg){: .align-center}

> Step 3 : 각 Feature 에 대한 **Information Gain 계산 후 Information Gain(Root노드와 자식노드의 불순도 차이)이 최대가 되는 분기조건을 찾아 분기**

![jpg](/assets/images/Stat/164_9.jpg){: .align-center}

> Step 4 : **모든 leaf 노드의 불순도가 0이 될때까지 2,3을 반복 수행한다.**

- 예를 들어, "맑음"으로 분류된 노드는 "날씨 = 맑음" 인 데이터만 가지고 와서 다시 분할 전 엔트로피를 계산한다.

![jpg](/assets/images/Stat/164_10.jpg){: .align-center}

- 위처럼 빨간색 nodes 로 분류된 데이터를, 다시 이전 step 을 동일하게 수행하여 nodes 를 나눕니다. 

![jpg](/assets/images/Stat/164_11.jpg){: .align-center}

> Step 5 : 반복적으로 수행합니다.

![jpg](/assets/images/Stat/164_12.jpg){: .align-center}



> ## Regression Example 

![jpg](/assets/images/Stat/164_13.jpg){: .align-center}

![jpg](/assets/images/Stat/164_18.jpg){: .align-center}

# Decision Tree 장점{: .btn .btn--primary}{: .align-center}

# [Decision Tree 단점](#link){: .btn .btn--primary}{: .align-center}

# 특징

![jpg](/assets/images/Stat/164_3.jpg){: .align-center}

- 위와 같이 Tree 의 분기는 이분법적으로 일어나기 때문에, 각 영역을 사각적으로 나누는것과 같게 됩니다.

**reference**

---

- https://www.youtube.com/watch?v=UFbJprjfS1E
- https://ko.wikipedia.org/wiki/%EA%B2%B0%EC%A0%95_%ED%8A%B8%EB%A6%AC_%ED%95%99%EC%8A%B5%EB%B2%95