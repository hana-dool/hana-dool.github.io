---
title: "Permutation importance - a corrected feature importance measure"
excerpt: "y target 을 permutation 한 뒤 importance 의 분포에서 p-value로 중요도 계산"
categories:
  - ML_Paper
last_modified_at: 2021-09-18

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

  많은 분야에서, 모델의 해석력은 매우 중요합니다. 그래서 선형 모델이 상대적으로 성능이 안좋음에도 불구하고, 사용되는 이유중에 하나일 것입니다. 하지만 지난 몇년동안 Random Forest 와 같은 매우 복잡한, 비모수 모델에 대해서 모델에 대한 해석력을 볼 수 있는 방법론이 개발되었습니다.(MDI 기반 중요도.) 하지만 최근 RF 모델은 High Cardinality 를 가지는 변수를 선호하는 방식으로 편향되었다고 합니다. <br> 이 논문에서는 이러한 편향을 수정할 수 있는 방법론을 제시합니다. Pimp - p value Permutation 방법론이 매우 도움이 된다는것을 증명하고, 다른 방법론보다 우수함을 보일것입니다.  
{: .notice--warning}

# [Methods](#link){: .btn .btn--primary} 

> ##  Random Forest model (RF)

- RF 방법론은 단일 트리의 단점(안정적이지 못함) 을 극복하기 위해 제안된 방법입니다. d아래의 두가지 스킬을 이용하여 모델을 적합시킵니다.
  - Bagging (샘플을 여러 번 뽑아(Bootstrap) 각 모델을 학습시켜 결과물을 집계(Aggregration)하는 방법) 
  - Random Subspace (각각의 Tree 를 구성할때에, 다양성을 위하여 변수도 무작위 선택) 
- RF 의 저자는 Feature Importance 를 measure 하기 위하여 두가지 방법론을 제시하였습니다. VI 와 GI 입니다.
  - VI : 키 라는 변수에 대해서 Feature IMportance 를 재고 싶다고 합시다. 이러한 경우, 키 변수를 무작위로 Permutation 한 경우와, 그대로 둔 경우, 2가지 경우에 대해 OOB Sample 을 이용해서 모델의 정확도가 얼마나 감소하는지를 측정합니다.
  - GI : GI 는 노드 분할 후 지니(불순도) 의 감소를, Feature Importance 를 측정합니다. VI 와 GI 는 높은 상관관계를 가진다고 하고, 비슷한 편향을 공유한다고 합니다. 
- 여기 논문에서는 , ntree = 100 의 Default 값을 사용합니다. 

> ## Mutual Information (MI)

- Mutual information 은 정보 이론에 근거한 방법론입니다.
- 우선 Entrophy 에 대해서 간략히 알아봅시다. 
  - 엔트로피는 특정한 Random 변수 X 가 얼마나 Uncertainty 가 있는지를 측정합니다. 즉 uniform 분포일때에는 고르게 흩어져 있으므로, 이러한 Uncertainty 가 최대라고 볼 수 있습니다.
  - 어떠한 R.V 에 대해서 Entrophy 는 $H(X) = -\sum_x P_X(x)log P_X(x)$ 로 정의됩니다.
  - 이 Entrophy 는 특정 R.V. 이 가지는 정보량을 나타낸다고도 볼 수 있습니다. (불확실할수록 정보가 높다고 봅니다.) Uniform 분포와 비슷할떄에 최댓값을 나타내게 됩니다. 
- 그 이후에 Mutual information $MI(X,Y)$ 에 대해서 알아봅시다. 
  - $MI(X,Y) = H(X) - H(X\mid Y)$
  - 위와 같이, 'Y' 를 가정하였을때에 얼마나 Unsertainty 가 감소하는지를 측정하게 됩니다. 
- Mutual information 이 0에 가깝다는것은 , MI 변수들이 독립에 가깝다는것을 의미합니다.
  - Y 를 가정하더라도 , X 의 엔트로피가 거의 변하지 않았다는것이기 떄문입니다.
- 주로 Feature 과 output 간의 MI 측정을 통해서, Feature Selection 을 할떄에 이용됩니다. 
  - 특정 Feature 가 Y 변수와 관련성이 있다면, MI 값이 높게 나올것이기 떄문입니다.
- 추후, 논문에서 이야기되는 MI 방법론은 위와 같은 Univariate Feature Selection 방법론입니다.

> ## PIMP Algorithm

- Pimp 는 Random Forest 모델의 GI 방법론의 Bias 를 보정하기 위한 방법론입니다.
  - 또한 PIMP 방법론을 사용하여 Mutual Information Feature selection 의 편향을 수정할수도 있다고 합니다.
- 이는 일반적인 Permutation Importance 와 약간 다릅니다. 

The PIMP algorithm permutes the response vector *s* times. For each permutation of the response vector, the relevance for all predictor variables is assessed
{: .notice}

- 위와 같이 PIMP 알고리즘은 , y 변수를 s번 permute 합니다. permute 된 y 변수에 대해서, predictor variable 과의 관계를 평가하게 됩니다.

 This leads to a vector of *s* importance measures for every variable, which we call the *null importances*
{: .notice}

- 이러한 방법은, 각각의 Feature 에 대해서 s 번 importance 를 계산할 수 있습니다. 우리는 이러한 Importance 를 Null importane 라고 부르겠습니다.

The PIMP algorithm fits a probabilty distribution to the population of null importances, which the user can choose from the following: Gaussian, lognormal or gamma. Maximum likelihood estimators of the parameters of the selected distribution are computed. Given the fitted distribution, the probability of observing a relevance of *v* or higher using the true response vector, can be computed (PIMP *P*-value). If the user does not know which distribution is most suitable for his or her problem, the PIMP algorithm uses Kolmogorov–Smirnov (KS) tests in order to automatically identify the most appropriate distribution.
{: .notice}

- pimp 알고리즘은 이러한 '중요도' 에 대해서 분포를 가정하게 됩니다. 
  - 일반적으로 가우시안 , Lognnormal , gamma 분포중 하나를 선택하게 됩니다.
  - 이렇게 Fitted 된 분포 하에서 우리는, the true response vector 를 사용하였을때의 Importance 보다 극단적인 값을 가지는 p-value 를 계산할 수 있습니다.

However, if the tests show little resemblence to any of the three proposed distributions, a non-parametric estimation of the PIMP *P*-values is used, simply by determining the fraction of null importances that are more extreme than the true importance *v*
{: .notice}

- 만일 , 계산된 importance 가 3가지 분포중 어떤것도 따르지 않는다면, 비모수 방법론을 사용하여, P-value 를 계산하게 됩니다.
- 위와 같이 Response vector 를 Permutation 하는것은 다음과 같은 이점을 가집니다.

1. dependent variable 이 바뀌지 않은 상태로 유지되게 떄문에, 각 Feature 끼리의 관계를 유지한채로 중요도를 측정할 수 있습니다.
2. 일반적인 permutation importanc 를 측정하는 방법에서 dependent variable(x) 을 permutation 하는것보다 Response vector(y) 만 permutation 하는것이 훨씬 계산량이 적습니다.
3. 이러한 방법론은 매우 general 합니다. 이는 Feature importance 를 생성하는 다른 방법론과 같이 쓰여서 참고가 될 수 있습니다.

> 자세한 방법 

![jpg](/assets/images/ML/11_10.png)

- 위의 경우는 Gaussian 분포를 가정할때에 Importance 를 계산하는 방식입니다.
- 이떄에 '중요도' 를 계산하는 방법은 여러가지 (Gini , MI) 가 될 수 있음을 기억합시다! 

> ## Correlated RF models

- Cart 방법론은 Training 시에 최적의 분기를 찾기 위하여 GINI Impurity 를 사용합니다.
  - 하지만 이러한 Gini impurity 의 선택에 의한 편향이 있습니다. 
  - 결과적으로 Cart 와 RF 모델 모두 편향이 존재하며, 이러한 모델에서 도출된 MDI 방법론의 Feature importance 또한 편향이 존재합니다.
- 우리는 여기에서 RF model 을 개선시키기 위해 PIMP 알고리즘을 이용한 RF 모델을 제안합니다. 
- 이 모델은 다음과 같은 순서를 가집니다.

1. train data 에 대해 일반적인 RF 모델을 적합시킵니다. 
2. 각 변수들에 대해서 PIMP Score 를 계산합니다. 
3. Pimp 에서 , p-value 가 0.05 보다 낮은 값을 가지는 변수만을 사용하여 RF 로 새 변수를 적합합니다. 

# [Simulations](#link){: .btn .btn--primary} 

> ## Simulation A

- importance 의 biased 를 살펴보기 위하여, 1000개의 instance 로 이루어진 데이터가 생성되었습니다. 
- 각 변수들을 31개의 category variable 로 이루어진 데이터입니다. (2~32 의 label 을 가짐)
- 예측변수(X) 와 반응변수(y) 는 서로 independent 하게 uniform 한 분포에서 생성되었습니다. 
- 이 경우 y 와 각 feature 들이 독립적으로 랜덤하게 측정되었기 때문에, 어떠한 X Feature 도 유용한 변수가 되지 않습니다. 
- 우리가 원하는것은 '모든 변수가 쓰레기 변수' 이므로, 모든 변수는 동일하게 낮은 Importance 를 지녀야 할 것입니다. 
- 각 변수에 대해 GI , MI 를 계산하였고, 모든 측정의 PIMP 는 s=100 을 사용하여 Permutation 되었습니다. Simulation 은 100회 반복하였습니다. 

> ## Simulation B

- 두번쨰  Simulation 에서는 정보량이 없는 많은 데이터 속에서, 정보량이 있는 예측 변수들을 얼마나 골라내는지에 대 실험입니다. 
- 이 경우 매우 많은 Predictors(p) 와 적은 nums of samples(n) 를 사용하였습니다.
  - p = 500 , n = 100 
- 자세한 세팅은 생략하겠습니다. 중요한것은 처음 1~12 번쨰 Feature 의 경우 target(y) 의 변수와 관련이 있습니다. 그러므로 이 변수들을 잡내기를 원합니다.

> ## Simulation C 

- 세번쨰 Simulation 은 우리의 PIMP 알고리즘이 통계를 이용해 p-value 를 나타내는것이 모델의 해석을 크게 높힌다는것을 입증하기 위해 구성되었습니다. 
- RF 모델에서 문제점중에 하나는, 관련성이 높은 그룹 변수의 중요도는, 각각의 변수들이 해석력을 나누어 가지게 되므로 그 중요도가 감소하게 된다는 것입니다.
  - 이렇게 된다면, 유의한 변수일지라도 ,correlated 된 변수가 많다는 이유 하나만으로 importance 가 작게 나올 수 있습니다.
- 이러한 그룹의 크기가 큰 경우(즉 관련성이 높은 변수들이 많을수록) 에도 Pimp - p value 가 유의하다는것을 보여주려 합니다. 
  - n = 100 , p = 500 으로 데이터를 설정하였으며, 변수는 1~21 개의 카테고리를 가집니다. 
  - binary output 은 uniform distribution 에서 랜덤하게 선택되었습니다. 
  - 첫번쨰 변수는 output vector 와 15% 만 다르고 나머지는 동일합니다.
    - 이는 첫번쨰 변수는 outcome 과 매우 큰 상관성을 나타난다는것을 의미합니다.
- 그리고 $k\in \{1,5,10,25,50\}$ 에 대해서, target 에 종속되고 서로 관련되어 있는 k 개의 vaiable 이 생성되었습니다.
  - 이떄 첫번째 변수는 output vector 와 15%만 다른, 매우 유용한 변수입니다.
  - 나머지 변수들은 서로 연관되어 있으며 , 또한 그 중요도가 모두 같게 설정되어 있습니다. (k-1 개 모두 output 과 연관성이 일치하게 만들어집니다.)
    - 즉 k 가 5던, 25던 모두 output 과 연관성이 같습니다.
  - k = 5를 선택한다면 , target 과 관련이 있는 5개의 변수 A1,A2,A3,A4,A5 를 만들어냅니다. A1 은 매우 연관성이 깊고 나머지 4개는 연관성이 같습니다.
- 이상적으로, model 은 그룹의 크기(k) 와 무관하게 첫번쨰 변수에 대해서 높은 중요도를 매기고 , 나머지 k-1 개의 변수에 대해서는 같은 중요도 값을 가지기를 기대합니다.

# [Results of Simulations](#link){: .btn .btn--primary} 

> ## Simulation A

- Simulation A 는 , 모든 변수가 다 y 변수와는 상관없는 쓰레기 변수였다는것을 기억합시다. 

![jpg](/assets/images/ML/11_2.png)

- 위와 같은 결과는 RF 가 MI, GI 중 어떠한 기준을 사용하더라도 Cardinality 가 높은 변수가, 높은 Importance 를 가진다는것을 알았습니다. 
- 하지만 Gamma 분포를 사용하여 계산된 Pimp 점수(p-value) 는 오른쪽 그림과 같습니다. 
  - y 축이 -log pvalue 이므로, 빨간색 점선을 넘는 값이 유의한 변수가 됩니다.
  - 하지만 위 그림을 보면, 유의한 변수가 없다고 말하고 있습니다.
- Note : p-value 를 작게 가진다는 것이 유의한 변수입니다.
  -  y - target 을 permutation 하였을때의 importance 들의 분포를 Dist_P 라 합시다. 
  - '실제 y -target' 을 사용하였을때의 Importance를 K 라 합시다.
  - p-value 가 작다는것은 Dist_P 에 대해서 K는 큰 값을 가지는 위치에 위치한다는 것입니다.
  - 즉 , y-target 이 True 인 위치에 있을떄에 , 이 변수의 중요도를 제일 높게 평가한다는 것이고 이는 이 변수가 유의하다는것을 나타내는 것입니다.

> ## Simulation B 

![jpg](/assets/images/ML/11_3.png)

- 위의 경우는, 각 Feature의 순서를 복원하는지 아닌지에 대한 실험입니다.
- 처음 12개의 Feature 를 순서대로 (1,2,3,4...) 복원하는것이 목적입니다.
- RF 의 Gini 는 1~5까지만 복원할 수 있으나, Pimp 의 경우는 최대 1~9까지의 Importance 를 중요하다고 복원하고 있습니다.

![jpg](/assets/images/ML/11_4.png)

- MI 의 경우에도 마찬가지인것을 볼 수 있습니다.
- 즉 Pimp 의 경우가 좋은 성능을 보이는것을 볼 수 있습니다.

> ## Simulation C

![jpg](/assets/images/ML/11_5.png)

![jpg](/assets/images/ML/11_6.png)

![jpg](/assets/images/ML/11_7.png)

![jpg](/assets/images/ML/11_8.png)

- 위와 같은 결과는 변수들간의 Correlation 이 높을떄에 Pimp - p value 를 사용하는것이 매우 좋다는것을 나타냅니다. 
- Correlated Group 의 크기가 증가할수록, 각각의 Gini Importance 가 조금씩 감소하는것을 볼 수 있습니다. 
- 이러한 Importance 는 일정하게 유지되어야 하나, Gini 는 그렇지 못합니다. 
  - 극단적으로 , k=50인 경우에는 그룹의 변수들을 모두 중요하지 않다고 판단할 수도 있을것입니다. (너무 작아서)
- 하지만 PIMP pvalue 의 경우는 그렇지 않습니다. 항상 어느정도 일정함을 유지하고 있음을 볼 수 있습니다.
  - k=50 인 경우에도 유의성을 유지하고 있음을 확인하세요~

# [Model Improvements](#link){: .btn .btn--primary}

![jpg](/assets/images/ML/11_9.png)

- Model Improvement 를 살펴보았습니다. 
- RF top 1% 는 , Feature importance 기준으로 상위 1% 기준의 변수만 선택한다는 것이 됩니다. 
- PImp 는 기본적으로 5% 의 유의수준으로 설정하였습니다.
- 위의 결과표를 볼떄에 , Pimp -RF 가 좋다는것을 볼 수 있습니다.

# [Coclusion](#link){: .btn .btn--primary}

> ## High Cardinality 편향문제 해결

- SImulation A 에서는 Random Forest 의 MI ,GI 기반 Improtance 가 High cardinality 일떄에 큰 값을 가지는것을 입증하였습니다.
- 이러한 향을 개선하기 위하여 , Pimp p value 방법론이 이러한 편향을 완하하는것을 보여주었습니다.

> ## 정확한 순위 생성

- Siulation B 에서 보다시피 , PImp - p value 방법론이 좀 더 나은 순위를 보여줍니다. 
- 그러므로 중요도의 Ranking 을 매길떄에 Pimp p value 방법론이 좀 더 좋다고 할 수 있습니다.

> ## High Correlated 편향문제 해결

- 일반적인 변수 중요도의 경우 , Correlated 된 변수들이 같이 Feature 로 들어가는 경우에, 상관된 변수들이 그 중요도를 서로 나누어 가집니다.
- 이로 인해서 상관된 변수가 많을수록, 그 중요도는 모두 같이 감소할 수 있습니다.
- 이렇게 된다면 상관성이 유의할지라고, 상관된 변수가 많다는 이유만으로 변수들을 쳐내게 될 수 있습니다.
- 하지만 Pimp - p value 는 이러한 편향이 없어 (즉 Correlate 된 변수가 많아도 p-value가 감소하지 않습니다.) 좋은 기준이 될 수 있습니다. 

> ## 추천되는 방법

- 결과의 안정성을 위해 Permutation 은 50~100번을 제안합니다.
- 또한 하나하나 순열마다 각 Feature 의 계산이 독립적으로 이루어지기 떄문에 병렬 연산화가 가능합니다.

---

**Reference**

- [https://academic.oup.com/bioinformatics/article/26/10/1340/193348?login=true](https://academic.oup.com/bioinformatics/article/26/10/1340/193348?login=true)

 생각보다 생각할점이 많은 방법론이네요. 일반적으로 쓰이는 Feature importance 방법론은 independent Variable 을 마구 섞어서 적합하는 방법이라 그 속도가 매우 느리다는 단점이 있는데 이 방법론은 dependent variable 을 이용하여 그 중요도를 체크한다는게 상당히 인상깊었습니다. 더군다나, 이런 방법론을 사용하면 independent data 의 구조를 해치지 않기떄문에 , permutation importance 방법론에서 문제로 제기되는 , Highly Correlated 변수일 경우 문제가 되는 경우를 해결한것 같더라구요. Python 에 구현된게 있으면 나중에 찾아봐야할듯..!  
{: .notice--success}

