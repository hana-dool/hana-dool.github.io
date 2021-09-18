---
title:  "Tree model Feature Importance"
excerpt: "불순도 기준으로 계산되는 Tree의 Feature Importance"
categories:
  - Interpretable_ML
date : 2021-09-17 01:00:00 +0900
last_modified_at: 2021-09-17

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

  Tree 모델의 경우 우리는 Feature importance 를 계산할 수 있습니다. 이러한 변수 중요도는 어떻게 계산되고, 어느정도 믿을 수 있는 값일까요? 이에 대해서 짧게 살펴보고 어떻게 이용할 수 있을지에 대해서 살펴봅시다.
{: .notice--warning}

# [Feature Importance in Tree](#link){: .btn .btn--primary} 

- Scikit-learn에서는 **지니 중요도(Gini Importance)**를 이용해서 각 feature의 중요도를 측정합니다. 

> ## Gini Impurity

- Class가 총 $K$개 있고, 각 샘플이 해당 class에 속할 확률을 각각 $p_i, i=1,\cdots, K$라고 할 때, 특정 노드 $N_j$에서 지니 불순도 아래와 같이 계산됩니다.

$$G(N_j)=\sum^{K}_{i=1} p_i(1-p_i) = 1-\sum^{K}_{i=1} p_i^2$$

- 노드 $N_j$ 에 가 마구잡이로 섞여있을떄에, 즉 모든 Class 가 골고루 분포되어 있을때 지니 불순도는 큰 값 (1에 가까운 값) 을 가지게 됩니다. 
- 위와 같은 Gini impurity 를 줄이는 방향으로 (Classification 의 경우) 분기가 진행되게 됩니다. 

- 총 샘플이 400개이고, Class가 두 종류, 즉 이항 분류하는 경우입니다. 이 때, 아래 세가지 노드 $C_1, C_{1_ left}, C_{1_ right}$의 지니 불순도 $G$를 계산하면 다음과 같습니다.

![jpg](/assets/images/ML/8_4.png)

$$\begin{aligned} G(C_1)&=1-\lbrace(\frac{200}{400})^2+(\frac{200}{400})^2\rbrace=0.5 \cr G(C_{1_left})&=1-\lbrace(\frac{150}{200})^2+(\frac{50}{200})^2\rbrace=0.25 \cr G(C_{1_right})&=1-\lbrace(\frac{50}{200})^2+(\frac{50}{200})^2\rbrace=0.25 \end{aligned}$$

> ## Node Importance

- 각 노드의 중요도를 계산해 봅시다.

- $I(C_j)$는 노드 $C_j$의 중요도(Importance)를 의미합니다.
- $w_j$는 전체 샘플 수에 대한 노드 $C_j$에 해당하는 샘플 수의 비율, 즉 **가중치**를 의미합니다.

$$I(C_j)=w_j\cdot G(C_j) – w_{j_left}\cdot G(C_{j_ left}) – w_{j_right}\cdot G(C_{j_right})$$

- 즉, 부모 노드의 가중치 불순도에서 자식 노드들의 가중치 불순도 합을 뺀 것이 됩니다. $I(C_j)$를 계산해보면 다음과 같습니다.

$$\begin{aligned} I(C_j)&=1\cdot G(C_j) – \frac{200}{400}\cdot G(C_{j_ left}) - \frac{200}{400}\cdot G(C_{j_ right})\cr &=0.5-0.5\cdot 0.25 – 0.5\cdot 0.25 \cr &= 0.25 \end{aligned}$$

- 노드 중요도는 그 노드에서의 Impormation gain 을 뜻합니다
- 노드가 중요하다는것은, 그 노드의 분기에서 , 'CLass 들이 잘 분류된다.' 라는 의미이므로 매우 합리적으로 보입니다.

> ## Feature Importance

- 이제 각 feature의 중요도를 계산해보겠습니다. $i$번째 feature, $f_i$의 중요도 $I(f_i)$는 다음과 같이 계산됩니다.

$$I(f_i)=\frac{\sum_{ j: f_i에\space 의해\space split된\space 모든 노드\space C_j} I(C_j)}{\sum_{ k\in all\space node\space C_k}{I(C_k)}}$$

- 전체 노드의 중요도를 합한 것 대비 $i$번째 feature에 의해 분기된 노드들의 중요도를 합한 것이 바로 $i$번째 feature의 중요도 $I(f_i)$가 됩니다. 
- 이 값이 클수록, 해당 feature가 트리를 생성하고 샘플을 분류하는데 큰 역할을 했다고 볼 수 있을 것입니다. 이 $I(f_i)$를 다시 정규화 하여 (즉 합이 1을 가지게 하는것입니다.) 비교하기 쉽게 만든다고 합니다.

$$I(f_i)^{norm}=\frac{I(f_i)}{\sum_{ i \in \space all\space feature\space f_i} I(f_i)} $$

- 이제까지가 Decision Tree의 변수 중요도였습니다. 

> ## Random Forest

- 랜덤 포레스트에서 변수 중요도는 어떻게 될까요? 
- 랜덤 포레스트는 의사결정나무들을 병렬적으로 합한 것이므로, 랜덤 포레스트에서 $I(f_i)$는 결국 각 트리에서의 $I(f_i)$를 모두 평균 낸 것에 해당합니다.

> ## Another Criteria

- 사실 위와 같은 지니 Impurity 말고 다른 기준도 있습니다.

![jpg](/assets/images/ML/8_1.png)

- 위와 같이 다양한 기준을 Gini Impurity 대신 쓸 수 있습니다.

# [Feature Importance Methods](#link){: .btn .btn--primary} 

- 위와 같이 Tree 는 Importance 를 기본적으로 제공하기때문에 좋습니다만. 다른 방법으로도 이러한 Importance 를 계산할 수 있습니다.

> ## MDI(Mean Decrease in Impurity) importance 

- MDI Importance는 가장 대표적인 변수 중요도로서, scikit-learn의 default로 내장되어 있는 방법론입니다.
- 각 변수가 split될 때 impurity 감소분의 평균을 중요도로 정의합니다.
- 이는 사실 위에서 알아보았던 방법론입니다. 

> 장점 

- 계산이 빠름 , 직관적 

> 단점

- 연속형 변수 , 또는 High Cardinality 변수에 대해서는 편향된 결과(나중에 더 알아보겠습니다.)

> ## Permuation Importance

- Permutation Importance는 "해당 변수가 랜덤으로 분포된다면, 어느 정도 성능이 떨어지는가?"라는 가정을 갖고 있습니다. 
- Permutation Importance는 랜덤포레스트의 각 나무에서 OOB(Out of Bag) sample에서 다음과 같이 구현됩니다.

Note : N개의 데이터에서 Boostrap Sampling으로 N개의 데이터를 선택하고, 선택되지 못한 데이터를 OOB Sample이라고 합니다. OOB Sample은 학습에 사용되지 않았기 때문에, validation 용도로 사용할 수 있다는 장점이 있습니다. 복원추출을 한번 시행할떄에 데이터 N개 중 관측치 A가 뽑히지 않을 확률은 N-1/N 입니다. 이 과정을 충분히 큰 N번 반복하면 $lim_{N-> inf}{} (N-1/ N)^N = 0.368$ 즉 약 37% 의 데이터는 늘 OOB 로 남는것입니다.
{: .notice}

![jpg](/assets/images/ML/8_2.png)

1. (①~③) b번째 tree를 생성할 때, bootstrap sample로 나무를 학습
2. (④) **OOB Samples** : 학습할 때 사용되지 않은 데이터 셋으로 Validation 데이터를 생성
3. (⑤) **Reference Measure** : OOB Sample로 나무의 예측력(accuracy, R-square, MSE 등)을 계산 및 저장
4. (⑥) **Permutation Measure** : OOB Sample에서 j번째 변수의 데이터를 무작위로 섞은 뒤, 학습된 나무의 예측력을 계산 및 저장
5. ⑤, ⑥단계에서 저장된 예측력 척도의 차이(Reference Measure - j번째 변수의 Permutation Measure)를 계산

- 위의 과정을 나무의 개수 B만큼 시행하여, 각 변수에서 계산된 중요도의 평균으로 Permutation Importance로 정의합니다.
- 위의 과정 중 **특정 변수를 무작위로 섞었을 때 기존 Reference 척도보다 낮아지게되면, 해당 변수는 중요하다고 판단되며 척도가 유사하거나 오히려 좋아지면 불필요하다고 판단**내릴 수 있습니다.

> 장점

- 모델을 다시 학습하지 않아도 되기 때문에, 계산이 빠름.
- 어떠한 모델에도 적용이 가능 

> 단점

- more computationally expensive than the default `feature_importances`

- Permutation importance overestimates the importance of correlated predictors — Strobl et al (2008)

> ##  Drop Columns Importance

- Drop Column Importance 방법은 모든 변수를 사용했을 때의 Reference척도에서 특정 변수를 빼고 랜덤포레스트를 다시 학습했을 때의 척도의 차이로 변수 중요도를 정의합니다.
- Permutation Importance와 동일하게, 변수를 뺏을 때의 성능이 많이 떨어진다면 해당 변수는 중요한 변수라고 할 수 있습니다.

> 장점 

- 개념이 매우 직관적임

> 단점

- 수의 개수만큼 모델 재학습이 필요하기 때문에, Computation 관점으로 매우 비효율적

---

Reference

- <https://soohee410.github.io/iml_tree_importance>
- [https://towardsdatascience.com](https://towardsdatascience.com/the-mathematics-of-decision-trees-random-forest-and-feature-importance-in-scikit-learn-and-spark-f2861df67e3)
- [https://velog.io](https://velog.io/@vvakki_/%EB%9E%9C%EB%8D%A4-%ED%8F%AC%EB%A0%88%EC%8A%A4%ED%8A%B8%EC%97%90%EC%84%9C%EC%9D%98-%EB%B3%80%EC%88%98-%EC%A4%91%EC%9A%94%EB%8F%84Variable-Importance-3%EA%B0%80%EC%A7%80)
- [https://explained.ai/rf-importance/](https://explained.ai/rf-importance/)
- [https://towardsdatascience.com/explaining-feature-importance](https://towardsdatascience.com/explaining-feature-importance-by-example-of-a-random-forest-d9166011959e)

 위와 같이 기본적으로 Tree Model 에서 어떻게 Feature Importance 를 계산하고 그것을 해석할 수 있는지를 알아보았습니다. 트리 모델은 흔치 않게 머신러닝 모델이면서도 해석력이 어느정도 내장되어있는 방법론이기도 합니다. 하지만 여전히 importance 를 안다고 해서 이 변수가 양의 영향력을 가지는지 , 아닌지는 알 수 없으므로 부가적인 해석이 필요할 수도 있을것입니다.
{: .notice--success}

