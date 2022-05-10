---
title:  "CounterFactual Explanations"
excerpt: "예측치에 도달하는 Sample 들을 자세히 살펴보는 방법"
categories:
  - Interpretable_ML
last_modified_at: 2021-09-20

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

  반 사실적인 방법론이란 사실, 우리가 원하는 예측치에 도달하는 Sample 들을 자세히 살펴보는 방법론입니다. 이를 어떻게 구현할 수 있고 장단점이 무엇인지 살펴봅시다.
{: .notice--warning}

# [CounterFactual Explanations](#link){: .btn .btn--primary}{: .align-center}

> ## What is Counter Factual Explanation

- 반사실적 설명은 인과관계를 x 가 발생하지 않았다면 y 가 발생하지 않았을것. 으로 설명하게 됩니다. 
- 이러한 반 사실적 설명은, 모순되는 가상의 현실을 상상하게 됩니다.
  - EX : 내가 과일을 자주 먹었다면 코로나에 걸리지 않았을거에요! 
- 이를 Explainable Machine learning 에 적용하면 어떻게 될까요? 
  - '원인' 이 모형에 입력되고, 이에대한 '해석' 이 발생합니다. 

![jpg](/assets/images/ML/13_1.png)

- 입력과 예측(perdiction) 사이에 인과관계가 아닐지라도, 우리는 Prediction 의 원인으로 입력을 볼 수 있습니다.

> ## Idea

- 위의 그래프를 참고하면 모델의 예측을 어떻게 해석할 수 있을지에 대한 아이디어를 얻을 수 있습니다.
- 특정한 인스턴스의 피쳐값을 변경하여 어떻게 예측이 변하는지를 분석할 수 있습니다.

EX) 피터는 대출을 신청하고 은행소프트웨어에 의해 거절됩니다. 당연히 피터는 내가 왜 거절되어야 하는지에 대해서 궁금해할 것입니다. 피터가 거절에서 승인으로 바뀌기 위해서 minimum 한 변화는 어떤것일까요? 피터가 연간 10000유로를 더 벌게 된다면대출을 받을거입니다. / 또는 신용카드를 3개 덜가지고 있다면 대출을 받을것입니다. 
{: .notice}

EX) 애나는 아파트를 임대하고싶지만 얼마가 필요할 지 모르기떄문에 임대료를 예측하는 ML 모델을 Training 시켰습니다. 그녀가 Training 에 넣은 특성값은 집의 크기, 애완동물 허가여부, 전자렌지 유무 등입니다. 모델의 예측 결과가 나왔는데 , 겨우 월당 10만원의 가치밖에 없었습니다. 그녀는 지금 바꿀 수 없는 변수 (집의 크기, 위치 등) 를 고정한 채로 내가 조절할 수 있는 변수 (전자렌지 유무 , 애완동물의 허가) 를 변화시키며 20만원 이상의 임대료를 가지는 조합을 찾아내었습니다.
{: .notice}

> ## Generating Counterfactual Explanations

- 이러한 반사실적 설명방법에 대한 가장 단순한 방법은 계~속 변경하는 것입니다
  - 즉 인스턴트의 Feature 를 계속 변경하는것에 있습니다
  - 위에서 애나가 20만원 이상의 임대료를 가지는 조합을 찾아냈던것처럼요
- 하지만 이러한 방법보다 더 나은 방법이 있습니다. 바로 손실함수를 정의하는 것입니다. 
  - 손실함수는 반사실적 예측 결과가 사전에 정의된 결과와 얼마나 멀리 떨어져있는지 등을 측정하게 됩니다. 
- 이러한 손실함수의 예는 Wachter et al. (2017) 가 제안한 접근법 을 설명해 보겠습니다.

$$L(x,x^\prime,y^\prime,\lambda)=\lambda\cdot(\hat{f}(x^\prime)-y^\prime)^5+d(x,x^\prime)$$

$y'$ : desired outcome (유저가 미리 설정해야함)<br>
$x'$ : counterfactual x<br>
$\lambda$ : 이 값이 높을수록 desired outcome 과 가까운 예측을 뱉는 counterfactual x 를 선호
{: .notice}

- 위 방법의 제안자는 , $\lambda$ 의 값을 선택하는것 대신에, counterfactual 인스턴스의 예측이 y' 에서 얼마나 멀리 허용되는지를 $\epsilon$ 로 제한할것을 제안하였습니다.

$$\mid \hat{f}(x^\prime)-y^\prime\mid\leq\epsilon$$

- 이를 최적화 하기 위해서 다양한 최적화 방법(Nelder-Mead, Adam) 을 사용할 수 있습니다. 
  - 먼저 설명해야하는 인스턴스 x , 원하는 값 y' , $\epsilon$ 을 설정해야합니다.
  - 최적의 $x'$ 가 발견될때까지$\lambda$ 을 증가시켜야 합니다. ($\epsilon$ 보다 적은 값을 가지는 범위 내에서) 

$$\arg\min_{x^\prime}\max_{\lambda}L(x,x^\prime,y^\prime,\lambda)$$

- instance 와 counterfactual x' 와의 거리를 측정하는 함수d 는 아래와 같이 맨허튼 거리를 이용해 측정됩니다.

$$d(x,x^\prime)=\sum_{j=1}^p\frac{|x_j-x^\prime_j|}{MAD_j}$$

- 이때에 역중위수 절대편차(MAD) 는 아래와 같이 정의됩니다.

$$MAD_j=\text{median}_{i\in{}\{1,\ldots,n\}}(|x_{i,j}-\text{median}_{l\in{}\{1,\ldots,n\}}(x_{l,j})|)$$

> ## How to?

1. 설명할 인스턴스 x, 원하는 결과 y, $\epsilon$ , $\lambda$에 대한 (낮은) 초기 값을 선택합니다.
2. 랜덤 인스턴스를 초기 반사실적으로 샘플링합니다.
3. 초기 샘플링된 반사실성을 시작점으로 하여 손실을 최적화합니다.
4. while $\mid \hat{f}(x^\prime)-y^\prime\mid\ge\epsilon$ :
   1. $\lambda$을(를) 늘립니다.
   2. 현재 반사실적 방법으로 시작점으로 손실을 최적화합니다.
   3. 손실을 최소화하는 반사실성을 반환합니다.
5. 2-4단계를 반복하고 loss 를 최소화하는 counterfact 를 반환합니다.

> ## 단점

- 하지만 위의 방법은 몇가지 단점이 있습니다. 
- 거리 d 는 10개의 Feature  를 1씩 상승시키는것이나, 1개의 feature 를 10 상승시키는것이나 같은 값을 가집니다.
  - 즉, Feature 의 수에 대한 penalty 가 없으므로, 단순성을 추구하지 않습니다. 
- 또한 비현실적인 Feature (아파트의 크기가 3000m^2) 과 같은 경우가 생성될 수 있습니다.
- 그리고 Categorical Feature 에 대해서는 계산할수가 없습니다. 
  - 저자는 다양한 Categorical Feature 의 조합별로 수행하라 하지만 이러한 조합은 수백 수천만가지가 될 수 있습니다.

> ## 대안

- Method by Dandl et al 이 제안한 방법이 있습니다.
- https://christophm.github.io/interpretable-ml-book/counterfactual.html 참조

# [Applications and Properties](#link){: .btn .btn--primary}{: .align-center}

> ## Example

- 먼저 Credit risk 를 예측하기 위해서 모델을 Fitting 했다고 합시다.
- 우리의 목표는 아래와 같은 특성을 지니는 고객을 Counterfactual Explanation 을 통해 해석하는것입니다.

| age  | sex  | job       | housing | savings | checking | amount | duration | purpose |
| ---- | ---- | --------- | ------- | ------- | -------- | ------ | -------- | ------- |
| 58   | f    | unskilled | free    | little  | little   | 6143   | 48       | car     |

- SVM 은 위 여성에 대해서 Good risk 를 가지는 확률을 24.2% 로 예측하였습니다.
- Counterfacutals 는 이 여성이 , Good risk 를 가질 확률을 50% 이상으로 상승시키시 위해서 어떤 변수가 변해야 할지 설명하려 합니다. 

| age  | sex  | job     | amount | duration | $o_1$ | $o_2$ | $o_3$ | $\hat{f(x')}$ |
| ---- | ---- | ------- | ------ | -------- | ----- | ----- | ----- | ------------- |
|      |      | skilled |        | -20      | 0.108 | 2     | 0.036 | 0.501         |
|      |      | skilled |        | -24      | 0.114 | 2     | 0.029 | 0.525         |
|      |      | skilled |        | -22      | 0.111 | 2     | 0.033 | 0.513         |
| -6   |      | skilled |        | -24      | 0.126 | 3     | 0.018 | 0.505         |
| -3   |      | skilled |        | -24      | 0.120 | 3     | 0.024 | 0.515         |
| -1   |      | skilled |        | -24      | 0.116 | 3     | 0.027 | 0.522         |
| -3   | m    |         |        | -24      | 0.195 | 3     | 0.012 | 0.501         |
| -6   | m    |         |        | -25      | 0.202 | 3     | 0.011 | 0.501         |
| -30  | m    | skilled |        | -24      | 0.285 | 4     | 0.005 | 0.590         |
| -4   | m    |         | -1254  | -24      | 0.204 | 4     | 0.002 | 0.506         |

- 위의 Table 은 10개의 Best Counterfactuals 를 보여줍니다.
  - 오로지 값을 변형시킨 경우만 나타낸 표입니다.
  - $o_1 \sim o_3$ 은 Method by Dandl et al 이 제안한 방법에 나오는 값입니다.
  - 마지막 Columns 는 예측된 확률을 나타냅니다. (대부분 목표인 0.5와 비슷함을 기억합시다.
- 위와 같은 Counterfactuals 들은 모두, 여성이 Good credit 이 50% 이상을 가지게 하기 위한 Solution 들의 집합들입니다.
  - 모든 Counterfactual 들은 duration 이 최소 20개월 줄어들기를 추천하고 있습니다. 
  - 또한 많은 부분에서 job 은 skilled 되기를 권유합니다.
- 이러한 Counterfactual 들의 추천들을 연구하면서 내가 어떤점이 부족하고 , 어떤 개선을 해야 좋은 신용등급 (Good Credit Probability) 를 가질 수 있는지에 대해서 설명해 주고 있습니다.

> ## Advantages

> 반사실적 설명의 해석은 매우 명확합니다

- 반사실성에 따라 인스턴스(instance)의 피쳐 값이 변경되면 예측이 미리 정의된 예측으로 변경됩니다. 
  - 이는 어떠한 가정도 들어가지 않습니다. (마치 Lime 처럼 국소적인 영역에서는 선형을 따른다 처럼요)

- 반사실적 방법은 새 인스턴스를 마구 만듭니다. 
  - 이를 통해 결과를 보고할 수 있는 두 가지 옵션이 제공됩니다. 반사실적 인스턴스를 보고하거나, 관심 인스턴스와 반사실적 인스턴스 간의 차이를 보고할 수 있습니다.

> 반사실적 방법은 데이터 또는 모델에 대한 액세스가 필요하지 않습니다.

- 데이터가 매우 민감(개인정보 등) 한 경우, 이러한 방법은 매우 보안이 훌륭합니다.

> 메서드는 기계 학습을 사용하지 않는 시스템에서도 작동합니다.

- 입력과 출력이 있는 모든 모델에 적용이 가능합니다. 
- 단순히 Sample 을 만들어내는 방법론이기 떄문입니다.

> 쉽게 구현이 가능합니다.

- 왜냐하면 단순히 정의된 Loss 에 따라서 Sample 을 만들기만 하면 되기 때문입니다.
- 피쳐 값을 유의한 범위로 제한(예: 양수 아파트 크기만)하는 등 일부 추가 세부 정보를 고려할 수도 있습니다.

> ## Disadvantages

> 각 인스턴스에 대해 일반적으로 여러 개의 반사실적 설명(Rashomon effect) 이 존재합니다.

- 이것은 불편합니다. 대부분의 사람들은 현실 세계의 복잡성보다 간단한 설명을 선호합니다. 
- 한가지의 instance 에 대해서 반사실적 Instance 가 30개 생성되었다고 합시다.
  - 몇개만 보고해야할까요 10개? 
  - 다 좋은 값을 지니지만 매우 상이한 데이터를 가지는 경우에는 어떡할까요?

> 정해진 $\epsilon$에 대해 반사실적 인스턴스가 발견된다는 보장은 없습니다.

- $\epsilon$ 에 대해서, 반사실적인 인스턴트를 찾을지 말지는 사전에 찾을 수 없습니다.

> 제안된 방법는 다양한 수준의 범주형 피쳐를 잘 처리하지 않습니다. 

- 이는 사실 처음 제안된 방법론에 한하는 단점입니다.
-  범주형 기능만을 위한 해결책은 Martens et al. (2014)[2]에 의해 제안되었습니다. 
- 범주형 변수에 대한 동요를 생성하기 위한 원칙적인 방법으로 수치 및 범주형 변수를 모두 처리하는 솔루션은 Python 패키지 [Alibi](https://docs.seldon.io/projects/alibi/en/stable/methods/CFProto.html))에서 구현됩니다.

---

**Reference**

- <https://christophm.github.io/interpretable-ml-book/counterfactual.html>
- <https://tootouch.github.io/IML/counterfactual_explanations/>

 반사실적인 Feature 들을 생성하여, 우리가 원하는 목표치를 넘는 Sample 들을 생성하는 방법입니다. 여기서 더 나아가 importance 가 어떻고, 어떤 feature 가 중요도가 얼마고... 같이 자질구레하게 설명하는게 아니라 그저 , Sample 만 제시함으로서 사용자에게 그 해석을 전가한다는 생각도 들지만, 어쩃든 유용한 방법론임은 확실한듯 합니다.. 근데 그냥 Sample 만 만들어주고 이를 해석하는건 사람한테 맞긴다는점에서 좀 무책임한듯?
{: .notice--success}

