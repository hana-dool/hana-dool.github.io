# 1.실험의 샘플 수가 늘 부족한 이유

## 1.1 

- Improving the Sensitivity of Online Controlled Experiments by Utilizing Pre-Experiment Data
- https://drive.google.com/drive/folders/1tukETQGaweAf-meVbcN2NjuidoTcSINR
- 해석본 : AB_Testing -> paper -> cuped

> Note 

- 이떄 Power 를 높히기 위한 제일 쉬운 방법은 표본 크기를 늘리는것입니다. 
  - 이때 온라인 실험은 이미 매우 큰 표본 크기를 가지므로, A/B Testing 에서 Power를 강조할 필요가 없어 보일 수 있습니다. 
- 하지만 정말로 Online 실험에서는 이미 샘플의 크기가 크므로 Sample 의 수를 고려하지 않아도 될까요?
- 하지만 현실에서는 많은 양의 트래픽이 있더라도, online 실험은 우리가 원하는 Statistical power 에 도달하지 못하는 경우가 있습니다. 
  - 구글에서는 매달 100억건 이상의 검색을 수행하는데에도, 그들이 가진 트래픽 양에 만족하지 않는다고 합니다.
- 이제 샘플이 필요한 이유를 하나하나 알아봅시다.

> 이유 1 : Treatment 효과는 매우 적음

- 우리가 탐지하고자 하는 Treatment 효과는 매우 작은 경향이 있습니다. (항상 모든 기능이 혁신적이라 큰 Treatment 의 증가를 나타내는게 아니기 때문이죠.. )
- Contolled Experiment 의 Sensitivity (이 문단에서는 delta 의 수준을 의미하는듯 함.) 는 사용자 수 제곱에 반비례하므로, 작은 사이트에서 5% 의 delta 를 감지하려면 10000명의 사용자가 필요할 수 있습니다. 
  - 즉 0.5% 의 delta 를 감지하려면 1/10 으로 감소된 delta 를 감지해야 하므로 100만명의 사용자가 필요하게 됩니다. 
- 이때 0.5% 가 별거 아니라고 생각할 수 있는데, 큰 서비스에서는 사용자당 0.5% 의 수익 변화만으로도 대형 온라인 사이트의 경우 수백만 달러에 해당한다는것을 기억하세요! 

> 이유 2 :  결과를 빨리 얻는것이 중요

- 결과를 빨리 얻는것이 중요하기 떄문입니다. 왜 결과를 빨리 얻는것이 중요할까요? 
  - 좋은 기능을 조기에 출시하고 싶을 수 있기 떄문
  - Treatment 가 사용자에게 안좋은 영향을 미칠때 빨리 중단해야 하기 때문
- 그러므로 Sensitivity 가 큰 실험을 해야 조기중단에 대해서 더 큰 신뢰성을 얻을 수 있습니다.

> 이유 3 : 영향을 받는 유저가 적을수 있음

- 낮은 Triggering rate 를 가진 실험이 있을때, 이러한 실험은 매우 적은 유저만이 실제로 Treatment 효과를 경험하게 됩니다.
  - 예를 들어서 레시피 관련 쿼리에만 영향을 미치는 실험에서 대부분의 사람들은 레시피를 검색하지 않기 때문에 Variant 를 경험하지 않습니다.
- 즉 이러한 경우 유효한 표본 크기는 작을 수 있으며, 통계 분석의 Statistical Power 는 매우 낮을 수 있습니다.

> 이유 4 : 실험이 많아질수록 샘플이 적어짐

- 실험이 많아질수록 , 각 실험은 샘플 사이즈를 서로 나눠써야하기 때문에 한 실험이 가용할 수 있는 샘플의 수가 적어지게 됩니다.
  - 이때 다양한 실험을 동시에 진행한다고 하면 Interaction Effect 를 고려해야 해서 설계가 매우 어렵습니다.
- 그러므로 데이터 중심 문화가 제대로 잡힌 기업에서는 혁신 속도에 맞추기 위하여 더 많은 실험을 항상 실험해야 하고, 이는 좋은 온라인 플랫폼의 경우 항상 샘플 사이즈 부족에 허덕일수밖에 없다는 의미입니다. 

# 2. 샘플 사이즈를 미리 계산해야하는 이유

- A Dirty Dozen: Twelve Common Metric Interpretation Pitfalls in Online Controlled Experiments 
  - 