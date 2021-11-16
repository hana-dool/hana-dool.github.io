---
title:  "Hyperopt Simple Example"
excerpt: "매우 간단한 1차, 2차 함수에 대해서 최적화 해보기"
categories:
  - Py_Hyperopt
last_modified_at: 2021-11-17

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 어떻게 하면 최적화 할 수 있을지에 대해서 정말정말 쉬운 예제를 통해서 알아봅시다.
{: .notice--warning}

# [Hyper Optimization](#link){: .btn .btn--primary}{: .align-center}

> ## HyperOpt

- HyperOpt는 베이지안 최적화의 접근 방식을 취합니다. 
- 베이시안 최적화는 objective function(목적 함수)를 최대/최소로 하는 최적해를 찾는 기법입니다. 목적함수와 하이퍼파라미터의 Pair를 대상으로 Surrogate Model을 만들어 평가하면서 순차적으로 업데이트 하면서 최적의 조합을 찾아 냅니다.
- 여기서 Acquisition function의 개념이 추가로 나오는데 Surrogate Model은 목적 함수에 대한 확률적인 추정을 하며, Acquisition function은 Surrogate Model이 추정한 확률적 추정 결과를 바탕으로 다음 후보를 선정하는 함수입니다.

![png](/assets/images/Python/54_1.png)

- 위처럼, 베이지안 방법을 이용해 최적화를 위한 위치 (hyperparameter) 를 배워가면서 tuning 하게 됩니다. 당연히 성능이 더 좋은것은 두말할 필요가 없겠죠?
- 아래에서는 어떻게 하면 이런 작업을 할 수 있는지 대충 알아봅시다.

# [Linear function example](#link){: .btn .btn--primary}{: .align-center}

> ## Examples 

- 특정 범위에 대해 정의된 함수가 있고 이를 최소화하려고 한다고 합시다!.
  - 즉, 가장 낮은 출력 값이 되는 입력 값을 찾고자 합니다. 

- 아래의 간단한 예 `x`는 선형 함수를 최소화하는 의 값을 찾습니다 `y(x) = x`

```python
from hyperopt import fmin, tpe, hp
best = fmin(
    fn=lambda x: x,
    space=hp.uniform('x', 0, 1),
    algo=tpe.suggest,
    max_evals=100)
print best
```

```
{'x': 0.00020883172726268804}
```

- 위에 대해서 어떻게 hyperopt 가 작동하는지에 대해서 붆해해 봅시다.

> fn : 최소화 하고자 하는 함수의 정의

- 위에서 fn 은 최소화 하고자 하는 함수를 정의합니다. 
  - 즉 `input` $\to$`output` 에 대해서, 어떤 input 을 설정해야, 최소의 output 을 내뱉는 input 을 찾을 수 있을까? 를 고민한다는 것입니다. 
- 이렇게 지정해줄 수 있는 함수는 어떠한 함수도 될 수 있습니다. 마치 `lambda x: x` 처럼요
- 나중에 할 이야기 이지만 fitting 된 모델에. input 에 대해 Loss 를 뱉는 함수를 정의한다면, 최적의 input (hyperparameter) 를 찾을 수 있겠죠! 

> space : 우리가 찾고자 하는 파라미터의 범위 

- 우리는 hyperparameter 를 search 하면서 함수를 최적화 하려고 할 것입니다.
  - 이때에 '어디를 Search 할 것인가?' 도 우리가 설정해주어야 하는 것이기 때문에, space 의 인자에 설정해 주는 것입니다.
- 위 예제에서는 , 이 범위는 $x\in [0,1]$ 로 설정된 uniform 으로 설정하였습니다. 
  - 이는 `hp.uniform('x', 0, 1)` 으로 표현되었습니다. 

> Algo : 어떤방식으로 search 를 할 것인가?

- 앞에서 어떤 Objective Function 을 최적화 할 것인가? 를 정의하였고, 뒤에서는 어떤 Parameter 를 최적화 할 것인가? 를 정의하였습니다. 
  - 즉 이를 이용한다면 어떤 방식으로 parameter 를 search 할 것인지를 알 수 있게 됩니다! 
- 위 예시에서는 `tpe.suggest` 를 사용하였는데요, 이는 *tree of Parzen estimators* 를 나타냅니다.
  - 이 방법을 다루는것은 시간문제로 하지 않겠지만.. 나중에 시간이 나면 커버해보도록 하겠습니다. ㅎㅎ;

> max_eval : 몇번 Evalutation 을 할 것인가? 

- 위에서 어떤 방식으로 어떻게 파라미터를 찾을지를 정했죠? 
  - 이제 '얼마나' 찾을지를 정해야 합니다.
- 위에서는 `max_evals=100` 을 사용하여 100번 search 를 하겠다고 되어있는것을 볼 수 있습니다.

> output : search 의 결과 

- search 를 수행하고 나서, 어떠한 변수를 찾았는지에 대해서 프로필이 나와야겠죠? 
- 위에서의 예제에서는 `{'x': 0.00020883172726268804}` 가 나왔음을 확인할 수 있습니다.

> ## Remark

![png](/assets/images/Python/55_1.png)

- 위에서 빨간점이 우리가 찾은 최소값임을 볼 수 있습니다. 
  - 어느정도 잘 맞는것을 볼 수 있죠? 

# [Quadratic function example](#link){: .btn .btn--primary}{: .align-center}

> ## Examples

- 이번에는 살짝 어려운 함수에 대해서 알아봅시다. 

```python
best = fmin(
    fn=lambda x: (x-1)**2,
    space=hp.uniform('x', -2, 2),
    algo=tpe.suggest,
    max_evals=100)
print best
```

```
{'x': 0.997369045274755}
```

- 자세한 설명은 이전에 했으므로 더 하지는 않겠습니다. 위 위치는 어디일까요 ?

![png](/assets/images/Python/55_2.png)

- 위 위치입니다! 이번에도 잘 찾은것을 알 수 있습니다.

# [Other Parameters](#link){: .btn .btn--primary}{: .align-center}

> ## Search Spaces

- Search Space 의 자세한 설명은 따로 포스팅을 참고해주세요 

```python
import hyperopt.pyll.stochastic
space = {
    'x': hp.uniform('x', 0, 1),
    'y': hp.normal('y', 0, 1),
    'name': hp.choice('name', ['alice', 'bob']),
}
print hyperopt.pyll.stochastic.sample(space)
```

```
{'y': -1.4012610048810574, 'x': 0.7258615424906184, 'name': 'alice'}
```

- 위를 보면 , optimization 공간은 다음과 같을것입니다. 
  - $x \in unif([0,1])$
  - $y\in N(0,1)$
  - $name \in \{ alice,bob\}$

> ## Trials

- 이제 우리는 hyperorp 라는 블랙박스에서 어떻게 최적화가 이루어지고 있는지 궁금해할 수 있을것입니다. 
- 이때 `Trial` 객체를 이용하면 이러한 블랙박스를 엿볼 수 있게 도와줍니다.

```python
from hyperopt import fmin, tpe, hp, STATUS_OK, Trials
fspace = {
    'x': hp.uniform('x', -5, 5)
}
def f(params):
    x = params['x']
    val = x**2
    return {'loss': val, 'status': STATUS_OK}
trials = Trials()
best = fmin(fn=f, space=fspace, algo=tpe.suggest, max_evals=50, trials=trials)
print(f'best :{best}')
print('trials:')
for trial in trials.trials[:2]:
    print(trial)
```

- 이때 위의 trials 객체를 fmin 에 넣어서, Optimization Procedure 를 저장할 수 있습니다.

```
100%|██████████| 50/50 [00:00<00:00, 833.78trial/s, best loss: 0.0006354990350066602]
best :{'x': 0.025209106192141367}
trials:
{'state': 2, 'tid': 0, 'spec': None, 'result': {'loss': 16.515765043440087, 'status': 'ok'}, 'misc': {'tid': 0, 'cmd': ('domain_attachment', 'FMinIter_Domain'), 'workdir': None, 'idxs': {'x': [0]}, 'vals': {'x': [4.063959281715318]}}, 'exp_key': None, 'owner': None, 'version': 0, 'book_time': datetime.datetime(2021, 11, 16, 17, 35, 36, 552000), 'refresh_time': datetime.datetime(2021, 11, 16, 17, 35, 36, 552000)}
{'state': 2, 'tid': 1, 'spec': None, 'result': {'loss': 4.42367094548546, 'status': 'ok'}, 'misc': {'tid': 1, 'cmd': ('domain_attachment', 'FMinIter_Domain'), 'workdir': None, 'idxs': {'x': [1]}, 'vals': {'x': [2.103252468317929]}}, 'exp_key': None, 'owner': None, 'version': 0, 'book_time': datetime.datetime(2021, 11, 16, 17, 35, 36, 553000), 'refresh_time': datetime.datetime(2021, 11, 16, 17, 35, 36, 553000)}
```

- 이때 위처럼 trials 객체에는 다양한 정보가 들어있으므로 잘 활용하면 많은 intuition을 얻을 수 있을것입니다.

---

**Reference**

- <https://medium.com/district-data-labs/parameter-tuning-with-hyperopt-faa86acdfdce>





