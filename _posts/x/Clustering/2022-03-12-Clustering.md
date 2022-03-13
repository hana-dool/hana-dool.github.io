---
title:  "Clustering"
excerpt: ""
tags:
  - ML_Model
last_modified_at: 2022-03-13

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 여기 쓰인 글들은 모두, 비공개 게시글입니다. 비공개로 남긴 이유는 상당수가 제 개인 작성이 아니라 여러 Reference 를 긁어오고, 정리한것에 불과하여, 저작권 이슈가 생길수도 있기 떄문입니다. 그러므로 이를 보신다면 Reference 로 쓰지 마시고 단순히 참고용으로만 보시기 바랍니다.
{: .notice--warning}

# [Clustering](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

> Clustering?

- Clustering 이란?

  - data를 다음의 두 가지 조건을 만족하는 cluster(군집, 집단)로 조직(organizing)화 하는것. 

> How Clustering? 

- ex : cluster 내부의 data들 간의 similarity(유사성)이 높도록 
- ex : cluster 외부의 data들 간의 similarity(유사성)이 낮도록

> Note : Clustering 과 Classification 

- 다만 여기서 주의해야 할 것은 클러스터링은 **분류(Classification)**와 구별해야 한다는 점입니다. 
- 클러스터링은 정답이 없는 **비지도학습(unsupervised learning)**입니다. 다시 말해 각 개체의 그룹 정보 없이 비슷한 개체끼리 묶어보는 거죠.
- 반면 분류는 정답이 있는 **지도학습(supervised learining)**입니다. 분류를 할떄에는 정답이 있기떄문에 성능을 알아내기가 쉽습니다.

> ## Similarity?

- What is Similarity?

  - similarity(유사성)은 정의하기 힘드나, 우리는 그것을 눈으로 보면 직관적으로 안다.
  - similarity의 실제 의미는 철학적인 문제입니다... 
  - 하지만 우리는 어찌되던 "Similarity 를 추정해야겠죠?"
- 두 개의 object사이의 similarity를 측정하기 위해서 두 object 사이의 거리 (distance, dissimilarity)를 측정해야 합니다.

![jpg](/assets/images/X/2_1.jpg){: .align-center}

- 위 두 Object(사람) 의 거리는 어떻게 측정해야 할까요? 
  - Patty와 Selma의 거리를 재기 위해서는, 예를 들어, 사람이라는 objects을 (입은 옷, 귀고리, 머리 모양, 몸무게. 키, 흡연)의 특성 벡터로 표현 될 수 있는 데이터로 mapping 해야 할 것입니다.

> ## Distance? 

- 거리(Distance)란?
  - Edit Distance (두 개의 objects 사이의 similarity를 측정하는 일반적인 기법)
  - 한 개의 object에서, 다른 한 개의 object으로 변화되기 위하여 필요한 노력(effort)를 측정한다.
- 거리(Distance)의 수학적인 개념
  - $O_{1}$ 과 $O_{2}$ 를 두 개의 object이라고 할 때, ${O}_{1}$ 과 $O_{2}$ 사이의 distance는 실수(real number)이고 $\boldsymbol{D}\left(\boldsymbol{o}_{1}, \boldsymbol{o}_{2}\right)$ 라고 표기
  - 주의할 것! distance는 우리가 고등학교 때 배워서 알고 있는 유클리드 거리만 의미하는 것이 아니다. distance function은 다양하게 설정할 수 있다.

> ## Mathmatical Definition

- Dsistance function 과 Similarity function의 예 $\mathbb{x}=\left(x_{1}, x_{2}, \ldots\right), \mathbb{y}=\left(y_{1}, y_{2}, \ldots\right)$ 라고 하자.

- (1) Euclidian distance (dissimilarity)

$$D(\mathbb{x}, \mathbb{y})=d(\mathbb{x}, \mathbb{y})=\sqrt{\sum_{i}\left(x_{i}-y_{i}\right)^{2}}$$

- (2) Manhattan distance (dissimilarity)

$$D(\mathbb{x}, \mathbb{y})=d(\mathbb{x}, \mathbb{y})=\sum_{i}\left|x_{i}-y_{i}\right|$$

- (3) "sup" distance (dissimilarity)

$$D(\mathbb{x}, \mathbb{y})=d(\mathbb{x}, \mathbb{y})=\max _{i}\left|x_{i}-y_{i}\right|$$

- (4) Correlation coefficient (similarity)

$$D(\mathbb{x}, \mathbb{y})=s(\mathbb{x}, \mathbb{y})=\frac{\sum_{i}\left(x_{i}-\mu_{\mathbb{x}}\right)\left(y_{i}-\mu_{\mathrm{y}}\right)}{\sigma_{x} \sigma_{y}}$$

- (5) Cosine similarity (similarity)

$$D(\mathbb{x}, \mathrm{y})=\cos (\mathbb{x}, \mathbb{y})=\frac{\mathbb{x} \cdot \mathbb{y}}{\|\mathbb{x}\|\|\mathbb{y}\|}=\frac{\sum_{i} x_{i} y_{i}}{\sqrt{\sum_{i} x_{i}^{2}} \sqrt{\sum_{i} y_{i}^{2}}}$$

> ## Example 

![jpg](/assets/images/X/2_2.jpg){: .align-center}

- 1: Euclidean distance : $\quad \sqrt[2]{4^{2}+3^{2}}=5$.
- 2: Manhattan distance: $4+3=7$.
- 3: "sup" distance: $\quad \max \{4,3\}=4$.

> ## Clustering 을 하는 이유 

- data를 cluster(군집)들로 조직하면(organizing), data의 내부 구조(internal structure)에 대한 정보를 얻을 수 있음
- data를 분할하는 것(partitioning) 자체가 목적이 될 수 있음
  - 이미지 분할(image segmentation)
- data에서 지식을 발견하는 것이 목적이 될 수 있음 (knowledge discovery in data)
  - Underlying rules
  - topic

# [Clustering 타당성 평가](#link){: .btn .btn--primary}{: .align-center}

> ## Introduction

![jpg](/assets/images/X/2_3.jpg){: .align-center}

- 클러스터링이 얼마나 잘 되었는가를 측정하는 방법으로 내부 평가 혹은 외부 평가, 크게 2가지 방법론을 이용할 수 있습니다.
- 내부 평가 (internal evaluation) : 데이터 집합을 클러스터링한 결과 그 자체를 놓고 평가하는 방식이다. 
  - 이러한 방식에서는 클러스터 내 높은 유사도 (high intra-cluster similarity)를 가지고, 클러스터 간 낮은 유사도 (low inter-cluster similarity)를 가진 결과물에 높은 점수를 준다. 
  - 이와 같은 평가 방법은 오로지 데이터를 클러스터링한 결과물만을 보고 판단하기 때문에, 평가 점수가 높다고 해서 실제 참값 (ground truth) 에 가깝다는 것을 반드시 보장하지는 않는다는 단점이 있다.
- 외부 평가 방식 (external evaluation) : 클러스터링의 결과물은 클러스터링에 사용되지 않은 데이터로 평가된다. 
  - 다시 말해, 클러스터링의 결과물을 전문가들이 미리 정해높은 모범답안 혹은 외부 벤치마크 평가 기준 등을 이용해서 클러스터링 알고리즘의 정확도를 평가하는 것이다. 
  - 이러한 평가 방식은 클러스터링 결과가 미리 정해진 결과물과 얼마나 비슷한지를 측정한다.

> ## 내부 평가 : Dunn Index

- Dunn Index는 군집 간 거리의 최소값을 분자, 군집 내 요소 간 거리의 최대값을 분모로 하는 지표입니다.

$$I(C)=\frac{\min _{i \neq j}\left\{d_{c}\left(C_{i}, C_{j}\right)\right\}}{\max _{1 \leq l \leq k}\left\{\Delta\left(C_{l}\right)\right\}}$$

- 군집 간 거리는 멀수록, 군집 내 분산은 작을 수록 좋은 군집화 결과라 말할 수 있는데요. 이 경우에 Dunn Index는 커지게 됩니다.

![jpg](/assets/images/X/2_4.jpg){: .align-center}

> ## 내부 평가 : Silhouette

- 실루엣 지표를 계산하는 식은 아래와 같습니다.

$$\begin{equation}
s(i)=\frac{b(i)-a(i)}{\max \{a(i), b(i)\}}
\end{equation}$$

- a(i)는 𝑖번째 개체와 같은 군집에 속한 요소들 간 거리들의 평균입니다.
- b(i)는 𝑖번째 개체와 다른 군집에 속한 요소들 간 거리들의 평균을 군집마다 각각 구한 뒤, 이 가운데 가장 작은 값을 취한 것입니다. 
  - 다시 말해 b(i)는 𝑖번째 개체가 속한 군집과 가장 가까운 이웃군집을 택해서 계산한 값이라고 보시면 됩니다.

> Example 

![jpg](/assets/images/X/2_5.jpg){: .align-center}

- 위 그림처럼 어떠한 클러스터링 기법에 의해 총 10개의 데이터 포인트들이 3개의 군집으로 나눠졌다고 합시다. 
- 클러스터 A의 데이터 포인트 i를 선택하고, 데이터 포인트 i의 실루엣 계수를 구할 것이다. 

![jpg](/assets/images/X/2_6.jpg){: .align-center}

- $a(i):$ 데이터 포인트 i가 속한 클러스터 내 데이터 포인트들과 거리 평균
  - 우선 데이터 포인트 i가 속한 클러스터 A 안에 있는 다른 데이터 포인트들과의 거리 평균을 구한다. 

![jpg](/assets/images/X/2_7.jpg){: .align-center}

- b(i)는 𝑖번째 개체와 다른 군집에 속한 요소들 간 거리들의 평균을 군집마다 각각 구한 뒤, 이 가운데 가장 작은 값을 취한 것입니다. 
  - 즉 $b(i)$ = min (5.3, 5.8) = 5.3 이됩니다.

![jpg](/assets/images/X/2_8.jpg){: .align-center}

- 클러스터 $\mathrm{B}$ 와 $\mathrm{C}$ 중 데이터 포인트 i와 가까운 클러스터(=이웃 클러스터)는 $\mathrm{B}$ 이므로 $b(i)$ 값은 5.3 이 되며, $a(i), b(i)$ 값으로 데이터 포인트 i의 실루엣 계수 $s(i)$ 값을 구한다.
  - 실루엣 계수 계산식의 분모는 두 군집 간 거리를 정규화하는 스케일러의 역할을 한다. 
  - 동일한 클러스터 내에 있더라도 데이터 포인트마다 이웃 클러스터는 다를 수 있다. 
  - 만일 클러스터 안에 1개의 데이터 포인트만 존재하는 경우, 해당 데이터 포인트의 실루엣 계수는 0으로 본다. 

![jpg](/assets/images/X/2_9.jpg){: .align-center}

- 위 그림처럼 모든 데이터 포인트들에 대해 실루엣 계수를 계산했다면, 실루엣 계수들의 평균값(overall average silhouette width)을 계산해준다. 만일 클러스터 개수별로 여러 번 군집화를 수행했거나, 여러 클러스터링 기법으로 여러 번 군집화를 수행한 경우 실루엣 계수의 평균값을 비교하여, 클러스터 개수를 몇 개로 할 것인지, 혹은 어떤 클러스터 기법을 선택할 것인지 판단할 수 있다.

> Note : interpret

- 실루엣 계수의 평균값이 1에 가까울수록 군집화가 잘 되었다고 생각할 수 있다. 
- 각 클러스터 내의 데이터 포인트들의 실루엣 계수 평균값을 구하여, 각 클러스터별 평균값도 구할 수 있다. 1에 가까운 평균값을 가지는 클러스터는 'clear-cut' 클러스터, 0에 가까운 값을 가지는 클러스터는 'weak' 클러스터로 표현된다. 

> 장단점

- 장점 
  - 클러스터링이 수행된 후 실제 구분된 클러스터에 따라 실루엣 계수를 구하기 때문에, 클러스터링 알고리즘에 영향을 받지 않는다. 
- 단점 
  - 데이터 양이 많아질수록 수행 시간이 오래 걸린다.

> ## 외부 평가 : 랜드측정 (Rand Measure)

- 랜드 측정(Rand measure)는 클러스터링 알고리즘에 의해 형성된 클러스터링 결과물이 미리 정해진 모범 답안과 얼마나 비슷한지를 계산한다.
- 이 척도는 클러스터링 알고리즘이 얼마나 답을 잘 맞추었는지를 퍼센티지로 표현해준다. 식은 아래와 같다.

$$R I=\frac{T P+T N}{T P+F P+F N+T N}$$

-  이와 같은 방식으로는 일부 클러스터링 알고리즘을 평가할 때 좋지 않을 수 있다.

**reference**

---

- https://ratsgo.github.io/machine%20learning/2017/04/16/clustering/
- 평가지표 등 
  - https://ko.wikipedia.org/wiki/K-%ED%8F%89%EA%B7%A0_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98#cite_note-hartigan1979-6

