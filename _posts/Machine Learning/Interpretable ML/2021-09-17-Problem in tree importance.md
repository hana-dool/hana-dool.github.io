---
title:  "Problem in Tree Feature Importance"
excerpt: "Tree 의 Feature Importance 문제점"
categories:
  - Interpretable_ML
date : 2021-09-17 17:00:00 +0900
last_modified_at: 2021-09-17

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

  트리 모델에서 우리는 다양한 기준들을 적용하여 Feature 들의 Importance 들을 알아보았습니다. 이러한 Importance 들은 무조건 맞을까요? 이러한 Tree importance 에 대한 각종 논란들을 살펴보고 어떻게 사용해야되는지에 대해서 알아봅시다.
{: .notice--warning}

# [Random Number is Important?](#link){: .btn .btn--primary}{: .align-center} 

- Impurity 기반으로 적용된 Feature Importance는 다소 편향되어있다고 합니다.
- 특히 랜덤 포레스트 모델일 경우 연속형 변수이거나 또는 카테고리의 갯수가 많은 변수 즉 High Cardinality 를 가지는 변수의 중요도를 과대평가 하게 됩니다.
  - 이러한 이유는 , Cardinaity 가 크다면, 노드를 좀 더 세밀하게 구분하여 분기할 수 있기 떄문인것으로 생각됩니다.
- 이러한 이유로 , 무조건 Default 의 Feature IMportance 를 믿는게 아니라 다른 방법 또한 같이 사용해 해석하는것을 선호한다고 합니다.
- 또한, 이러한 불순도를 기반으로 한 변수 중요도는 데이터를 학습하는 과정에서 얻은 결과입니다. 다시 말해서, train 데이터셋으로부터 얻은 통계량으로 계산된 것입니다. 
- test 데이터셋에서는 이 변수 중요도가 어떻게 변하는 지 알 수 없습니다. 실제로 test 데이터셋에서는 안 중요한 변수가 학습 과정에서는 가장 중요한 변수로 계산될 수 있는 것입니다.

> ## 난수가 중요도 1등? 

- <https://scikit-learn.org/stable/auto_examples/inspection/plot_permutation_importance.html>
- 위의 sklearn 에서 소개하고 있는 글이다. 타이타닉 데이터에 대해서 엉터리 High Cardinailty 변수를 생성하고, 이를 적합해 보았습니다. 

![jpg](/assets/images/ML/10_1.png)

- 그러자 위처럼 Random_num 가 제일 높은 Feature importance 를 나타나게 되었습니다.

> ## 왜그랬을까?

![jpg](/assets/images/ML/10_2.png)

- 그 이유는 위에서 어느정도 찾을 수 있습니다. 위의 그림을 보시면 이 Tree 는 과적합된 데이터에 대한 Importance 입니다.
- 현재 Importance 는 '분기를 하였을떄에 얼마나 Calss 들을 잘 분류하였는지' 로 구분되고 있습니다. 
- 즉 이는 '과적합된 Train' 에 대해서 계산된 Gain 에 근거한 Importance 라는 것입니다... 
  - 과적합 되기 시작하면, 아무리 Random 으로 적용된 변수라 하더라도 높은 Gain 을 얻을 수 있을것입니다. 
- 그러므로, 과적합된 경우에는 MDI 기반의 Importance 는 신뢰할 수 없을것입니다! 

> ## Experiment

- 과연 위와 같은일은 과적합 떄문에 일어난 일일까요?
- 이러한 원인을 알아보기 위해 , soohee410 님은 아래와 같은 실험을 기획해 보았습니다.

- UCI Machine Learning의 [Adult Census Income](https://www.kaggle.com/uciml/adult-census-income) 데이터를 이용했습니다.
  - **Target** : income(평균 연봉이 $50,000 초과면 ‘>50K’, 이하이면 ‘<=50K’)
  - **범주형 변수** : Sex(2개 범주), Marital.status(3), Relationship(6), Native.country, Race(5), Workclass(8), Occupation(14), Education.num(7)
  - **연속형 변수** : Hours.per.week, Capital.gain, Capital.loss, age

> 과적합 시킨 경우의 Importance 

- 이 경우 가장 중요한 변수는 **age(나이)** 입니다. 나이는 당연히 **high-cardinality 연속형** 변수이고, 독보적으로 변수 중요도가 높은 것을 확인할 수 있습니다. 
- 두번째로 중요한 변수 **education.num** 은 학력을 의미하는 변수로, 범주형이지만 범주 개수가 7개로 범주형 변수 치고 적지 않은 cardinality를 가졌습니다.

![jpg](/assets/images/ML/10_3.png)

> Max_depth = 15

- , 독보적으로 중요도가 높았던 **age** 가 4등으로 밀려났습니다. 
- age 변수의 중요도가 급감한 것을 확인할 수 있습니다. 한편, **capital.gain**, 즉 자본 이득을 의미하는 또 다른 연속형 변수가 1등이 되었습니다.

![jpg](/assets/images/ML/10_4.png)

> Max_depth = 10 

- max_depth를 10으로 더 낮춘 결과, 여전히 1등은 **capital.gain**이지만, 결혼 상태를 의미하는 **marital.status** 범주가 2등이 되었습니다. 
- 이 변수는 (1)결혼 하고 같이 현재 살고 있음, (2)결혼은 했지만 같이 살고 있지 않음, (3)결혼을 안했음 으로 범주가 3개입니다. 
- max_depth를 더 낮게 낮추니, **low-cardinality 범주형** 변수가 점차 높은 중요도를 차지하게 된 것을 확인할 수 있습니다.

![jpg](/assets/images/ML/10_5.png)

> Max_depth = 6

- 마지막으로 max_depth를 6으로 낮춘 결과입니다. 이 때에는 **marital.status** 변수의 변수 중요도가 가장 높게 나타났습니다. 
- 가족 관계를 의미하는 **relationship** 범주형 변수도 처음에 비해 많이 올라온 것을 확인할 수 있습니다.

![jpg](/assets/images/ML/10_6.png)

> ## Conclusion

- 과적합을 멈추지 않는 경우에는 높은 Cardinality 를 가진경우의 중요도가 커지게 됩니다. 
- 과적합을 시키지 않으면 그래도 Cardinality 에 휘둘리지는 않으나 역시 모델에 따라서 중요도가 다소 변하는것을 볼 수 있습니다.
- Model 중심의 해석이라, 사실 Model - Agnostic 방법에 비해 좀 더 Robust 하고 일관된 해석을 보여줄것 같지만 사실 다양한 Parameter 를 조절할때마다 그 중요도가 조금씩 변하는 점이 실망스러울지도 모르겠습니다.
- 그래도 이미 fitting 작업과 동시에 Importance 계산이 가능하기때문에 매우 계산이 빠른점을 이용한다면 Baseline 으로 참고하기는 좋을것 같습니다. 

 과적합이 되었을떄에는 , MDI 기반 Importance 는 High Cardinailty 에 휘둘리기때문에 좋은 방법이 아닙니다. 과적합을 하지 않은 경우에도 파라미터가 변할때마다 살짝씩 순위가 변하기때문에 절대적으로 좋은 기준은 아닙니다. Test set 에 대하여 가장 좋은 성능을 보이는 model 기준으로 MDI 기반 Importance 를 어느정도 '참고' 할 수 있을것으로 예상됩니다.
{: .notice}

# [Permutation importance in Tree model](#link){: .btn .btn--primary}{: .align-center}

![jpg](/assets/images/ML/10_7.png)

- 위에서 MDI 기반 Importance 가 아니라 이번에는 Permutation Importance 기반의 방법론을 살펴봅시다. 
- 이전 Experiment 와 똑같은 설정을 한 뒤에 여러 모델을 적합시켜 본 뒤에 feature 들의 importance 들을 살펴보았습니다. 
-  이번에는 Permutation Importance 를 이용해 보았습니다. 

> ## Experiment 

> xgboost

![jpg](/assets/images/ML/10_8.png)

> Catboost

![jpg](/assets/images/ML/10_9.png)

> Random Forst

![jpg](/assets/images/ML/10_10.png)

> ## Colclusion

- 위의 결과를 보자면, 상위 Feature 들에 대해서 변수 중요도가 과적합 / 모델 과는 상관없이 어느정도 일관된 순서를 보여주고 있습니다.
  - 또한, 각 변수에 대해서 긍정 / 부정의 효과 또한 알려준다는것(Weight) 도 매우 희망적인 결과입니다.
- 이는 permutation 기반 importance 의 경우 model 기반이 아니라 오로지 Test set 에 대하여 평가가 이루어지기 떄문으로 보입니다.
- 즉 어느정도 모델이 비슷한 좋은 성능으로 적합되었다면, 그 작동성능이 비슷한 트리 모델끼리는 Importance 가 일치하게 나타난다고 볼 수있겠습니다.

Reference

- <https://soohee410.github.io/iml_tree_importance>
- [https://towardsdatascience.com](https://towardsdatascience.com/the-mathematics-of-decision-trees-random-forest-and-feature-importance-in-scikit-learn-and-spark-f2861df67e3)
- [https://velog.io](https://velog.io/@vvakki_/%EB%9E%9C%EB%8D%A4-%ED%8F%AC%EB%A0%88%EC%8A%A4%ED%8A%B8%EC%97%90%EC%84%9C%EC%9D%98-%EB%B3%80%EC%88%98-%EC%A4%91%EC%9A%94%EB%8F%84Variable-Importance-3%EA%B0%80%EC%A7%80)
- [https://explained.ai/rf-importance/](https://explained.ai/rf-importance/)
- [https://towardsdatascience.com/explaining-feature-importance](https://towardsdatascience.com/explaining-feature-importance-by-example-of-a-random-forest-d9166011959e)

 위와 같이 기본적으로 Tree Model 에서 어떻게 Feature Importance 를 계산하고 그것을 해석할 수 있는지를 알아보았습니다. 트리 모델은 흔치 않게 머신러닝 모델이면서도 해석력이 어느정도 내장되어있는 방법론이기도 합니다. 하지만 여전히 importance 를 안다고 해서 이 변수가 양의 영향력을 가지는지 , 아닌지는 알 수 없으므로 부가적인 해석이 필요할 수도 있을것입니다.
{: .notice--success}

