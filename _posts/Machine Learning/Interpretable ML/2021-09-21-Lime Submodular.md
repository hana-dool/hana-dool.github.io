---
title:  "SP-Lime &#58; Submodular Pick"
excerpt: "전체적인 모델 해석을 위해 대표적인 Instance 를 선택하는 방법"
categories:
  - Interpretable_ML
last_modified_at: 2021-09-20

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Lime 이란게 사실, 국소적인 데이터의 설명을 위해서 만들어진거라 특정 instance 에 대한 해석은 어느정도 훌륭히 해내는데에 비해서, 모델이 전체적으로 어떻게 해석하는지에 대한 능력은 약했습니다. 이를 해결하고자 한 방법론이 바로 Submodular Pick 방법론입니다.
{: .notice--warning}

- 제가 리뷰한 Lime 논문에도 자세히 실려있는 부분이라, 이 내용은 논문 내용중 SP - lime 부분을 요약한 것입니다.
- Notation 이나 자세한게 이해가 안되면 Lime 논문 리뷰한것을 다시 읽어보세요

# [Submodular pick for explaining models](#link){: .btn .btn--primary}{: .align-center}

- SP-LIME : 모델 자체의 신뢰 문제를 풀기 위해 대표적인 인스턴스를 선택하는 알고리즘 입니다. 

> ## Pick problem

- 데이터 $X \in R^{n*d}$ 를 고려합시다.
- 모든 데이터를 살펴볼 수 없기 때문에, 특징이 다르고 중요한 데이터만을 뽑아서 생각한다.
- 살펴볼 데이터 budget B를 정한다. 이는 데이터를 총 몇 개 뽑아서, 내 데이터를 대표할 샘플로 만들지의 값이다
  - 이 값을 100개를 정한다면, 총 100개의 Sample 을 뽑게 됩니다.
- original representataion 으로부터, 해석가능한 표현   $X' \in R^{n*d'}$    를 만든다. 
- 데이터의 local 한 importance를 나타낼 matrix W 를 아래와 같이 정의합시다.
  - linear model을 explanation 으로 사용했다면 데이터 $x_i$ 에 대하여 explanation $g_i = \xi(x_i)$  를 얻을 수 있고, $W_{ij} = \mid w_{g_{ij}} \mid$  로 정의할 수 있습니다.
  - 이떄에, $g_{i}$ 는 데이터 $x_i$ 에 대한 Explainable model 입니다. (linear)
  - 그리고 $g_{ij}$ 는  linear model 의 j번째 feature 에 대한 계수입니다. 
- 추가적으로  $I_j$ (j column 의 global importance를 정의) $I_j = \sqrt{(\sum_i W_{ij})}$ 을 정의합니다.
  - 모든 instance i 에 대하서 , 설명 가능한 모델 $g_i$를 Construct 한 뒤에 , j 번째 feature 의 계수의 절댓값 모두 더한것입니다.
  - 당연히 '중요한 feature' 라면, 많은 샘플에 대해서, 왜 이런 예측을 하였는니? 에 대한 Local 적인 해석을 하더라도 계속 포함될 것입니다.
  - 예시로 월급을 예측한다고 할떄에 Feature 에 나이가 있다면,각 instance (철수, 영희,.....) 에 대한 월급 설명을 할때에 대부분 나이 변수가 크게 영향을 끼칠것이기 떄문입니다.
- 최대한 특징이 다르며 많은 정보를 포함하고 있는 데이터를 추출하기 위해서 $c(V,W,I) = \sum_{j=1}^{d'}1_{\exist i \in V : W_{ij}>0}I_j $라고 converge function 을 정의합니다.

![jpg](/assets/images/ML/14_3.png)

- 우선 위와 같이 예시를 들어보겠습니다. 
- 각 instance x_i 에 대하여, 설명모델은 가로줄과 같습니다. 
  - x1 은 $1\cdot f_1 + 1 \cdot f_2  = x_1$ 로 설명되고 있다고 보시면 됩니다. 
- $V=\{1,3\}$ 인 경우에 $c(V,W,I)$ = (1+4) + (4+2) 가 됩니다.
  - 그 이유는 $x_1$ 의 경우 $f_1, f_2$ 에 의해 설명이 되고, 각각의$I_1, I_2$ 는 1,4 이기 때문입니다.
  - $x_3$ 의 경우 $f_2,f_3$ 에 의해 설명이 되고, 각각의 $I_2, I_3$ 은 4,2 이기 떄문입니다.
- 이렇게 Coverage function 을 최대화 하는 집합 V 를 찾으면 중요한 데이터들을 쏙쏙 뽑아낼 수 있을것입니다.
  - 모두, 다양한 local 모델들에 대해서 중요하다고 생각되었던 Feature 들이기떄문에 중요한 데이터일것입니다.

$$Pick(\mathcal{W},I)=\underset{\mathcal{V},|\mathcal{V}|\leq B}{\operatorname{argmax}}c(\mathcal{V},\mathcal{W},I)$$

- 이러한 집합 V 를 찾아내는것은 위와 같이 정의됩니다. 

> ## SP Lime

- 하지만 , 위와 같이 , '최대화 하는 집합' 을 찾는것은 Global 한 optimization 문제로 매우 어렵습니다. 
- 그러므로 차선책으로 Greedy 하게 골라내려고 합니다. 

![jpg](/assets/images/ML/14_4.png)

- 그 방법론은 위와 같습니다.   

---

**Reference**

- <https://christophm.github.io/interpretable-ml-book/counterfactual.html>
- <https://tootouch.github.io/IML/counterfactual_explanations/>

 Global 한 해석을 가지기 위하여, Local 적인 해석에 맞춰져 있는 Lime 을 이용해 어떻게 하면, 모델을 해석할 수 있을지 탐구해본게 SP lime 입니다. 
{: .notice--success}

