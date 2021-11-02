---
title:  "Posterior Predictive Plot"
excerpt: "사후 분포가 실제적으로 데이터와 얼마나 잘 맞는지 점검하기"
categories:
  - Py_Arviz
last_modified_at: 2021-10-31
date : 2021-10-31 11:00:00 +0900

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 우리가 만든 모델이 과연 좋은지? 에 대한 검정
{: .notice--warning}

# [Posterior Predictive check](#link){: .btn .btn--primary}{: .align-center}

> ## Posterior Predictive check

- Posterior Predictive check 는 '적합된 모델' 에서 데이터를 시뮬레이션 한 다음 이를 관찰된 데이터와 비교하는 방법입니다. 
  - Fit the model to the data to get the posterior distribution of the parameters $p(\theta \mid D)$
  - Simulate data from the fitted model : $p(\tilde{D} | \theta, D)$
  - Compare the simulated data (or a statistic thereof) to the observed data and a statistic thereof. The comparison between data simulated from the model can be formal or visual.
- 즉 Posterior 를 이용하여 '실제 데이터' 와 '시뮬레이션 된 데이터' 간의 불일치를 찾는 방법입니다. 
- 베이즈 분석은 다양한 파라미터나, 고려중인 모형에 대한 '상대적인' 신뢰도 만을 나타내게 됩니다.
  - 즉 사후 분포는 어느 파라미터들이 데이터를 고려할떄에 상대적으로 다른 값보다 좋은지(확률이 높을지) 안좋을지 (확률이 낮은지) 에 대해서만 알려줄 뿐이라는 것이죠. 
- 사후분포는 이러한 파라미터들이 '실제로' 좋을지에 대해서의 여부는 알려주지 않는다는 것입니다.

> Example

- 예를 들어서 어떤 동전이 무게 면에서매우 편향된 요술 동전이라고 합시다. 
  - 그래서 앞면이 99% 만 나오는 동전이거나 / 뒷면이 99% 나오는 동전 두가지 경우의 수가 있습니다. 
  - 단 우리는 이 동전이 앞면으로 편향된 동전인지 뒷면으로 편향된 동전인지를 알 수없는상태입니다.
- 이 동전을 40번 던졌고, 30번 앞면이 나왔다고 합시다. 
  - 우리는 이러한 결과를 통해서 99% 앞면인 동전의 사후 확률이 99% 뒷면인 동전의 사후 확률보다 엄청 클 것이라는것을 알 수 있습니다. 
- 하지만 앞면이 99% 확률인 모형은 데이터 (40번중 30번 앞면) 를 고려할떄면 , 매우 나쁜 동전 모형이라고도 할 수 있을것입니다. 
- 즉 '데이터를 고려할때에' 업데이트 된 posterior 는 '실제 측면에서는' 다를 수 있다고 볼 수 있다는 것입니다.

> Conclusion

- 즉 정리하자면 사후 분포는 사용 가능한 최상의 매개변수 값이 실제로 데이터에 잘 맞는지 여부를 나타내지 않고 사용 가능한 매개변수 값 중 어느 것이 다른 것보다 덜 나쁜지를 나타냅니다. 이러한 점에서 사후 예측 검사(Posterior Predictive Check)는 Posterior 의 예측이 실제 데이터와 체계적으로 일치하지 않는지 여부를 평가하는 데 중요합니다.
- 즉 'Posterior' 가 실제를 잘 나타내는가? 를 검정하는 방법이라 할 수 있겠습니다.

> ## Plot_ppc

```python
import arviz as az
data = az.load_arviz_data('radon')
az.plot_ppc(data, data_pairs={"y":"y"})
```

![png](/assets/images/Python/48_4.png)

- 위와 같이 파란색은 각각의 Poseterior 에 대해서 Posterior Predictive 를 형성합니다.
- 위의 그림을 본다면 'Posterior Predictive' 를 다수 그려보고 (Analytic 하게는 안되겠죠.... 너무 어려운 Form 이니까요), 그러한 Posterior Predictive 에 대해서 평균을 형성해본것이 주황색 점선입니다.
- 위 모형을 볼때 어느정도 합리적인 예측이라고 생각되어 지네요.

> ## num_pp_samples : 몇개의 Posterior 를 그릴지

```python
az.plot_ppc(data, num_pp_samples=30, random_seed=7)
```

- 위와 같이 설정한 경우 30개의 Predictive 만 계산하게 됩니다.

---

**Reference**

- <http://doingbayesiandataanalysis.blogspot.com/2012/09/posterior-predictive-check-can-and.html>
- <https://arviz-devs.github.io/arviz/api/generated/arviz.plot_ppc.html>
- <https://jrnold.github.io/bayesian_notes/model-checking.html>



